# Network protocols

The following notes are based on Practical Networking's [Network Protocols - ARP, FTP, SMTP, HTTP, SSL, TLS, HTTPS, DNS, DHCP](https://www.youtube.com/watch?v=E5bSumTAHZE&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=12) video.

A Protocol is a set of rules and messages that form an internet standard. Some of the most common protocols are listed below.

* ARP - Address Resolution Protocol

This protocol is used for connecting IP addresses to a fixed MAC address. A host sends out an ARP message asking on the layer 2 network what MAC address is attached to a specific IP address. The host with the appropriate IP address responds back with an ARP message containing its IP address and MAC address.

* FTP - File Transfer Protocol

This is a protocol that allows for transfering files from one host to the other. The requesting host sends out an RETR file request and the FTP server sends back the file.

* SMTP - Simple Mail Transfer Protocol

This is the protocol used for sending mails. The client sends out a HELO request to the smtp server which responds back with a 250 response. These two machines can now exchange mails.

* HTTP - Hyper Text Transfer Protocol

This is the protocol used on the web. A client sends out a GET request and the web server responds back with a 200 OK and the requested page.

* SSL/TLS - Secure Sockets Layer/ Transport Layer Security

TLS is now more common than SSL. TLS is a cryptographic protocol that provides secure communications over a network. It is used most commonly in HTTP (which then because HTTPS), but also mail, instan messaging and other apps.
TLS is used primarily to provide security, integrity and authenticity, usually by using certificates. It is running in the presentation layer. A TLS connection is building a secure tunnel through which the communication flows.

* DNS - Domain Name System

Usually we don't remember IP addresses but rather domain names. But these have to be translated into IP addresses in order for the connection to work out. This is where the DNS protocol comes into play.

This protocol is used to convert a domain name into an IP address. The way this protocol works is through a DNS server. A client asks the server for the IP address associated to a specific domain name. The DNS server sends back the IP address, and the client can then directly use that IP address to communicate with the requested server.

* DHCP - Dynamic Host configuration protocol

In order to have internet connectivity, a host needs to have four elements :

* An IP Address - this is the hosts address
* A subnet mask - this is used in order to know how many other hosts are on the same subnet as the host. It is also used to determine if a request is sent inside the subnet or outside of it.
* A default gateway - The router's IP address used for escaping the subnet when a request goes out to a host that is not on the same subnet
* A DNS - So that domain names can be translated into IP addresses.

All of these things are automatically configured when one connects to a network using DHCP. This way the information doesn't need to be configured manually every time I connect to another internet access point.

When you connect to a network, my device sends out a discover request to a DHCP server which configures all of the information for me and sends back an Offer response.

# Subnetting

This part is mostly based on  Practical Networking's [Subnetting Mastery](https://www.youtube.com/watch?v=BWZ-MHIhqjM&list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE&index=1) youtube playlist.

Subnetting is the action of dividing a network into smaller sub-networks.

There are seven essential attributes of subnetting

* Network ID - First IP Address in each subnet. Cannot be assigned to a host.
* Broadcast - IP Last IP in each subnet. Cannot be assigned to a host.
* First Host IP - IP address after the network ID. First usable IP for a host.
* Last Host IP - IP Address before the broadcast IP. Last usable IP for a host.
* Next network - IP address after the broadcast IP.
* \# IP Addresses - Number of IP addresses in the sub-network
* CIDR/Subnet mask - Two notations used to represent the number of IP addresses in a subnet. The two are equivalent.

As an easy way to convert between CIDR and Subnet mask notation, one can use following cheat sheet.

1. Start with 1, double until you reach 128 (right to left)
2. Substract top row from 256.
3. From /32 list CIDR notation (right to left)

![](/Learning%20Path/Images/Networking/networking_subnetting_cheat_sheet.png)

Subnets break large networks into smaller, more manageable networks that run more efficiently.

Each subnet is a logical subdivision of the bigger network. Connected devices with enough subnet share common IP address identifiers, enabling them to communicate with each other.

Routers manage communication between subnets.

The size of a subnet depends on the connectivity requirements and the network technology used.

An organisation is responsible for determining the number and size of the subnets within the limits of address space available, and the details remain local to that organisation. Subnets can also be segmented into even smaller subnets for things like Point to Point links, or subnetworks supporting a few devices.

Among other advantages, segmenting large networks into subnets enable IP address reallocation and relieves network congestion, streamlining, network communication and efficiency.

Subnets can also improve network security. If a section of a network is compromised, it can be quarantined, making it difficult for bad actors to move around the larger network.

![](/Learning%20Path/Images/Networking/networking_subnetting_example.png)

Example : 10.1.1.55/28 in CIDR notation.

* Network ID - 10.1.1.48
* Broadcast - 10.1.1.63
* First Host IP - 10.1.1.49
* Last Host IP - 10.1.1.62
* Next network - 10.1.1.64
* \# IP Addresses - 16 of which 14 are usable
* Subnet mask - 255.255.255.**240**