## Observed Internal IP Addresses

During traffic analysis, the following internal hosts were observed generating anomalous network activity. They have been labeled as Suspicious Host 1–5 for tracking and further investigation.

| IP Address       | Role / Observation Summary                         |
|------------------|----------------------------------------------------|
| 192.168.0.172    | Suspicious TCP traffic patterns                    |
| 192.168.0.151    | Network anomalies observed during analysis         |
| 192.168.0.134    | TCP retransmissions detected                       |
| 192.168.0.197    | Duplicate TCP acknowledgements (ACKs) observed     |
| 192.168.0.185    | SSDP M-SEARCH discovery traffic detected           |

### Assessment
The listed IP addresses are internal hosts that exhibited abnormal or notable behavior during packet inspection. While no confirmed compromise was identified, the observed activity may indicate misconfigurations, background service activity, or indirect participation in reconnaissance-related traffic. Continued monitoring and detailed host-level review are recommended
