# OSI model

The materiel I'm following for learning about the OSI model comes from the Practical Networking's [Networking Fundamentals series](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi). And more specifically following videos:

* [The OSI Model: A Practical Perspective - Layers 1 / 2 / 3](https://www.youtube.com/watch?v=LkolbURrtTs&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=3)
* [The OSI Model: A Practical Perspective - Layers 4 / 5+](https://www.youtube.com/watch?v=0aGqGKrRE0g&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=4)


## The 7 layers

In order for the hosts to understand each other, a set of rules has to be put into place, similarly to the rules in a language. In networking those rules are divided into the 7-layer OSI model.

![](/Learning%20Path/Images/Networking/networking_OSI.png)


This order can be retained using the **All People Seem To Need Data Processing** sentence.

The important part is that the OSI is just a *model*, it is more of a guideline and there are regularly some exceptions.

## Physical layer

Something has to exist in order to transport the bits in-between hosts. Layer one technologies are the ones used to physically transport the information. Those are all sorts of cables and wireless networks.

Repeaters and hubs are considered layer 1 technologies as they are used to transport information from one computer to the next.

## Data Link

This layer directly interacts with the physical layer. Examples include network interface cards (NIC)/ wifi cards.
Layer 2 uses a specific addressing scheme - the mac addresses. Those addresses are 48 bits represented using 12 hexadecimal digits.
Every single NIC has a unique MAC address.
Switches are considered layer 2 technologies. A layer 2 technology takes care of sending the data from one NIC to the other. There are usually multiple such hops that occur in a communication, and the next layer is used to know starting and endpoints of the whole journey (end-to-end delivery as opposed to a single hop from one NIC to the next).

## Network

As mentionned above, this layer is used for the end-to-end communication. It has its own addressing scheme called the IP address (which has been covered in the previous section).
Layer 3 technologies all have IP addresses, so hosts and routers are layer 3 technologies.

![](/Learning%20Path/Images/Networking/networking_layer_3.png)

Why do we need both IP and MAC addresses ?
Each of the addresses serve different purposes. 
A layer 3 header is added at the beginning of the communication, contianing source and destination IP addresses. For each hop from one NIC to the next, a Layer 2 header is added containing source et destination MAC address. It is replaced at each new hop. Layer 3 header is discarded once the data packet arrives at the destination host.
There is a specific protocol - the Address Resolution Protocol (ARP) that links both layers that will be discussed in another section of the course.

## Transport

The layer 4 is used for distinguishing data streams. It is used as service to service transport method. For example on a computer runnninng a chat session, visiting a web site and playing an online video game, the layer 4 is useful for routing the data streams to the appropriate service.
It also has its own addressing scheme, which involves ports. Each service is assigned a port number and this information is added on top of the layer 2 and 3 layers.
Each browser tab for example has its own random port assigned by the host.
TCP and UDP are two strategies that can be used for accomplishing service to service communication.

## Layers 5,6,7

Usually the distinction between those layers is vague and they are grouped into a single layer in reality. For example the TCP/IP Model usually groups all those layers together into a signal Application layer.


## How data is sent

The source host is encapsulating the data with the successive layer headers. This encapsulated data is then sent through the physical layer to the destination host which de-encapsulates the data.
At each layer there is a specific name for the encapsulated data.

![](/Learning%20Path/Images/Networking/networking_encapsulation.png)