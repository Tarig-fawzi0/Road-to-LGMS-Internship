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

# ICMP, TTL & Traceroute Notes (Web Pentesting Perspective)

## What I Learned
- ICMP is used for network testing and error reporting.
- Ping uses ICMP Echo Request and Echo Reply to test host reachability.
- Traceroute uses TTL values to discover the path packets take across routers.
- Each router decreases TTL by 1.
- When TTL reaches 0, the router sends an ICMP Time Exceeded message.
- A hop represents one router in the network path.

---

## Private vs Public IP Addresses

### Private IP Ranges
- 10.0.0.0 – 10.255.255.255
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 – 192.168.255.255

### Public IP
- Reachable on the internet
- Assigned by ISPs or hosting providers

---

## Practical Traceroute Analysis

Command used:
bash
tracert google.com

# Transport Layer Fundamentals

## Overview
The Transport Layer is responsible for reliable communication between devices and applications.

## Important Concepts Learned
- TCP vs UDP
- TCP 3-Way Handshake
- Source and Destination Ports
- Socket Communication
- TCP Reliability
- Flow Control
- Congestion Avoidance

## Practical Networking Observations
- Analyzed TCP traffic using Wireshark
- Observed SYN, SYN-ACK, and ACK packets
- Monitored HTTP traffic and GET requests
- Used netstat to inspect active connections and ports
- Identified HTTP (80) and HTTPS (443) communications

## Web Security Relevance
Understanding the Transport Layer is essential for:


- Web traffic analysis
- Burp Suite interception
- Packet analysis with Wireshark
- Understanding HTTP/HTTPS communication
- Reconnaissance and service identification
- Understanding how browsers communicate with web servers

# Presentation and Session Layer

## Presentation Layer
The Presentation Layer is responsible for:
- Data formatting
- Compression
- Encryption and decryption

Examples:
- JSON
- HTML
- PNG
- HTTPS/TLS encryption

## Session Layer
The Session Layer manages communication sessions between applications.

Important concepts:
- Sessions
- Cookies
- Authentication
- User login tracking

## Web Security Relevance
Understanding these layers is important for:
- HTTPS encryption
- Session management
- Cookie analysis
- Authentication mechanisms
- Web application security testing
