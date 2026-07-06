# Task 5: Capture and Analyze Network Traffic Using Wireshark

## Objective

Capture live network traffic using Wireshark, analyze captured packets, identify common network protocols, and understand how devices communicate over a network.

---

# Tools Used

- Wireshark v4.6.6
- Npcap 1.88
- Windows 11 (Host Machine)
- Wi-Fi Network Interface
- Microsoft Edge
- Command Prompt

---

# Capture Statistics

| Parameter | Value |
|-----------|-------|
| Capture Interface | Wi-Fi |
| Total Packets Captured | 4,161 |
| Dropped Packets | 0 (0.0%) |
| Capture Duration | Approximately 1 Minute |
| Packet Capture Format | `.pcapng` |

---

# Procedure

### Step 1
Installed **Wireshark 4.6.6** together with **Npcap 1.88**, which enables live packet capture on Windows.

### Step 2
Opened Wireshark and selected the active **Wi-Fi** network interface.

### Step 3
Started live packet capture.

### Step 4
Generated network traffic by:

- Visiting websites:
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

Allowed the capture to continue for approximately one minute while network traffic was generated.

### Step 6

Stopped packet capture using the **Stop Capture** button.

### Step 7

Applied Wireshark display filters to analyze different network protocols.

### Step 8

Saved the packet capture as:

```
task5_capture.pcapng
```

---

# Display Filters Used

| Protocol | Display Filter |
|-----------|----------------|
| DNS | `dns` |
| TCP | `tcp` |
| TLS | `tls` |
| ICMP | `icmp` |
| ARP | `arp` |

---

# Protocols Identified

## 1. DNS (Domain Name System)

### Purpose

DNS translates domain names into IP addresses before a connection is established.

### Observation

Captured DNS queries and responses for:

- google.com
- www.bing.com
- Microsoft services

Example:

```
Query:
www.bing.com

Response:
CNAME e86303.dscx.akamaiedge.net

Resolved IP:
23.65.124.88
```

---

## 2. TCP (Transmission Control Protocol)

### Purpose

TCP provides reliable, connection-oriented communication between network devices.

### Observation

Observed TCP communication over HTTPS (port 443), including connection establishment and data transfer.

Example:

```
Destination:
52.98.123.226

Port:
443
```

---

## 3. TLS (Transport Layer Security)

### Purpose

TLS encrypts data exchanged between a client and a server over HTTPS.

### Observation

Captured:

- TLS 1.2
- TLS 1.3
- Client Hello
- Server Hello
- Change Cipher Spec
- Application Data

Observed Server Name Indication (SNI):

```
substrate.office.com
```

```
s-ring.msedge.net
```

---

## 4. ICMP (Internet Control Message Protocol)

### Purpose

ICMP is used for network diagnostics and connectivity testing.

### Observation

Generated ICMP traffic using:

```cmd
ping google.com
```

Observed:

- Echo Request
- Echo Reply

Example destination:

```
142.250.207.238
```

---

## 5. ARP (Address Resolution Protocol)

### Purpose

ARP maps IP addresses to MAC addresses within the local network.

### Observation

Captured broadcast requests such as:

```
Who has 192.168.1.18?

Tell 192.168.1.6
```

---

## 6. QUIC (Additional Observation)

### Purpose

QUIC is a modern encrypted transport protocol developed by Google that operates over UDP and improves connection performance.

### Observation

Captured QUIC Initial packets containing:

- CRYPTO
- PING
- PADDING

This indicates that some web services were using QUIC instead of traditional TCP + TLS.

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

- DNS queries occurred before HTTPS connections were established.
- TCP provided reliable communication for encrypted web traffic.
- TLS encrypted application data while exposing metadata such as the Server Name Indication (SNI).
- ICMP Echo Requests and Replies confirmed successful network connectivity.
- ARP traffic was limited to local network communication.
- QUIC traffic was observed for some Google services, demonstrating modern encrypted communication over UDP.
- Both broadcast and unicast traffic were captured during analysis.
- Wireshark display filters made it easy to isolate and inspect individual protocols.

---

# Screenshots

The repository contains screenshots demonstrating packet analysis using Wireshark.

- Full Packet Capture
- DNS Filter
- TCP Filter
- TLS Filter
- ICMP Filter
- ARP Filter

---


---

# Outcome

Successfully captured and analyzed live network traffic using Wireshark.

Identified and analyzed multiple network protocols including:

- DNS
- TCP
- TLS
- ICMP
- ARP
- QUIC

Applied protocol-specific display filters, examined packet-level information, and gained practical experience in packet capture, protocol analysis, and network troubleshooting.

---

# Conclusion

This project provided practical experience in capturing and analyzing real-time network traffic using Wireshark. Multiple network protocols were successfully identified and examined, improving understanding of packet structures, protocol communication, encrypted traffic analysis, and troubleshooting techniques. The task strengthened practical skills in network monitoring and protocol analysis, which are essential in cybersecurity and network administration.
