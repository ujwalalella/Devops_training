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

### What is a TCP Handshake?

A TCP handshake is the process used by TCP to establish communication between a client and a server.

TCP is connection-oriented, so before application data is normally exchanged, the two sides establish a TCP connection.

The main handshake to remember is:

```text
SYN → SYN-ACK → ACK
```

This is called the TCP three-way handshake.

TCP also uses a multi-step exchange when closing a connection, commonly:

```text
FIN → ACK → FIN → ACK
```
This is commonly called the four-way handshake/termination.

### Why do we need a handshake?

Before sending application data, both sides need to establish that:

- The other side is reachable.
- Both sides are willing to communicate.
- Each side knows the other's initial sequence number.
- Both sides have received the necessary connection information.

A simple two-message exchange is not enough to reliably establish this.

## Two-Way Handshake

<img width="564" height="854" alt="Screenshot 2026-09-02 110439" src="https://github.com/user-attachments/assets/b2414f89-cd4e-4780-a700-5769087ff26b" />

A simplified two-way handshake would look like:

```text
Client                         Server

req_conn(x) ──────────────────>

             <──────────────── acc_conn(x)
```
Meaning:
```text
Client → "I want to establish a connection."

Server → "Okay, connection accepted."
```
It looks reasonable, but there is a problem.

Problem with two-way handshake

Network packets can be:

- Delayed
- Lost
- Duplicated
- Reordered

Imagine the client's connection request is delayed:
```text
Client                         Server

req_conn(x) ────────X
                    |
                 delayed
                    |
                    ↓

Client times out
and sends another request

req_conn(x) ──────────────────>

             <──────────────── acc_conn(x)
```
The original delayed request might eventually arrive at the server.

The server could potentially mistake an old delayed request for a new connection request.

##### The important idea is:

A two-way exchange does not provide enough confirmation to reliably establish the current connection in the presence of delayed or duplicate messages.

## Three-Way Handshake

<img width="302" height="432" alt="image" src="https://github.com/user-attachments/assets/48f5add0-5ee1-4279-a4cd-3ee34ea831d2" />

TCP solves this using three messages:
```text
Client                         Server

SYN ──────────────────────────>

       <────────────────────── SYN-ACK

ACK ──────────────────────────>
```
The three steps are:

1. SYN
2. SYN-ACK
3. ACK
5. Step 1 — SYN

The client sends a SYN (Synchronize) packet.

Conceptually:
```text
Client                         Server

SYN, Seq=x ───────────────────>
```
The client is saying:

"I want to establish a TCP connection. My initial sequence number is x."

x represents the client's initial sequence number.

##### Step 2 — SYN-ACK

The server responds with SYN-ACK.
```text
Client                         Server

SYN, Seq=x ───────────────────>

       <────────────────────── SYN-ACK
                              Seq=y
                              ACK=x+1
```
The server does two things:

ACK

It acknowledges the client's sequence number:

ACK = x + 1

Meaning:

"I received your SYN."

SYN

The server also chooses its own initial sequence number:

Seq = y

Meaning:

"My initial sequence number is y."

So SYN-ACK essentially means:

"I received your request,
and here is my connection information."

##### Step 3 — ACK

The client sends the final ACK.
```text
Client                         Server

SYN, Seq=x ───────────────────>

       <────────────────────── SYN-ACK
                              Seq=y
                              ACK=x+1

ACK, ACK=y+1 ─────────────────>
```
The client is saying:

"I received your sequence number y."

Now both sides have confirmation.
```text
Client knows:
Server received my SYN.

Server knows:
Client received my SYN-ACK.
```
The TCP connection is now established.

### Why Three Messages?

The important sequence is:
```text
Client → Server
       SYN
       "I want to connect."

Server → Client
       SYN-ACK
       "I received you, and here's my sequence number."

Client → Server
       ACK
       "I received your sequence number."
```
Therefore:
```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```
Then:

TCP CONNECTION ESTABLISHED
#####  What are x and y?

The diagrams use x and y to represent the initial sequence numbers chosen by each side.
```text
Client → Server
Client's initial sequence number = x

Server → Client
Server's initial sequence number = y
```
The important concept is:

Client has its own sequence number
Server has its own sequence number

During the handshake, each side learns and acknowledges the other's sequence information.

You don't need to memorize the exact sequence-number arithmetic yet. The important pattern is:
```text
SYN(x)
SYN-ACK(y, ACK x+1)
ACK(y+1)
```

##### After the Handshake

Once the connection is established, application data can be exchanged.
```text
Client                         Server

SYN ──────────────────────────>

       <────────────────────── SYN-ACK

ACK ──────────────────────────>

       CONNECTION ESTABLISHED

DATA ─────────────────────────>

       <────────────────────── ACK

DATA ─────────────────────────>

       <────────────────────── ACK
```
TCP uses acknowledgements and sequence numbers to support reliable, ordered delivery.

## Four-Way TCP Connection Termination

The TCP connection is full-duplex, meaning both sides can independently send data.

Therefore, closing the connection generally involves separately closing each direction.

A common four-segment exchange is:
```text
Client                         Server

FIN ──────────────────────────>

       <────────────────────── ACK

       <────────────────────── FIN

ACK ──────────────────────────>
```

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/b9be9d8e-2432-47e2-bfb7-5b3d5e5109af" />

This is commonly referred to as a four-way handshake or four-way termination.

##### Step 1 — Client sends FIN

Suppose the client has finished sending data.

It sends:
```text
FIN
```
Meaning:

"I am finished sending data in this direction."
```text
Client                         Server

FIN ──────────────────────────>
```
The server may still have data to send.

##### Step 2 — Server sends ACK

The server acknowledges the FIN:
```text
Client                         Server

FIN ──────────────────────────>

       <────────────────────── ACK
```
Meaning:

"I received your request to close your sending direction."

The server can still continue sending data if it has any remaining data.

##### Step 3 — Server sends FIN

Once the server has finished sending its data, it sends its own FIN:
```text
Client                         Server

FIN ──────────────────────────>

       <────────────────────── ACK

       <────────────────────── FIN
```
Meaning:

"I am also finished sending data."

##### Step 4 — Client sends ACK

The client acknowledges the server's FIN:
```text
Client                         Server

FIN ──────────────────────────>

       <────────────────────── ACK

       <────────────────────── FIN

ACK ──────────────────────────>
```
Now the TCP connection can be fully closed.

### Three-Way vs Four-Way
Purpose	Exchange
TCP connection establishment	3-way
TCP connection termination	4 segments commonly
Establishment
```text
SYN
 ↓
SYN-ACK
 ↓
ACK
Termination
FIN
 ↓
ACK
 ↓
FIN
 ↓
ACK
```
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
<img width="713" height="768" alt="image" src="https://github.com/user-attachments/assets/4b5c8398-d8e4-480b-a25e-df1f1db121c2" />

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
<img width="1600" height="1290" alt="image" src="https://github.com/user-attachments/assets/66ac9294-0eeb-4fdd-a0f9-425f24614bfd" />

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


