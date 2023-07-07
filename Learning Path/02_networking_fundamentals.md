# Networking devices

## Hosts

Hosts are any device which sends or receives traffic over a network. For example:
- Computer
- Laptop
- Phone
- Server
- Cloud server
- Anything IoT related
    - TV
    - Speakers
    - Lights

All of these devices use the same rules for communicating.

There are two types of hosts. Clients and servers. Clients initiate requests and servers respond to requests.
These notions are relative to a specific communication. A server might initiate a request as well.
A server is a computer that runs software which responds to specific requests.

## IP Address

The IP address is the identity of each host, a bit like a phone number.
Each communication features the source IP address and the destination IP address.
An IPv4 address is 32 bits, and we usually write it in octets.

The IP addresses are hierarchically assigned. This is a process called subnetting.

## Networks

A network is what transports traffic between hosts. Anytime two hosts are connected there is a network. It is a logical grouping of hosts which require similar connectivity.
A network can contain another network (subnet).
Networks connect to other networks via the internet. The internet is a bunch of interconnected networks.

## Repeater

The purpose of a repeater is to repeat an input data transfer to send it further. Repeaters are needed because the signal decays over longer distances. Without repeaters signals would not reach the destination.

## Hub

Instead of interconnecting all hosts, which wouldn't scale, hubs are used to create a centralized node that redistributes the signals. The hub redistributes the signal to all connected hosts.


## Bridge

A bridge sits in-between two hub connected hosts. The hubs will send all signals to the bridge, but the bridge will decide if the signal needs to be sent from one group of hub connected hosts to the other group of hub connected hosts.


## Switch

Switches are a combination of hubs and switches. The switch learns which hosts are on each of its ports. It can then redistribute a message only to the concerned hosts.
It facilitates communication *within* a network.

Switching is therefore the process of moving data within networks.

## Router

A router facilitates communication *between* networks.
They provide traffic control points (security, filtering, redirecting).
Routers learn which networks they are connected to. A router keeps the routes it learns in a routing table.
A router has an IP address in each network it is attached to.
This IP address is what is known as a gateway, it is a way out of the local network.

They are what creates the hierarchy in networks and the internet.

Routing is therefore the process of moving data between networks.


There are many other devices that exist, but each of them implement switching and/or routing. Some of devices are:

- Access Points
- Firewalls
- Load Balancers
- Layer 3 Switches
- IDS / IPS
- Proxies
- Virtual Switches
- Virtual Routers

# Resources

- [Networking fundamentals](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi)