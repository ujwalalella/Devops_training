# Networking Basics — Notes

## 1. IP Address

An **IP (Internet Protocol) address** is a logical address used to identify a network interface and to deliver IP packets across networks.

### IPv4

IPv4 addresses are **32 bits**, written as four decimal octets:

```text
192.168.1.10
```

Each octet is 8 bits and can have a value from `0` to `255`.

```text
192 . 168 . 1 . 10
 |      |    |    |
 8      8    8    8 bits
```

Total:

```text
8 + 8 + 8 + 8 = 32 bits
```

### IP Address vs Network

An IP address identifies an address/interface:

```text
192.168.1.10
```

A network/subnet represents a range:

```text
192.168.1.0/24
```

---

# 2. MAC Address

A **MAC (Media Access Control) address** is a Layer 2/link-level address associated with a network interface.

Example:

```text
00:1A:2B:3C:4D:5E
```

A MAC address is normally represented as **6 hexadecimal bytes**:

```text
00 : 1A : 2B : 3C : 4D : 5E
```

Each pair represents 8 bits:

```text
6 × 8 = 48 bits
```

### IP vs MAC

| IP Address | MAC Address |
|---|---|
| Layer 3 | Layer 2 |
| Logical/network address | Link/local address |
| Used for routing between networks | Used for local-link delivery |
| Example: `192.168.1.10` | Example: `00:1A:2B:3C:4D:5E` |

A useful mental model:

```text
IP  → Where is the host/network?
MAC → Which interface on this local link?
```

---

# 3. Representations

Networking information can be represented in different forms.

### IPv4 — dotted decimal

```text
192.168.1.10
```

Internally it is 32 binary bits:

```text
11000000.10101000.00000001.00001010
```

### MAC — hexadecimal

```text
00:1A:2B:3C:4D:5E
```

### CIDR

A network can be represented using CIDR notation:

```text
192.168.1.0/24
```

The `/24` means the first 24 bits are the network prefix.

---

# 4. Packet

A **packet** is a unit of data carried by the network layer (IP).

Conceptually, an IP packet contains:

```text
+--------------------------------+
| Source IP                      |
| Destination IP                 |
| Protocol information           |
| Payload                        |
+--------------------------------+
```

Example:

```text
Source IP:      192.168.1.10
Destination IP: 10.20.30.40
Payload:        Application data
```

More generally, the data unit depends on the layer:

```text
Application → Data / Message
Transport   → TCP Segment / UDP Datagram
Network     → IP Packet
Data Link   → Frame
Physical    → Bits
```

---

# 5. Protocol

A **protocol** is a defined set of rules that devices follow to communicate.

Examples:

| Protocol | Purpose |
|---|---|
| HTTP | Web communication |
| HTTPS | Secure web communication |
| TCP | Reliable transport |
| UDP | Connectionless transport |
| IP | Addressing and routing |
| DNS | Name resolution |
| SSH | Secure remote access |
| DHCP | Automatically obtains network configuration |

Protocols operate at different layers.

For example:

```text
HTTP
 ↓
TCP
 ↓
IP
 ↓
Ethernet/Wi-Fi
```

---

# 6. Host

A **host** is a network-connected device that can communicate using network protocols.

Examples:

- Laptop
- Server
- Virtual machine
- Cloud instance
- Phone

Example:

```text
Server
IP: 10.20.30.40
```

A server can be considered a host.

---

# 7. Node

A **node** is a broader term for a device or point participating in a network.

Examples:

```text
Laptop
Server
Router
Switch
Printer
IoT device
```

A host is generally an endpoint, while node is a broader networking term.

---

# 8. Switch

A **switch** primarily operates at **OSI Layer 2 (Data Link)**.

It connects devices within a local network and forwards Ethernet frames using MAC addresses.

```text
PC1 ─┐
PC2 ─┤
PC3 ─┼── Switch
PC4 ─┘
```

The switch learns which MAC addresses are reachable through its ports.

### Key idea

```text
Switch
→ Layer 2
→ MAC addresses
→ Frames
→ Local network
```

---

# 9. Router

A **router** primarily operates at **OSI Layer 3 (Network)**.

It connects different IP networks and forwards packets based on destination IP addresses and its routing table.

```text
Network A
192.168.1.0/24
       |
     Router
       |
Network B
10.0.0.0/24
```

### Key idea

```text
Router
→ Layer 3
→ IP addresses
→ Packets
→ Between networks
```

---

# 10. Firewall

A **firewall** controls network traffic according to security rules.

For example:

```text
Allow TCP 443
Allow TCP 22
Deny everything else
```

Conceptually:

```text
Internet
   |
   v
Firewall
   |
   +---- Allowed → Application
   |
   +---- Blocked → DROP
```

Firewalls can exist as:

- Host-based software firewalls
- Network firewalls/appliances
- Cloud-based network security controls

The exact OSI layer depends on the firewall and the type of rule being applied.

---

# 11. Subnet

A **subnet (subnetwork)** is a smaller logical network created within a larger IP network.

For example:

```text
192.168.1.0/24
```

can be divided into smaller subnets.

Why use subnets?

- Organize networks
- Separate groups of hosts
- Improve address utilization
- Control routing
- Provide network segmentation

Example:

```text
Large Network
192.168.1.0/24

       ↓ subnetting

192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

---

# 12. Types of IP Addresses

## Public IP

A **public IP address** is globally routable on the Internet.

Example:

```text
203.0.113.10
```

(Note: `203.0.113.0/24` is reserved for documentation/examples.)

## Private IP

Private IPv4 addresses are used inside private networks and are not directly routable on the public Internet.

The three main private ranges are:

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

Examples:

```text
10.0.0.5
172.20.10.5
192.168.1.10
```

## Static IP

An IP address that is deliberately configured to remain stable.

Commonly useful for:

- Servers
- Network devices
- Services that need a stable address

## Dynamic IP

An IP address assigned dynamically, commonly using DHCP.

---

# 13. Subnet Mask

A **subnet mask** tells us which part of an IPv4 address is the network portion and which part is the host portion.

Example:

```text
IP:
192.168.1.10

Subnet mask:
255.255.255.0
```

Binary mask:

```text
11111111.11111111.11111111.00000000
```

`1`s represent the network portion.

`0`s represent the host portion.

```text
11111111.11111111.11111111.00000000
<--------- network ----------><host>
```

---

# 14. CIDR Notation

**CIDR (Classless Inter-Domain Routing)** represents an IP network using a prefix length.

Example:

```text
192.168.1.0/24
```

The `/24` means:

```text
24 network bits
32 - 24 = 8 host bits
```

Equivalent subnet mask:

```text
255.255.255.0
```

## Usable Addresses Example

For:

```text
192.168.1.0/24
```

Host bits:

```text
32 - 24 = 8
```

Total addresses:

```text
2^8 = 256
```

Traditionally, two addresses are reserved:

```text
Network address:   192.168.1.0
Broadcast address: 192.168.1.255
```

Therefore traditional usable host addresses are:

```text
192.168.1.1 → 192.168.1.254
```

Number of traditional usable hosts:

```text
256 - 2 = 254
```

### Common CIDR examples

| CIDR | Subnet Mask | Total Addresses | Traditional Usable Hosts |
|---|---|---:|---:|
| `/8` | `255.0.0.0` | 16,777,216 | 16,777,214 |
| `/16` | `255.255.0.0` | 65,536 | 65,534 |
| `/24` | `255.255.255.0` | 256 | 254 |
| `/25` | `255.255.255.128` | 128 | 126 |
| `/26` | `255.255.255.192` | 64 | 62 |
| `/27` | `255.255.255.224` | 32 | 30 |
| `/28` | `255.255.255.240` | 16 | 14 |
| `/30` | `255.255.255.252` | 4 | 2 |

> Note: The traditional "subtract two" rule does not apply to every special IPv4 prefix/use case, and cloud providers may reserve additional addresses.

---

# 15. Subnetting

**Subnetting** means dividing one IP network into smaller networks.

Example:

```text
Original:
192.168.1.0/24
```

Suppose we need 4 subnets.

We need:

```text
2^2 = 4
```

So we borrow 2 host bits:

```text
/24 → /26
```

The four subnets are:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

Each `/26` has:

```text
6 host bits

2^6 = 64 total addresses

64 - 2 = 62 traditional usable hosts
```

---

# 16. Ports

A **port** identifies a transport-layer endpoint/service on a host.

IP identifies the host/interface.

The port helps identify the application/service.

Example:

```text
192.168.1.10:50000
        |
        +-- IP address: 192.168.1.10
        +-- Port: 50000
```

A connection can be represented as:

```text
Client:
192.168.1.10:50000

        TCP

Server:
10.20.30.40:443
```

Here:

```text
192.168.1.10 → Source IP
50000        → Source port

10.20.30.40  → Destination IP
443          → Destination port
```

Common ports:

| Port | Common use |
|---:|---|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |

Ports belong to the **Transport layer**.

---

# 17. DNS

**DNS (Domain Name System)** translates domain names into information such as IP addresses.

Instead of remembering:

```text
142.x.x.x
```

we can use:

```text
example.com
```

Conceptually:

```text
Browser
   |
   | "What is the IP for example.com?"
   v
Recursive Resolver
   |
   v
DNS infrastructure
   |
   v
Authoritative DNS Server
   |
   v
IP address
```

## Recursive Resolver

The **recursive resolver** receives a DNS query from the client and performs the work needed to find the answer, often using cached results.

Examples include resolvers provided by ISPs, organizations, or public DNS services.

## Authoritative DNS Server

An **authoritative DNS server** holds the official DNS records for a domain/zone and provides authoritative answers.

## Common DNS Records

### A record

Maps a hostname to an IPv4 address.

```text
example.com → 93.184.216.34
```

### CNAME record

Creates an alias from one hostname to another hostname.

```text
www.example.com → example.com
```

A CNAME points to a **name**, not directly to an IP address.

### MX record

Specifies the mail servers responsible for receiving email for a domain.

```text
example.com → mail.example.com
```

---

# 18. TCP vs UDP

Both are Transport Layer protocols.

## TCP

**TCP (Transmission Control Protocol)** is connection-oriented and provides mechanisms for reliable, ordered delivery.

It provides features such as:

- Connection establishment
- Acknowledgements
- Retransmission
- Ordering
- Flow/congestion control

Commonly used for:

```text
HTTP/1.1
HTTP/2
SSH
```

## UDP

**UDP (User Datagram Protocol)** is connectionless.

It does not establish a TCP-style connection and does not provide TCP's built-in reliability, ordering, or retransmission mechanisms.

It is useful when low overhead or application-controlled behavior is desirable.

Examples include:

```text
DNS
DHCP
Real-time applications
```

---

# 19. TCP Handshake

A **handshake** is a sequence used to establish or negotiate communication.

## 2-way handshake

A simple conceptual two-message exchange:

```text
A → B : Request
B → A : Response
```

It is not the normal TCP connection-establishment mechanism.

A two-way exchange cannot provide the same confirmation properties as TCP's three-way handshake.

## 3-way TCP handshake

TCP normally establishes a connection using three messages:

```text
Client                  Server

   SYN  ───────────────>

        <────────────── SYN-ACK

   ACK  ───────────────>
```

Meaning:

```text
1. SYN
   Client requests to establish a TCP connection.

2. SYN-ACK
   Server acknowledges the request and sends its own synchronization information.

3. ACK
   Client acknowledges the server.
```

After this, the TCP connection is established and application data can be exchanged.

## 4-way termination

TCP connection termination commonly uses a four-segment exchange because each direction of the connection is closed independently:

```text
Client                  Server

   FIN  ───────────────>

        <────────────── ACK

        <────────────── FIN

   ACK  ───────────────>
```

So remember:

```text
TCP connection establishment → 3-way handshake
TCP connection termination   → commonly 4 segments
```

The "2-way handshake" is a general two-message exchange, not the normal TCP connection setup.

---

# 20. OSI 7-Layer Model

The **OSI (Open Systems Interconnection) model** is a conceptual model that divides networking into seven layers.

```text
7  Application
6  Presentation
5  Session
4  Transport
3  Network
2  Data Link
1  Physical
```

## Layer 7 — Application

Closest to applications.

Examples:

```text
HTTP
DNS
SSH
SMTP
FTP
```

Purpose:

```text
Provides network services used by applications.
```

---

## Layer 6 — Presentation

Deals conceptually with how data is represented.

Examples/concepts:

```text
Encoding
Encryption
Compression
Data representation
```

Purpose:

```text
Translate/transform data into a representation that communicating systems can understand.
```

---

## Layer 5 — Session

Deals conceptually with managing communication sessions.

Responsibilities include:

```text
Session establishment
Session management
Session termination
```

Modern protocols do not always implement this as a distinct layer.

---

## Layer 4 — Transport

Provides end-to-end transport between application endpoints.

Examples:

```text
TCP
UDP
```

Important concepts:

```text
Ports
Reliability
Ordering
Retransmission
Connection management
```

Data units:

```text
TCP → Segment
UDP → Datagram
```

---

## Layer 3 — Network

Responsible for logical addressing and routing.

Examples:

```text
IPv4
IPv6
```

Important concepts:

```text
IP addresses
Routing
Routers
Packets
```

---

## Layer 2 — Data Link

Responsible for communication over the local link/network.

Examples:

```text
Ethernet
Wi-Fi
```

Important concepts:

```text
MAC addresses
Frames
Switching
```

---

## Layer 1 — Physical

Responsible for transmitting raw bits/signals.

Examples:

```text
Ethernet cable
Fiber
Radio/Wi-Fi signals
Electrical signals
```

Data unit:

```text
Bits
```

---

# 21. OSI Quick Reference

| Layer | Name | Main Concepts |
|---:|---|---|
| 7 | Application | HTTP, DNS, SSH |
| 6 | Presentation | Encoding, encryption, compression |
| 5 | Session | Sessions |
| 4 | Transport | TCP, UDP, ports |
| 3 | Network | IP, routing, packets |
| 2 | Data Link | MAC, Ethernet, Wi-Fi, frames |
| 1 | Physical | Cables, fiber, radio, bits |

Easy mental model:

```text
L7 → What application/service?
L6 → How is the data represented?
L5 → How is the session managed?
L4 → How is data transported? Which port?
L3 → Where is the destination network/host?
L2 → Which local interface?
L1 → How do the bits physically travel?
```

---

# 22. TCP/IP 4-Layer Model

The **TCP/IP model** is a practical networking model used to describe the Internet protocol suite.

The four layers are:

```text
4  Application
3  Transport
2  Internet
1  Network Access
```

## Application Layer

Combines roughly the responsibilities of OSI Layers 5, 6, and 7.

Examples:

```text
HTTP
HTTPS
DNS
SSH
SMTP
```

## Transport Layer

Corresponds roughly to OSI Layer 4.

Examples:

```text
TCP
UDP
Ports
```

## Internet Layer

Corresponds roughly to OSI Layer 3.

Examples:

```text
IP
Routing
Packets
```

## Network Access Layer

Combines roughly OSI Layers 1 and 2.

Examples:

```text
Ethernet
Wi-Fi
MAC
Frames
Physical transmission
```

---

# 23. TCP/IP ↔ OSI Mapping

```text
OSI MODEL                    TCP/IP MODEL

7 Application ───────┐
6 Presentation ──────┤
5 Session ───────────┤──→ Application
                     │
4 Transport ─────────────→ Transport
                     │
3 Network ───────────────→ Internet
                     │
2 Data Link ────────┐
1 Physical ─────────┤──→ Network Access
```

| OSI Layer | OSI Name | TCP/IP Layer |
|---:|---|---|
| 7 | Application | Application |
| 6 | Presentation | Application |
| 5 | Session | Application |
| 4 | Transport | Transport |
| 3 | Network | Internet |
| 2 | Data Link | Network Access |
| 1 | Physical | Network Access |

---

# 24. Putting Everything Together

Suppose a browser wants to access:

```text
https://example.com
```

A simplified view is:

```text
Application
    ↓
HTTPS
    ↓
Transport
    ↓
TCP + port 443
    ↓
Internet
    ↓
IP packet
    ↓
Network Access
    ↓
Ethernet/Wi-Fi frame
    ↓
Physical bits/signals
```

The packet may travel through several routers:

```text
Your PC
   |
   v
Switch
   |
   v
Router 1
   |
   v
Router 2
   |
   v
Router 3
   |
   v
Server
```

Routing happens **hop-by-hop**.

The destination IP generally remains the end-to-end destination while the Layer 2 MAC addresses are changed for each local link.

---

# 25. Key Things to Remember

```text
IP
→ Logical Layer 3 address

MAC
→ Layer 2/link address

Packet
→ Layer 3 data unit

Protocol
→ Rules for communication

Host
→ Network-connected endpoint

Switch
→ Primarily Layer 2, uses MAC addresses

Router
→ Primarily Layer 3, uses IP addresses

Firewall
→ Controls traffic using security rules

Subnet
→ Smaller logical IP network

Subnet mask
→ Defines network/host boundary

CIDR
→ Prefix-length notation such as /24

Port
→ Identifies a transport-layer service/endpoint

DNS
→ Resolves names to DNS information such as IP addresses

TCP
→ Connection-oriented, reliable/ordered transport

UDP
→ Connectionless transport with lower protocol overhead

TCP setup
→ 3-way handshake

TCP termination
→ Commonly 4 segments

OSI
→ 7-layer conceptual model

TCP/IP
→ 4-layer practical model
```

---

# 26. The Big Picture

```text
                         APPLICATION
                  HTTP / HTTPS / DNS / SSH
                              │
                              ▼
                         TRANSPORT
                     TCP / UDP / PORTS
                              │
                              ▼
                          INTERNET
                        IP / ROUTING
                              │
                              ▼
                      NETWORK ACCESS
                    MAC / ETHERNET / Wi-Fi
                              │
                              ▼
                          PHYSICAL
                     Cables / Radio / Bits
```

And for a real request:

```text
Browser
   │
   ├── DNS → Find destination information
   │
   ├── TCP → Establish transport connection
   │
   ├── Port 443 → Identify HTTPS service
   │
   ├── IP → Identify destination network/host
   │
   ├── Router → Forward packet toward destination
   │
   ├── Switch → Forward local frames
   │
   └── Firewall → Allow/block traffic according to rules
```

This gives the foundation needed for the next networking topics:

```text
Routing
   ↓
TCP/UDP
   ↓
DNS
   ↓
Load Balancing
   ↓
Network troubleshooting
   ↓
Cloud networking
   ↓
Docker/Kubernetes networking
```
