## Traffic Monitoring Summary and Applied Wireshark Filters

This section summarizes my role as a traffic monitor during the tracking of the attack team’s network activity, conducted from my host system with IP address 192.168.0.122. Wireshark was used as the primary analysis tool to capture, filter, and interpret live network traffic, allowing for focused inspection of both unencrypted and encrypted communications observed across the three screenshots.

To analyze basic web communication and session flow, display filters such as `tcp` and `http` were applied. These filters made it possible to observe connection behavior, packet sequencing, acknowledgments, and the reassembly of fragmented data into complete HTTP objects. This provided clear visibility into how standard web traffic was exchanged between internal hosts and external servers.

For encrypted traffic and modern web protocols, filters including `tls`, `quic`, and `udp` were used. These revealed HTTPS sessions protected by TLS, as well as HTTP/3 traffic operating over QUIC, shown as protected payloads within Wireshark. This helped confirm the use of secure, contemporary communication methods and highlighted how encrypted traffic limits payload visibility while still exposing useful metadata.

To assess reliability and error conditions, filters such as `tcp.analysis.retransmission`, `tcp.analysis.duplicate_ack`, and `tcp.flags.reset == 1` were applied. These filters exposed packet loss, retransmission events, and server-initiated connection resets, allowing for differentiation between normal network instability and potentially suspicious behavior.

Finally, for deeper application-layer analysis, filters like `http2`, `http.response`, and `http.response.code == 301` were used to examine reconstructed requests and responses, as well as HTTP redirection behavior. This enabled detailed inspection of application-level interactions and supported accurate documentation of how traffic was handled during the monitoring activity.

---

Bamidele Oloruntobi David
