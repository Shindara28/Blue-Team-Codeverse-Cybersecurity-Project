## Traffic Monitoring Summary and Applied Wireshark Filters

This section documents my work as a traffic monitor while tracking the attack team’s network activity from my host system with IP address 192.168.0.122. Throughout the monitoring process, Wireshark display filters played a critical role in reducing background noise and isolating traffic relevant to the investigation. By selectively applying these filters, I was able to closely observe connection behavior, protocol usage, and data flow patterns reflected across the three captured screenshots.

To identify and analyze basic network and web traffic, the following filters were applied:

- `tcp`
- `http`

These filters made it possible to follow TCP sessions, observe acknowledgments and push flags, and understand how HTTP data was segmented and reassembled across multiple packets. This behavior was clearly demonstrated in the first screenshot, where large HTTP responses were reconstructed from several TCP segments, confirming normal session handling and data transfer.

For analyzing secure and modern web communications, the following filters were used:

- `tls`
- `quic`
- `udp`

These filters highlighted encrypted HTTPS traffic protected by TLS 1.3, as well as HTTP/3 communication over QUIC. In these cases, payloads appeared as protected data, confirming the use of encryption by the attack team. Although the actual content could not be inspected, connection patterns, endpoints, and protocol usage remained visible, as shown in the second screenshot.

To identify reliability and error-related behavior, the following filters were applied:

- `tcp.analysis.retransmission`
- `tcp.analysis.duplicate_ack`
- `tcp.flags.reset == 1`

These filters exposed retransmissions, duplicate acknowledgments, and TCP reset packets. Such events are important indicators of packet loss, temporary network instability, or forced connection termination, and they provided valuable insight into how sessions were maintained or disrupted during the monitored activity.

Finally, for application-layer inspection and session reconstruction, the following filters were used:

- `http2`
- `http.response`
- `http.response.code == 301`

These filters enabled deeper analysis of reconstructed HTTP/2 requests and responses, including server-side redirection behavior. This was clearly visible in the third screenshot, where Wireshark displayed a complete HTTP transaction and confirmed how the server responded to the client’s request.

Overall, the structured and methodical use of these filters allowed me to efficiently narrow down traffic of interest, interpret complex packet flows, and accurately document meaningful network behavior while monitoring and tracking the attack team’s activities.

---


Bamidele Oloruntobi David
