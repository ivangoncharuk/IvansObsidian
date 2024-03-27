**1. Socket Programming** 
Screenshots
![[Pasted image 20230929213947.png]]

Demonstrating terminating connection with "Over"
![[Pasted image 20230929221318.png]]

**2.1** Take a screenshot of your Wireshark display similar to Figure 1.
![[Pasted image 20230929213243.png]]
**2.2** Is your browser running HTTP version 1.0, 1.1, or 2? What version of HTTP is the server running?
> My browser and the server is running HTTP version 1.1

**2.3** What languages (if any) does your browser indicate that it can accept to the server?
> **en-US**,en;q=0.9

**2.4** What is the IP address of your computer? What is the IP address of the `gaia.cs.umass.edu` server?
>My computer (source IP): 192.168.10.1
>Server (destination IP): 128.119.245.12

**2.5** What is the status code returned from the server to your browser?
> Status Code: 200 
> Response Phrase: OK

**2.6** When was the HTML file that you are retrieving last modified at the server?
> Last Modified: Fri, 29 Sep 2023 05:59:01 GMT

**2.7** How many bytes of content are being returned to your browser?
> Content-Length: 128 bytes


1. Suppose a packet is `L = 1500` bytes long (one byte = 8 bits), and link transmits at `R = 1 Gbps` (i.e., a link can transmit bits `1,000,000,000 bits per second`). What is the transmission delay for this packet? 
	- `transmission_delay = L / R`
	- `L` is the length of the packet in bits
	- `R` is the transmission rate of the link in bits per second
	- `transmission_delay = 1500 bytes * 8 bits/byte / 1 Gbps = 1.875e-07 seconds`
	- `18.75 microseconds.`
2. Consider the network shown in the figure below, with three links, each with the specified transmission rate and link length. Assume the length of a packet is `8000 bits`, and the speed of light propagation delay on each link is `3x108 m/sec`. What is the total delay? Just consider the transmission delay and propagation delay for each link.
- ![[transmission_linkLength_cosc350_problem.png|800]]
	- `total_delay = transmission_delay_link1 + propagation_delay_link1 + transmission_delay_link2 + propagation_delay_link2 + transmission_delay_link3 + propagation_delay_link3`
3. In the scenario below, imagine that you're sending an http request to another machine somewhere on the network. What layer corresponds to box 6,7,8,9, and 10, respectively
	- ![[five_layer_protocol_stack.png|400]]
	- **Box 6:** Application layer
	- **Box 7:** Transport layer
	- **Box 8:** Network layer
	- **Box 9:** Data link layer
	- **Box 10:** Physical layer
4. Consider an HTTP server and client as shown in the figure below. Suppose that the RTT delay between the client and server is `30 msecs`; the time a server needs to transmit an object into its outgoing link is `0.75 msecs`; and any other HTTP message not containing an object has a negligible (zero) transmission time. Suppose the client again makes `60` requests, one after the other, waiting for a reply to a request before sending the next request. Assume the client is using `HTTP 1.1` and the `IF-MODIFIED-SINCE` header line. Assume `30%` of the objects requested have NOT changed since the client downloaded them (before these `60` downloads are performed). How much time elapses (in milliseconds) between the client transmitting the first request, and the completion of the last request?
	- ![[originServer_browserCache.png|400]]
	- `Total time = (RTT delay + server transmission delay) * number of requests * (1 - percentage of requests that have not changed)`
	- `Total time = (30 ms + 0.75 ms) * 60 requests * (1 - 0.3)`
	- `1291.5ms`

5. Suppose the server-to-client HTTP RESPONSE message is the following. Answer each question below. 
```
HTTP/1.1 200 OK 
Date: Wed, 06 Sep 2023 00:38:55 +0000 
Server: Apache/2.2.3 (CentOS) 
Last-Modified: Wed, 06 Sep 2023 01:05:15 +0000 ETag:17dc6-a5c-bf716880. 
Content-Length: 2440 Keep-Alive: timeout=45, max=92 Connection: Keep-alive Content-type: text/html
```

- 5a. Is the response message using HTTP 1.0 or HTTP 1.1?
	- The response message is using HTTP 1.1 because the first line of the message starts with `HTTP/1.1`.

- 5b. Was the server able to send the document successfully? Yes or No
	- Yes, the server was able to send the document successfully because the status code in the response message is 200 OK.

- 5c. How big is the document in bytes?
	- The document is 2440 bytes big because the `Content-Length` header in the response message is set to `2440`.

- 5d. Is the connection persistent or non-persistent?
	- The connection is persistent because the `Connection` header in the response message is set to `Keep-alive`.

- 5e. What is the type of file being sent by the server in response
	- The type of file being sent by the server is an HTML file because the `Content-type` header in the response message is set to `text/html`.

6. Suppose within your Web browser you click on a link to obtain a Web page. The IP address for the associated URL is not cached in your local host, so a DNS lookup is necessary to obtain the IP address. Suppose that three DNS servers are visited before your host receives the IP address from DNS. The first DNS server visited is the local DNS cache, with an RTT delay of RTT0 = 2 msecs. The second and third DNS servers contacted have RTTs of 42 and 11 msecs, respectively. Initially, let's suppose that the Web page associated with the link contains exactly one object, consisting of a small amount of HTML text. Suppose the RTT between the local host and the Web server containing the object is $RTT_{HTTP} = 98 \text{msecs}$. Assuming zero transmission time for the HTML object, how much time (in msec) elapses from when the client clicks on the link until the client receives the object?
	- the DNS lookup time is `RTT0 + RTT1 + RTT2 = 2 ms + 42 ms + 11 ms = 55 ms`
	- $\text{RTT}_{\text{HTTP}} = 98 ms$
	- `Total time = DNS lookup time + HTTP round-trip time`
	- `Total time = 55 ms + 98 ms = 153 ms`
	- **Answer:** 153 ms
7. Fill in the missing Java socket code from the following choices.
	- Choices: `ServerSocket`, `11111`, `22222`, `Socket`, `“localhost”`, `DatagramSocket`, `DatagramPacket`, `length`, `InetAddress`, `accept`
```java
ServerSocket y = new ServerSocket(11111);
Socket x = y.accept();
Socket a = new Socket("localhost", 11111);
DatagramSocket p = new DatagramSocket();
InetAddress q = InetAddress.getByName("localhost"); DatagramPacket s = new DatagramPacket(r, r.length, q, 22222);
```

| Blank | Answer         | 
| ----- | -------------- |
| 1     | ServerSocket   |
| 2     | accept         |
| 3     | Socket         |
| 4     | 11111          |
| 5     | DatagramSocket |
| 6     | InetAddress    |
| 7     | "localhost"    |
| 8     | DatagramPacket |
| 9     | length         |
| 10    | 22222          |