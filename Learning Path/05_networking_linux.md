# Linux networking tools

These notes concern some of the most common networking tools used in linux. Those tools are used for toubleshooting network issues, configuring network rules, copying data...
This section is more of a collection of tools. The goal will be to use them when setting up a VPS for my personnal project.

## traceroute

The traceroute command is used for checking what route a packet takes to reach the destination host. This tool is useful for troubleshooting slow network connections as it shows how long the journey of a packet is.

Usage : 

```bash
traceroute [options] host_Address [pathlength]
```

The output is made up of 3 columns. First column shows the hop count. The second column is the IP address of that hop. And the 3 numbers in the last column represent the time taken by a packet to reach that hop (this is performed 3 times and we thus have 3 numbers).

## ping (Packet Internet Groper)

This command is used to for troubleshooting, testing and diagnosing network connectivity issues.

The ping command send one or more Internet Control Message Protocol (ICMP) ech request packages to a destination IP address on the network and waits for a reply.

This way one can diagnose if the remote destination can be reached, how long the roundtrip takes and if there is data loss along the way. It also returns the number of hops (time to live or TTL) a packet needs to reach the destination. TTL is the number of hops a data packet is allowed to make before it is discarded. The ping command sends out packets with an increasingly larger TTL until the destination is reached.

Usage : 

```bash
ping [options] destination
```

## mtr

mtr is combination of ping and traceroute. It provides the same information but in a unique command.

```bash
ping [options] host
```

## nmap

nmap (network mapper) is an open-source linux command line tool that can scan IP addresses and ports in a network. This allows network administrators to find what devices are on the network, discover open ports and services and detect vulnerabilities.

Usage : 

```bash
nmap [ <Scan Type> ...] [ <Options> ] { <target specification> }
```

## Netstat

This tool is used to display all tcp, udp and unix socket connections. It also displays the listening sockets waiting for incoming connections.


## UFW & iptables

uncomplicated firewall (UFW) is a utility for managing firewall rules in Arch Linux, Debian and ubuntu. It is supposed to make the experience as simple as possible. It is actually a frontend to the *iptables* utility.
*iptables* is used to create firewall rules that will allow or block traffic.

Configuring a firewall will be the subject of another distinct section in my learning journey.

## tcpdump

tcpdump is a tool used for analysing network traffic passing through the system. It can be used to to capture and filter packets and also displays the informations in a human-readable format. A dump can be created and analysed later as well.


## dig (Domain Information Groper)

This tool is used to retrieve information from DNS servers. It used usually used for troubleshooting DNS problems.

Usage : 

```bash
dig {target host}
```

## scp (Secure Copy Protocol)

This tool is to securely copy files and directories between two locations. The two locations are usually linux based/unix based. SCP uses an encrypted connection via SSH. This ensures the transferred data is correctly protected.

Usage :

```bash
scp [OPTIONS] [[user@]src_host:]file1 [[user@]dest_host:]file2
```

# Resources

* [Geeks for geeks - Traceroute with examples](https://www.geeksforgeeks.org/traceroute-command-in-linux-with-examples/)
* [Linuxsize - Ping command in Linux](https://linuxize.com/post/linux-ping-command/)
* [javatpoint - Linux mtr command](https://www.javatpoint.com/linux-mtr)
* [Free code camp - What is namp and how to use it](https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-scanning-tool-of-all-time/)
* [Tutorialspoint - netstat command in Linux with examples](https://www.tutorialspoint.com/unix_commands/netstat.htm)
* [Linux.com - An introduction to Uncomplicated Firewall (UFW)](https://www.linux.com/training-tutorials/introduction-uncomplicated-firewall-ufw/)
* [Hostinger - Iptables Tutorial - Secruing Ubuntu VPS with Linux Firewall](https://www.hostinger.in/tutorials/iptables-tutorial)
* [Opensource.com - Introduction to tcpdump](https://opensource.com/article/18/10/introduction-tcpdump)
* [geeks for geeks - dig command in linux with examples](https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/)