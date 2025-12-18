1. 
────────────────────────
WIRESHARK CAPTURE ANALYSIS
────────────────────────
General overview
The capture shows plain HTTP traffic over TCP between:
Client: 192.168.0.166 (private IP, likely your local machine)
Server: 146.75.90.172 (public IP, web server)
Destination port: 80 (HTTP)
This is unencrypted HTTP traffic, meaning payload data is visible and reassembled inside Wireshark.
Protocol behavior observed
TCP 3-way handshake has already occurred before the first visible packet.
Multiple TCP segments are being reassembled into full HTTP responses.
Large HTTP responses are split across several TCP packets.
Frequent [PSH, ACK] flags indicate active data transfer.
[ACK] packets confirm reliable delivery.
“TCP PDU reassembled in frame 431” confirms Wireshark successfully reconstructed full HTTP objects.
Key packet details (from the highlighted frame)
Frame example:
Frame length: 2762 bytes
Ethernet II → IPv4 → TCP → HTTP
Source port: 80
Destination port: 60203
Sequence number: 1
Acknowledgment number: 1
TCP window size: ~88–424 (varies)
HTTP data: continuation of a larger response
This indicates the server is sending a large web object (likely HTML, image, JS, or CSS).
────────────────────────
IMPORTANT WIRESHARK FILTERS
────────────────────────
Basic protocol filters:
http
tcp
ip
Conversation-specific filters:
ip.addr == 146.75.90.172
ip.addr == 192.168.0.166
Port-based filters:
tcp.port == 80
tcp.srcport == 80
tcp.dstport == 60203
Packet flag filters:
tcp.flags.syn == 1
tcp.flags.ack == 1
tcp.flags.push == 1
tcp.flags.reset == 1
HTTP object filters:
http.request
http.response
http.response.code == 200
http.response.code == 404
Reassembly and errors:
tcp.analysis.retransmission
tcp.analysis.lost_segment
tcp.analysis.out_of_order
────────────────────────
TCP FLOW VISUAL (SIMPLIFIED)
────────────────────────
Client (192.168.0.166) Server (146.75.90.172)
────────────────────────────────────────────────────
ACK ───────────────────────▶
◀──────── HTTP Response (Segment 1)
ACK ───────────────────────▶
◀──────── HTTP Response (Segment 2)
ACK ───────────────────────▶
◀──────── HTTP Response (Segment 3)
ACK ───────────────────────▶
Multiple segments are reassembled into one HTTP response.
────────────────────────
PACKET STRUCTURE VISUAL
────────────────────────
Ethernet Header
↓
IP Header
Src: 146.75.90.172
Dst: 192.168.0.166
↓
TCP Header
Src Port: 80
Dst Port: 60203
Flags: PSH, ACK
↓
HTTP Payload
Response body (continued)
Reassembled across multiple frames
────────────────────────
WHAT THIS TRAFFIC INDICATES
────────────────────────
Normal web browsing activity
No encryption (HTTP, not HTTPS)
Large content download
No obvious attack signatures
No retransmissions or resets visible in the shown frames
Healthy TCP session with proper acknowledgments
────────────────────────
USEFUL WIRESHARK FEATURES FOR THIS CAPTURE
────────────────────────
Follow → TCP Stream (to view full HTTP conversation)
Statistics → Conversations (to analyze data volume)
Statistics → Protocol Hierarchy (to confirm protocol usage)
File → Export Objects → HTTP (to extract transferred files)
────────────────────────
SUMMARY
────────────────────────
This capture represents a clean, well-formed HTTP session where a local client downloads a large web resource from a public server over TCP port 80. Wireshark correctly reassembles fragmented TCP segments into readable HTTP data, confirming normal network behavior and proper session handling.
If you want, I can also:
Write this as a lab report
Map it to OSI layers
Turn it into an exam answer
Identify possible security risks of HTTP vs HTTPS

2.
Below is a focused Wireshark analysis of this second screenshot, centered on HTTP, TLS, QUIC, and TCP behavior you captured.
────────────────────────
HIGH-LEVEL OVERVIEW
────────────────────────
This capture shows mixed encrypted web traffic involving:
Local host: 192.168.0.112
External servers:
192.178.223.188 (Google infrastructure)
34.8.7.18 (Google / QUIC endpoint)
140.82.121.6 (GitHub)
102.132.101.61 (HTTP server)
Protocols observed:
TCP
TLSv1.3 (HTTPS)
QUIC (HTTP/3)
SSDP
Plain HTTP (port 80)
The display filter applied is:
http
────────────────────────
KEY EVENTS IN THE PACKET LIST
────────────────────────
TLSv1.3 encrypted traffic (HTTPS)
Frames 449–451:
Protocol: TLSv1.3
Info: Application Data
Meaning:
Payload is encrypted
Wireshark cannot decode HTTP headers or content
Indicates HTTPS over TCP (HTTP/1.1 or HTTP/2)
Source:
192.178.223.188 → 192.168.0.112
Port:
443 → ephemeral port (58253)
TCP retransmission and loss handling
Frame 453 (highlighted in red):
TCP Retransmission
Flags: PSH, ACK
Indicates:
Previous packet was not acknowledged in time
Network congestion or packet loss
TCP reliability mechanism in action
Frame 458:
TCP Dup ACK
Indicates:
Receiver is missing data
Sender should retransmit
These frames show real-world network instability, not an attack.
QUIC traffic (HTTP/3)
Frames 455, 457, 459, 460, 462:
Protocol: QUIC
Info: Protected Payload (KP0)
Ports: UDP-based (no TCP handshake)
Meaning:
HTTP/3 traffic
Fully encrypted
Faster connection setup compared to TCP+TLS
Example:
192.168.0.112 ↔ 34.8.7.18
This is modern browser behavior (Chrome/Edge).
TCP reset (RST)
Frame 461:
TCP RST
Src: 192.178.223.188
Dst: 192.168.0.112
Meaning:
Server forcefully closed the connection
Often happens after timeout, protocol switch (to QUIC), or browser cancel
This is normal and not malicious.
SSDP discovery traffic
Frame 463:
Protocol: SSDP
Destination: 239.255.255.250
Info: M-SEARCH * HTTP/1.1
Meaning:
Local network device discovery
UPnP / smart devices
Multicast traffic
Plain HTTP traffic
Frame 467:
Protocol: HTTP
Port: 80
Payload visible
Meaning:
Unencrypted web traffic
Full HTTP headers and content can be inspected
────────────────────────
IMPORTANT FILTERS FOR THIS CAPTURE
────────────────────────
Protocol filters:
tcp
tls
quic
udp
http
ssdp
Encryption-focused filters:
tls.record.content_type == 23
quic
udp.port == 443
Error and reliability filters:
tcp.analysis.retransmission
tcp.analysis.duplicate_ack
tcp.flags.reset == 1
Host-specific filters:
ip.addr == 192.168.0.112
ip.addr == 192.178.223.188
ip.addr == 34.8.7.18
HTTP-only cleartext:
http && tcp.port == 80
────────────────────────
PACKET FLOW VISUAL (SIMPLIFIED)
────────────────────────
HTTPS over TCP:
Client ──▶ SYN
Server ──▶ SYN, ACK
Client ──▶ ACK
Server ──▶ TLS Application Data (Encrypted)
Client ──▶ ACK
Server ──▶ Retransmission
Server ──▶ RST
HTTP/3 over QUIC:
Client ──▶ QUIC Initial
Server ──▶ QUIC Protected Payload
Client ──▶ QUIC Protected Payload
HTTP (Cleartext):
Server ──▶ HTTP Response
Client ──▶ ACK
────────────────────────
WHY YOU SEE “PROTECTED PAYLOAD”
────────────────────────
TLSv1.3 encrypts all application data
QUIC encrypts everything except minimal headers
Wireshark cannot decode payload without session keys
This is expected behavior on modern browsers
────────────────────────
SECURITY OBSERVATIONS
────────────────────────
Positive:
Most traffic is encrypted (TLS + QUIC)
Modern protocols in use
Proper retransmission handling
Potential risk:
Any HTTP on port 80 exposes data
SSDP can be abused if exposed externally
────────────────────────
SUMMARY
────────────────────────
This capture shows normal modern web activity with HTTPS (TLSv1.3), HTTP/3 over QUIC, occasional TCP retransmissions, and a fallback to plain HTTP for one connection. The “Protected Payload” entries confirm encrypted traffic, while retransmissions and duplicate ACKs indicate minor packet loss rather than malicious activity.
If you want, I can:
Turn this into a lab report or exam answer
Explain QUIC vs TLS visually
Decode HTTP objects
Map packets to OSI layers

3.
Below is a clear, structured analysis of this third screenshot, which shows Wireshark’s HTTP object / stream inspection view for a web request to zonetransfer.me.
────────────────────────
HIGH-LEVEL OVERVIEW
────────────────────────
This view is not the packet list itself, but the decoded HTTP transaction reconstructed from multiple TCP packets.
Host: zonetransfer.me
Protocol: HTTPS (HTTP/2 over TLS)
Method: GET
Status code: 301 (Moved Permanently)
Browser: Chrome on Linux
Purpose: Redirecting the client to a new HTTPS location
────────────────────────
REQUEST ANALYSIS
────────────────────────
Request line:
GET / HTTP/2
Important request headers visible:
Host: zonetransfer.me
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 Chrome/139
Accept-Language: en-GB,en;q=0.9
Accept: text/html,application/xhtml+xml,application/xml
Upgrade-Insecure-Requests: 1
Sec-Fetch-* headers (modern browser security context)
What this means:
The browser is requesting the site root (/)
HTTP/2 is being used (multiplexed, efficient)
Request originates from a modern Chrome browser
The request prefers HTTPS resources
────────────────────────
RESPONSE ANALYSIS
────────────────────────
Status:
HTTP/2 301 Moved Permanently
Key response headers:
Location: https://digi.ninja/projects/zonetransfer.php
X-Powered-By: Rainbows
Strict-Transport-Security: max-age=63072000
Permissions-Policy: controls browser feature access
Cache-Control: max-age=600
Expires: Thu, 11 Dec 2025
Response body:
Short HTML message
Confirms permanent redirect
What this means:
The server does not host content directly
It redirects users permanently to DigiNinja’s hosted page
HSTS enforces HTTPS for future connections
────────────────────────
PACKET-TO-HTTP RECONSTRUCTION
────────────────────────
Wireshark behavior here:
Multiple encrypted TLS packets
Decrypted via browser session keys
Reassembled into:
Full HTTP/2 request
Full HTTP/2 response
This is why you can see headers even though TLS is used.
────────────────────────
SECURITY AND NETWORK INSIGHTS
────────────────────────
Positive security indicators:
HTTPS enforced
HTTP/2 enabled
HSTS active
Permissions-Policy defined
Important learning point:
A 301 redirect is cached by browsers
Tools and scripts should follow redirects
DNS-based labs like zonetransfer.me intentionally redirect
────────────────────────
USEFUL WIRESHARK FILTERS FOR THIS VIEW
────────────────────────
HTTP/2 filters:
http2
http2.headers
Redirect-specific:
http.response.code == 301
http.location
Host-specific:
http.host == "zonetransfer.me"
TLS-related:
tls
tls.handshake.type == 1
────────────────────────
FLOW VISUAL
────────────────────────
Client
└── GET / (HTTP/2)
└── Server
└── 301 Moved Permanently
└── Location: digi.ninja
────────────────────────
WHY THIS MATTERS (LAB CONTEXT)
────────────────────────
Demonstrates HTTPS inspection in Wireshark
Shows HTTP/2 request/response flow
Shows server-side redirection
Reinforces why following redirects is necessary during testing
────────────────────────
SUMMARY
────────────────────────
This capture shows a clean HTTPS HTTP/2 request to zonetransfer.me that returns a permanent redirect (301) to DigiNinja’s hosted lab page. Wireshark successfully reconstructs and displays the full request and response, confirming correct TLS decryption and HTTP/2 analysis.
If you want, I can:
Write this as a full lab report
Explain how to decrypt TLS in Wireshark
Map this to OSI layers
Show how tools like curl handle this redirect






Bamidele Oloruntobi David
