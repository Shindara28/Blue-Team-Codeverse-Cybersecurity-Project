Incident ID

INC-001

Date & Time

11th December 2025
Approx. 12:30 PM – 2:30 PM (WAT)

Team

Blue Team

System Affected

Web Server (HTTP)

Internal IP Address: 192.168.0.166




1. Executive Summary

During routine network monitoring, the Blue Team detected suspicious HTTP and network traffic targeting the internal web server at 192.168.0.166. The activity involved repeated HTTP requests, large payload transfers requiring TCP reassembly, and anomalous TCP behaviors including retransmissions, duplicate acknowledgements, and reset packets. Additional SSDP discovery traffic was also observed.

Based on traffic patterns and behavior, the activity was assessed as web reconnaissance and potential automated scanning, likely aimed at identifying exposed directories or vulnerable endpoints. No confirmed system compromise or data breach was identified. The incident was documented, monitored, and contained through increased observation and simulated defensive actions.




2. Monitoring Setup

The incident was detected using the following tools and configurations:

Tool Used: Wireshark

Monitoring Method: Live packet capture and offline PCAP analysis

PCAP File: wire.pcapng

Protocols Monitored:

HTTP

TCP

TLS

QUIC

SSDP



Network traffic was observed for anomalies such as repeated requests, unusual packet behavior, and unexpected discovery traffic.
 


3. Attack Detection Log

Time Range	Source IP	Destination IP	Protocol	Observation

12:30–2:30 PM	146.75.90.172	192.168.0.166	HTTP/TCP	Repeated HTTP requests with large payloads
Various	192.168.0.172	Internal host	TCP	Suspicious traffic patterns
Various	192.168.0.151	Internal host	TCP	Network anomalies
Various	192.168.0.134	Internal host	TCP	TCP retransmissions
Various	192.168.0.197	Internal host	TCP	Duplicate ACKs
Various	192.168.0.185	Internal host	SSDP	M-SEARCH discovery requests




4. Traffic Analysis (Wireshark)

Analysis of the PCAP and screenshots revealed the following:

Repeated HTTP traffic from an external IP to the internal web server.

Large HTTP packets requiring TCP PDU reassembly, suggesting automated or scripted interaction.

TCP anomalies, including:

Duplicate ACKs

Retransmissions

Reset (RST) packets


SSDP M-SEARCH traffic, indicating possible service discovery or noisy background scanning.


These indicators are commonly associated with reconnaissance or enumeration activity, rather than direct exploitation.



5. Incident Response Actions

The following actions were taken by the Blue Team:

Incident was formally documented and logged.

Suspicious IP addresses were identified and recorded.

Simulated blocking of identified IPs was recommended to demonstrate defensive response.

Enhanced traffic monitoring was applied to observe post-incident behavior.

No system shutdown or isolation was required due to lack of confirmed compromise.




6. System Weaknesses Identified

Open HTTP service exposed to external traffic.

Lack of visible rate-limiting controls.

Absence of automated alerts for abnormal request frequency.

SSDP traffic visible within the network, indicating potential unnecessary service exposure.



7. Mitigation Recommendations

The following security improvements are recommended:

Implement rate limiting on web endpoints.

Restrict access to sensitive directories and administrative paths.

Disable or restrict unnecessary discovery services such as SSDP.

Enable automated alerts for abnormal HTTP request behavior.

Apply firewall rules to block suspicious IP addresses proactively.


8. Final Assessment

The incident was successfully detected, analyzed, and contained by the Blue Team. No evidence of data loss, system compromise, or service disruption was found. The activity is classified as low-to-moderate risk reconnaissance, and the defensive response demonstrated effective monitoring and incident handling capabilities.

Overall, the Blue Team’s performance met the objectives of the simulated defense exercise.
