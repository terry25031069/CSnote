---
title: CN Chapter 2
---
# Chapter 2: Application layer
## Application architectures
### Client-server arch.
* 伺服器端：永遠在線且有常駐ip位址
* 客戶端：和伺服器連結、可能會間歇性的鏈接、可能為動態ip、客戶端與客戶端彼此不互相連接
### P2P(peer-to-peer) arch.
* 無隨時在線的伺服器，點對點傳輸，越多點會使得傳輸速度更快
### Process communicating
* process: program running within a host
### Socket
* process sends/receives messages to/from its socket
* socket像是現實中的門(出入口)
### Addressing process
* to receive messages, process must have "identifier".
* identifer = IP address + port number
## Internet transport protocols services
### TCP
* reliable transport between sending and receiving process
* flow control: sender won't overwhelm receiver
* congestion control (擁塞控制): throlle (限制) sender when network overloaded
* DOESN'T provide: timing, minimum throughput, guarantee, security
* connection-oriented: setup required between client and server processes
### UDP
* DOESN'T provide that TCP service have
## Securing TCP
### TCP and UDP
* no encryption(加密), cleartext->socket->cleartext
### SSL
* provides encrypted TCP connection, data integrity, end-point auth.
* apps use SSL libraries, that "talk" to TCP
* cleartext->socket->encrypt
## HTTP overview
### use TCP
* client initiates TCP connection(creates socket) to server, port 80
* server accepts TCP connection from client
* HTTP messages exchanged between browser and Web server.
* TCP connection closed
### HTTP is "stateless"
* server maintains no information about past client request
### HTTP connections
#### non-persistent HTTP
* at most one object send over TCP connection, connection then closed
* downloading multiple objects required multiple connections
* RTT: time for a small packet to travel from client to server and back
* response time = 2RRT + file transmission time(很重要)
#### persistent HTTP
* multiple objects can be sent over single TCP connection between client, server
* client sends requests as soon as it encounters a referenced object
* as least one RTT for all referenced objects
### HTTP request message
* Two types of HTTP messages: request, response(由可見ASCII字元組成)
* 分為request line(GET, POST與其他指令), header lines與body
* status code: 200 OK, 301 Moved Permanently, 400 Bad Request, 404 Not found, 505 Http Version Not Supported
* 詳情請看[Http貓](https://http.cat/)
### Method types
* HTTP/1.0: GET, POST, HEAD
* HTTP/1.1: 1.0 + PUT + DELETE
## User-server state: cookies
* Four components: 
1. cookie header line of HTTP response message
2. cookie header line of HTTP request message
3. cookie file kept on user's host, managed by user's browser
4. back-end DB at Web site
## Web caches(proxy server)
* satisfy client request without involving origin server
* user sets browser: Web accesses via cache 
* browser sends all HTTP requests to cache
* object in cache: cache returns object 
* else cache requests object from origin server, then returns object to client
## Electronic mail
* Three major components: user agents, mail servers, Simple Mail Transfer Protocol(SMTP)
### user agent
* function: composing, editing, reading mail messages.
* e.g., Outlook, Thunderbird
### mail servers
* mailbox contains incoming messages for user
* message queue of outgoing (to be sent) mail messages
* SMTP protocol between mail servers to send email messages
### SMTP(RFC 2821)
* uses TCP to reliably transfer email message from client to server, port 25
* three phase of transfer: handshaking, transfer of messages, closure
### SMTP: final words
* SMTP uses persistent connections, and requires message(header & body) to be in ASCII 
* SMTP server used CRLF.CRLF(\r\n\r\n) determine end of message
#### comparison with HTTP
* protocol type: HTTP: pull, SMTP: push
* (HTTP：TCP由想要「接收」檔案的主機建立，SMTP則是由想要「送出」的檔案建立)
* both have ASCII command/response interaction, status codes
* HTTP: each object encapsulated(封裝) in its own response message
* SMTP: multiple objects sent in multipart message
### Mail message format
* SMTP: protocol for exchanging email messages
* RFC822: standard for text message format
* header(To:, From:, Subject:), blank line and body(the message, ASCII char only)
### Mail access protocols
* SMTP: delivery/storage to receiver's server
* mail access protocol: retrieval from server
* POP: Post Office protocol(RFC 1939): authorization, download
* IMAP: Internet Mail Access protocol(RFC 1730): more feature, including manipulation of stored messages on server
* HTTP: gmail, Hotmail, etc.
#### POP3(POP version 3)
* auth. phase: 
* client commands: user, pass
* server responses: +OK, -ERR
* transaction phase: list, retr, dele, quit
#### IMAP
* keeps all messages in server
* allows user to organize messages in folders
* keeps user state across sessions
## DNS(Domain name system)

## [IMPORTANT]Peer to peer(P2P)
* no always-on server
* End systems connect with each other
* peers can connected\disconnect and change IP addresses during operation
## File distribution time 
### Client server(CS)
* Server sends.
    * $u_s$ is the upload speed of the server.
* Client downloads.
    * $d_{min}$ is the minimum client download rate
#### time to distribution F to n Clients using CS model.
$D_{c-s} \ge max(NF/u_s , F/d_{min})$
* $F/u_s$ is the distribution time when $NF/u_s <= d_{min}$
* $F/d_{min}$ is the distribution time when $NF/u_s >d_{min}$
* ## File distribution time 
### P2P
* client
    * ![](https://i.imgur.com/ePoz0X9.png) is the sum of client upload rate
#### time to distribution F to n Clients using CS model.
![](https://i.imgur.com/sB1SpD9.png)
* $F/u_s$ is the distribution time when $Us<= ( u_s + \sum_{}^{}u_i)/N$ 
* $F/d_{min}$ is the distribution time for the slowest client to receive file
*   $NF/( u_s + \sum_{}^{}u_i)$ is the distribution time when $Us>= ( u_s + \sum_{}^{}u_i)/N$


###### tags: `Computer Network` `CSnote`