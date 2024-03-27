---
tags:
  - fall2023
  - COSC-350
---

 - Suppose that TCP's current estimated values for the round trip time (estimatedRTT) and deviation in the RTT (DevRTT) are 220 msec and 27 msec, respectively. 

[[Hoax]]

 - Suppose that the next three measured(sampled) values of the RTT are 320 msec, 220 msec, and 200 msec respectively.
 - Compute TCP's new value of DEVRTT, estimated RTT, and the TCP timeout value after each of these three measured RTT values is obtained. 
 - Use the values of $\alpha = 0.125$ and $\beta = 0.25$. Round answer to two decimal places after leading zeros. 
 - Reference formula: 
	 - DevRTT for RTT1 = $$(1- \beta) *DevRTT + \beta * \lvert\text{SampleRTT} - \text{Estimated RTT}\rvert$$
	 - estimatedRTT for RTT1 = $$(1-\alpha)*\text{EstimatedRTT} + \alpha * \text{SampleRTT} $$
	 - timeout for RTT1 = $$\text{EstimatedRTT} + 4*\text{DevRTT}$$


**Variables:**

- estimatedRTT: The average time it takes for a packet to travel from the sender to the receiver and back.
- DevRTT: The amount of variation in the round trip time.
- SampleRTT: The time it takes for a single packet to travel from the sender to the receiver and back.
- timeout: The amount of time that TCP will wait for an ACK before retransmitting a packet.
- α: A parameter that controls how quickly the estimatedRTT is updated.
- β: A parameter that controls how quickly the DevRTT is updated.

**How to approach the problem:**

1. TCP keeps track of the estimatedRTT and DevRTT values.
2. When TCP sends a packet, it starts a timer.
3. When TCP receives an ACK for the packet, it stops the timer and calculates the SampleRTT.
4. TCP uses the SampleRTT to update the estimatedRTT and DevRTT values.
5. TCP uses the estimatedRTT and DevRTT values to calculate the timeout value.
6. If the timer expires before TCP receives an ACK, TCP retransmits the packet.

**Example:**

Suppose that the current estimatedRTT and DevRTT values are 220 msec and 27 msec, respectively. Suppose that TCP sends a packet and the SampleRTT is 320 msec. TCP will update the estimatedRTT and DevRTT values as follows:

```
DevRTT = (1-beta) *DevRTT + beta * abs(SampleRTT - EstimatedRTT)
DevRTT = (1-0.25) * 27 msec + 0.25 * abs(320 msec - 220 msec)
DevRTT = 28.25 msec

estimatedRTT = (1-alpha) * EstimatedRTT + alpha * SampleRTT
estimatedRTT = (1-0.125) * 220 msec + 0.125 * 320 msec
estimatedRTT = 234.38 msec
```

TCP will then calculate the timeout value as follows:

```
timeout = estimatedRTT + 4 * DevRTT
timeout = 234.38 msec + 4 * 28.25 msec
timeout = 429.5 msec
```

TCP will wait for 429.5 msec for an ACK before retransmitting the packet.

**Why is this important?**

The TCP timeout value is important because it helps to ensure that TCP connections are reliable and efficient. If the timeout value is too short, TCP may retransmit packets that have not actually been lost. This can lead to wasted bandwidth and decreased performance. If the timeout value is too long, TCP may not retransmit packets quickly enough, which can lead to dropped connections.

The TCP timeout value is adjusted dynamically based on the estimatedRTT and DevRTT values. This allows TCP to adapt to changing network conditions and maintain a high level of reliability and performance.
