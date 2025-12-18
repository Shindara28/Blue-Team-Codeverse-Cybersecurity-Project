## Observed Internal IP Addresses

During traffic analysis, the following internal IP addresses were observed generating or participating in anomalous network activity. These hosts were reviewed as part of the investigation to identify unusual TCP behavior and discovery traffic.

| IP Address       | Role / Observation Summary                         |
|------------------|----------------------------------------------------|
| 192.168.0.172    | Suspicious TCP traffic patterns                    |
| 192.168.0.151    | Network anomalies observed during analysis         |
| 192.168.0.134    | TCP retransmissions detected                       |
| 192.168.0.197    | Duplicate TCP acknowledgements (ACKs) observed     |
| 192.168.0.185    | SSDP M-SEARCH discovery traffic detected           |

### Assessment
The listed IP addresses are internal hosts that exhibited abnormal or noteworthy behavior during packet inspection. While no confirmed compromise was identified, the observed activity suggests misconfigurations, background service noise, or indirect involvement in reconnaissance-related traffic. Continued monitoring and host-level review are recommended.
