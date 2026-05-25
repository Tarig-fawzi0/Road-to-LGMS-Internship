# DNS and TCP Observation

## Objective

Observe how a browser resolves a domain name and establishes a TCP connection.

---

# Practical Steps

### Step 1

Opened Wireshark.
<img width="1208" height="1025" alt="Screenshot 2026-05-26 025858" src="https://github.com/user-attachments/assets/2533467c-fe7d-4807-a70b-da0bdb25983f" />

 

### Step 2

Visited a website.

 <img width="1878" height="1035" alt="image" src="https://github.com/user-attachments/assets/a83d25a8-5a32-43e8-a15c-17764cea202f" />


### Step 3

Observed DNS packets.

 <img width="1757" height="42" alt="image" src="https://github.com/user-attachments/assets/e324a0ee-470c-4072-a1ee-64a4cf86e461" />


### Step 4

Observed TCP Handshake.
 <img width="1221" height="409" alt="image" src="https://github.com/user-attachments/assets/89a28878-d06e-47b8-955a-59e7fc4cbbeb" />


# Observations

DNS resolves domain names to IP addresses.

TCP establishes reliable communication before data transmission.

---

# Findings

Observed:

- DNS Query
- DNS Response
- SYN
- SYN-ACK
- ACK

---

# Lessons Learned

- DNS translates domain names into IP addresses.
- TCP uses a three-way handshake.
- HTTP communication depends on successful TCP connections.

---

# Conclusion

Successfully observed DNS resolution and TCP connection establishment.
