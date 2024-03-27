---
name: Ivan Goncharuk
date: 2023-11-14
class: COSC-350
---
- Name
	- `Ivan Goncharuk`
- Date
	- `2023-11-14`
- Class
	- `COSC-350`

## Forwarding Table

![[Pasted image 20231215165726.png | 1000]]

### My answer
- For address (a) `11001000 00010111 01000000 10110000`
	- the packet will be forwarded to interface 1.
- For address (b) `11001000 00010111 00000011 10110000`
	- the packet will be forwarded to interface 3.
- For address (c) `11001000 00010111 00001000 10110000`
	- the packet will be forwarded to interface 2.
- For address (d) `11001000 00010111 10001000 10110000`
	- the packet will be forwarded to interface 1.

## Subnets and Subnet Mask
![[Pasted image 20231215170007.png  | 1000]]

### My answer
#### (a)
- The smallest IP address is `200.23.16.0`. 
	- In binary, it is `11001000 00010111 00010000 00000000`
- The largest IP address is `200.23.17.255`. 
	- In binary, it is `11001000 00010111 00010001 11111111`

#### (b)
- If Santa is to request a block of 32 IP addresses, 
- then the block of addresses assigned would be `200.23.16.0/27`. 
- The subnet provides (32 IP addresses)
- Range: `200.23.16.0` to `200.23.16.31`.


## NAT
![[Pasted image 20231215170709.png | 1000]]

### My answer
**NAT translation table:**
- WAN side addr: `138.76.29.7, 5001`
- LAN side addr: `10.0.0.1, 3345`

#### 1) Outgoing packet before NAT
- Source (S): `10.0.0.1`
- Source Port: `3345`
- Destination (D): `128.119.40.186`
- Destination Port: `80`

#### 2) Outgoing packet after NAT

- Source (S): `138.76.29.7`
- Source Port: `5001`
- Destination (D): `128.119.40.186`
- Destination Port: `80`

#### 3) Returning packet before reaching NAT

- Source (S): `128.119.40.186`
- Source Port: `80`
- Destination (D): `138.76.29.7`
- Destination Port: `5001`

#### 4) Returning packet after NAT

- Source (S): `128.119.40.186`
- Source Port: `80`
- Destination (D): `10.0.0.1`
- Destination Port: `3345`

## Routing Algorithms

![[Pasted image 20231215171650.png | 1000]]

### My answer

| Step  | N'    | D(B),p(B) | D(C),p(C) | D(D),p(D) | D(E),p(E) | D(F),p(F) |
|-------|-------|-----------|-----------|-----------|-----------|-----------|
| Step 0 | A     | $\infty$, -      | $\infty$, -      | $\infty$, -      | $\infty$, -      | $\infty$, -      |
| Step 1 | AE    | 5, A      | $\infty$, -      | 5, A      | 2, A      | 4, E      |
| Step 2 | AED   | 5, A      | 6, D      | 4, E      | 2, A      | 4, E      |
| Step 3 | AEDF  | 5, A      | 6, D      | 4, E      | 2, A      | 4, E      |
| Step 4 | AEDFB | 5, A      | 6, D      | 4, E      | 2, A      | 4, E      |
| Step 5 | AEDFBC| 5, A      | 6, D      | 4, E      | 2, A      | 4, E      |


## Distance Vector Routing Algorithms
![[Pasted image 20231215173058.png | 1000]]

### My answer

Step (a) - Initial State:

| Information Stored at Node | A | B | C | D |
| -------------------------- | - | - | - | - |
| A                          | 0 | 4 | 1 | $\infty$ |
| B                          | 4 | 0 | 2 | 3 |
| C                          | 1 | 2 | 0 | $\infty$ |
| D                          | $\infty$ | 3 | $\infty$ | 0 |

Step (b) - After First Update:

| Information Stored at Node | A | B | C | D |
| -------------------------- | - | - | - | - |
| A                          | 0 | 3 | 1 | 7 |
| B                          | 3 | 0 | 2 | 3 |
| C                          | 1 | 2 | 0 | 5 |
| D                          | 7 | 3 | 5 | 0 |

Step (c) - After Second Update:

| Information Stored at Node | A | B | C | D |
| -------------------------- | - | - | - | - |
| A                          | 0 | 3 | 1 | 6 |
| B                          | 3 | 0 | 2 | 3 |
| C                          | 1 | 2 | 0 | 5 |
| D                          | 6 | 3 | 5 | 0 |

## IPV6 Tunneling and Encapsulation

![[Pasted image 20231215173415.png | 1000]]

### My answers

#### 4.1
IPv6
#### 4.2
D2A1:61B4:DCE9:CDC4:14AC:C816:3E23:3273
#### 4.3
5E15:65CE:7696:94B6:CCB4:965B:742F:7B6E
#### 4.4
No
#### 4.5
D2A1:61B4:DCE9:CDC4:14AC:C816:3E23:3273
#### 4.6
5E15:65CE:7696:94B6:CCB4:965B:742F:7B6E
#### 4.7
IPv4
#### 4.8
20.13.140.57
#### 4.9
18.106.122.93
#### 4.10
Yes
#### 4.11
D2A1:61B4:DCE9:CDC4:14AC:C816:3E23:3273
#### 4.12
5E15:65CE:7696:94B6:CCB4:965B:742F:7B6E
#### 4.13
IPv6
#### 4.14
D2A1:61B4:DCE9:CDC4:14AC:C816:3E23:3273
#### 4.15
5E15:65CE:7696:94B6:CCB4:965B:742F:7B6E

## Addressing and Forwarding
![[Pasted image 20231215174501.png | 1000]]
### My answers

#### 5.1
20-9F-78-B7-B7-CF
#### 5.2
55-56-2D-F5-C2-89
#### 5.3
128.119.72.47
#### 5.4
128.119.49.243
#### 5.5
Yes
#### 5.6
55-56-2D-F5-C2-89
#### 5.7
B7-C1-62-7C-5D-BF
#### 5.8
No

