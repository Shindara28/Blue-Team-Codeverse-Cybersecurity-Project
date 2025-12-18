# Wireshark Capture Summary

This document presents an expanded summary of three Wireshark screenshots captured during network traffic analysis. The purpose of these captures is to demonstrate how common web protocols operate at the packet level, how Wireshark reconstructs and interprets traffic, and how to distinguish normal network behavior from potentially suspicious activity. Together, the screenshots provide clear examples of unencrypted HTTP communication, modern encrypted web traffic, and secure redirection mechanisms.

## Capture 1: Plain HTTP over TCP

The first capture illustrates a traditional HTTP session running over TCP port 80 between a local client (192.168.0.166) and a public web server (146.75.90.172). Because the traffic is unencrypted, Wireshark is able to display and reassemble the full HTTP payload. Large responses are divided into multiple TCP segments and later reconstructed into a single readable HTTP object.

The TCP three-way handshake occurred before the visible packets, indicating an already established session. Frequent PSH and ACK flags confirm continuous data transfer and reliable delivery. No retransmissions, resets, or errors are visible in the shown frames, which indicates a stable and healthy connection. This capture represents normal web browsing behavior and highlights the main weakness of HTTP: all transmitted data is exposed and readable on the network.

## Capture 2: Mixed Encrypted Web Traffic and Protocol Behavior

The second capture demonstrates a more realistic modern browsing session, combining multiple protocols and encryption methods. Traffic includes HTTPS over TLSv1.3, HTTP/3 over QUIC, plain HTTP, SSDP discovery messages, and standard TCP control packets. Most of the web traffic is encrypted, resulting in “Protected Payload” entries that Wireshark cannot decode without session keys.

This capture also shows TCP reliability mechanisms in action. Retransmissions and duplicate acknowledgments indicate minor packet loss or congestion, while a TCP reset reflects a normal connection closure or protocol transition, such as a browser switching from TCP-based HTTPS to QUIC-based HTTP/3. The presence of QUIC traffic highlights current browser behavior, prioritizing performance and reduced latency. Overall, the observed activity is consistent with normal web usage rather than malicious behavior.

## Capture 3: HTTPS Redirect and HTTP/2 Inspection

The third capture focuses on Wireshark’s ability to reconstruct encrypted traffic when decryption keys are available. It shows an HTTPS request using HTTP/2 to zonetransfer.me, followed by a 301 Moved Permanently response that redirects the client to DigiNinja’s hosted page. Both the request and response headers are visible after TLS decryption, despite the traffic being encrypted on the wire.

This capture demonstrates several important concepts, including HTTP/2 multiplexing, secure redirection, and enforcement of HTTPS through HSTS. It also reinforces the importance of following redirects during testing and analysis, as permanent redirects are cached by browsers and commonly used in security labs and real-world deployments.

## Overall Summary
Across all three captures, the traffic represents normal and expected network behavior. Wireshark effectively reassembles fragmented TCP streams, identifies encrypted and unencrypted traffic, and provides insight into how modern web protocols function. Minor retransmissions, resets, and redirects are part of standard network operations and do not indicate attacks. Together, these captures serve as practical examples of protocol analysis, security awareness, and real-world packet inspection using Wireshark.



## Role and Scope of Traffic Monitoring

This work documents my role as a traffic monitor during the tracking and observation of an attack team using Wireshark. Operating from the host with IP address 192.168.0.122, I captured and analyzed live network traffic in real time to understand how internal systems communicated with external servers throughout the engagement. The focus of this task was on visibility, accuracy, and evidence collection at the network layer.

During the monitoring process, I applied targeted protocol-based display filters such as TCP, HTTP, TLS, and QUIC to isolate relevant packets and reduce background noise. These filters allowed me to closely examine connection behavior, session establishment, data transfer patterns, and reliability mechanisms such as acknowledgments and retransmissions. Stream-following and packet inspection techniques were used to reconstruct conversations and observe end-to-end communication flows.

The captured screenshots provide clear evidence of detailed web traffic analysis. They include plain HTTP sessions where payloads are visible, encrypted HTTPS traffic protected by TLS 1.3, and modern HTTP/3 communication operating over QUIC. The captures also show normal network reliability behavior, including packet retransmissions, duplicate acknowledgments, and server-initiated TCP resets, all of which are common in real-world networks.

In addition, the screenshots demonstrate HTTP redirection behavior through HTTP/2 responses, as well as Wireshark’s ability to reconstruct full requests and responses from multiple packets when session data is available. By combining protocol filtering, packet-level analysis, and stream reconstruction, I was able to trace communication paths, identify protocol usage, and document how both encrypted and unencrypted traffic was handled during the activity. This work provides clear network-level visibility and supporting evidence used in tracking and understanding the actions of the attack team.

---

Bamidele Oloruntobi David

