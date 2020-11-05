## Classless Interdomain Routing (CIDR)

Our today's lesson is on Classless Interdomain Routing, CIDR,
another very powerful technique for efficiently utilizing IP addresses.
Dividing the IP address space into A,
B, C classes is inflexible.
On one hand, most organization utilize class A and B space inefficiently.
On the other hand,
most organizations typically need
more addresses that can be provided by a class C address space.
Meanwhile, the IP routing table size grows
quickly due to the growth in number of networks in the internet.
Larger routing tables put a stress on router processing power and memory.
In short term, techniques such as CIDR,
new allocation policy, network address translation,
they can utilize IP address more efficiently.
But in long term,
IPv6 with much bigger address space is a solution.
CIDR uses an arbitrary prefix length to
indicate the network number in place of the class flow scheme.
A prefix 205.100.0.0 of length 22
is written as 205.100.0.0/22.
The /22 notation indicates that a network mask is 22 bits long.
With CIDR, packets are routed according to the prefix without address classes.
An entry in CIDR routing table contains 32-bit IP address and a 32-bit mask.
CIDR enables supernetting technique to allow
a single routing entry to cover a block of classful addresses.
For example, a company is allocated a four contiguous/24 networks, 128.56.24.0,
128.56.25.0,
125.56.26.0, and 128.56.27.0.
At some router, it is often true that
all of these four networks use the same outgoing line.
CIDR aggregation can be done to reduce the number of entries at the router.
CIDR scheme converts the four/22 network addresses into binary streams,
performs per-bit and logical operation,
and resulted 128.56.24.0/22.
That is resulted a single prefix for all four/24 networks.
Before CIDR, four networks,
and therefore four entries needed in the router for this company.
But after CIDR, only one entry needed in the router.
CIDR was proposed to deal with routing table explosion problem.
By CIDR, networks are represented by prefix and mask.
It has summarized our contiguous group of class C addresses using variable-length mask,
if all of them use the same outgoing line.
Routing is performed according to the prefix of address instead of class.
For example, IP address and mask in
122.32.136.0/21 stands for to do one-bit IP mask.
By IP masking, it represents a network with a minimal IP address
192.32.136.1 to
the maximum IP address 192.32.143.254.
You may be able to figure out that it indeed represents eight class C networks
from 192.32.136.0/24
to 192.32.143.0/24.
CIDR summarize our contiguous group of class C addresses using variable-length mask.
Let's look at an example 150.158.16.0/20.
So last 20 stands for 20 bits IP mask.
By IP masking, we can find it that it represent
16 C networks from
150.158.16.0/24 to 150.158.31.0/24.
In the second example,
a router has the following CIDR entries in its routing table.
Address with mask 128.56.24.0/22 corresponds to interface zero.
Address with mask 128.56.60.0/22 corresponds to interface two.
Default goes to router two.
The question is, if a packet coming with IP address of 128.56.63.10,
what does this router do?
First, the address 128.56.63.10 is converted into a binary string.
Then, 22 bits IP masking is performed,
that is to perform
per-bit logical and operation between the binary string with the 22 bits IP mask.
The resulting binary string corresponds to 128.56.60.0.
There is a match in the routing table,
and the packet is forwarded to the interface one.
New address allocation policies were proposed to capitalize on
CIDR ability to aggregate routers and reduce routing table size.
Classes A and B are assigned only for clearly demonstrated need.
Consecutive blocks of class C is assigned up to
64 blocks so that all IP address in the range have a common prefix.
By CIDR aggregation, only one entry is required for this blocks.
Address assignments should reflect the physical topology of the network to
facilitate the aggregation of logical packet flows into physical flows.
The use of variable-length prefixes require that the routing table be
searched to find the longest prefix match
when multiple entries match up given IP address.
For example, 3/24 IP addresses,
128.56.24.0/24 to 26.0/24 to 27.0/24,
all belong to company A,
but the network 128.56.24.0/24
belongs to a different company with a different port number.
By CIDR aggregation on the three networks of the company A,
we can get 128.56.24.0/22.
Now, if a packet with destination IP address 128.56.24.1 comes,
which port should we route this packet to?
The problem is, it will match both entries as shown here.
The longest prefix match requires our packet
must be routed using the most specific route.
That is, 128.56.24.0/24.
And the packet is forward by port zero.
Please note that several fast longest prefix
matching algorithms are available for implementation.
This concludes today's lesson. 

## ARP, Fragmentation and Reassembly


This class focus on several IP address and techniques.
IP addresses are said to be logical,
because they are defined in terms of logical topology of the routers and end systems.
The logical IP addresses need to be converted into
specific physical addresses for the underlying network technology.
Currently, Ethernet is the most common network that IP runs on.
Ethernet uses 48-bit MAC address format.
How does the host map the IP address to the MAC address?
Address resolution protocol, ARP,
provides conversion between IP address and physical address.
This figure illustrates the main idea.
Suppose H1 wants to send an IP packet to H3,
but doesn't know the MAC address of H3.
H1 first broadcasts an ARP request packet asking the destination host,
which is identified by H3's IP address, to reply.
All hosts in the network receive the packet,
but only the intended host,
H3, responds to H1.
The ARP response packet contains H3's MAC and IP addresses.
From now on, H1 knows how to send a package to H3.
Further questions are how to speed up this mapping process.
Caching is an effective scheme.
For example, H1 can cache H3's MAC and IP address in it's
ARP table so that H1 can simply look up H3's MAC address in the table for future use.
In order to refresh caching results,
each entry in the IP table is usually H so that
its contents are erased if no activity occurs within a certain period,
say 5 to 15 minutes.
One of the strengths of IP is that it can work on a variety of physical networks.
Each physical networks usually impose
a certain packet size limitation on the packets that can be carried.
This is called the maximum transmission unit, MTU.
When IP wants to send a packet that is larger than the MTU of the physical network,
IP must break packet into smaller fragments to fit.
Fragmentation can be done at a source level or at an intermediate router,
as illustrated in the figure.
The destination IP is the only entity that is
responsible for assembling the fragments to the original packet.
To reassemble the fragments,
the destination waits until it
has received all the fragments belonging to the same packet.
If one or more fragments are lost in the network,
the destination abandons the assembly process.
Although fragmentation may seem to be a good feature,
it involves a subtle performance penalty.
There are three fields in IP header: Identification, Flags, and Fragment Offset.
They have been assigned to manage fragmentation and reassembly.
The identification field is used to
identify which packet a particular fragment belongs to,
so that fragments for different packets do not get mixed up.
The Flag field has three bits: One unused bit,
one "do not fragment" bit,
and one "more fragment" bit.
If the "don't fragment" bit is set to one,
it will force the router not to fragment the packet.
If "more fragment" bit is set to one,
it tells the destination host that there are more fragments to follow.
The Fragment Offset field identifies the location of a fragment in the packet.
The value matches offset in units of 8 bytes between
the beginning of the packet to be fragmented and the beginning of the fragment.
The reason that offset is measured in units of 8 bytes is to
address the problem that the packet length has 16 bits,
while the offset only has 13 bits.
The audience should verify that
these three fields give sufficient information to hosts and
routers to perform fragmentation and reassembly.
Let's look at the example.
Suppose a packet arrives at a router and it is to be
forwarded to a network having an MTU of 576 bytes.
The packet has an IP header of 20 bytes and a data part of 1484 bytes.
We need to perform fragmentation and include the pertinent values of the IP header.
The MTU per fragment equals to 576 minus 20 bytes of header,
which becomes 556 bytes.
However, 556 is not a multiple of 8.
Therefore, we need to set the maximum data length to 552,
and we can break 1482 into 552 plus 552 plus 380.
So we need three fragments.
This table shows the pertinent values for
the IP header where X denotes a unique identification value.
All the value except the header checksum are the same as in original packet.
This concludes today's class. 

## DHCP, NAT
Today's class focus on DHCP and Network Address Translation techniques.
Both of them are very useful in maximizing the usage of limited IP addresses.
The Dynamic Host Configuration Protocol,
DHCP automatically configures hosts that connect to a TCP/IP network.
An earlier protocol, Bootstrap Protocol,
allowed a diskless workstations to be remotely booted in a network.
It used a well known UDP port number 67 for the server port and a 68 for the client port.
DHCP builds on the capability of
Bootstrap Protocol to deliver configuration information to a host.
This capability is used extensively by Internet service providers to assign
temporary IP addresses to hosts and maximize the usage of their limited IP address space.
When a host wish to obtain an IP address,
the host broadcasts a DHCP-discover message in its physical network.
The server in the network responds with
a DHCP offer message that provides an IP address and another configuration information.
Several servers and memory apply to the host says the host select one of the offers and
a broadcast a DHCP request message that includes the ID of the server.
The selected server then allocates the giving IP address to the host and assigns
a DHCP accurate message assigning
the IP address to the host for some period or release time.
Previously we have seen three ranges of private addresses or
called unregistered addresses have been set aside for use in private Internets.
Packets with private unregistered addresses are valid inside of their private networks.
However, they are discarded out by routers in the global Internet.
Network Address Translation, NAT refers to a method for mapping
packets from hosts in private Internet into packets that can traverse the Internet.
It also transfers packets arriving from
the global Internet to the appropriate destination machine in the private network.
To do so, a device acts as an agent between a private network and a public network.
By NAT a number of hosts can share a limited number of registered IP addresses.
We limit our discussion to the case where
a single register IP address is shared by machines
in a private network networks as follows.
When a machine in a private network generates
a packet that has a destination outside as a private network,
the packet is transferred to a NAT router.
For example, this figure shows a packet with source IP
address 10.0.0.1, a private address.
When the packet leave the NAT box after translation,
it has a router-source IP address 198.60.42.12,
unregistered global IP address of the NAT box.
The NAT router maintains a table for
mapping packets from the private network into the Internet and back.
Each time a machine generates a packet destined for the Internet,
a new entry is created in a table in the NAT router.
The entry contains the private IP address of the machine,
say 192.168.0.10 as well as a TCP or UDP port number of the packet,
say X, in this example.
Another port number that is not already in
use is selected assigned to the given packet, say Y.
The NAT router then sends a packet into the Internet with a registry
that global IP address that is 128.100.10.15 in this example.
When the response packets arrive,
although they have been the same global IP address as the destination,
the port number is used to retrieve
the original private IP address and port number by looking at the table.
So packets can then be delivered to the appropriate machine.
In theory, one public IP address can support up
to 2^16 different private IP addresses by network address translation technique,
because a TCP/UDP port number has
16 bits so that it can be used for the table entries in NAT box.
But one has to consider the overhead of NAT operation and a runtime.
And one potential problem is that NAT is implementing it at its IP layer,
but it takes advantage of up
transport layer information using TCP/UDP port number for the lookup table.
This actually violates the OSI layer architecture.
That is, a higher layer utilizes
a service provided by the lower level but not vice versa.
This concludes today's. 

## IPv6

We discuss IPv6 in today's lesson.
IPv4 has played an essential role in the internet working for many years.
However, 32 bits of the IPv4 address
eventually cannot accommodate its explosive growth.
New version IPv6 was designed to interoperate with IPv4 since it
would take years to complete the transition from v4 to v6.
Two major changes from IPv4 to IPv6 a longer
address field and the simplified header format.
IPv6 uses 128 bits for addressing that can support 3.4x10 to the 36 hosts.
IPv6 also simplifies header format.
So as to speed to a processing of each packet header,
all fields are of fixed size in IPv6.
Let's take an overview of IPv4 and IPv6 comparison.
Both keep the version, IPv6 jumps header length, ID,
flags, offset and a header checksum.
IPv6 further replace the datagram length by payload length.
Protocol type by next header,
time to leave by Hop limit and type of service by traffic class.
It also created a new field, flow field.
The IPv6 header consists of a header and optional extension header.
The format of the basic header is shown in the figure.
So, traffic class is intended to support a differentiated of services.
The flow label field can be used to identify quality of service
requested by the packet.
The IPv6, a flow is defined as a sequence of packets
from particular source to a particular destination for
which source requires special handling by the intervening routers.
Payload length indicates the length of date excluding header
with 16 piece allocated to this field.
The payload at length is limited to 64K bytes, but it
is possible to send it larger payloads by using the option in the extension header.
To support extra functionalities that are not provided by the basic header,
IPv6 allows an arbitrary number of extension headers
to be placed between the basic header and the payload.
The extension headers are chained up by the next header field.
Extension headers act like options in IPv4, but are more efficient and flexible.
IPV6 allows a payload size of more than 64K bytes called
a Jumbo packet by using an extension header.
The use of larger payload size is promoted by high speed networks,
by bigger data applications and by super computing applications.
The figure shows the format of the extension header for
a packet with a Jumbo Payload.
The next header field identifies the type of header immediately
following this header.
The value 194 defines the Jumbo Payload option.
The payload lengths in the basic header must be set to zero.
The option lengths field specifies the size of the Jumbo Payload
lengths field in the bytes.
Finally, the 32-bit Jumbo Payload lengths field specifies
that payload size which can be as large as 4 gigabytes.
IPv6 allows only the source host to perform fragmentation.
Intermediate routers no longer perform fragmentations.
The rationale is to speed up routing under the intermediate routers.
If the packeting lengths is greater than the max of transfer unit,
MTU of the network, a router simply discards the packet and
it sends an SMP error message back to the source.
A source hold can find a minimal MTU along the path from the source
to the destination by performing a path MTU discovery procedure.
One disadvantage is that the path between a source and
destination must remain reasonably static.
So that as a path, MTU discovery doesn't make that updated information.
If a source was to fragment a packet, the source will include a fragment
extension header as shown in the figure for each fragment of the packet.
Like IPv4, IPv6 allows a soft host to specify the sequence of
routers to be visited up by a packet to reach the destination.
This option is defined by a routing extension header shown in this figure.
IPv6 addresses are divided into three categories.
Unicast addresses, multicast addresses and anycast addresses.
So, don't leave the decimal notation would have been right along when applied to IPv6
long addresses.
A more compact notation to use is hexadecimal notation.
Because IPv4 networks and hosts widely deployed, migration
issues need to be resolved to insure that the transition from IPv4 to IPv6 is small.
Current solutions are mainly based on the dual IP layer or
dual stack approach whereby both IPv4 and IPv6 functions are present.
Routers support both IPv4 and IPv6 protocols, and
can forward both types of packets.
When islands of IPv6 networks are separated by IPv4 networks,
one approach is to build a tunnel across an IPv4 network
connecting two IPv6 networks.
As shown you this figure, a tunnel is a path created between two nodes,
so that a tunnel appears as a single link to the users.
A tunnel is typically realized by encapsulating each user packet and
another packet that can be forwarded along the tunnel. 
