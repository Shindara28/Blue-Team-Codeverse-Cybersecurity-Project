# Incident Response Report

## Incident Details

- **Incident ID:** INC-001  
- **Date & Time:** 11th December 2025  
  **Time Window:** Approx. 12:30 PM – 2:30 PM (WAT)  
- **Team:** Blue Team  
- **System Affected:** Web Server (HTTP)  
- **Internal IP Address:** 192.168.69.175  

---

## 1. Executive Summary

During routine network monitoring, suspicious HTTP traffic was observed targeting the web server at IP address 192.168.69.175. The activity involved repeated HTTP requests and anomalous TCP behaviors, including retransmissions, duplicate acknowledgements, and reset packets. Additionally, SSDP (Simple Service Discovery Protocol) discovery traffic was observed within the network.

Based on the observed traffic characteristics and behaviors, the activity was assessed as web reconnaissance and potential automated scanning, likely targeting exposed directories or vulnerable endpoints. No evidence of successful exploitation, system compromise, or data exfiltration was identified. The incident was documented, monitored, and contained through enhanced observation and simulated defensive measures
---

## 2. Monitoring Setup

**Detection and Analysis**
- The incident was detected and analyzed using the following tools and configurations
_ **Tool Used:** Wireshark and Burpsuite
 
- **Monitoring Method:**
     - Live packet capture
     - Offline PCAP (Packet Capture) analysis
     - **PCAP File:** wire.pcapng
- **Protocols Monitored**
  - HTTP
  - TCP
  - TLS (Transport Layer Security)
  - QUIC (Quick UDP Internet Connections)
  - SSDP (Simple Service Discovery Protocol)
- Traffic was analyzed for anomalies, including repeated requests, abnormal packet behaviors, and unexpected service discovery activity.

## 3. Attack Detection Log

| Time Range        | Source IP        | Destination IP     | Protocol   | Observation                                   |
|-------------------|------------------|--------------------|------------|-----------------------------------------------|
| 12:30–2:30 PM     | 146.75.90.172    | 192.168.69.175      | HTTP/TCP  | Repeated HTTP requests    |                    
| Various           | 192.168.0.172    | Internal Host      | TCP       | Suspicious traffic patterns                   |
| Various           | 192.168.0.151    | Internal Host      | TCP       | Network anomalies                             |
| Various           | 192.168.0.134    | Internal Host      | TCP       | TCP retransmissions                           |
| Various           | 192.168.0.197    | Internal Host      | TCP       | Duplicate acknowledgements (ACKs)             |
| Various           | 192.168.0.185    | Internal Host      | SSDP      | M-SEARCH discovery requests                   |

---

## 4. Traffic Analysis (Wireshark and Burpsuite)

Analysis of the PCAP file and supporting screenshots revealed the following indicators:

- Repeated HTTP requests originating from an external IP address.
- TCP anomalies, including:
  - Duplicate acknowledgements  
  - Retransmissions  
  - Reset (RST) packets  
- SSDP M-SEARCH traffic indicating possible service discovery or background scanning activity.

These indicators are consistent with reconnaissance or enumeration behavior rather than direct exploitation attempts.

---


## 5. System Weaknesses Identified

- Open HTTP service exposed to external traffic.
- Lack of visible rate-limiting mechanisms on web endpoints.
- Absence of automated alerting for abnormal request frequency.
- Presence of SSDP traffic, indicating potentially unnecessary service exposure within the network.

---

## 6. Mitigation Recommendations

To reduce future risk, the following measures are recommended:

- Implement rate limiting on web services.
- Restrict access to sensitive directories and administrative endpoints.
- Disable or limit unnecessary discovery services such as SSDP.
- Enable automated alerts for abnormal HTTP request patterns.
- Apply proactive firewall rules to block suspicious or malicious IP addresses.

---

## 7. Final Assessment

The incident was successfully detected, analyzed, and contained by the Blue Team. No evidence of data loss, system compromise, or service disruption was identified. The activity is classified as **low-to-moderate risk reconnaissance**.

Overall, the Blue Team demonstrated effective monitoring, analysis, and incident response capabilities, meeting the objectives of the simulated defensive exercise.

---

## **Incident Responder**

**SAADU AMINULLAHI ABDULLAHI and AYILEKA NAHEEM ABIODUN**
