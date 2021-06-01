---
title: CN Chapter 3
---
# Chapter 3: TRANSPORT LAYER
## Introduction and Transport layer services
* Transport-layer is an **end-to-end**(point-to-point) layer used to deliver messages.
* From an application process perspective, it views the communication as if the hosts running the processes are connected directly.
* Transport-layer protocols are **implemented on end-systems** not on network routers.
* On the sending side, transport-layer converts application-layer messages into transport-layer packets(a.k.a. transport-layer **segments**). This is done by breaking messages into smaller chunks and adding a transport-layer header. The segments will be passed to the network-layer to be encapsulated within a network-layer packet(datagram) and sent to destination.
* On the receiving side, The network-layer extracts the segments from the datagram and passes it to the transport-layer. The transport layer then processes the received segments making it available to the application-layer.
### Relationship between transport and network layer
* Transport-layer is just above the network-layer in the protocol.
* Transport-layer protocol provides logical communication between **processes** on  different hosts.
* Network-layer protocol provides logical communication between **hosts**.
### Overview of the transport layer in the internet
* IP service model is a **best-effort delivery service**. It tries its best but could not guarantee segment delivery.
* Extending host-to-host delivery into process-to-process delivery is called **transport-layer multiplexing** and **demultiplexing**.
* UDP only provides process-to-process delivering and error checking. Is unreliable.
* TCP provides reliable data transfer and congestion control.
* Congestion control is done by regulating the rate of the sending sides of TCP connections.
## Multiplexing And Demultiplexing
* Segments knows their source port number and destination source number.

### [IMPORTANT]Python codes
Create socket e.g. 
`sock = socket(AF_INET,SOCK_DGRAM)`
* `AF_INET` means the ip assigned to the socket will be IPv4. For IPv6 use `AF_INET6`.
* `SOCK_DGRAM` is for UDP connection. `SOCK_STREAM` is for TCP connection.

Bind a socket with a port(Server side OPs)
`sock.bind(('',19156))`
* 19156 is the port binded.

Connect a socket to a server(Client side OPs)
`sock.connect((servername,12000))`
* 12000 is the port to connect on server.

Accept a connection(Server side OPs)
`sock,addr = sock.accept()`
## Connectionless transport: UDP
* Best effort service. 
Means UDP segments can be lost or delivered out of order.
* Connectionless
No handshaking.
Each UDP segment is handled independently.
* UDP use:
  Loss tolerant, rate sensitive situation. e.g. Internet phone, video conferencing
### UDP: segment header
![](https://i.imgur.com/XWRiOnq.png)
### UDP Checksum
* Provides error detection.
#### Sender:
* Treats all contents as sequence of 16-bit integers.
* checksum is the sum of segment contents in one's complement(i.e. turn all 1s into 0s, turn all os into 1's).
* Checksum is put into the UDP segement header.
#### Receiver:
* Computes the checksum.
* If the computed checksum is equal to the checksum in the segment header. There might be no errors.
* if not, error exists.
## [IMPORTANT]Principles of Reliable data transfer(rdt)
* **懶得看英文可以看[這個](https://blog.csdn.net/xlinsist/article/details/75950327)**，30分鐘帶你搞懂兩個星期的課。

* Terms:
`rdt_send()` : Send side in RDT.
`rdt_rcv()`  : Receive side in RDT.
`deliver_data()` : Deliver data to upper layer.
`make_pkt()`  : Creates a packet containing data.
`extract()`  : Extracts the packet.
#### Service model
![](https://i.imgur.com/ZaFVJoG.png)

**RDT IS IMPORTANT AND WILL ALWAYS APPEAR ON TESTS!!!**
96年 40%, 97年 40%, 100年 30%

### rdt1.0
* Regard transmission as ideal. No loss of packets, bit error, timeout will happen.

![](https://i.imgur.com/HgjGrNf.png)

### rdt2.0
* Takes bit errors into consideration.
* Use checksum to detect errors

How to recover from errors?
* Acknowledgements(**ACKs**): Reciever tells the sender the packet is correct.
* Negative Acknowledgements(**NAKs**):
Receiver tells the sender the packet is incorrect.

If a packet is corrupted. the receiver can use NAKs to request the sender to retransmit.

![](https://i.imgur.com/fcJ8Q7P.png)

If the ACK/NAK is corrupted, this will fail. How to fix this?
* Choice 1 : Add checksum bits to recover from bit errors, this solves the problem but does not lose it.
* Choice 2: When the receiver receives a corrupted ACK/NAK retransmit. This will introduce a new problem, duplicate packets.

#### Solution: Stop and wait:
Sender sends a packet then wait for respond.
* Sender adds a sequence(seq) number to packet. (0 or 1)
By doing this the sender can know whether the ACK or NAK is associated with the newest packet sent.

rtd2.1 sender:
![](https://i.imgur.com/jle8Fg2.png)

rtd2.1 receiver:
![](https://i.imgur.com/yfBzOzK.gif)


#### rdt2.2
rdt2.2 functions like rdt2.1 but without NAK.
* Receive side sends ACK with the last correct packet's sequence number.
* If the sender received an ACK whose sequence number is not equal to the most recent sequence number, it is a NAK.
* Sender

![](https://i.imgur.com/vB4EvyD.gif)

* Receiver

![](https://i.imgur.com/xvqLG7i.gif)


### rdt3.0
Takes bit lose and lose packets into consideration.

Difference with rdt2.2:
* Sender waits reasonable amount of time for ACK. 
* Sender retransmits if no ACK received in time.(countdown timer)

Sender:
![](https://i.imgur.com/KZVnEp4.gif)

Receiver:
![](https://i.imgur.com/2k5hqSJ.png)

* Because packet sequence numbers alternate between 0 and 1. rtd3.0 is also known as alternating-bit protocol.

Downside of rdt3.0
* slow

### Pipelined protocols
Pipelining:
Sender starts to send subsequent packets before ACK/NAK comes back.
Two generic forms: Go-back-N, selective repeat. 
#### Go-back-N(GBN)
##### Sender
* Sender can have up to N packets in pipeline.
* k-bit sequence number.
* Sender has timer for oldest unACKed packet. Retransmit all unACKed packets if time expires.

![](https://i.imgur.com/4R2GLbn.png)
##### receiver
* receiver send cumulative ACK.(i.e. doesn't ACK if there's a gap)
* ACKs the highest in-order sequence number only.
* Discard out-of-order packet

![](https://i.imgur.com/7hQ8MIp.png)
#### Selective receive(SR)
##### Sender
* Sender can have up to N packets in pipeline.
* Sender has timer for each unACKed packet.If timeout happens ,resend the packet.

##### receiver
* receiver sends individual ACKs for each packets.
* if Received in-order packet, deliver it.
* if Received out-of-order packet,put it into buffer.
## connection-oriented transport: TCP
#### Overview:
* point-to-point
* reliable ,in-order byte stream
* Full duplex(bidirectional)
* Connection-oriented. Needs handshaking to init sender and receiver.
* Flow controlled. Sender will not overwhelm receiver.

TCP header: 
![](https://i.imgur.com/V2SlHWw.png)
sequence number:
* Byte stream number of the first byte in segment.

acknowledgement number:
* Is the sequence number of the next segment.
### Round-Trip Time estimation and timeout

#### How to set TCP time out value?
* Longer than round trip time (RTT). But RTT isn't stable.
* too short: Premature timeout.
* too long: slow reaction to segment loss

#### How to estimate RTT? 
* SampleRTT: measure time until ACK received.
* Because RTT isn't stable, use average of recent transmissions(EstimatedRTT).

$ExacEstimatedRTT = (1- α)\times EstimatedRTT + α\times SampleRTT$
* α is typically 0.125
### Reliable data transfer
#### TCP sender
![](https://i.imgur.com/PPF72Rq.png)

#### TCP fast transmit
* If sender receives 3 ACKs for same data, resend unACKed segment with smallest sequence number. (A segment is likely lost)
### Flow control
* Receiver tells the sender how much free buffer space it has. The limits amount of unACked data according to free space left.
### Connection management
#### starting a connection
Handshake:
* Agree to connection
* Agree on connection parameters.

2-way handshake sometimes doesn't
work. Three way handshake is preferred.

Three way handshake:
![](https://i.imgur.com/s8FZ3xr.png)

#### Closing a connection
* Send FIN bit = 1.
* Respond to FIN with ACK.

## Principles  of congestion control
Congestion:
* Too many sources sending too much data too fast for the network to handle.
* Manifestations: Lost packets, long delays.
#### Ideal scenario
known loss: packets can be lost on route. Ideally, sender only resends if packet is known to be lost
#### Realistic scenario
duplicates: Sender times out prematurely , two copies of packet is delivered.
#### cost of congestion: 
* More things(copies of packets) has to be sent.
* multiple copies of packets are sent across the network, leading to more congestion.

## TCP congestion control
Principles:
* Lost segment implies that congestion is happening, TCP sender's rate should reduce.
* An ACKed segment means network is delivering data well, sender's rate can be increased.
* Bandwidth probing. Transmission rate should be as fast as possible near to congestion.
#### AIMD(Additive Increase, Multiplicative Decrease)
* Saw tooth behavior
* approach: sender increases transmission rate (window size), probing for usable bandwidth, until loss occurs
1. additive increase: increase cwnd by 1 MSS(Maximum segment size) every RTT until loss detected
2. multiplicative decrease: cut cwnd in half after loss
#### TCP Slow Start
* Initial rate is low but ramps up exponentially fast.
    * initially cwnd = 1 MSS
    * double cwnd every RTT
    * done by incrementing cwnd for every ACK received
* loss is indicated by timeout. if occurs, reduce to initial rate then grows exponentially to threshold, the grows linearly.
    * Threshold is half the rate of timeout.
* Loss is indicated by 3 ACKs: TCP Reno.
    * cwnd is cut in half window then grows linearly
* TCP Tahoe always sets cwnd to 1 (timeout or 3 duplicate acks)
#### Fairness
* With the strategy mentioned in **TCP Slow Start**, multiple competing sessions will have equal bandwidth share.
##### Fairness and UDP
* Multimedia apps often do not use TCP. Do not want rate throttled by congestion control
* Use UDP to send audio/video at constant rate, tolerate packet loss.
#### Explicit congestion Notification
##### network-assisted congestion control
* Two bits in IP Header marked by network router to indicate congestion.
* Congestion indication is carried to receiving host.
* Receiver notifies the sender that congestion is occurring. 

# END
###### tags: `Computer Network` `CSnote`