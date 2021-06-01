---
title: CN Chapter 4
---
# Chapter 4: Network layer(Under Construction)
## Network layer overview
* transport segment from sending to receiving host 
* sending: encapsulates segments into datagrams
* receiving: delivers segments to transport layer
* network layer protocols in every host and router
* router examines header field in all IP datagrams passing through it
## Functions of network-layer
* forwarding: move packets from router to another appropriate router
* routing: determine packet route from source(下稱src) to destination(下稱dst)
* 類比：forwarding像轉程點，routing像是路線規劃。
## Data and control plane
### Data plane
* local, per-router function
* determine how datagram arriving on router input port and forwarding(轉發) to output port
* forwarding function
### Control plane
* network-wide logic
* determines how datagram is routed among routers from src and dst
* two approaches: traditional routing implemented in routers, softward-defined networking(SDN): implemented in (remote) servers
### Per-router control plane
* Individual routing algorithm in each router interact in the control plane
### Logically centralized control plane
* A distinct (typically remote) controller interacts with local control agents(CAs)
## Network service model
* What service model for "channel" transporting datagrams from sender to recevier?
* example services for individual datagrams: guarateed delivery with no or certain time
* example services for a flow of datagrams: in-order datagram delivery, guaranteed minimum bandwidth to flow, restrictions on changes in inter-packet spacing.
* ATM stands for Asynchronous Transfer Mode here, NOT Automatic teller machine!!
* [ATM網路架構的四種模式](https://zhidao.baidu.com/question/36641986)
![](https://i.imgur.com/U4TZuwA.png)
## Router arch. overview
* high-level view of generic router arch:
![](https://i.imgur.com/6SVmXOo.png)
### Input port functions
![](https://i.imgur.com/J4jmw52.png)
* physical layer(Green rectangle): bit-level reception
* data link layer(Blue rectangle): e.g. Ethernet(Chapter 5)
#### Decentralize switching(Red rectangle): 
* using header field value, lookup output port using forwarding table in input port memory("match plus action")
* goal: complete input port processing at "line speed"
* queuing: if datagrams arrive rate > forwarding rate
* dst-based forwarding: forward based only on dst IP addr
* generalized forwarding: forward based on any set of header field value
### Longest prefix matching
* longest prefix matching is used shortly
* often performed using ternary(三個一組的) content addressable memories(TCAMs)
* content addressable: present address to TCAM: retrieve address in one clocy cycle, regardless of table size
* Cisco Catalyst: can up ~1M routing table entries in TCAM
### Switching fabries
* transfer packet from input buffer to appropriate output buffer
* switching rate: rate at which packets can be transfer from inputs to outputs
* 3 types of switching fabrics![](https://i.imgur.com/e6NNDJc.png)









###### tags: `Computer Network` `CSnote`