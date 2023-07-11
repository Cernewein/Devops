# Linux networking tools

These notes concern some of the most common networking tools used in linux. Those tools are used for toubleshooting network issues, configuring network rules, copying data...

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

# Resources

* [Geeks for geeks - Traceroute with examples](https://www.geeksforgeeks.org/traceroute-command-in-linux-with-examples/)
* [Linuxsize - Ping command in Linux](https://linuxize.com/post/linux-ping-command/)
* [javatpoint - Linux mtr command](https://www.javatpoint.com/linux-mtr)
* [Free code camp - What is namp and how to use it](https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-scanning-tool-of-all-time/)