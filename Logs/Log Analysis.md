# Log Analysis Report

**Incident ID:** INC-001
**Analyst Role:** SOC Analyst – Blue Team
**Date of Analysis:** 11 December 2025

---

## Data Source

* **Packet Capture File:** `IMAGE2`
* **Analysis Tool:** Wireshark
* **Traffic Type:** Network Packet Capture (PCAP)

---

## 1. Executive Summary

This report documents the analysis of network traffic captured during routine monitoring activities. Review of the packet capture revealed a sustained **HTTP-over-TCP session** between an internal host and an external public IP address. The traffic involved **large HTTP payloads**, **TCP segmentation**, and **packet reassembly**, consistent with high-volume web content delivery.

No indicators of compromise (IOC), exploitation attempts, or data exfiltration were identified during this analysis. However, the use of **unencrypted HTTP** presents a potential security exposure and should be addressed to reduce risk.

---

## 2. Traffic Overview

| Attribute     | Details                                     |
| ------------- | ------------------------------------------- |
| Protocol      | HTTP over TCP                               |
| Encryption    | None (plaintext HTTP)                       |
| Internal Host | 192.168.69.175                               |
| External Host | 146.75.90.172                               |
| Server Port   | 80                                          |
| Client Ports  | 60203, 60194                                |
| Capture Type  | TCP stream with segmentation and reassembly |

---

## 3. Session Flow Analysis

### 3.1 TCP Session Behavior

The TCP session demonstrates standard and expected behavior:

* Proper TCP three-way handshake inferred (SYN, SYN-ACK, ACK)
* Sequential progression of sequence and acknowledgment numbers
* No observed TCP reset (RST) flags
* Stable TCP window sizes without congestion indicators

**Assessment:**
The TCP connection appears healthy and stable, with no network-layer anomalies detected.

---

### 3.2 HTTP Data Transfer Characteristics

The following indicators were consistently observed:

* `HTTP Continuation`
* `TCP PDU reassembled`
* Packets flagged with `[PSH, ACK]`

These indicators confirm:

* HTTP responses exceeding single TCP segment size
* Multiple TCP segments reassembled into complete HTTP messages
* **Frame 431** identified as containing the fully reassembled HTTP payload

---

## 4. Packet-Level Observations

Key packet details extracted from the capture include:

* **Frame size:** 2762 bytes
* **TCP payload length:** 2696 bytes
* **Source Port:** 80
* **Destination Port:** 60203
* **Traffic Direction:** Server → Client

The server actively transmitted large data segments, while the client primarily issued acknowledgment packets, indicating normal data delivery behavior.

---

## 5. Directional Traffic Analysis

| Traffic Direction             | Interpretation                       |
| ----------------------------- | ------------------------------------ |
| 146.75.90.172 → 192.168.69.175 | Server delivering HTTP response data |
| 192.168.69.175 → 146.75.90.172 | Client acknowledgments               |

This traffic pattern is consistent with web content delivery, such as HTML pages or static assets.

---

## 6. TCP Health Assessment

The following TCP anomalies were **not observed**:

* Duplicate acknowledgments
* Retransmissions
* Out-of-order packets
* Zero-window conditions

**Conclusion:**
The TCP session shows no signs of packet loss, congestion, or forced termination.

---

## 7. Likely Nature of Traffic

Based on the following factors:

* Use of TCP port 80
* Large HTTP payloads
* Multiple continuation packets
* External IP range commonly associated with Content Delivery Networks (CDNs)

The traffic most likely represents:

* Web page content
* JavaScript, CSS, or image assets
* CDN-served resources

While automated scanning or enumeration activity cannot be fully ruled out, no supporting indicators were observed at the application layer.

---

## 8. Security Observations

### Identified Risk

* Communication occurred over **unencrypted HTTP**
* Payload contents are transmitted in plaintext
* Any credentials, session tokens, or sensitive data would be exposed to interception

---

## 9. Analyst Actions & Recommendations

### Actions Taken

* Documented observed traffic session
* Identified and recorded relevant IP addresses
* Preserved evidence via packet capture file

### Recommendations

* Enforce HTTPS for all web-based communications
* Monitor repeated or sustained HTTP sessions from external IP addresses
* Correlate PCAP findings with web server and proxy access logs
* Implement rate limiting and alerting for abnormal HTTP request volumes

---

## 10. Conclusion

The analyzed network traffic represents a stable HTTP session with high-volume data transfer and no immediate indicators of malicious activity. Despite the benign nature of the observed traffic, the use of plaintext HTTP introduces unnecessary risk. Continued monitoring and implementation of encryption and security controls are recommended to reduce exposure

---

Report Status: **Submitted**
Prepared by: SOC Analysts:**OMOLEWA OYINDOLAPO AYOMIDE AND TIMOTHY VICTOR ONYEDIKACHUKWU** – Blue Team
