---
title: CN Final 考題大補帖
---
# 1. 
Try to describe the GO-Back-N(GBN) and Selective Repeat(SR) protocols?
Year 97, 98
## ANS
![](https://i.imgur.com/kbZ98ox.png)

# 2.
Draw the extended FSM descriptions of GBN sender and receiver?
Year 97, 98
## ANS
* Sender: 
![](https://i.imgur.com/Rwob5rx.png)
* Receiver
![](https://i.imgur.com/vtvcshI.png)

# 3. 
Try to describe the differences and the mechanisms of flow control and congestion control
Year 97, 98
## ANS
* flow control:
    receiver controls sender, so sender won’t overflow receiver’s buffer by transmitting too much, too fast.
    * receiver “advertises” free buffer space by including rwnd value in TCP header of receiver-to-sender segments
    * sender limits amount of unacked data to receiver’s rwnd value 
* congestion control
    Sender reduce sending speed to prevent congesting the network.
    * approach:sender increases transmission rate, probing for usable bandwidth, until loss occurs
    * AIMD, slow start

# 4. 
How to perform the network address translation(NAT)?
Year 97, 98
## ANS
* outgoing datagrams: replace (source IP address, port #) of every outgoing datagram to (NAT IP address, new port #)
* remember (in NAT translation table) every (source IP address,port #) to (NAT IP address, new port #) translation pair
* incoming datagrams: replace (NAT IP address, new port #) in dest fields of every incoming datagram with corresponding (source IP address, port #) stored in NAT table
# 5.
How to perform the tunneling to the transition from IPv4 to IPv6.
Year 97, 98
## ANS
IPv6 datagram carried as payload in IPv4 datagram among IPv4 router
# 6. 
It has been said that when IPv6 tunnels through IPv4 routers, IPv6 treats the IPv4 tunnels as link-layer protocols.
Do you agree with this statement? Why or why not?
Year 96
## ANS
Yes, because the entire IPv6 datagram(including header fields) is encapsulated in an IPv4 datagram

# 7. 
compare and contrast link-state and distance-vector routing algorithms
year 96,97,98
## ANS
Link state algorithms: Computes the least-cost path between source and destination using complete, global knowledge about the network.  

Distance-vector routing: The calculation of the least-cost path is carried out in an iterative, distributed manner. A node only knows the neighbor to which it should forward a packet in order to reach given destination along the least-cost path, and the cost of that path from itself to the destination.

# 8.
Consider the following plot of TCP window size as a function of time:
![](https://i.imgur.com/mt13Hp9.png)
1. What is the value of threshold at the 18th transmission round?
2. What is the value of threshold at the 24th transmission round?
3. Identify the intervals of time when TCP slow start is operating.
4. Assuming a packet loss is detected after the 26th round by the receipt of a triple duplicate ACK, what will be the values of the congestion-window size and of threshold?
5. After the 16th transmission round, is segment loss detected by a triple duplicate ACK or by a timeout?
6. After the 22th transmission round, is segment loss detected by a triple duplicate ACK or by a timeout?
7. Identify the intervals of time when TCP congestion avoidance is operating (AIMD)
8. What is the initial value of threshold at the first transmission round?
9. During what transmission round is the 70th segment sent?  
year 98
## ANS
1. 21
2. 13
3. 1-6, 23-26
4. threshold = 4, cwnd = 7
5. dupack. The threshold is set to half the value of the congestion window when packet loss is detected. When loss is detected during transmission round 16, the congestion windows size is 42. Hence the threshold is 21 during the 18th transmission round.
6. time out. After the 22nd transmission round, segment loss is detected due to timeout, and hence the congestion window size is set to 1 (remember that this means that TCP can send up to 1 MSS ).
7. 6-16, 17-22
8. 32
9. 7

# 9.
Suppose datagrams are limited to 2,500 bytes (including header) between source Host A and destination Host B. Assuming a 40-byte IP header, how many datagrams would be required to send an MP3 consisting of 3 million bytes?
year 97
## ANS
* TCP header is 20 bytes.
* Datagram can carry 2500 - 20(TCP header) - 40(IP header) = 2440 Bytes  
* $\lceil\frac{3 \times 10 ^ 6}{2440}\rceil =1230$
# 10.
1.
![](https://i.imgur.com/SUjOsvt.png)
year 96, 97
2. Consider the following network. With the indicated link costs, use Dijkstra’s shortest-path algorithm to compute the shortest path from X to all network nodes. Show how the algorithm works by computing a table similar to Table 4.3.
![](https://i.imgur.com/kI1rkzq.png)
year 98

## ANS
1.
* Dijkstra algorithm: 剛開始將起始點加入樹，依序選擇樹周圍，但權重最小的邊加入樹中。  
![](https://i.imgur.com/7vR4Sko.jpg)

2.
![](https://i.imgur.com/QZWQLT7.png)

# 11.
1. 
![](https://i.imgur.com/pMYnSKc.png)
year 96, 97
2. 
    Consider the network shown below, and assume that each node initially knows the costs to each of its neighbors. Consider the distance-vector algorithm and show the distance table entries at node z.
![](https://i.imgur.com/CxKufKm.png)
year 98
## ANS
1.
* Bellmen-Ford algorithm: 宣告一個distance陣列，剛開始除了起始點distance = 0之外，其餘設定為infinite，重複(node數量-1)次以下動作：對於每條邊(a,b)，distance[b] = min(distance[b], distance[a] + edge(a,b))

![](https://i.imgur.com/i4FoKUP.png)


2.
![](https://i.imgur.com/bhGSKIc.png)



# 12(Openflow data plane)
* 教授說會考
![](https://i.imgur.com/yMuG7pA.png)
## P19
*  Consider the SDN OpenFlow network shown in Figure 4.30 . Suppose that the desired forwarding behavior for datagrams arriving at s2 is as follows:
    * any datagrams arriving on input port 1 from hosts h5 or h6 that are destined to hosts h1 or h2 should be forwarded over output port 2;
    * any datagrams arriving on input port 2 from hosts h1 or h2 that are destined to hosts h5 or h6 should be forwarded over output port 1;
    * any arriving datagrams on input ports 1 or 2 and destined to hosts h3 or h4 should be delivered to the host specified;
    * hosts h3 and h4 should be able to send datagrams to each other.
* Specify the flow table entries in s2 that implement this forwarding behavior.
## P20
* Consider again the SDN OpenFlow network shown in Figure 4.30 . Suppose that the desired forwarding behavior for datagrams arriving from hosts h3 or h4 at s2 is as follows:
    * any datagrams arriving from host h3 and destined for h1, h2, h5 or h6 should be forwarded in a clockwise direction in the network;
    * any datagrams arriving from host h4 and destined for h1, h2, h5 or h6 should be forwarded in a counter-clockwise direction in the network.
* Specify the flow table entries in s2 that implement this forwarding behavior.
## P21 
* Consider again the scenario from P19 above. Give the flow tables entries at packet switches s1 and s3, such that any arriving datagrams with a source address of h3 or h4 are routed to the destination hosts specified in the destination address field in the IP datagram. (Hint: Your forwarding table rules should include the cases that an arriving datagram is destined for a directly attached host or should be forwarded to a neighboring router for eventual host delivery there.)
##  Ans
![](https://i.imgur.com/6WNSpN5.png)

###### tags: `Computer Network` `CSnote`