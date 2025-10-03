# 🔌 Socket Pairs Study Guide  
*CNS-101: Intro to Cybersecurity — Networking Foundations*  

---

## 📖 1. What is a Socket?  
A **socket** is one endpoint of a two-way communication link between two programs running on a network.  
It consists of:  

- **IP address** (identifies the host)  
- **Port number** (identifies the process/service on that host)  

---

## 🔗 2. What is a Socket Pair?  
A **socket pair** is the combination of two sockets that define a unique communication session.  

```
(Source IP : Source Port)  <-->  (Destination IP : Destination Port)
```

**Example:**  

```
192.168.1.25:49152  <-->  142.250.72.238:443
```

- `192.168.1.25` = client’s private IP  
- `49152` = client’s ephemeral port  
- `142.250.72.238` = Google’s server IP  
- `443` = HTTPS port  

---

## 🌐 3. Why Socket Pairs Matter  

- They uniquely identify **TCP connections**  
- Enable **multiplexing** (many simultaneous sessions)  
- Help in **firewall rules** (allowing/denying traffic by IP:port)  
- Used in **digital forensics** to track malicious connections  

---

## ⚙️ 4. TCP vs UDP and Socket Pairs  

### TCP (Connection-Oriented)  
- Requires a 4-tuple:  

```
(Source IP, Source Port, Destination IP, Destination Port)
```

- Each TCP session is uniquely identified by its socket pair  
- **Example:** SSH, HTTPS  

### UDP (Connectionless)  
- Also uses socket pairs, but:  
  - No handshake  
  - Multiple datagrams may share the same pair  
- **Example:** DNS, streaming apps  

---

## 📊 5. Example Flow (TCP Handshake)  

```
Client: 10.0.0.5:54321  --->  Server: 8.8.8.8:80
          SYN

Client: 10.0.0.5:54321  <---  Server: 8.8.8.8:80
          SYN-ACK

Client: 10.0.0.5:54321  --->  Server: 8.8.8.8:80
          ACK
```

At this point, the socket pair `(10.0.0.5:54321, 8.8.8.8:80)` defines the connection.  

---

## 🔍 6. Common Use Cases  

- **Web Browsing:**  

```
(client_IP:random_port, server_IP:443)
```

- **SSH Sessions:**  

```
(client_IP:random_port, server_IP:22)
```

- **Malware C2 Tracking:** Analysts trace malicious socket pairs to find attackers.  
- **Firewall/IDS Rules:** Blocking by specific IP:port pairs.  

---

## 🧪 7. Lab Exercises  

### Exercise 1: Identify Socket Pairs with `netstat`  

```
# Linux / Mac
netstat -n

# Windows PowerShell
netstat -n
```

1. List 3 active socket pairs.  
2. Identify which ones are **TCP** vs **UDP**.  

---

### Exercise 2: Trace an HTTPS Connection  

```
# Windows
netstat -an | findstr 443

# Linux
ss -t -a
```

- Note the socket pair:  
  - Source IP:Port = your device’s IP and ephemeral port  
  - Destination IP:443 = the web server  

---

### Exercise 3: Firewall Thought Experiment  

```
Policy: Block all outgoing socket pairs to port 22
```

Questions:  
- Which type of traffic is being blocked?  
- Why might this be important in cybersecurity?  

---

## ✅ 8. Key Takeaways  

- Socket pairs = **two endpoints (IP:Port <-> IP:Port)**  
- They uniquely identify TCP sessions  
- Critical for networking, forensics, and cybersecurity defense  

---

*End of Guide*  
