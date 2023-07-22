# Hands on : setting up a VPS

The overall goal of my learning journey is to learn the basics of the whole software lifecyle. This means knowledge spanning from managing a linux system all the way to deploying and managing an app. The end goal is to deploy an app, and this is why I chose to get a VPS where the future app can then be deployed. On this VPS I should be able to install all tools I will need for the whole software lifecyle (docker, jenkins etc...). It will also teach me the basics of managing a system.

## Getting a VPS

I chose getting a VPS from [OVH](ovh.com) as they offer cheap solutions for small machines (I got a VPS for 5€/month). When ordering the VPS you can choose the appropriate machine size and the operating system. I chose Debian 12 as OS for my VPS.
Once the VPS has been ordered a small setup time is necessary, before receiving an email containing all credentials necessary for connecting to the VPS (public IP address, default sudo user/password).

## Connecting to the VPS

One can connect to a VPS using SSH.

### What is SSH ?

These notes are largely based on [Baeldung - Introduction to SSH](https://www.baeldung.com/cs/ssh-intro).

Secure Shell (SSH) is a network protocol that allows us to access a remote computer over a (usually insecure) network. It is a protocol on the 7th layer : the application layer.
SSH supports two authentication methods : password and key-based. The key-based authentication allows users to authenticate through a key-pair. The Key-pairs are two cryptographically secure keys (private and public). The public key is shared with the remote server, while the private key is kept secret for security. When the user tries to connect to the remote server, it sends a message that has been encrypted using the public key to the client. The client has to decrypt it, and then sends back the decrypted message combined with the session key (defined by the host and the client together) that will be used for encrypting the data shared between the two during the session. This combination is a hash. The host also creates that hash on its side. If the two hashes match, the user is authenticated.

SSH has a client-server architecture. A server program has to be installed on the server that accepts of rejects the incoming connections. The client also installs a software that allows it to connect to the server. By default the server listens on port 22.

Connecting to a remote computer:

```bash
ssh user@host
```

Creating a key pair : 

```bash
ssh-keygen -t ed25519
```

Copying a file : 

```bash
scp fileName user@host:destinationPath
```

### Connecting to the VPS


I can now connect the first time to the server using the provided credentials. By default the connection happens on a sudo user, and thus with very high privileges. To secure the user, the default password should be changed.

```bash
sudo passwd user
```

The root user doesn't have any password set yet and also needs one.

```bash
sudo su -
passwd
```

The server then has to be rebooted:

```bash
reboot
```

### Securing the VPS

#### Updating the system

In order to secure the system it should always be up to date. To do this on a debian machine two actions need to be performed:

Update the packet lists :

```bash
sudo apt update
```

And the package updates per se :

```bash
sudo apt upgrade
```

#### Changing the default SSH port

Hackers usually aim for the default ports when scanning for open ports on a system. It is therefore a good idea to change the default SSH port.
To do this the configuration file needs to be modified:

```bash
sudo nano /etc/ssh/sshd_config
```

The SSH service then needs to be restarted:

```bash
sudo systemctl restart sshd
```

Now when connecting through SSH the new port needs to be specified:

```bash
sudo user@host -p port
```

In order to make things simpler, an alias can be created for connecting to the vps. For this one needs to add the following line to the ~/.bashrc file:

```bash
alias vps='ssh user@host -p port'
```

#### Configuring the internal firewall

The default configuration tool on linux distributions for setting up firewall rules is iptables. We'll be using this to set up the vps firewall.

The following script can be used to configure the most common things:

```bash
#!/bin/bash
IPT="/sbin/iptables"

# Your DNS servers you use: cat /etc/resolv.conf
DNS_SERVER="213.186.33.99"

# Allow connections to these package servers
PACKAGE_SERVER="ftp.us.debian.org security.debian.org"

echo "flush iptable rules"
$IPT -F
$IPT -X
$IPT -t nat -F
$IPT -t nat -X
$IPT -t mangle -F
$IPT -t mangle -X


## Authorize SSH connection. This needs to be the first rule so that the SSH connection is not cut off.
echo "Allow all incoming connections to ssh port"
$IPT -A OUTPUT -p tcp --sport ssh_port -j ACCEPT
$IPT -A INPUT  -p tcp --dport ssh_port -j ACCEPT

echo "Set default policy to 'DROP' on FORWARD"
$IPT -P FORWARD DROP


## Allowing dns lookups
for ip in $DNS_SERVER
do
	echo "Allowing DNS lookups (tcp, udp port 53) to server '$ip'"
	$IPT -A OUTPUT -p udp -d $ip --dport 53 -m state --state NEW,ESTABLISHED -j ACCEPT
	$IPT -A INPUT  -p udp -s $ip --sport 53 -m state --state ESTABLISHED     -j ACCEPT
	$IPT -A OUTPUT -p tcp -d $ip --dport 53 -m state --state NEW,ESTABLISHED -j ACCEPT
	$IPT -A INPUT  -p tcp -s $ip --sport 53 -m state --state ESTABLISHED     -j ACCEPT
done

echo "allow all and everything on localhost"
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT


## Allow sending requests and receiving data from the package servers, over FTP, HTTP, HTTPS
for ip in $PACKAGE_SERVER
do
	echo "Allow connection to '$ip' on port 21"
	$IPT -A OUTPUT -p tcp -d "$ip" --dport 21  -m state --state NEW,ESTABLISHED -j ACCEPT
	$IPT -A INPUT  -p tcp -s "$ip" --sport 21  -m state --state ESTABLISHED     -j ACCEPT

	echo "Allow connection to '$ip' on port 80"
	$IPT -A OUTPUT -p tcp -d "$ip" --dport 80  -m state --state NEW,ESTABLISHED -j ACCEPT
	$IPT -A INPUT  -p tcp -s "$ip" --sport 80  -m state --state ESTABLISHED     -j ACCEPT

	echo "Allow connection to '$ip' on port 443"
	$IPT -A OUTPUT -p tcp -d "$ip" --dport 443 -m state --state NEW,ESTABLISHED -j ACCEPT
	$IPT -A INPUT  -p tcp -s "$ip" --sport 443 -m state --state ESTABLISHED     -j ACCEPT
done


#######################################################################################################
## Global iptable rules. Allow multiple incoming/outgoing connections to/from local FTP, HTTP and HTTPS ports 

echo "Allowing new and established incoming connections to port 21, 80, 443"
$IPT -A INPUT  -p tcp -m multiport --dports 21,80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A OUTPUT -p tcp -m multiport --sports 21,80,443 -m state --state ESTABLISHED     -j ACCEPT

echo "Allow outgoing icmp connections (pings,...)"
$IPT -A OUTPUT -p icmp -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
$IPT -A INPUT  -p icmp -m state --state ESTABLISHED,RELATED     -j ACCEPT

echo "Allow outgoing connections to port 123 (ntp syncs)"
$IPT -A OUTPUT -p udp --dport 123 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A INPUT  -p udp --sport 123 -m state --state ESTABLISHED     -j ACCEPT

# Default rule is DROP for all other ports
$IPT -A INPUT  -j DROP
$IPT -A OUTPUT -j DROP

exit 0
```

Now the rules need to be saved for reboot:

```bash
sudo apt install iptables-persistent
```

The iptables-persistent utility automatically loads the iptables rules at system boot. If the rules are changed they need to be updated.

```bash
sudo /sbin/iptables-save > /etc/iptables/rules.v4
```

#### Configuring Fail2ban

Fail2ban is tool that is used to prevent intrusions by blocking IP addresses from where bots or hackers try to penetrate the system. This is particularly useful against Brute Force or Denial Of Service attracks as Fail2ban bans IP addresses that make too many requests.

First install the package

```bash
sudo apt install fail2ban
```

Create a custom jail configuration :
```bash
sudo nano /etc/fail2ban/jail.d/custom.conf
```

```bash
[DEFAULT]
ignoreip = 127.0.0.1 your_ip # ignore specific IPs from banning
findtime = 10m
bantime = 24h # A long ban time limits attack possibility
maxretry = 3

# Add active services, and most importantly ssh

[sshd]
enabled = true
port = ssh_port # the ssh port used by the system
backend = systemd # This allows specifying that ssh is using systemd and thus the systemd journal for logging
```
Start the service :

```bash
sudo systemctl start fail2ban
```

Activate the service on system startup :

```bash
sudo systemctl enable fail2ban
```

Check that the service started correctly :

```bash
systemctl status fail2ban
```


# Resources
* [Baeldung - Introduction to SSH](https://www.baeldung.com/cs/ssh-intro)
* [OVH guideline for getting started with the VPS (french)](https://help.ovhcloud.com/csm/fr-vps-getting-started)
* [OVH guideline for securing a VPS (french)](https://help.ovhcloud.com/csm/fr-vps-security-tips)
* [Configurer fail2ban (french)](https://doc.ubuntu-fr.org/fail2ban)