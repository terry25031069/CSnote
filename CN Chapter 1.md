---
title: CN Chapter 1
---
# Chapter 1: Introduction
## 前言
老師syllabus的配分都是寫開心的，實際上配分沒人知道。
108學年度電腦網路配分：作業ch1-2(16%)、作業ch3-5(12%)、期中期末(30% * 2=60%)、程式小作業(8%)、出席(4%，感謝ㄨㄏㄈㄧ)
107學年度電腦網路配分：作業ch1-2(10%)、作業ch3-5(10%)、期中期末(30% * 2=60%)、程式小作業(10%)、出席(10%)

★109學年開始，陳裕賢已經擺明要跟學生懟著幹了。期中考古題除了必考的FSM和Python程式碼外完全不一樣，有人在導生聚反應考太難他也只是說想要換種(跟考古題不一樣)的方式考。甚至助教改鬆，他還重改扣分。
考試內容均為講義上的題目，每個圖都要記得看，上課說會考的一定會考，上課輕輕帶過的也會有可能考。講義一定要讀熟。109-2期中考題與作業 **完全沒有任何關聯** ，請以PPT講義上的內容為準備方向。

~~這門課的準備方式：請將資工人社群裡面老到爆炸的考古寫過一次，當然這邊已經有學長將社群內的考古[期中](/XDS_OcFJSl-zV2XrC6uIyQ)[期末](/bnYwDPdTQri3M_6KYAVr6A)聯集起來變成大補帖，所以看大補帖就好，然後作業請全部搞懂，強烈建議程式小作業在期中考之前寫完，然後請想辦法把程式碼背下來。~~

~~由於這份筆記是講義向的，不會僅包含考點，會連著講義的其餘非考點一起寫進去，所以markdown裡面會考出來的部分會用**考點**表示。~~

期中考點：RDT(1.0, 2.0, 2.1, 3.0)FSM圖跟原理, TCP、UDP的Client、Server端的Python code ← 這個還是會考，還是要背，算送分題
期末考點：Go-Back-N, congestion control, Openflow, 網路拓樸演算法(Bellmen-Ford, Dijkstra)

## Network edge
### Digital subscriber line(DSL)
* 利用電話線路的未使用頻段載入數位訊號，以提供資料通訊
* data goes to Internet, voice goes to telephone net
### Cable network 
* FDM: 頻道用頻寬做區隔
* fiber attaches homes to ISP router
* homes share access network to cable headend
* unlike DSL, which has dedicated access to central office
### Enterprise access networks(Ethernet, 乙太網)
* typically used in companies, universities, etc.
* today, end systems typically connect into Ethernet switch
### Wireless access networks
#### wireless LANs(local area network, e.g. WiFi)
* within building(short distance)
* protocol: IEEE 802.11 a/b/g/n/ac/ax
#### wide-area wireless access
* provided by telco(cellular) operator
* 3G, 4G:LTE
### Host:sends packets of data
* message break into L-bit packets
* transmits packet into access network at transmission rate R
* link transmission rate, aka link capacity or link bandwidth
* packet transmission delay = time needed to transmit L bit packet into link = L(bits)/R(bits/second)
### Physical media 
* bit: propagates(傳播) between transmitter/receiver pairs
* physical link: what lies between transmitter and receiver
* guided/unguided media: solid media: copper(銅),fiber(光纖)/ signal: radio 
* twisted pair(TP, 雙絞線): CAT(category)-5,CAT-6
## Network core
### Packet switching 
* definition: hosts break application-layer messages into packets
* take L/R seconds to transmit(push out) L-bit packet into link at R bps(bit per second)
* store and forward: entire packet must arrive at router before it can be transmitted on next link
* end-end delay = 2L/R(assuming zero propagation delay)
### Packet switching: queueing delay, loss
if arrival rate(in bits) to link exceeds transmission rate of line for a period of time:
* packet will queue, wait to be transmitted on link
* packet can be dropped(lost) if memory(buffer) fills up
### Two key network-core functions
* routing: determines source(src)-destination(dst) route taken by packets
* forwarding: move packets from router's input to appropriate router output
### Alternative core: circult switching
* end-end resources allocated to the reservation for "call" between src and dst
* dedicated resourse, circuit-like performance
* circuit segment idle if not used by call
* commonly used in traditional telephone networks
### packet switching versus circuit switching
* Q: How did we get value 0.0004?
* A: $0.0004 =\displaystyle\sum_{i=11}^{35}\binom{35}{i}(0.9)^{35-i}(0.1)^i$
* Is packet switching a "slam-dunk" winner?
* pros: great for bursty data, resource sharing, simpler, no call setup
* cons: excessive congestion(壅塞) possible: packet delay and loss, protocol needed for reliable data transfer, congestion control
* Q: How to provide circuit-like behavior?
* A: bandwidth guarantees needed for audio/video apps, but still an unsolved problem (Chapter 7)
### Internet structure: networks of networks
* tier-1 commercial ISPs(e.g. Level 3, Sprint, AT&T, NTT), national and international coverage
* content provider network(e.g. Google): private network that connects it data center to Internet, often bypassing tier-1 or regional ISPs
## Delay, loss, throughput in networks
### How do loss and delay occur?(考點)
* packet arrival rate to link(temporarily) exceed output link capacity
* if free(available) buffer, then packets will arrive, or the packets drop(loss)
* d_proc: nodal processing: check bit errors, determine output link, typically < msec
* d_queue: queueing delay: time waiting at output link for transmission, depends on level of router.
* d_trans: transmission delay: L(bits)/R(transmission rate, bits/second)
* d_prop: propagation delay: d means length of physical link, and s means propagation speed(about 2/3 of light speed), d_prop = d/s
* d_nodal = d_proc + d_queue + d_trans + d_prop
* 因為 d_proc跟d_prop很短，所以d_nodal可以變成 d_trans + d_queue
### Queueing delay(考點)
* R: link bandwidth(bps), L: packet length(bits), a: average packet arrival rate
* La/R~0: queueing delay small
* La/R~1: queueing delay large
* La/R>1: queueing delay infinite!
### Traceroute
**[Traceroute的維基解釋](https://zh.wikipedia.org/wiki/Traceroute)**
* 總之就是丟一堆壽命不一樣的封包過去，然後就會依序回傳delay time
### Packet loss
* queue有空間限制，滿了封包有可能會掉落，這時候就會從上一個節點或源頭重寄，或者乾脆不寄
### Throughput
* definition: rate(bits/time unit) at which bits transferred between sender/receiver
* instantaneous(瞬時), average(平均)
* average throughput is the minimum of the edge
## Protocol layers, service models
### Why layering?
* dealing with complex systems
* explicit structure allows identification relationship of system's pieces, layered reference model for discussion
* modularization eases maintenance and updating of system (模組化減輕維護與系統升級難度)
### INTERNET PROTOCOL STACK
* application(應用層): support network appclitions, like FTP, SMTP and HTTP
* transport(傳輸層): process-process data transfer, like TCP and UDP
* network(網絡層): routing of datagram from src to dst, like IP and routing protocols
* link(鍵結層): data transfer between neighboring network elements, like Ethernet, 802.11(WiFi) and PPP
* physical(實體層): bits "on the wire"
### ISO/OSI(Open System Interconnection) Model
* presentation: allow applications to interpret meaning of data, e.g. encryption, compression, machine-specific conventions
* session: synchronization, checkpointing, recovery of data exchange
* These missing layers are combined by application layer.

###### tags: `Computer Network` `CSnote`