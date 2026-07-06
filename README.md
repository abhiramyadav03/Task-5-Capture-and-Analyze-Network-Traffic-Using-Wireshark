# Task 5: Capture and Analyze Network Traffic Using Wireshark

## Objective

Capture live network traffic using Wireshark, analyze captured packets, identify common network protocols, and understand how devices communicate over a network.

---

## Tools Used

- Wireshark v4.6.6
- Npcap 1.88
- Windows 11 (Host Machine)
- Wi-Fi Network Interface
- Google Chrome / Microsoft Edge
- Command Prompt

---

## Capture Statistics

| Parameter | Value |
|-----------|-------|
| Capture Interface | Wi-Fi |
| Total Packets Captured | 4,161 |
| Dropped Packets | 0 (0.0%) |
| Capture Duration | ~1 Minute |
| Packet Capture Format | `.pcapng` |

---

# Procedure

### Step 1
Installed **Wireshark 4.6.6** together with **Npcap 1.88**, which enables live packet capturing on Windows.

### Step 2
Launched Wireshark and selected the active **Wi-Fi** network interface.

### Step 3
Started live packet capture.

### Step 4
Generated network traffic by:

- Browsing websites:
  - Google
  - Bing
  - GitHub
  - ChatGPT
  - Microsoft Office services
- Running the following commands:

```cmd
ping google.com -n 10
```

```cmd
ping 142.250.207.238
```

### Step 5

Allowed the capture to run for approximately one minute while various protocols were exchanged.

### Step 6

Stopped the capture using the **Stop Capture** button.

### Step 7

Applied Wireshark display filters to isolate individual protocols.

### Step 8

Saved the packet capture as:

```
task5_capture.pcapng
```

---

# Display Filters Used

| Protocol | Filter |
|-----------|---------|
| DNS | `dns` |
| TCP | `tcp` |
| TLS | `tls` |
| ICMP | `icmp` |
| ARP | `arp` |

---

# Protocols Identified

## 1. DNS (Domain Name System)

### Purpose
Resolves domain names into IP addresses before communication begins.

### Observation

Captured DNS queries and responses including:

- www.bing.com
- google.com
- Microsoft services

Example:

```
Query:
www.bing.com

Response:
CNAME e86303.dscx.akamaiedge.net

IP:
23.65.124.88
```

---

## 2. TCP (Transmission Control Protocol)

### Purpose

Reliable, connection-oriented communication.

### Observation

Observed:

- SYN
- SYN-ACK
- ACK

forming the TCP Three-Way Handshake.

Example:

```
Destination:
52.98.123.226

Port:
443 (HTTPS)
```

---

## 3. TLS (Transport Layer Security)

### Purpose

Encrypts communication between client and server.

### Observation

Captured:

- TLS 1.2
- TLS 1.3
- Client Hello
- Server Hello
- Change Cipher Spec
- Application Data

Observed SNI:

```
substrate.office.com
```

and

```
s-ring.msedge.net
```

---

## 4. ICMP (Internet Control Message Protocol)

### Purpose

Used for diagnostics and network testing.

### Observation

Generated using:

```cmd
ping google.com
```

Observed:

- Echo Request
- Echo Reply

Destination:

```
142.250.207.238
```

---

## 5. ARP (Address Resolution Protocol)

### Purpose

Maps IP addresses to MAC addresses on the local network.

### Observation

Captured broadcast requests such as:

```
Who has 192.168.1.18?

Tell 192.168.1.6
```

---

## 6. QUIC (Bonus Protocol)

### Purpose

Modern encrypted transport protocol developed by Google over UDP.

### Observation

Captured QUIC Initial packets containing:

- CRYPTO
- PING
- PADDING

This protocol provides faster encrypted communication than traditional TCP + TLS.

---

# Sample Packet Details

| Field | Value |
|-------|-------|
| Source IP | 192.168.1.6 |
| Destination IP | 192.168.1.1 |
| Protocol | DNS |
| Transport | UDP |
| Source Port | 57157 |
| Destination Port | 53 |
| Purpose | Domain Name Resolution |

---

# Key Observations

- DNS resolution always occurred before HTTPS connections were established.
- TCP performed reliable connection establishment using the Three-Way Handshake.
- TLS encrypted application data while still exposing metadata such as the Server Name Indication (SNI).
- ICMP packets confirmed successful communication between hosts using Echo Requests and Replies.
- ARP traffic was limited to the local network and used broadcast communication.
- QUIC traffic was observed alongside TLS, demonstrating that modern browsers use UDP-based encrypted communication.
- Both unicast and broadcast packets were present throughout the capture.
- Request-response communication patterns were successfully observed for DNS, ICMP, and ARP.

---

# Screenshots

The repository contains screenshots demonstrating packet analysis using various display filters.

- Full Packet Capture
- DNS Filter
- TCP Filter
- TLS Filter
- ICMP Filter
- ARP Filter

---

# Repository Structure

```
Task-5-Capture-and-Analyze-Network-Traffic-Using-Wireshark
│
├── README.md
├── task5_capture.pcapng
│
└── screenshots
    ├── 01-full_capture.png
    ├── 02-dns_filter.png
    ├── 03-tcp_filter.png
    ├── 04-tls_filter.png
    ├── 05-icmp_filter.png
    └── 06-arp_filter.png
```

---

# Outcome

Successfully captured and analyzed live network traffic using Wireshark.

Identified and analyzed multiple protocols including:

- DNS
- TCP
- TLS
- ICMP
- ARP
- QUIC

Applied protocol-specific display filters, examined packet-level details, interpreted protocol behavior, and gained practical experience in packet capture, protocol analysis, and network troubleshooting.

---

# Interview Questions

## 1. What is Wireshark?

Wireshark is a network protocol analyzer that captures and analyzes network traffic in real time. It is widely used for network troubleshooting, protocol analysis, and cybersecurity investigations.

---

## 2. What is a packet?

A packet is a small unit of data transmitted across a network. It contains a header with addressing information and a payload containing the actual data.

---

## 3. How do you filter packets in Wireshark?

Packets can be filtered using display filters such as:

```
dns
tcp
tls
icmp
arp
ip.addr==192.168.1.1
tcp.port==443
```

---

## 4. What is the difference between TCP and UDP?

| TCP | UDP |
|------|------|
| Connection-Oriented | Connectionless |
| Reliable | Faster |
| Guarantees Delivery | No Delivery Guarantee |
| Error Checking | Minimal Error Recovery |
| Used for HTTP/HTTPS, Email | Used for DNS, Streaming, Gaming, QUIC |

---

## 5. What is a DNS query packet?

A DNS query packet is a request sent to a DNS server asking it to resolve a domain name into an IP address.

Example:

```
google.com

↓

142.250.x.x
```

---

## 6. How can packet capture help in troubleshooting?

Packet capture helps identify:

- DNS failures
- Network latency
- Packet loss
- Connection failures
- TCP retransmissions
- Protocol errors
- Unexpected or malicious traffic

---

## 7. What is a protocol?

A protocol is a standardized set of rules that governs how devices communicate over a network.

Examples include:

- HTTP
- HTTPS
- DNS
- TCP
- UDP
- ICMP
- ARP

---

## 8. Can Wireshark decrypt encrypted traffic?

Not by default.

However, Wireshark can decrypt TLS traffic if the appropriate decryption keys or SSL/TLS key log file is provided. Without these keys, encrypted application data remains unreadable.

---

# Conclusion

This project provided practical experience in capturing and analyzing real-time network traffic using Wireshark. Various protocols including DNS, TCP, TLS, ICMP, ARP, and QUIC were successfully identified and analyzed. The task improved understanding of packet structures, protocol communication, encrypted traffic analysis, and network troubleshooting techniques used in cybersecurity and network administration.
