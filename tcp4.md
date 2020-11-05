## Mobile IP

Our today's class focus on Mobile IP Technique.
Mobile networking is becoming increasingly important as
portable devices as such as smartphones are becoming so prevalent.
The link between the portable device and as
a fixed and communication network is usually wireless.
So problem is IP address specifies point of attachment to the internet
and changing IP address at run time involves terminating all connections and sessions.
Here we look had a simple mobile IP solution where devices can change
point of attachment while retaining IP address and maintaining communications.
This figure illustrates Routing in Mobile IP that allows the portable devices called
a mobile hosts to roll from one area to
another while maintaining the communicating sessions.
One look common in Mobile IP that a mobile host must
continuously use its permanent IP address either as it roams to another area.
Otherwise, existing sessions will stop working and new sessions should be
started when a mobile host move to another area.
A host agent keeps track of location of each mobile host in its network.
Home agent periodically announce its presence.
It manages all mobile host in its home network that use the same address prefix.
If a mobile host is in the home network for example,
mobile host number one,
home agent forwards packets directly to the mobile host.
When a mobile host move to a foreign network for example,
mobile host number two,
the mobile host obtains a care-of-address from
the foreign agent and registers as its new address with its home agent.
So, Mobile IP routing are arranged as follows:
when a correspondent host want to send a packet to
a mobile host that transmits the standard IP packet with
its address as the source IP and the mobile host addresses as a destination IP.
This is illustrated as step one in the figure.
This packet will be intercepted by the mobile host home agent.
If the mobile host is located in the foreign network,
the home agent simply forwards a packet to its foreign agent.
This is illustrated as step two.
That foreign agent forwards a packet to the mobile host and
a mobile host sends packet to the correspondent host as usual,
as illustrated as the steps three.
So question is, how does a home agent send
a packet to the mobile host in a foreign network?
The problem is solved by providing
a tunnel between the home agent and as a foreign agent.
And implement here by encapsulating
each IP packet as a home agent was an outer IP address
containing the home agent address as
the source IP address and care-of address as a destination IP address.
When the foreign agent received the packet,
the foreign agent decapsulates the packet that are produced the original IP packet with
the correspondent host address as
a source IP address and mobile host address at the destination address.
The foreign agent can then deliver the packet to the mobile host.
Packets transmitted by their mobile host to the correspondent host typically use
a normal IP packet format with a mobile host addresss as
a source IP address and correspondent host address as destination IP address.
These packet follow the default route.
We can observe that there's a lot time traveled by the packet from
the correspondent host to the mobile host is typically
longer than that from the mobile host to the correspondent host.
Several proposals exist to improve this routing mechanism.
So, that the correspondent host may send a packet
directly to the care-of-address end point in subsequent exchange.
One solution is illustrated here.
When the home agent receives a packet from
a correspondent host then send to a mobile host as illustrated by step one.
It then tunnels packet to current care-of-address as before as illustrated by step 2A.
However, it also sends a binding message back to the correspondent host
containing the current care-of-address as illustrated by step 2B.
The correspondent host can save this information,
it is a fighting cache.
So, is that a future packet to the mobile host can be directly tunneled to
the care-of-address as illustrated by step four.
This concludes our lesson on mobile IP. 

## Multicast Routing

In today's lesson we discuss multicast routing and it's a foundation broadcast.
Previously, we discussed the many routing mechanisms that
assume a given source transmits its packets to a single destination.
But in some circumstances, such as teleconferencing,
a source may want to send its packets to multiple destinations simultaneously.
This calls for another type of routing called multicast.
As illustrated in the figure,
source S wants to transmit to jet destinations with multicast group G1.
Though you can send each copy of the packet separately
to each destination using conventional unicast routing,
a more efficient method would be to minimize the number of copies.
For example, when router one receives a packet from the source,
it copies a packet to routers two and five simultaneously.
Upon receipt of these packets router two forwards the packets to its local network.
And the router five copies the packets to routers seven and eight.
The packets will eventually be received by each intended destination.
There are many ways to generate a multicast tree.
One approach that is used in multicast backbone is called reverse-path multicasting.
The easiest way to understand a reverse-path multicasting is by
first considering a simpler approach called reverse-path broadcasting.
Which you use is the fact that as a set of shortest paths to
a node forms a shortest path tree that spans the network.
Assuming that each router already knows the current shortest path to a given destination,
the operation of reverse-path broadcasting is quite simple.
Upon receipt of a multicast packet,
a router further records the source address of the packet and the port it arrives on.
If the shortest path from the router back to the source is through the same port,
we call it parent port the packet arrives on.
The router forwards a packet to all other ports except as a one packet arrive on.
Otherwise that router drops a packet.
The advantage of this approach is that each packet is forwarded a router exactly once.
The basic assumption underlying
the algorithm is that is the shortest path from the source to
a given router must be the same as the shortest path from the router back to the source.
This assumption [inaudible] each link to be symmetric.
Let's see an example: the port over which the router expects to
receive multicast packets from a given source is referred to as a parent port.
The figure shows the spanning tree of shortest paths to
a node S and parent ports are shown in color red.
First, router one receive a packet on port one from
source S. Because the packet comes from the parent port,
the router copies the packet to all other ports.
Assume these packets reach routers two,
three, four, and five.
Router two computes the shortest path from intercept
to s and finds that parent port is one.
Due to the match it copies the packet as through to all other ports.
Similarly, routers three, four,
and five find and that as a packet arrives on the parent port,
as a result, each router copies a packet to its other ports as shown in the figure.
Note that the bidirectional link indicates that
each router forwards a packet to the other.
Next, let's assume that as the packets arrive at routers two, three, eight.
Because the router two receives the packet from port four which is not its parent port,
router two drops a packet.
Routers three, four, and five also drop the packets for the same reason.
Router six, however, finds that the parent port is port one.
So it copies a packet coming from router four to its other ports.
The packet that came from router five to router six is dropped.
Router seven and eight copies the packet that
came from router five and forward it to other ports.
The figure illustrates this process.
Please verify that as a packet will no longer be propagated after this point.
Note that although the hosts connected to
routers three and six belong to different multicast groups,
the packets for group G one are still forwarded by these routers.
Unnecessary bandwidth is wasted,
regardless of the multicast group.
This problem can be solved by having the router truncate its transmission to
the local network if none of the hosts
attached to the network belong to the multicast group.
This refinement is called truncated reverse-path broadcasting.
The Internet Group Management Protocol, IGMP,
allows a host to signal its multicast group membership to its attached router.
A multicast router periodically issues an IGMP query message,
to check whether there are hosts belonging to multicast groups.
Routers determine which multicast groups are associated with a certain port.
Routers only forward packets on ports that have hosts belonging to the multicast group.
Briefly speaking, reverse-path multicasting is
an enhancement of truncated reverse-path broadcasting.
But unlike truncated reverse-path broadcasting,
reverse-path multicasting forwards a multicast packet only
to a router that will lead it to a leaf router with group non-members.
To do so, it relies on IGMP to identify multicast group memberships. 

## OpenFlow, SDN, and NFV

In today class, we will do an introduction to Openflow, SDN, and NFV.
Openflow is an open standard that enables
us to run experimental and innovative protocols in production networks.
Openflow is added as a feature to commercial Ethernet switches,
routers, and wireless access points.
And it provides and standardize the tool to allow us to run
experiments without requiring vendors
to expose the internal workings of their network devices.
Today, Openflow is a standard communication interface defined between
the control and a forwarding layer of a Software-Defined-Network (SDN) architecture.
It's currently being implemented by
many vendors with Openflow enabled switch, now commercially available.
Openflow became common in 2010.
Its concept was first published in an ACM SIGCOMM 2008 paper,
and its version 1.1 was released in early 2011 as
a protocol for programming forwarding plane of a network switch or router.
Based on it, Open SDN was proposed in 2011.
All the views of SDN includes SDN via API model,
used by Cisco, which allows developers to
manipulate network devices using an extended API.
Also, VMware use SDN might overlays.
However, for this lesson we refer to only one view: the Open SDN.
In late 2012, the concept on Network Function Virtualization, NFV,
was defined, which is not our replacement for SDN,
but rather both SDN and NFV complement each other.
In a classical router or switch,
the datapath and the control path occur on the same device.
An Openflow switch separates these two functions.
The datapath portion still resides on the switch where
high level routing decisions are moved to a separate controller,
typically a standard server.
The Openflow switch and Controller
communicates via the Openflow protocol which defines messages.
The Openflow protocol is used as a communication path between the infrastructure layer,
consisting of routers and switches,
and the control layer,
which handles centralized intelligence for simplified provisioning,
optimized performance and granularity of policy management.
There are some general misconceptions: It is important
to point out that Openflow is not an SDN and vice versa.
There have been other misconceptions such as,
if SDN means standard southbound API,
centralization of control plane and a separation of control data plane.
All of these misconceptions back the question,
if Software-Defined Network is a mechanism.
Well, SDN is not a mechanism,
rather it is a framework to solve a set of problems implying many solutions,
while Openflow is an open API that
provides a standard interface for programming the data plane switch.
Software-Defined Network, SDN, is a new technology
that was designed to make a production network more agile and flexible.
Production networks are often quite astatic,
slow to change and dedicated to single services.
With software-defined networking we can create
a network that handles many different services in a dynamic fashion,
allowing us to consolidate multiple services into one common infrastructure.
It does this by using a centralized network control,
so separation of control logic that enables automation and the coordination of
network services via open programmatic interface which includes the cloud,
management and business applications.
The main advantages of SDN includes efficiency,
by optimizing existing applications,
services and infrastructure, scalability and innovation.
Now, developers can create and deliver new types of application,
and services and new business models.
The need of SDN is driven by several factors: visualization,
that remove the need to know where network resources are physically located,
resource cost, organization and so on.
Orchestration, that is the need to
control and manage thousands of devices with one command can be achieved.
Programmability, the ease of changing network behaviors without horrible upgrades.
Dynamic scaling that should be able to change size and quantity.
Automation, that requires minimal manual involvement in operation as cushion,
such as troubleshooting and resource provisioning.
Visibility, that allows resource monitoring on network connectivity.
Performance, that is due to traffic engineering,
capacity optimization, load balancing and the high utilization.
Multi-tenancy, that allows administration access of address, topology,
routing, security and service integration of load of balancer,
intrusion detection system and firewalls.
Network Function Virtualization is a consolidation of different network functions within
a virtual server rather than deploying different hardware for different network function.
As such, it decouples functions like a firewall or
encryption from dedicated hardware and move the function to virtual servers.
The term NFV refer to the strategy of virtualizing network function,
moving from separate pieces of hardware to software
running on virtual servers using standard hardware.
There are four major innovations of Network Function Virtualization,
which includes standard API between modules.
Network functions are implemented in virtual machines.
Network function modules that enhance
easy programmability and a software implementation of network.
We conclude our today lesson by summarizing the relationship between NFV and SDN.
For more information, please refer to additional readings. 

## Network Security Threats

Today's lesson discus network security threats on a security departments.
Combination of low-cost powerful computing and high-performance networks is
a two-edged sword, while new services and application are enabled.
Computer systems and
network become highly susceptible to a wide variety of security threats.
In particular, the internet and TCP/IP protocols were designed for
openness and intrusiveness, but they expose security concerns as well.
Network security involves countermeasures to protect computer systems
from intruders.
Typical measures include firewalls,
security protocols, security practices and so on.
Public packet switching networks,
such as the Internet traditionally hundreds of things are secure in sense
of providing high level of security for the information that is transmitted.
And these networks are increasingly used for commercial transactions.
They're need to provide security become critical.
Let's bravely reveal several representative threats.
What is eavesdropping?
Information transmitted over network is not secure, and
can be observed and recorded by eavesdroppers.
For example, using a packet sniffer,
information can be replayed in attempts to access server.
Client imposters attempt to gain unauthorized access to the server.
So to access bank account or database of personal records.
For example, in IP spoofing,
an imposter sends packets with false source IP address.
Our server imposter impersonates a legitimate server to gain sensitive
information from a client.
We have witnessed many denial of service attacks,
including distributed denial of service attacks.
In those scenarios an attack can flood a server with requests overloading
the server resources so as to result in denial of service to legitimate clients.
Distributed denial of service attack on a server involves
coordinated attack from multiple, usually hijacked, computers.
TCP SYN Flood is a type of distributed denial-of-service,
that exploits parts of the normal TCP three-way handshake,
to consume resources on a targeted server and render it unresponsive.
Essentially, we're seeing Flood DDoS.
The offender sends TCP connection request
faster than the target in the machine can process, causing network saturation.
Procedure cause a TCP streetway,
hind-shaped procedure, as shown in the left figure.
In a SYN Flood attack, and
shown in the right figure, the attacker sends a repeated same packet
to every port on the targeted server over using a fake IP address.
The server unaware of the attack
receive multiple apparently legitimate requests to establish a communication
in response to each attempt with the same ACK packet from each open port.
The attacker doesn't send the expected ACK or if the IP address is spoofed,
never receive a SYN ACK in the first place.
The server under attack will wait for
acknowledgement of it's SYN to ACK packet for some time.
During this time, the server cannot cross bounds a connection
by sending an RST packet and the connection stays open.
Before the connection can time out, another SYN packet will arrive.
This leaves an increasingly larger number of connections half open.
And indeed SYN flood attacks are also referred to as half open attacks.
Eventually, as the server connection overflow table fill.
Server to legitimate clients, will be denied and
the server may even not function or crash.
While the classic SYN flood described above tries to exhaust network parts.
SYN packets can also be used DDOS attacks
that try to clog your pipes with fake packets to achieve network saturation.
The type of packet is not important.
Still, SYN packets are often used
because they are the least likely to be rejected by default.
An imposter manages to place itself as a man in the middle,
convincing the server that it is the legitimate client and
the legitimate client that it is the legitimate server.
A client becomes infected with malicious code.
For example, when opening attachments in email message, or
executing code from bulletin boards or other sources.
Virus is code that when executed, inserts itself in other programs.
Worms is a code that install copies of themselves in
other machines attached to the network.
There are many variations of malicious code.
These threats give rise to one or more of the following security requirements for
information that is transmitted over a network.
Privacy, the information should be readable only by the intended recipient.
Integrity, the recipient of information
should confirm that a message hasn't been altered during transmission.
Authentication, it is possible to verify that sender or
receiver is who he claims to be.
Non-repudiation sender cannot deny having sent
a given message and availability of information and service.
Counter measures for secure communication channels include encryption,
cryptographic checksum and hash authentication and digital signature.
Counter measures for securing borders include firewalls, virus checking,
intrusion detection, authentication and access control.
Interest the readers please take another specialization in network and
system security.
This concludes today's lesson. 
