# Hands on : setting up a VPS

The overall goal of my learning journey is to learn the basics of the whole software lifecyle. This means knowledge spanning from managing a linux system to deploying and managing an app through app development. The end goal is to deploy an app, and this is why I chose to get a VPS where the future app can then be deployed. On this VPS I should be able to install all tools I will need for the whole software lifecyle. It will also teach me the basics of managing a system.

## Getting a VPS

I chose getting a VPS from [OVH](ovh.com) as they offer cheap solutions for small machines (I got a VPS for 5€/month). When ordering the VPS you can choose the appropriate machine size and the operating system. I chose Debian 12 as OS for my VPS.
Once the VPS has been ordered a small setup time is necessary, before receiving an email containing all credentials necessary for connecting to the VPS (public IP address, default sudo user/password).

## Connecting to the VPS

One can connect to a VPS using SSH.

### What is SSH ?

There notes are largely based on [Baeldung - Introduction to SSH](https://www.baeldung.com/cs/ssh-intro).

Secure Shell (SSH) is a network protocol that allows us to access a remote computer over a (usually insecure) network. It is a protocol on the 7th layer : the application layer.
SSH supports two authentication methods : password and key-based. The key-based authentication allows users to authenticate through a key-pair. The Key-pairs are two cryptographically secure keys (private and public). The public key is shared with the remote server, while the private key is kept secret for security. When the user tries to connect to the remote server, it sends a message that has been encrypted using the public key. The client has to decrypt it, and then sends back the decrypted message combined with the session key (defined by the host and the client) that will be used for encrypting the data shared between the two during the session. This combination is a hash. The host also creates that hash on its side. If the two hashes match, the user is authenticated.

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

(RSA should avoided now)

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

# Resources
* [Baeldung - Introduction to SSH](https://www.baeldung.com/cs/ssh-intro)