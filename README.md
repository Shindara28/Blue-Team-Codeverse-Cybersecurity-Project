# 🟦 Blue Team – Defense & Incident Response  
## Operation CodeVerse Breach

## 📌 Overview
This repository contains the Blue Team’s defensive monitoring, analysis, and incident response documentation for the **Operation CodeVerse Breach** simulated cybersecurity exercise.  
The objective of the exercise was to detect, analyze, and respond to reconnaissance and enumeration activity targeting a controlled environment, while strictly adhering to defined Rules of Engagement (ROE).

**Assessment Target:** `zonetransfer.me`  
**Team Role:** Blue Team (Defenders)

---

## 🎯 Objectives
- Monitor network and web traffic for anomalous behavior  
- Detect reconnaissance and enumeration activity  
- Analyze traffic using packet capture tools  
- Preserve forensic evidence  
- Perform structured incident response  
- Identify system weaknesses  
- Recommend appropriate security mitigations  

---

## 🛠 Tools & Techniques
- **Wireshark** – Network traffic capture and analysis  
- **PCAP Analysis** – Inspection of HTTP, TCP, DNS, and service discovery traffic  
- **Manual Log Review** – Identification of abnormal traffic patterns  
- **SOC-Style Documentation** – Incident logging and reporting  

---

---

## 🚨 Incident Summary
- **Incident ID:** INC-001  
- **Date:** 11th December 2025  
- **Time Window:** 12:30 PM – 2:30 PM  
- **System Affected:** Web traffic related to `zonetransfer.me`  
- **Detection Method:** Continuous Wireshark traffic monitoring  

### Observed Activity
- Repeated HTTP traffic over TCP (port 80)  
- Large HTTP payloads requiring TCP segmentation and reassembly  
- TCP anomalies including retransmissions and duplicate acknowledgments  
- SSDP M-SEARCH service discovery traffic  
- DNS-related activity suggesting information exposure risks  

No payload-based exploitation or confirmed system compromise was observed.

---

## 🧠 Key Findings
- Plaintext HTTP traffic introduces confidentiality risks  
- Reconnaissance and enumeration behavior was detected  
- DNS and service discovery configurations pose exposure risks  
- Lack of rate limiting increases susceptibility to automated requests  

---

## 🛡 Incident Response Actions
- Suspicious traffic identified and logged  
- IP addresses documented  
- Evidence preserved using PCAP files and screenshots  
- Enhanced monitoring applied  
- Defensive actions simulated in accordance with ROE  

---

## 🔐 Mitigation Recommendations
- Enforce HTTPS and disable plaintext HTTP  
- Secure DNS configurations and restrict zone transfers  
- Improve monitoring and alerting for abnormal traffic  
- Restrict unnecessary service discovery protocols  
- Implement rate limiting on web services  

---

## 📜 Blue Team Rules of Engagement (ROE)
- Blue Team operated strictly in a defensive capacity  
- Only approved monitoring and analysis tools were used  
- No services were shut down or disrupted  
- All containment actions were simulated and documented  
- Monitoring was limited to the approved scope (`zonetransfer.me`)  
- All findings were supported with evidence  
- Professional conduct and documentation were maintained  

---

## ✅ Final Assessment
The Blue Team successfully detected, analyzed, and documented reconnaissance and enumeration activity targeting the assessment environment. No confirmed breach occurred.  
The exercise demonstrated effective defensive monitoring, structured incident response, and actionable security recommendations.

---

## 📄 Documentation Included
- PCAP files  
- Wireshark analysis screenshots  
- SOC Log Analysis Report  
- Incident Report (INC-001)  
- Final Blue Team Defense Report  

---


**Prepared by:** Blue Team (Defenders)  
**Exercise:** Operation CodeVerse Breach
