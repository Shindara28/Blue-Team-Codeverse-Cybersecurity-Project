Packets Capture Threat Hunting Report

Assignment Type: Packet Analysis & Threat Hunting
Student Name: Simon Daniel Mathew

1. Introduction

This report presents an examination of captured network traffic in order to determine whether malicious activity, data exfiltration, or command-and-control (C2) communication is present. The analysis is based on browser-level HTTP inspection and packet-level Wireshark captures provided as screenshots.

2. Scope & Objectives

Objectives

	•	Analyze HTTP and encrypted network traffic
	•	Identify indicators of compromise (IOCs)
	•	Assess network behavior using threat-hunting hypotheses
	•	Produce a defensible conclusion

Scope

	•	HTTP/2 browser traffic
	•	TLS 1.3 encrypted sessions
	•	QUIC (HTTP/3) traffic
	•	TCP retransmissions and resets

3. Evidence Overview

Evidence ID	Description	Tool
E-01	HTTP redirect traffic	Browser Network Inspector
E-02	Encrypted packet capture	Wireshark

4. Analysis

4.1 Evidence E-01 — HTTP Redirect Analysis

Observations

	•	HTTP/2 GET requests for / and /favicon.ico
	•	Server response: 301 Moved Permanently
	•	Redirects client to HTTPS resource
	•	Presence of security headers:
	•	Strict-Transport-Security
	•	X-Frame-Options
	•	X-Content-Type-Options
	•	Permissions-Policy

Analysis

A 301 Moved Permanently response indicates an intentional server-side redirect. The inclusion of multiple security headers demonstrates a hardened configuration designed to protect against downgrade attacks, clickjacking, and MIME-type confusion.

Finding

	This traffic represents legitimate web behavior with proper security enforcement.
No indicators of malicious redirection or exploitation were identified.

4.2 Evidence E-02 — Packet-Level Network Analysis

Protocols Identified

	•	TCP
	•	TLSv1.3
	•	QUIC (UDP/443)
	•	HTTP/3

TLS 1.3 Traffic

Encrypted application data was observed over TCP port 443. No malformed packets or handshake anomalies were present.

Assessment: Normal HTTPS communication.

QUIC Traffic

QUIC packets labeled as “Protected Payload” indicate encrypted HTTP/3 traffic, commonly used by modern browsers for performance optimization.

Assessment: Expected behavior; not evidence of evasion.

TCP Retransmissions

Several retransmitted packets and duplicate acknowledgements were observed.

Interpretation:
Likely caused by transient packet loss or network congestion. This is common in real-world networks and does not inherently indicate malicious activity.

TCP Reset (RST)

A limited number of TCP reset packets were observed.

Interpretation:
Likely caused by normal session termination, timeouts, or firewall behavior. No repeated pattern suggesting interference was identified.

5. Threat Hunting Analysis

Threat hunting focuses on testing hypotheses rather than relying solely on known signatures.

Hypothesis 1: Command-and-Control (C2) Activity

Evaluated Indicators

	•	Unusual ports ❌
	•	Beaconing intervals ❌
	•	Repeated outbound callbacks ❌

Result:
🟢 Hypothesis rejected — no C2 behavior detected.

Hypothesis 2: Data Exfiltration

Evaluated Indicators

	•	Large outbound transfers ❌
	•	DNS tunneling ❌
	•	Protocol misuse ❌

Result:
🟢 Hypothesis rejected — no exfiltration indicators observed.

Hypothesis 3: Malware Delivery

Evaluated Indicators

	•	Malicious redirects ❌
	•	Executable downloads ❌
	•	Suspicious MIME types ❌

Result:
🟢 Hypothesis rejected — no malware delivery observed.

Hypothesis 4: Network Evasion Techniques

Evaluated Indicators

	•	Encrypted traffic ✔ (expected)
	•	QUIC usage ✔ (expected)
	•	Fragmentation abuse ❌

Result:
🟢 Hypothesis rejected — no evasion techniques detected.

6. Risk Assessment

Category	Risk Level
Malware Presence	None
Data Loss	None
Network Instability	Low
Policy Violation	None

7. Limitations

	•	Encrypted payloads could not be decrypted
	•	No raw PCAP file available
	•	No endpoint telemetry provided

Despite these limitations, the evidence supports a confident conclusion.

8. Conclusion

Based on examination and threat-hunting analysis, the observed traffic represents normal, secure web communication using modern protocols. No indicators of compromise, malicious activity, or policy violations were identified.

9. References

	•	Wireshark User Guide
	•	NIST SP 800-61 (Incident Handling)
	•	MITRE ATT&CK Framework
