---
title: CN MID-TERM 考題大補帖
---

>★109學年開始，陳裕賢已經擺明要跟學生懟著幹了。期中考古題除了必考的FSM和Python程式碼外完全不一樣，有人在導生聚反應考太難他也只是說想要換種(跟考古題不一樣)的方式考。甚至助教改鬆，他還重改扣分。
>考試內容均為講義上的題目，每個圖都要記得看，上課說會考的一定會考，上課輕輕帶過的也會有可能考。講義一定要讀熟。
>109-2期中考題與作業 **完全沒有任何關聯** ，請以PPT講義上的內容為準備方向。


# 1. Suppose two hosts, A and B, are separated by 100,000 kilometers and are connected by a direct link of R = 2 Mbps. Suppose the propagation speed over the link is $2.5\times10^8 meters/sec$.
* a. Calculate the bandwidth‐delay product, $R\times D_{prop}$
* b.Consider sending a file of 800,000 bits from Host A to Host B. Suppose the file is sent continuously as one large message. What is the maximum number of bits that will be in the link at any given time? (year 96, 97)
## ANS
### A
$D_{prop}= 100000 \times10^3/(2.5\times10^8) = 1 / 2.5 = 0.4$ 
$R\times D_{prop} = 2 \times 1024 \times 1024 \times 0.4 bits = 838,861$
### B
$800,000 < 838,861$
ANS: $800,000$ bits
# 2. Consider an overlay network with 100 active peers, with each pair of peers having an active TCP connection. Additionally, suppose that the TCP connections pass through a total of 10 routers. How many nodes and edges are there in the corresponding overlay network? (year 96, 97)
## ANS
Given there is N active peers and m routers
There will be N nodes and $N(N-1)/2$ edges
# 3. Consider the queuing delay in a router buffer. Let *I* denote traffic intensity; that is, *I = La/R*. Suppose that the queuing delay takes the form $IL/R(1-I)$ for $I<1$.
A. Plot the total delay as a function of $L/R$.
B. Provide a formula for the total delay, that is, the queuing delay plus the transmission delay. (year 100)
## ANS
* Problem from chapter 1 P14.
### B
total delay = transmission delay + queing delay = $\frac{IL}{R(1-I)} + \frac{L}{R} = \frac{L}{R(1-I)}$
### A
Let *x* = L/R. Use the result from **B** you can get: 
total delay = $\frac{x}{1 - ax}$
# 4. Consider sending a large file of *F* bits from Host A to Host B. There are two links (and one switches) between A and B, and the links are uncongested (that is, no queuing delays). Host A segments the file into segments of *L = 80+S* bits each and adds 80 bits of header to each segment, forming packets of S bits. Each link has a transmission rate of R bps. Find the value of *S* that minimizes the delay of moving the file from Host A to Host B. Disregard propagation delay. (year 100)
## ANS
There are *F/S* packets.
time for last packet to be received 2 routers:
$\frac{S+80}{R} \times 2$
Thus delay of the whole file is:
$\frac{S+80}{R} \times2 + (\frac{F}{S} - 1)\times\frac{S+80}{R} = \frac{S+80}{R} \times (\frac{F}{S} + 1)$
d/ds*delay = 0 
![](https://i.imgur.com/G7ertgk.jpg)
S = $\sqrt[]{80F}$

# 5. Consider distributing a file of *F = 100 Gbits* to N peers. The server has an upload rate of *Us = 10 Mbps*, and each peer has a download rate of *Di = 5 Mbps* and an upload rate of u. For N = 10, 100 and 1,000 and U = 100 Kbps, 500 Kbps and 1 Mbps, prepare a chart giving the minimum distribution time for each of the combinations of N and u for both client-server distribution and P2P distribution.(year 100)
## ANS
### 
minimum distribution time for client-server distribution:
$D_{cs} =$ **max**{$NF/u_s,F/d_{min}$}
minimum distribution time for P2P distribution:
$D_{P2P} =$ **max**{$F/u,F/d_{min},NF/(u+\sum_{i=1}^{n}u_i)$}
$F=100\times1024$ Mbits
$U_s = 10$ Mbps
$D_i = 5$ Mbps

Service client
| U\N | 10 | 100 |  1000   |
| -------- | -------| -------- | --- |
| 100      | 102400 | 1024000 | 10240000 |
| 500      | 102400 | 1024000 | 10240000 |
| 1000     | 102400 | 1024000 | 10240000 |

P2P APPROXIMATE

| U\N | 10 | 100 |  1000   |
| -------- | -------| --------| ---      |
| 100      | 93290  | 518061  | 951175   |
| 500      | 68804  | 174066  | 205506   |
| 1000     | 51808  | 95120   | 103798   |

# 6.
![](https://i.imgur.com/OdKb5Rr.png)
## ANS
chapter 2
### A
![](https://i.imgur.com/4hDxQqz.png)

### b
![](https://i.imgur.com/Q8SugPb.png)

# 7 FSMs.
### year
* 96, 97, 100
## 2.0
Draw finite state machines(FSMs)  of protocol **rdt2.0**
### ANS
![](https://i.imgur.com/fcJ8Q7P.png)

## 2.1
Draw finite state machines(FSMs) for (a)sender (b)receiver sides of protocol **rdt2.1 (handling duplicates)**
### ANS
#### A(Sender)
![](https://i.imgur.com/jle8Fg2.png)
#### B(receiver)
![](https://i.imgur.com/yfBzOzK.gif)

## 2.2
Draw FSMs for (a)sender (b)receiver sides of protocol **rdt2.2 (a NAK-free protocal)**
### ANS
#### A(Sender)
![](https://i.imgur.com/vB4EvyD.gif)

#### B(receiver)
![](https://i.imgur.com/xvqLG7i.gif)
## 3.0
Draw FSMs for (a)sender (b)receiver sides of protocol **rdt3.0 (underlying can also lose packets)**
#### A(Sender)
![](https://i.imgur.com/KZVnEp4.gif)
#### B(receiver)
![](https://i.imgur.com/2k5hqSJ.png)
## GBN
### ANS
#### Sender
![](https://i.imgur.com/d48TlP5.png)
#### RECEIVER
![](https://i.imgur.com/6xSnR7p.png)

# 8. Answer true or false to the following questions and briefly justify your answer:
a. With the Selective Repeat (SR) protocol, it is possible for the sender to
receive an ACK for a packet that falls outside of its current window.
b. With Go-Back-N (GBN), it is possible for the sender to receive an ACK for a
packet that falls outside of its current window
c.The alternating-bit protocol is the same as the SR protocol with a sender and
receiver window size of 1
d..he alternating-bit protocol is the same as the SR protocol with a sender and
receiver window size of 1
### Year
* 96
## ANS
### A.
True.
Suppose the sender has a window size of 3 and sends packets 1, 2, 3 at 𝑡0. At 𝑡1 (𝑡1 > 𝑡0) the receiver ACKs 1, 2, 3. At 𝑡2 (𝑡2 > 𝑡1) the sender times out and resends 1, 2, 3. At 𝑡3 the receiver receives the duplicates and re-acknowledges 1, 2, 3. At 𝑡4 the sender receives the ACKs that the receiver sent at 𝑡1 and advances its window to 4, 5, 6. At 𝑡5 the sender receives the ACKs 1, 2, 3 the receiver sent at 𝑡2. These ACKs are outside its window.
### B. 
By essentially the same scenario as in (a).
### C.
Note that with a window size of 1, SR, GBN, and the alternating-bit protocol are functionally equivalent. The window size of 1 precludes the possibility of out-of-order packets (within the window). A cumulative ACK is just an ordinary ACK in this situation, since it can only refer to the single packet within the window.
### D.
he explanation is the same as (c).


# 9. TCP program by java and do some thing. server and client.
### Year
* 96 97 100
## ANS
### Server lines to know
```
ServerSocket serverSocket = new ServerSocket(8080); // Create Socket
Socket socket = serverSocket.accept(); // Listen to connection

InputStream input = socket.getInputStream(); // 
BufferedReader reader = new BufferedReader(new InputStreamReader(input));
String line = reader.readLine();    // reads a line of text

OutputStream output = socket.getOutputStream();
PrintWriter writer = new PrintWriter(output, true);
writer.println(“This is a message sent from the server”); // write

```
### client lines to know

```
Socket socket = new Socket(host, port);
OutputStream output = socket.getOutputStream();

OutputStream output = socket.getOutputStream();
PrintWriter writer = new PrintWriter(output, true);
writer.println(“This is a message sent to the server”);)

InputStream input = socket.getInputStream();
BufferedReader reader = new BufferedReader(new InputStreamReader(input));
String line = reader.readLine();    // reads a line of text
```

## python
### server
```
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((ip, port)) 
server.listen(5)
while True:
      connection, client_address = server.accept()
      data = connection.receive(1024) ##read
      connection.sendall(data) #write
      connection.close()
```
      
### client
```
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect(host, port)
sock.sendall(data)
data = sock.recv(1024)
```

###### tags: `Computer Network` `CSnote`