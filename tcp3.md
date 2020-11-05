## UDP and TCP

Starting today, we will take a deeper look at a two transporter layer protocols,
UDP and TCP that are built upon the best effort IP service.
We will focus more on the TCP.
UDP is unreliable and connectionless.
It is a very simple protocol that provides only two additional services beyond IP,
de-multiplexing and error checking on data.
IP knows how to deliver a package to a host.
UDP adds a mechanism that distinguish among multiple applications and has a host.
Connectionless means there is no handshaking and no stated information.
Therefore the protocol is of low overhead.
By UDP datagrams can be lost or out of control.
There is no flow control,
no error control and then no congestion control.
The format of the UDP datagram is shown in the figure.
The destination port allows the UDP module to
de-multiplex datagrams to the correct application in the host.
The source port identifies
the particular application in the source host to receive replies.
Porter numbering has set of rules,
for example from 0 to 255 are reserved for well-known ports.
This diagram illustrates the de-multiplexing process.
All UDP datagrams arrive into IP address B
and destination port number N are delivered to the same process.
Source port number is not used in de-multiplexing.
The UDP checksum field detects end-to-end errors in datagram.
It covers a so-called the pseudo header followed up by the UDP datagram.
The pseudo header includes the IP addresses in order to detect misdelivery.
UDP receiver recalculates the checksum and
silently discards the datagram if error is detected.
By silently, it means no error message is generated.
The use of UDP checksums is optional.
The hosts are required to have checksum enabled.
The transmission control protocol TCP provides us connection oriented,
reliable, in a sequence byte-stream service.
It enables error control,
flow control and the congestion control mechanisms.
It has high overhead but most applications use TCP because of the reliability.
A TCP connection is uniquely identified by four factors,
the sender IP address and phone number,
and the destination IP address and phone number.
And any sytem can then support a multiple, simultaneously TCP connections.
TCP doesn't presume message boundaries and treats
the data it receive from the application layer as a byte-stream.
It groups the bytes into a segments and transmit segments as convenient for efficiency.
For example application writes 45 bytes,
15 bytes and 20 bytes to that TCP circuit.
The transporter layer may split,
combine the information and pack it into segments in
the way it finds most appropriate for transmitting over the underlying networks.
In this example, it may send two segments each of 40 bytes to the connection.
Error detection and retransmissions are enforced in TCP.
Please refer to an earlier lesson on TCP reliable stream service for more information.
TCP flow control function is implemented as well and
advertise the window field in the TCP segment header.
Segments that travel in the reverse direction contains advertized window size that
informs the transmitter the number of bytes
that can be currently accommodated in the receiver buffer.
This figure shows the format of the TCP segment.
The header consists of a fixed part plus a variable side optional field.
By padding the length of the header must be in multiples of 32-bit words
Minimal header length is 20 and the maximum header length is 60 bytes.
Header length specifies the length of the TCP header in 32-bit words.
This information allows the receiver to know the beginning of
the data area because options field is variable length.
The 16-bit window size field
specifies the number of bytes the sender is willing to accept.
This field can be used to control the flow of data and congestion.
Sender will accept bytes with sequence number from ACK to ACK+ plus window.
The TCP checksum calculation procedure is similar to that used to compute an IP checksum.
It calculates the checksum for the TCP pseudo header and data segment.
This ensures the receiver that the segment has reached
the correct destination host and port and the prototype is correct.
Note that a pseudo header created by
source and destination hosts during the checksum state is not actually transmitted.
The TCP pseudo header has similar format as that of UDP this concludes today's lesson. 


## TCP Three-way Handshake

In today's class, we discuss two important fields in TCP header,
the sequence number and acknowledgement number,
and how they are used for TCP three-way handshake.
As TCP was built upon the best effort IP,
it is possible for older segments from previous connections to arrive at the receiver,
complicating the task of eliminating duplicate assignments.
TCP deals with this problem by using
a 32 bit long sequence number and by
establishing randomly selected initial sequence numbers during collection set up.
At any given time,
your receiver is accepting sequencing number from a much smaller window.
So the likelihood of accepting a very old message is very low.
Further, TCP enforce a timeout period at
the end of each connection called maximum segment lifetime,
to allow the network to clear old segments from the network.
The maximum segment lifetime is usually two minutes,
but it is a round trip delay dependent.
The TCP sequence number identifies the position of
the first byte of this segment in the sender's byte stream,
the sequence number reps back to zero after two powers 32 bytes data transferred.
Note that TCP identifies a sequence number for each byte.
For example, if the sequence number is 100 and the data area contains 5 bytes,
the next time this TCP sends a segment,
the sequence number will be 105.
The initial sequence number,
ISN is selected during connection setup when the flag bit SYN is set one,
the sequence number of the first byte of data for
this byte of stream will be ISN plus one.
It is important to note that a TCP connection is 40 plex,
so that at each point independently maintains its own sequence number.
The acknowledgement number identifies a sequence number of
the next data byte that the sender expects to receive.
This field also indicates that the sender has successfully received all prior data.
It is valid only if ACK fag bit is set.
In TCP header, there are six control bits.
The ACK bit is to set as acknowledgement.
If RST bit is set,
it tells the receiving TCP module to abort the connection.
SYN bit is to request a new connection,
FIN bit is to tell the receiver that the sender doesn't have more data to send.
The sender can still receive data from
the other direction and here it will receive a second from the FIN bit set.
Before any host can send data,
a connection must be established.
TCP establish the connection using a three-way handshake protocol as shown in the figure.
The handshake is described in the following three steps.
In the first step,
host A randomly generates an initial sequence number
x and a sends a connection request to a host B by setting the sync bit.
The host A also registers its initial sequence number to use.
In the second step,
host B acknowledges the request by setting that ACK bit,
and indicating the expected byte to receive,
that is, ACK number it is x plus one.
The pathway is needed because acknowledgement consumes one sequence number.
At the same time,
host B also randomly generates an initial sequence number Y from its side,
sets as a SYN bit and registered its initial sequence number to use.
In the second step, host A acknowledges the request from
B by setting the ACK bit and computes the next data byte to receive.
In this case, ACK number is y plus one.
Note that the sequence number from this connection is x plus one.
On receipt at the host B,
the connection is established.
If during a connection establishment interface,
one of the host decides to refuse a connection request,
it will send a reset segment.
By setting the IST bit because the TCP segment can be delayed, lost and duplicated.
The initial sequence number should be different each time a host requests a connection.
To see why, consider a case that a host always uses
the same initial sequence number n as shown in the figure.
Of the connection established,
at the latest segment from the previous connection arrives.
Host B accepts this segment,
since the sequence number turns out to be legal.
If the segment from the current connection arrives later,
it will be rejected by host B thinking that the second one is a duplicate.
Therefore host B cannot distinguish a delayed segment from the new one.
The three-way handshake protocol can ensure
that both end points agree on their initial sequence numbers.
TCP provides for a graceful close that involves
an independent termination of each direction of the connection.
That TCP entity completes transmission of
its data and upon receiving acknowledgment from the receiver.
It assures a segment with the FIN bit set.
Upon receiving a FIN segment,
the TCP entity informs its application that
the other entity has terminated its transmission of data.
For example, in this figure,
the TCP entity in host A,
terminates its transmission by issuing a FIN segment.
Host B sends an acknowledgment to act as a receipt of the FIN segment from A.
Note that the FIN segment uses one byte,
so the acknowledgement number is 5,087 in this example.
After B receives the FIN segment,
the direction of the flow from B to A is still open.
The TCP in host A enters the time-wait state for graceful close.
Usually for true maximum segment alines.
This concludes today's lesson.

## TCP Flow Control and Data Transfer

Today we discuss TCP flow control and data transfer.
After our TCP connection is established, by three way hand shake procedure,
to provide a reliable data transfer, TCP uses a selective repeat ARQ protocol,
with positive acknowledgement implemented by a sliding window.
The differences here is that the window slides on a byte basis
instead of per packet basis.
TCP can also apply flow control over a connection
by dynamically advertising the window size.
But let's first revisit a connection establishment
in the context of a client server application that will use TCP service.
Let the client reside in Host A, and a server in Host B.
This figure shows that the server must first carry out a passive
open to indicate to TCP that it is willing to accept connections.
When using BSD sockets, a passive open
is performed by the core sockets, bind, listen, and accept.
When client A wish to initiate a session, it performs an active open.
This step involves making a socket call at a time t1 and
a connection call at a time t2.
So that initiates the TCP connection.
This action causes the kind of TCP module to initiate the three way handshake.
When the server TCP receives the first sync connection,
it returns a sentiment with ACK and its own sync number.
When the client TCP receives this ACK,
it connects call returns at a time t3, and client sends an ACK.
Upon receiving the ACK, accept call returns at time t4 in the server.
And the server is ready to read data.
The client and the server can then request and reply message by write and recalls.
This figure illustrates an sample of TCP flow control and data transfer.
At time t0, the TCP module in host B advertised a window size of 2,048 bytes,
and expected the next byte received to have a sequence number 3,000.
The advertised window size allows host A to transmit
up to 2,048 bytes of unacknowledged data.
At time t1, TCP module A only has 1,024 bytes to transmit.
So it transmits all the data starting with sequence number 2000.
The TCP module at A also advertise its own window size,
let's say 1,024 bytes, to host B, and
the next byte is expected to have a sequence number 1.
When the segment is received, host B choose to delay the acknowledgement
in the hope, that acknowledgement may get a free ride with data.
Meanwhile, at a time t2,
Host A has another one solved in 24 bytes of data and then it transmits.
After the transmission, Host A's sending window closed completely.
It is not allowed to transmit any more data until an acknowledgment comes back.
At time t3, Host B has 128 bytes of data to transmit.
And also wants to acknowledge the first two segments of data from Host A.
Host B can simply piggyback acknowledgement by specifying the ACK
number, 4008, to the data segment.
At this time, Host B also finds it can allocate only 512 bytes of
receiver buffer space, due to the buffer competition from other connections.
So it shrinks the advertised window from 2048 to 512 bytes.
When Host A receives the segment, it changes the send window to 512 bytes.
If at time t4, Host A has 2048 bytes of data
to transmit, it will only transmit 512 bytes.
We see that the window advertisement controls the flow of data
from the sender to the receiver.
And it prevents the receiver buffer from overflow.
The initial sequence number is used to protect against segments from
previous connections.
Then it may circulate in the network and arrive at a much later time.
TCP uses a local clock to select the initial sequence number.
Time to clock to go through a full cycle should be greater than
the maximum lifetime of a segment, which is usually 120 seconds.
But the high bandwidth links pose a problem.
Let's see how long it takes to wrap around the sequence numbers space
using our high speed transmission line.
The 32 bit sequence number wraps around when 2 power 32 bytes data have been sent.
But at 1 gigabit per second transmission line,
the sequence number may wrap around in just 34 seconds,
which is smaller than the maximum segment life time.
And that means new segments could mix up with old segments.
When the timestamp option is used, the sending TCP can insert another 32 bit
timestamp into a 4 byte field, in the header of each segment it transmits.
By combining the 32 bit timestamp with a 32 bit sequence number, we
actually can obtain our 64 sequence number to deal with this wraparound problem.
This concludes our lesson today. 

## TCP Congestion Control

We focus on TCP Congestion Control in today's lesson.
TCP protocol use an advertised window
to ensure that receiver buffer will not overflow.
However, buffers at immediate routers may still overflow.
As the figure shows, congestion occurs when the total
arrival rate from all packet flows exceeds the outgoing
bandwidth of the router over a sustained period of time.
During congestion, the buffer at the router's multiplexer will fill and
the packets may be lost.
In general, there are three phase in the traffic load.
The first one is called light traffic, where the total arrival rate
at a router is far smaller than its outgoing length of bandwidth.
Incoming packets experience low delay.
The second phase is knee stage.
As a total arrival rate keeps increasing, it approached the knee point that
it is total arrival rate at a router is close to the outgoing length of bandwidth.
Packets experience increase in delay and the total slope begins to saturate.
The surface is congestion collapse when the total arrival rate is
greater than other outgoing length of bandwidth.
Packets experience a larger delay and loss.
Effective throughput drops significantly.
If the TCP senders are too aggressive by sending too many packets,
the network may experience congestion.
But if the TCP senders are too conservative,
the network will be under utilized.
Ideally, the objective of TCP congestion control is to have each sender transmit
just the right amount data to keep the network saturated but not overloaded.
TCP protocol defines a congestion window,
which specifies the maximum number of bytes that a TCP sender is
allowed to transmit without triggering congestion.
In TCP header, this effective window is the minimum of
the congestion window and advertised window.
But the problem is the sender doesn't know what its fair
share of available bandwidth should be.
The TCP solution is probe and
adapt dynamically to available network boundaries.
Ideally, sending rate stabilize near the optimal point.
How does the TCP congestion algorithm attack a congestion window
dynamically according to the current status of the network?
The rationale is that in light traffic, each segment should be
acknowledged quickly so the sender can increase congestion window quickly.
Near the knee point, segment acknowledgements arrive, but more slowly.
So senders should slow down increase in congestion window.
When congestion detected, segments encounter larger delay,
so retransmission timeouts occur.
And the segments are dropped in router buffers,
resulting in duplicate acknowledgements.
The sender should reduce transmission rate, then probe again.
Accordingly, the operation of the TCP
congestion control can be divided into three phase.
The first one is called a slow start,
that is accomplished by first setting the congestion window to a small value.
Usually just one segment.
Each time the sender receive an acknowledgement from the receiver
before it time out, sender increase congestion window by one segment.
Therefore, after sending the first segment,
if the sender receive an acknowledgement before timeout,
the congestion window is increased up to two segments.
Later, if these two segments acknowledge it,
the congestion window is increased to four.
So as shown in the figure, actually the congestion window size
grows exponentially during the slow start phase.
The rationale for exponential growth is it needs to fill the pipe as
quickly as possible to utilize network resource maximally.
After a certain point, it may be unwise to keep increasing
the congestion window exponentially, since overshoot can be significant.
The algorithm progressively sets a congestion threshold.
When congestion window size is greater than the threshold,
slow start phrase ends.
On phase two, congestion avoidance takes over.
It'll increase congestion window linearly by one segment per round-trip-time.
The congestion window stops increasing when TCP detects network
congestion due to timeout or receipt of duplicate acknowledgement.
Algorithm enters the surface congestion and sets the congestion threshold to
one-half of the current congestion window for probing the link bandwidth next time.
So it aggressively sets the congestion window back to one segment.
And it restarts using the slow start technique.
The figure shows the dynamics of the congestion window as time progresses.
We can observe that initial congestion threshold was set to 16 segments.
And later,
it got cut to half of the congestion window when the congestion detected.
When the congestion was not as severe, cutting the congestion
window's size back to one segment might be too aggressive.
Indeed, if only one segment is dropped during transmission,
the TCP sender can recover more quickly.
The reason is that subsequent segments trigger the TCP receiver to
transmit duplicate acknowledgements, as shown in the figure.
And these triggered acknowledgements usually arrive at the TCP
center before the retransmission timer expires.
When the TCP center receives the three duplicate acknowledgements, it
performs faster to transmit by immediately retransmitting the last segment.
The center then performs fast recovery by setting the congestion threshold,
as explained earlier.
But setting the congestion window size to the congestion threshold
plus three segments, instead of cutting back to just one segment.
The algorithm then remains in congestion avoidance phase.
This figure shows the dynamics of the congestion window as time progresses.
So in absence of time-outs,
the congestion window size will oscillate around as the optimal value.
This concludes today's lesson. 

