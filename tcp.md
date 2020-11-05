## TCP 1

Today, we begin our lessons on TCP/IP protocols and advanced topics. TCP/IP Protocol Suite, is to build a network of networks or the Internet that can operate over multiple, coexisting, and heterogeneous network technologies. The goal is to provide ubiquitous connectivity through the IP packet transfer. The TCP/IP Protocol Suite usually refers, not only to the two most well-known protocols called Transmission Control Protocol (TCP), and as the Internet Protocol (IP), but also to other protocols, such as a User Datagram Protocol (UDP), the Internet Control Message Protocol (ICMP), the Address Resolution Protocol (ARP), and other basic applications. The Protocol Data Unit of a given layer is encapsulated in a protocol data unit of the layer below, as shown in the figure. For example, an HTTP request is passed to the TCP layer, which encapsulates the message into a TCP segment. The TCP header contains the source and destination port numbers. So TCP segment in turn is passed to the IP layer where it is encapsulated in an IP packet. The IP packet header contains an IP network address for the sender and an IP network address for the destination. The IP packet is then passed through the network interface. Each host in the Internet is identified by a globally unique IP address. An IP address is divided in two parts, a network ID and a host ID. Routing decision is done based on destination IP address. The Internet Protocol (IP), provides a connection-less best effort delivery service to the transport layer. The term best effort indicates that the IP we're tryi- it's best to forward a packet to the destination, but it doesn't guarantee that a packet will be delivered to the destination, nor its quality of service. Higher layer protocols must deal with the reliability issue, if necessary. This design decision, however, reduce the complexity of the IP and increases its flexibility. So IP packet contains a header port and a data port. The format of the header port is shown in this figure. The header has a fixed length component of 20 bytes plus a variable length component consisting of options that it can be up to 40 bytes. Let's briefly discuss the meaning of each field in the IP header. The version of the header indicates the version number used by the IP packet, 4 or 6 currently. As IP header can be of different lengths, the field of header lengths specifies the length of the header into 32-bit words. The type of service field traditionally specifies the quality of the packet. The fear is not in common use. Recently, a work in differentiated associates redefines the field to include other services besides the best effort. As a packet may have different amount of data, the total length field specifies a number of bytes of the IP packet including header and data. Notice the maximum possible length, 64 kilobytes is rarely used. As the internet often limits the payload length to 1,500 bytes. The identification flex under fragmented offset fields are used for fragmentation and reassembly. The time-to-live field was originally defined to indicate the amount of time in seconds the packet is allowed to remain in the network. However, the routers interpreted this field to indicate the number of hops the packet is allowed to traverse in the network. If the field reaches 0, the router discards the packet. It can be used to limit the scale and remove the duplicates due to flooding. The protocol field specifies the upper layer protocol that it is to receive IP data at a destination. The header checksum field verifies the integrity of the IP header. Please recall the calculation of the Internet checksum that was discussed in ella control. Also note that the data part is not verified and is left to upper layer protocols. Source and destination IP addresses contains the address of source and destination hosts. The options field, which is of variable length, allows a packet to request special features such as security level, route to be taken by the packet, and timestamp at each router. As option is of variable lengths, the padding is used to make the header, a multiple of the 32-bit words. When an IP packet is passed to the router, the following processing takes place. First, the router calculates the header checksum for correctness and then checks that field in header. For example, version and a log- total length contains valid values. Next, the router identifies the next hop for the IP packet by consulting the routing table, then the router changes the fields such as time-to-live and header checksum and forwards the packet along the next hop. This concludes today's lesson.

## IP addressing

We discuss IP addressing in today class.
The IP address structure was defined to have a two level hierarchy,
network ID and host ID.
Network ID identifies the network that a host is connected to.
All hosts connect you to the same network have the same network ID.
The host ID identifies a network connection to the host,
this aggregation facilitates packet routing.
That is a router forwards packets based on network ID
only thereby reducing the size of the routing table significantly.
The host ID is assigned by the network administrator at the local site.
But the network ID for an organisation may be assigned by internet service providers.
IPV4 addresses often use dotted-decimal notation.
The IP address structure is divided into five address classes.
Class A, B, C, D,
and E. Class A addresses have seven bits for network IDs and 24 bits for
host IDs allowing for up to 128 networks and about 16 million hosts per network.
Very few organizations and companies can have so large Class A network.
Class B addresses have 14 bits for network IDs and 16 bits for
host IDs allowing about 16000 networks and about a 64000 hosts for each network.
Class C addresses have 21 bits for network IDs and eight bits for
host IDs allowing about 2 million networks and 254 hosts per network.
We can observe that a Class B address offers
a moderate size network while a class C address offers a small network.
Class D addresses are used for multicast services
that allows one to send information to a group of hosts simultaneously.
They have fixed a prefix 1110.
A multi-cast address have 28 bits allowing up to about 250 million multicast groups.
Class E addresses are used for experiments.
They are reserved to host IDs consisting of all ones or all zeroes for special purpose.
An internet address used to refer to a network has host ID set to all zeroes.
A host ID that contains all ones meant to
broadcast the packet to all hosts on the network specified by the network ID.
When the network ID contains all ones,
the packet is broadcast on the local network.
This explains why A to B host ID only allows 254 hosts instead of 256.
Interestingly, they are specific range or
private IP addresses that are designated for use in private networks.
Their use are restricted to private internet.
Routers in public internet will discard packets with these addresses.
So your ranges are defined and as shown here.
Network Address Translation (NAT) is
used to convert between private and a global IP addresses.
Let's look at an example of IP addresses.
In the figure, two networks are connected with a router network
128.135.0.0 and a 128.140.0.0.
Note that are an address with all host IDs be zeros refers to their network.
So a router is connected to two networks and that
therefore this two network interface have IP addresses belong in two networks.
As two networks have 16 bits in their host ID,
they are Class B networks.
The original class for IP addressing scheme has drawbacks.
Classes A and B might be too large for an organization where Class C might be too small.
Consider a typical university that has
a class B network address which can support about 64000 hosts.
First, it would be a gigantic task for
the local network administrator to manage all 64000 hosts.
Second, a university typically has more than one local network.
For example, one department may have
one local network so there is a need a much more of network addresses.
The question is, how to allow one large network to be split into
several smaller parts for internal use but still act like a single network to offsite.
The popular scheme is called a Subnet which will be discussed in our next. 


## Subnetting

This class continues on IP addressing
and the focus is on subnet addressing
that efficiently utilize IP addresses.
The basic idea of subnetting is to add another hierarchical level called a subnet,
as shown in the figure.
The beauty of subnet addressing is that it is
oblivious to the network outside of the organization.
That is a host on outside of this organization would still
see the original address structure with two levels.
The inside of the organization,
the local network administrator is free to choose
any combination of LANs for the subnet and host ID fields.
It simplifies the management of multiple LANs within the organization.
But when a packet comes into the main router,
how does it know which subnet to give the packet to?
IP address masking is used to find a subnet ID.
Let's look at the subnetting scheme.
Consider an organization that has a class B address with network ID 150.100.0.0.
So, a network has 16 bits for host IDs.
Suppose an organization has many local area networks,
each consisting of no more than 100 hosts in each subnet.
Then, 7 bits in host IDs are sufficient to uniquely identify each host in
the subnet and it has suppose 2+7-2 that is 126 hosts.
The other 9 bits can be used to identify the subnets within the organization,
which can identify 2+9-2 subnets.
The question is, if a packet with a destination IP address,
say 150.100.12.176 arrived at the site from the outside network,
which subnet should the router forward this packet to?
To find the subnet number,
a router needs to store an additional quantity called a subnet mask,
which consists of binary ones for every bit position
of the address except in the host ID field where binary zeros are used.
As 7 bits are used for host ID,
the subnet mask in binary string is given inside,
which corresponds to 250.250.250.128 in dotted decimal notation.
The router can determine the subnet number by performing a perfect logic and
operation between the subnet mask and its IP address bit by bit.
Therefore, the resulted subnet number is shown in the slide that corresponds
to 150.100.12.128 in dotted decimal notation.
This number is used to forward the packet to the correct subnet inside the organization.
Note that if a subnet has to support more hosts,
then the host ID would need more bits but will leave fewer bits for the subnet ID.
In a subnet 150.100.12.128,
the IP address 150.100.12.128 is used to
identify this subnet while IP address
150.100.12.250 is used to broadcast packets in the subnet.
The range of the subnet IP address is given in the slide that corresponds
to 150.100.12.129 to 150.100.12.254.
Lets look at example of address assignment with subnetting.
Consider a site that has been assigned a Class B IP address of 150.100.0.1.
The site has a number of subnets and many hosts denoted in
each connected routers denoted in R.
The figure only shows three subnets and five hosts for simplicity.
Three subnets are 150.100.12.108, 150.100.12.0 and 150.100.15.0.
Assume that subnet field in
9 bits long and the host ID field in 7 bits long.
When a host located outside the network wants to send a packet to a hosting network,
all the external routers have to know is how to get to network address 150.100.0.1.
So the subnetting concept is very
powerful as internal network configuration details are hidden from outside.
The IP layer in the end system hosts and in
the routers work together to route packets from IP network source to destination.
The IP layer in each host and the router maintains
a routing table that is used to determine how to handle each IP packet.
Considers action of an originating host to send an IP packet,
it consults its routing table.
If the destination host is in the same network,
it sends the packet directly using a appropriate network interface.
Otherwise, the routing table typically specifies that the packet is to be
sent to a default router that is directly connected to the originating host.
Now consider the action of a router.
When a router receive an IP packet,
it examines the IP destination address in
the arriving packet by consulting its routing table.
If the packet is destined to itself,
it delivers the packet to the appropriate higher layer protocol.
If the destination IP address is not the router's own address,
router consults the routing table to determine the next hub and
associated network interface and then forwards the packet.
This concludes today's lesson. 


## Subnetting examples
Share
0:03/5:42

Take notesHighlight
Share
Help Us Translate
Interactive Transcript - Enable basic transcript mode by pressing the escape key

You may navigate through the transcript using tab. To save a note for a section of text press ⌘ + S. To expand your selection you may use ⌘ + arrow key. You may contract your selection using shift + ⌘ + arrow key. For screen readers that are incompatible with using arrow keys for shortcuts, you can replace them with the H J K L keys. Some screen readers may require using ⌘ in conjunction with the alt key
Today, we examine Subnet Routing Examples
to help have a deeper understanding of subnet technique.
In a routing table, be a router or in its host,
each row must provide the following information: destination IP address,
IP address of next-hop router, flag fields,
physical address of outgoing network interface and other information such as statistics.
Several types of flags may be defined, for example,
the H flag indicates whether the route in the giving role is to a host or to a network.
The G flag in the case where the route in
the giving role is to a router or to a directly connected destination.
Each time a packet is to be routed,
the routing table is search in orders.
First, the destination column is searched to see whether
the table contains an entry for the complete destination address.
If so, the IP packet is forwarded according to the next-hop entry.
Otherwise, the routing table is searched for the destination network ID.
If an entry is found,
the IP packet is forwarded according to the next-hop entry.
If above doesn't work out,
the table is searched for
a default router entry and if one is available the packet is forwarded there.
Finally, if none of above search are successful,
the packet is declared undeliverable and ICMP
host unreachable error packet is sent back to the originating host.
In the first example,
suppose our packet having a destination IP address of
150.100.15.11 arrive from the outside network,
the main router R1 has to know the next hub router to send the packet to.
The IP address 150.100.15.11 is converted into a binary string.
As router R1 knows that a nine bit subnet field is in use,
it has seven base in host ID and thus it gets the mask.
It applies a mask to extract as a subnet address
from the IP address by performing per bit logical and operation.
So the result is 150.100.15.0.
Router 1 looks up
this subnet number in its routing table and finds the corresponding entry
to specify the next-hop router address for router R2 which is 150.100.12.1.
R1 simply puts the packet to the article import 150.100.12.4.
And by broadcasting R2 will get the packet from
its port 150.100.12.1 as they are in the same network.
When R2 receives the packet,
it performs the same process and finds out that
destination host is connected to one of its network interface.
It sends the packet directly to the destination.
Let's look at the second example.
Here, host H5 wants to send an IP packet to host H2.
H2 has IP address 150.100.12.176.
In its routing table,
the first entry is a loopback interface whereas H indicates a host address.
The second entry is a default entry with the next-hop router R2 150.100.15.54.
As it is a router,
the flag bit G is set to one and with its net interface emd0.
The sudden entry is a network address.
By convention the next-hop entry is IP address of algorithm network interface.
Host H5 first search its routing table for the IP packet at destination address
150.100.12.176.
As it doesn't find its entry in its routing table,
it'll search for that destination network ID that's 150.100.12.108.
But still no match,
it finds a default route to R2 and forwards IP packet across the network.
Router R2 search its routing table and forwards the IP packet to Router R1.
Using the default route,
R2 search its routing table and it finds a match to
the destination network ID that's 150.100.12.128.
It sends a packet so the network interface which delivers a packet to
the local area network by broadcasting and host H2 receive the packet.
So routing is finished in this example.
This concludes this lesson on subnetting. 
