#fall2023 #MATH-330 

## Fundamentals
- **Network:** A system of interconnected devices for communication.
- **Network Edge:** Includes hosts (PCs, servers) and clients connected via access networks (Residential, Institutional, Mobile).
- **Network Core:** Mesh of routers that forward data packets.
- **Internet:** 
	- "Network of networks," interconnected via [[ISP]]s.

## Key Metrics
- **Bandwidth:** Data rate in bps.
- **Transmission Delay:** 
$$
  \frac{L_{\text{(bits)}}}{R_{\text{(bits/sec)}}} 
$$
- **Access Network Types:**
  - HFC: 40 Mbps - 1.2 Gbps downstream, 30-100 Mbps upstream.
  - DSL: 24-52 Mbps downstream, 3.5-16 Mbps upstream.

## Media Types
- **Coaxial Cable:** Bidirectional, supports broadband.
- **Fiber Optic:** High-speed, low latency.
- **Wireless Radio:** No wire, impacted by environment.

## Core Concepts
- **Protocols:** Control data exchange (HTTP, TCP, IP, etc.).
- **Services:** Web, streaming, email, and more.
- **Packet Switching:** Data broken into packets and routed at full link capacity.

| Quick Ref  | Info                                                  |
|------------|-------------------------------------------------------|
| Hosts & Clients | Devices connected via access networks           |
| Packet Switches | Forward data packets                               |
| Media Types | Coaxial, Fiber Optic, Wireless Radio                  |
| Core Mechanics | Protocols, Services, [[Packet Switching]]             |

## Core Network Functions

- **Forwarding:** Moving packets from a router's input link to the appropriate output link. (Local action)
- **Routing:** Determining the paths that packets will take from source to destination. (Global action)

## Switching Methods

### Circuit Switching

- **FDM (Frequency Division Multiplexing):** Allocates a narrow frequency band to each call. Transmissions happen at the max rate of this band.
- **TDM (Time Division Multiplexing):** Time is divided into slots. Each call gets periodic slots and transmits at max rate, but only during its slots.

### Packet Switching vs. Circuit Switching

- **Example:**
    - 1Gb/s link
    - Each user is 100Mb/s when active and active 10% of the time.
    - Circuit-switching can handle `10` users.
    - Packet-switching can handle 35 users with less than 0.0004 probability of more than `10` being active at the same time.

#### Binomial Distribution in Networking

- The value of 0.0004 is calculated using a binomial distribution.
- Binomial distribution can model the number of "active" users among a total number of users. In the example, $n=35$ and $p=$ `0.10`(since each user is active `10`% of the time).
- You'd calculate the probability of more than `10` users being active at the same time using binomial distribution formulae.
- If $> 35$ users, the probability of more than `10` users being active at the same time will increase, potentially causing issues.

---

How do packet loss and delay occur?
packets queue in router buffers
- packets queue, wait for turn
- arrival rate to link (temporarily) exceeds output link capacity: packet loss

Packet delay: four sources

$$d_\text{nodal} = d_\text{proc} + d_\text{queue} + d_\text{trans} + d_\text{prop}$$

$d_\text{nodal}$: nodal processing
- check bit errors
- determine output link
- typically < m_sec

$d_\text{queue}$: queueing delay
- time waiting at output link for transmission
- depends on congestion level of router

$d_\text{trans}$: transmission delay
- L: packet lengths (bits)
- R: link transmission rate (bps)
- $d_\text{trans}$ = $\frac{L}{R}$

$d_\text{prop}$: propagation delay
- d: length of physical link (distance)
- s: propagation speed (2*10^8 m/sec in copper wire; ~3*10^8 m/sec for w.c)
- $d_\text{prop}$ = d/s