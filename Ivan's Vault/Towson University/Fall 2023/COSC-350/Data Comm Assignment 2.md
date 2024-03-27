---
name: Ivan Goncharuk
date: 2023-10-17
class: COSC-350
---
- Name
	- `Ivan Goncharuk`
- Date
	- `2023-11-14`
- Class
	- `COSC-350`

## 1

1.1) 
- The source port number will be y
- The destination port number will be x.

1.2) 
- R/2 bps.

1.3) 
- a. 
	- sequence number = 90 
	- second sequence number 110
	- the amount of data in the first segment is 110 - 90 = 20 bytes. 
- b. 
	- The acknowledgment number will be 90.

![[Pasted image 20231215181126.png | 1000]]

Source port: `80`
Destination port: `26145` (server to Host A) 
Destination port: `7532`(server to Host C)

Source IP address: `B` (IP address of server B) 
Destination IP address: `A` (traffic to Host A) 
Destination IP address: `C` (traffic to Host C)

1.5) 
- No, the receiver cannot be absolutely certain that no bit errors have occurred, even if the checksum matches.

1.6) 
- a. EstimatedRTT after each SampleRTT (in ms):
	- After 106 ms: `100.750`
	- After 120 ms: `103.156`
	- After 140 ms: `107.762`
	- After 90 ms: `105.542`
	- After 115 ms: `106.724`

- b. DevRTT after each SampleRTT (in ms):
	- After 106 ms: `5.0625`
	- After 120 ms: `8.008`
	- After 140 ms: `14.065`
	- After 90 ms: `14.434`
	- After 115 ms: `12.895`

- c. TCP TimeoutInterval after each SampleRTT (in ms):
	- After 106 ms: `121.000`
	- After 120 ms: `135.188`
	- After 140 ms: `164.023`
	- After 90 ms: `163.279`
	- After 115 ms: `158.303`




## 2

![[Pasted image 20231215182126.png | 1000]]

- 2.1
	- A) TCP

- 2.2
	- A) network layer

- 2.3 
	- A) all UDP packets are treated independently by the transport layer

- 2.4
	- B) process to process communication

- 2.5
	- B) Three-Way Handshaking

![[Pasted image 20231215182459.png | 1000]]

- 2.6
	- B) 16-bits and 16-bits

- 2.7
	- B) checksum

- 2.8
	- C) Congestion

- 2.9
	- C) slow start


## 3

**3.1** What is the IP address and TCP port number used by the client computer (source) that is transferring the alice.txt file to gaia.cs.umass.edu? Please give a screen shot of your captured HTTP protocols.
- IP: `192.168.86.68`
- Source Port: `55639`
- Destination port: `80`
![[Pasted image 20231215183722.png | 700]]

**3.2** What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection? Please give a screen shot of your captured HTTP protocols.
- IP Address of gaia.cs.umass.edu: `128.119.245.12`

![[Pasted image 20231215183804.png | 700]]

**3.3** What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? (Note: this is the “raw” sequence number carried in the TCP segment itself). Please give a screen shot of your captured TCP protocols.
- Raw sequence number: `4236649187`
- 
![[Pasted image 20231215184213.png | 700]]


**3.4** What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is the value of the Acknowledgement field in the SYNACK segment? Please give a screen shot of your captured TCP protocols.

- Sequence Number (raw): `1068969752`
- Relative Acknowledgment Number: `1`
- Acknowledgement Number (raw): `4236649188`

![[Pasted image 20231215184414.png | 700]]

**3.5** What is the sequence number of the TCP segment containing the header of the HTTP POST command? Note that in order to find the POST message header, you’ll need to dig into the packet content field at the bottom of the Wireshark window, looking for a segment with the ASCII text “POST” within its DATA field. 
How many bytes of data are contained in the payload (data) field of this TCP segment? Please give two screen shots of your captured TCP protocols to indicate your sequence number and payload, respectively.

- Payload: `1385 bytes`
![[Pasted image 20231215185319.png | 700]]
- Sequence number: `152041` (relative)
- Sequence number: `4236801228` (raw)
![[Pasted image 20231215185423.png | 700]]

**3.6** What is the length (header plus payload) of each of the first four data-carrying TCP segments? Please give a screen shot of your captured TCP protocols.
- Length: either `1514` or `1500` (given by the total-length field)

![[Pasted image 20231215185730.png | 700]]

**3.7** What is the minimum amount of available buffer space (receiver window size) advertised to the client by gaia.cs.umass.edu received for the entire trace? It can be retrieved by the first acknowledgment from the server with the corresponding window size information.
- Window size: `131712`
![[Pasted image 20231215190359.png | 700]]

**3.8** Are there any retransmitted segments in the trace file? 
What did you check for (in the trace) in order to answer this question? 
Plot the figure TimeSequence-Graph (Stevens) to justify your ideas. 
Tips: you could the trace over TimeSequence-Graph (Stevens). 
Then select: Statistics->TCP Stream Graph->TimeSequence-Graph (Stevens). 
If there are no retransmitted segments, all sequence numbers should increase monotonically with respect to time. 
If there is a retransmitted segment, the sequence number of this retransmitted segment should be smaller than those of its neighboring segments.

- No
- I used the filter `tcp.analysis.retransmission` to answer this question
![[Pasted image 20231215190709.png | 700]]
![[Pasted image 20231215190640.png | 700]]

**3.9** How much data does the receiver typically acknowledge in an ACK among the first ten data-carrying segments sent from the client to gaia.cs.umass.edu? 
Try to fill out the table below to answer this question. 
Can you identify cases where the receiver is ACKing every other received segment (see Table 3.2 in the text) among these first ten data-carrying segments? 
Use the results in the table and the following tips to answer this question.

- 1448 Bytes

| data-carrying segments | sequence number | acknowledged data |
| ---------------------- | --------------- | ----------------- |
| 1                      | 1               | 1449              |
| 2                      | 1449            | 2897              |
| 3                      | 2897            | 4345              |
| 4                      | 4345            | 5793              |
| 5                      | 5793            | 7241              |
| 6                      | 7241            | 8689              |
| 7                      | 8689            | 10137             |
| 8                      | 10137           | 11585             |
| 9                      | 11585           | 13033             |
| 10                     | 13033           | 14481             |

3.10 Plot the figure in terms of throughput (bytes transferred per unit time) for the TCP connection sent from theclient to gaia.cs.umass.edu. Based on the figure you plot, what is the maximum throughput after time 0.15seconds?
Note: Wireshark has a nice feature that allows you to plot the throughput of the TCP segments. Select a TCPsegment in the “listing of captured packets” window that is being sent from the client to the gaia.cs.umass.eduserver. Then select: Statistics->TCP Stream Graph-> Throughput.

![[Pasted image 20231215194502.png | 700]]

$$\frac{153kB×8×1024\frac{bits}{Kb}}{0.155s} = 8,086,296.77bps$$


`The maximum throughput after 0.15 seconds is approx 8,086,296.77 bits per second (bps).