# 🟦 Blue Team – Defense & Incident Response Report

## Operation CodeVerse Breach

### Team
**Blue Team (B1 / B2)**

### Members (11 Students)
Oluwashindara Toluwanimi Majiyagbe

Oba Abdulkadir

Abdulrasheed Abdulmalik Abbey

Simon Daniel Mathew

Bamidele Oloruntobi David

Ayileka Naheem Abiodun 

Saadu Aminullahi Abdullahi

Oyindolapo Ayomide Omolewa

Timothy Victor Onyedikachukwu

Habeeb Abdulrahman

Olohun-oyin Ayomide Ibrahim

Yusuf Abdulqoyum Ayodeji

### Date
11th to 18th of December 2025

---
## Role Assignment
**Defence Team Lead:** Oluwashindara Toluwanimi Majiyagbe
She coordinated all team activities and task assignments while overseeing monitoring, detection, and incident response operations. She ensured compliance with the Rules of Engagement and reviewed and finalized the incident report.

**SOC Analysts:** Oyindolapo Ayomide Omolewa, Timothy Victor Onyedikachukwu and Olohun-oyin Ayomide Ibrahim 
They reviewed system, server, and SOC logs to identify abnormal patterns and potential threats. They logged timestamps, source and destination IPs, and correlated network events with observed suspicious activity.

**Incident Responders:** Saadu Aminullahi Abdullahi and Ayileka Naheem Abiodun 
The Incident Responders investigated alerts and unusual traffic patterns while preserving evidence including PCAPs, screenshots, and logs. They simulated containment actions such as IP blocking or traffic restrictions in accordance with the Rules of Engagement.

**Traffic Monitors:** Bamidele Oloruntobi David, Simon Daniel Mathew and Habeeb Abdulrahman
They captured and analyzed network traffic using Wireshark and Burpsuite, identifying suspicious HTTP, TCP, and service discovery activity. They applied filters to isolate anomalous behavior and reported all findings to the team.

**Evidence Analysts:** Oba Abdulkadir, Abdulrasheed Abdulmalik Abbey and Yusuf Abdulqoyum Ayodeji
They maintained detailed SOC records of monitoring and response activities. They prepared supporting evidence for the final report and ensured accurate record-keeping for lessons learned and future reference.

## Blue Team Objectives
- Monitor network and system activity for suspicious or anomalous behavior.  
- Detect reconnaissance, enumeration, and potential attack attempts.  
- Respond to incidents by analyzing traffic and preserving evidence.  
- Simulate defensive actions within the Rules of Engagement.  
- Identify system weaknesses and provide actionable mitigation recommendations.  
- Document all findings, responses, and lessons learned for reporting.

## Rules of Engagement (ROE)
- Only approved defensive tools were used.  
- Actions were limited to the authorized domain/IP scope.  
- All observations and responses were logged with evidence.  
- No server shutdowns or service disruptions; all actions were simulated.  
- No configuration changes beyond the exercise scope.  
- A final report documenting findings and actions was submitted.

## Executive Summary
This report presents the Blue Team’s defensive monitoring, detection, and incident response activities conducted during the Operation CodeVerse Breach simulated cybersecurity exercise. The assessment focused on monitoring network and web traffic related to the domain **zonetransfer.me**, with the objective of identifying reconnaissance, enumeration, and anomalous activity.

During the exercise window, the Blue Team detected:

- Repeated HTTP traffic  
- Large data transfers requiring TCP segmentation and reassembly  
- Anomalous TCP behavior  
- Service discovery traffic  
- DNS-related activity  

These indicators were consistent with reconnaissance and information-gathering techniques. All suspicious activity was documented and preserved as evidence. No confirmed system compromise or data breach was observed.

---

## Monitoring Setup

### Tools Used
- **Wireshark** – Network packet capture and analysis  
- **PCAP Analysis** – Inspection of HTTP, TCP, DNS, and service discovery traffic  
- **Manual Log Review** – Identification of abnormal patterns  
- **Burpsuite** – Network packet capture and analysis 

### Monitoring Scope
- Target domain: **zonetransfer.me**  
- Web traffic over HTTP (port 80)  
- DNS traffic and service discovery protocols  

---

## Attack Detection Log

| Date       | Time Range       | Source IP      | Destination      | Protocol | Observed Activity                  |
|-----------|----------------|----------------|-----------------|----------|-----------------------------------|
| 11-12-2025 | 12:30 PM – 2:30 PM | 146.75.90.172 | 192.168.0.166   | HTTP/TCP | Repeated HTTP communication       |
| 11-12-2025 | Various        | 192.168.0.172 | Internal hosts  | TCP      | Anomalous traffic patterns        |
| 11-12-2025 | Various        | 192.168.0.151 | Internal hosts  | TCP      | Suspicious network behavior       |
| 11-12-2025 | Various        | 192.168.0.134 | Internal hosts  | TCP      | Retransmissions observed          |
| 11-12-2025 | Various        | 192.168.0.197 | Internal hosts  | TCP      | Duplicate acknowledgments         |
| 11-12-2025 | Various        | 192.168.0.185 | Internal hosts  | SSDP     | M-SEARCH discovery traffic        |

---

## Traffic Analysis (Wireshark)

### Key Findings
- HTTP over TCP communication on port 80  
- Large HTTP responses requiring TCP PDU reassembly  
- Sustained request-response traffic patterns  
- TCP anomalies including retransmissions and duplicate ACKs  
- SSDP M-SEARCH packets indicating service discovery activity  
- DNS-related traffic suggesting potential information exposure  

### Filters Used
tcp
http
dns
ssdp


### Security Observation
All observed HTTP traffic was transmitted in plaintext, presenting confidentiality risks.

---

## Incident Response Actions
The Blue Team executed the following response steps:

1. Identified suspicious traffic through continuous monitoring  
2. Logged timestamps, IP addresses, and traffic patterns  
3. Preserved evidence using PCAP files and screenshots  
4. Conducted detailed traffic analysis using Wireshark  
5. Simulated defensive actions, including IP blocking recommendations  
6. Increased monitoring of HTTP, DNS, and discovery traffic  

> No server shutdowns were performed, in compliance with the Rules of Engagement.

---

## System Weaknesses Identified
- Use of unencrypted HTTP traffic  
- Exposure to reconnaissance and enumeration techniques  
- Potential DNS misconfigurations leading to information disclosure  
- Lack of rate limiting on web services  
- Presence of unnecessary service discovery traffic  

---

## Mitigation Recommendations
- **Enforce HTTPS** – Disable plaintext HTTP where possible  
- **Secure DNS Configuration** – Restrict DNS zone transfers; remove sensitive info from DNS records  
- **Improve Monitoring & Alerting** – Enable alerts for abnormal HTTP and DNS behavior  
- **Restrict Service Discovery** – Disable or limit SSDP where not required  
- **Implement Rate Limiting** – Prevent excessive automated requests  

---

## Final Assessment
The Blue Team successfully detected and analyzed network activity consistent with reconnaissance and information-gathering behavior targeting **zonetransfer.me**. Evidence was properly collected and documented, and simulated response actions were performed in accordance with the Rules of Engagement.

No confirmed breach or exploitation occurred. The exercise demonstrated effective defensive monitoring while highlighting areas for security improvement.

---



**Report Status:** Final  
**Prepared by:** 
Defence Team Lead (Oluwashindara Toluwanimi Majiyagbe)and The Evidence Analysts (Oba Abdulkadir, Abdulrasheed Abdulmalik Abbey and Yusuf Abdulqoyum Ayodeji)

**Supporting Evidence:**
- Wireshark Analysis & Screenshots  
- Log Analysis Report  
- Incident Report INC-001
