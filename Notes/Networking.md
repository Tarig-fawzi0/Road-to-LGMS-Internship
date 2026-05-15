# Networking Fundamentals

---

# Layer 1 - Physical Layer

The Physical Layer is responsible for transmitting raw bits through physical media such as cables, electrical signals, and wireless communication.

## Main Functions
- Sending raw bits
- Electrical and physical transmission
- Network cables and signals

## Web Security Relevance
Although this layer is not directly related to Web Application Security, it represents the physical foundation of all network communication.

---

# Layer 2 - Data Link Layer

The Data Link Layer is responsible for node-to-node communication inside the same local network.

## Main Functions
- MAC addressing
- Frame transmission
- Error detection
- Switching

## Web Security Relevance
Understanding Layer 2 helps in understanding local network communication and how devices communicate within the same network.

---

# Layer 3 - Network Layer

The Network Layer is responsible for delivering packets between networks using IP addresses.

## Main Functions
- Logical addressing (IP addresses)
- Routing packets
- Path selection

## Important Concepts

### IP Address
An IP address identifies a device on a network.

Example:
192.168.1.1

### Packet
A packet is a unit of data transmitted through the network.

### Router
A router forwards packets between different networks.

### Routing
Routing is the process of selecting the best path for packets to reach their destination.

### Source and Destination IP
Every packet contains:
- Source IP → sender address
- Destination IP → receiver address

## Web Security Relevance
Understanding Layer 3 is important for:
- Reconnaissance
- Network scanning
- Understanding packet flow
- Identifying servers and web infrastructure

## Practical Observation
Using traceroute/tracert shows how packets travel across multiple routers before reaching a web server.
