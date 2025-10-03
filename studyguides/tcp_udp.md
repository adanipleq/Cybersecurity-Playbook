# 🔌 TCP vs UDP Study Guide

## 🌍 Overview
TCP and UDP are **Transport Layer protocols** in the OSI (Layer 4) and TCP/IP (Transport) models.  
They both provide communication between applications but differ in **reliability, speed, and use cases**.

---

## 📦 TCP (Transmission Control Protocol)
**Key Features:**
- Connection-oriented (requires a handshake)
- Reliable (ensures delivery, error-checking, retransmission)
- Ordered delivery (segments arrive in sequence)
- Flow control (windowing, congestion management)

**Header Fields:**
- Source Port, Destination Port
- Sequence Number, Acknowledgment Number
- Flags: SYN, ACK, FIN, RST, PSH, URG
- Window Size
- Checksum
- Urgent Pointer

**Common Ports (examples):**
- HTTP: 80
- HTTPS: 443
- SMTP: 25
- FTP: 20, 21
- SSH: 22
- Telnet: 23

---

## 📡 UDP (User Datagram Protocol)
**Key Features:**
- Connectionless (no handshake)
- Unreliable (no delivery guarantee)
- Faster, lightweight
- No flow control or ordering
- Good for real-time apps

**Header Fields:**
- Source Port, Destination Port
- Length
- Checksum
- Data

**Common Ports (examples):**
- DNS: 53
- DHCP: 67/68
- TFTP: 69
- SNMP: 161/162
- VoIP, streaming, gaming

---

## ⚡ TCP vs UDP Comparison

| Feature           | TCP                               | UDP                          |
|-------------------|-----------------------------------|------------------------------|
| Connection        | Connection-oriented (handshake)   | Connectionless               |
| Reliability       | Reliable, retransmits lost data   | Unreliable, no retransmission|
| Ordering          | Guarantees ordered delivery       | No ordering                  |
| Speed             | Slower (more overhead)            | Faster (lightweight)         |
| Use Cases         | Web, Email, File Transfer, SSH    | Streaming, DNS, VoIP, Gaming |

---

## 🛠 Study Tips
- **TCP = Reliable, Ordered, Slower → Email, Web, File Transfer**
- **UDP = Fast, Lightweight, Unreliable → Streaming, DNS, Games**
- Use mnemonics:
  - **"T" in TCP = Trustworthy** (reliable, ordered)
  - **"U" in UDP = Unreliable** (but Ultra-fast!)

---
