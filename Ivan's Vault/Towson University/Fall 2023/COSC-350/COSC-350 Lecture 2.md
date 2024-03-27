#COSC-350 #fall2023 

- P2P Applications
- Video Streaming

- Our goal is to have conceptual and implementation aspects of application-layer protocols
- Transport-layer service models
- Client-server paradigm
- peer-to-eer paradigm
- programming network applications
	- socket API
- learn about protocols by examining popular application layer protocols 
	- HTTP
	- SMTP, IMAP
	- DNS

### Client server paradigm
**Server**:
- always-on host
- permanent IP address
- often in data centers, for scaling

**Clients**: 
- contact, communicate with server
- may be intermittently connected
- may have dynamic IP addresses
- do not communicate directly with each other
- examples: HTTP, IMAP, FTP

### Processes communicating
*process*: program running within a host
- within same host, two processes communicate using inter-process communication (defined by OS)
- processes in different hosts communication by each messages

- Clients, Servers
	- **client process**: process that initiates comm
	- **server process**: 

### Sockets
- process sends/receives messages to/from its socket
- socket analogous to door
	- sending process shoves message out door
	- sending process relies on transport infrastructure on other side of door to deliver message to socket at receiving process
	- **two sockets involved**: one on each side


### Application-Layer protocol defines:
- Types of messages

Internet transport protocols services

TCP
- reliable between sending and receiving process
- flow control: sender won't overwhelm receiver
- congestion control
- does not provide: timing, minimum tbroughput guarantee, security
- connection-oriented: setup required beteen client and server processes

UDP

Securing TCP
- Vanilla TCP & UDP sockets: 
	- no encryption
	- cleartext passwords sent into socket traverse internet in cleartext!!

- HTTP is stateless, meaning the server maintains no information about past client requests
- HTTP uses TCP
	- client initiates TCP connection to port 80
	- server accepts TCP connection from client
	- HTTP messages (app-layer protocol layer) 


Two types of HTTP
- persistent HTTP
	- tcp connection opened to a server
- non persistent HTTP
	- tcp connection opened
	- at most one object sent over TCP connection


### Exercise
```
HTTP/1.1 404 Not Found
Date: Tue, 05 Sep 2023 20:07:09 +0000
Server: Apache/2.2.3 (CentOS)
Content-Length: 58454
Keep-Alive: timeout=43, max=98
Connection: Keep-alive
Content-type: image/html
```

1) Is the response message using HTTP 1.0 or HTTP 1.1?
	- The response message is using HTTP 1.1, as indicated by the "HTTP/1.1" in the first line.
2) Was the server able to send the document successfully? Yes or No
	- No, the server was not able to send the document successfully. The status code "404 Not Found" indicates that the requested resource could not be found on the server.
3) How big is the document in bytes?
	- The document size is 58,454 bytes, as indicated by the "Content-Length: 58454" field.
4) Is the connection persistent or nonpersistent?
	- The connection is persistent. This is indicated by the "Keep-Alive: timeout=43, max=98" and "Connection: Keep-alive" fields. 
	- Persistent connections remain open for multiple requests/responses between the client and server.
5) What is the type of file being sent by the server in response?
	- The type of file being sent by the server in response is "image/html," as indicated by the "Content-type: image/html" field. 
	- However, it's worth noting that "image/html" is not a standard MIME type
		- it's likely a mistake and should probably be "text/html" for an HTML document or an image type like "image/png" for an image.
6) What is the name of the server and its version? Write your answer as server/x.y.z?
	- The name of the server and its version is Apache/2.2.3, as indicated by the "Server: Apache/2.2.3 (CentOS)" field.
7) Consider an HTTP server and client as shown in the figure below. 
   Suppose that the RTT delay between the client and server is 20 msecs; 
   the time a server needs to transmit an object into its outgoing link is 0.25 msecs;
   and any other HTTP message not containing an object has a negligible (zero) transmission time. Suppose the client again makes 70 requests, one after the other, waiting for a reply to a request before sending the next request.
   - 	For 70 requests with a Round-Trip Time (RTT) of 20 ms and a server transmission time of 0.25 ms:
   - Time for one request 
		    = RTT + Server Transmission Time 
> 		= 20 ms (RTT) + 0.25 ms (Server Transmission Time) 
> 		= **20.25 ms
**
> 	Time for 70 requests 
> 		= 70 * 20.25 ms 
> 		= **1417.5 ms**
> 		
> 	The client makes 70 requests one after the other, waiting for a reply before sending the next request, so the total time would be 1417.5 ms.



