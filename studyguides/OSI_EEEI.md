# 🌐 OSI & TCP/IP Models Quick Reference

## 🏗 OSI Model (Open Systems Interconnection — 7 Layers)

**Mnemonic:** *Please Do Not Throw Sausage Pizza Away* (top → bottom)

| Layer | Number | Purpose | Example Protocols |
|-------|--------|---------|-------------------|
| Application   | 7 | End-user interaction | HTTP, FTP, DNS, SMTP |
| Presentation  | 6 | Data format, encryption, compression | TLS, JPEG, PNG |
| Session       | 5 | Establish/manage sessions | NetBIOS, RPC |
| Transport     | 4 | Reliable delivery, segmentation | TCP, UDP |
| Network       | 3 | Logical addressing, routing | IP, ICMP |
| Data Link     | 2 | Framing, MAC addressing | Ethernet, Wi-Fi, ARP |
| Physical      | 1 | Transmission of bits | Cables, Fiber, Radio |

---

## 🌍 TCP/IP Model (DoD / IEEE — 4 Layers)

**Mnemonic:** *All Teachers Need Pizza*

| Layer | Purpose | Example Protocols |
|-------|---------|-------------------|
| Application   | User applications and data | HTTP, FTP, DNS, SMTP, SSH |
| Transport     | End-to-end communication | TCP, UDP |
| Internet      | Logical addressing & routing | IP, ICMP, ARP |
| Network Access (Link) | Physical transmission | Ethernet, Wi-Fi, PPP |

---

## ⚡ Key Differences: OSI vs TCP/IP

| Feature | OSI Model (7 Layers) | TCP/IP Model (4 Layers) |
|---------|----------------------|--------------------------|
| Layers  | 7                    | 4                        |
| Presentation & Session | Separate layers | Merged into Application |
| Data Link & Physical   | Separate layers | Merged into Link layer |
| Usage   | Theoretical, teaching | Practical, internet standard |

---

## 🎯 Why It Matters in Cybersecurity
- Firewalls/IDS filter traffic at specific layers.
- Wireshark and packet analyzers decode data layer by layer.
- Attacks target specific layers:
  - DoS/DDoS → Network/Transport layers
  - MITM → Data Link/Network
  - Phishing/Malware → Application layer

---

✍️ **Tip for Memorization:**
- OSI → *“Please Do Not Throw Sausage Pizza Away”*
- TCP/IP → *“All Teachers Need Pizza”*
