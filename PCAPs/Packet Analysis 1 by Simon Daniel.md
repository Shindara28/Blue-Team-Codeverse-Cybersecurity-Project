# Packet Capture Threat Hunting Report

**Assignment Type:** Packet Analysis & Threat Hunting  
**Student Name:** Simon Daniel Mathew  

---

## 1. Introduction

This report examines captured network traffic to determine the presence of malicious activity, data exfiltration, or command-and-control (C2) communications. Analysis is based on browser-level HTTP inspection and packet-level Wireshark captures provided as screenshots.

---

## 2. Scope & Objectives

**Objectives**
- Analyze HTTP and encrypted network traffic  
- Identify indicators of compromise (IOCs)  
- Assess network behavior using threat-hunting hypotheses  
- Draw defensible conclusions  

**Scope**
- HTTP/2 browser traffic  
- TLS 1.3 encrypted sessions  
- QUIC (HTTP/3) traffic  
- TCP retransmissions and resets  

---

## 3. Evidence Overview

| Evidence ID | Description                | Tool                        |
|------------|----------------------------|-----------------------------|
| E-01       | HTTP redirect traffic       | Browser Network Inspector   |
| E-02       | Encrypted packet capture    | Wireshark                   |

---

## 4. Analysis

### 4.1 Evidence E-01 — HTTP Redirect Analysis

**Observations**
- HTTP/2 GET requests for `/` and `/favicon.ico`  
- Server responded with `301 Moved Permanently`  
- Redirected client to HTTPS resource  
- Security headers present: `Strict-Transport-Security`, `X-Frame-Options`, `X-Content-Type-Options`, `Permissions-Policy`  

**Analysis**  
The 301 response indicates an intentional redirect. Security headers demonstrate a hardened server configuration to prevent downgrade attacks, clickjacking, and MIME-type issues.  

**Finding**  
This traffic represents normal, secure web behavior. No evidence of malicious redirection or exploitation was detected.  

---

### 4.2 Evidence E-02 — Packet-Level Network Analysis

**Protocols Observed**
- TCP  
- TLS 1.3  
- QUIC (UDP/443)  
- HTTP/3  

**TLS 1.3 Traffic**  
Encrypted application data over TCP port 443 was observed. No malformed packets or handshake anomalies were detected.  
**Assessment:** Normal HTTPS communication.  

**QUIC Traffic**  
QUIC packets labeled as "Protected Payload" indicate encrypted HTTP/3 traffic, consistent with modern browser behavior.  
**Assessment:** Expected behavior; not indicative of evasion.  

**TCP Retransmissions**  
Some retransmitted packets and duplicate acknowledgements were seen.  
**Interpretation:** Likely caused by transient packet loss or network congestion; not necessarily malicious.  

**TCP Reset (RST)**  
A limited number of TCP reset packets were observed.  
**Interpretation:** Likely due to normal session termination, timeouts, or firewall behavior. No pattern suggesting interference was detected.  

---

## 5. Threat Hunting Analysis

Threat hunting focused on testing hypotheses rather than relying solely on known signatures.  

**Hypothesis 1 — Command-and-Control (C2) Activity**  
- Unusual ports ❌  
- Beaconing intervals ❌  
- Repeated outbound callbacks ❌  
**Result:** Rejected; no C2 behavior detected.  

**Hypothesis 2 — Data Exfiltration**  
- Large outbound transfers ❌  
- DNS tunneling ❌  
- Protocol misuse ❌  
**Result:** Rejected; no exfiltration observed.  

**Hypothesis 3 — Malware Delivery**  
- Malicious redirects ❌  
- Executable downloads ❌  
- Suspicious MIME types ❌  
**Result:** Rejected; no malware activity observed.  

**Hypothesis 4 — Network Evasion Techniques**  
- Encrypted traffic ✔ (expected)  
- QUIC usage ✔ (expected)  
- Fragmentation abuse ❌  
**Result:** Rejected; no evasion techniques detected.  

---

## 6. Risk Assessment

| Category              | Risk Level |
|----------------------|------------|
| Malware Presence      | None       |
| Data Loss             | None       |
| Network Instability   | Low        |
| Policy Violation      | None       |

---

## 7. Limitations
- Encrypted payloads could not be decrypted  
- Raw PCAP file was not available  
- No endpoint telemetry provided  

Despite these limitations, the evidence supports a confident conclusion.  

---

## 8. Conclusion

Analysis indicates that the observed traffic reflects **normal, secure web communication using modern protocols**. No indicators of compromise, malicious activity, or policy violations were identified.  

---


## 9. References
- Wireshark User Guide  
- NIST SP 800-61 (Computer Security Incident Handling Guide)  
- MITRE ATT&CK Framework  
