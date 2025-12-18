## 1. Detailed Traffic Findings and Indicators of Suspicious Activity

This section highlights specific network behaviors observed during packet analysis that were flagged as suspicious due to their abnormal patterns, repetition, or unexpected session termination.

---

### 2. Large HTTP Continuation Packets

Multiple HTTP continuation packets were observed originating from an external IP address and targeting the internal web server.

**Observed Behavior:**
- Source: `146.75.90.172`
- Destination: `192.168.0.166` (Port 80)
- Repeated HTTP continuation segments
- Large payload sizes with limited visible request context

**Why This Is Suspicious:**
Large, repetitive continuation packets without clear HTTP request headers may indicate automated scanning, bulk data transfer attempts, or scripted enumeration activity rather than normal browser behavior.

---

### 3. Reassembled TCP Payloads

Repeated TCP payload reassembly events were identified on the same network flow.

**Observed Behavior:**
- Source: `146.75.90.172`
- Destination: `192.168.0.166`
- Multiple packets marked as `[TCP PDU reassembled in frame 431]`

**Why This Is Suspicious:**
Frequent TCP reassembly suggests unusually large or fragmented data transfers. This behavior is often associated with automated tools, aggressive crawling, or attempts to transfer large payloads not typical of standard HTTP interactions.

---

### 4. QUIC Activity with Abnormal Resets

QUIC traffic was observed initiating normally but terminating abruptly via TCP reset packets.

**Observed Behavior:**
- QUIC / Protected Payload traffic between:
  - `192.168.0.112` ↔ `34.87.1.8`
  - `192.168.0.112` ↔ `192.168.223.188`
- TCP RST packets terminating QUIC sessions:
  - `34.87.1.8` → `192.168.0.112`

**Why This Is Suspicious:**
Abrupt session resets following QUIC traffic may indicate blocked connections, failed handshakes, misconfigured services, or defensive network controls interrupting potentially unwanted communication.

---

### 5. Spurious TCP Retransmissions

TCP retransmissions were detected without evidence of a stable or completed handshake.

**Observed Behavior:**
- Source: `192.168.0.112`
- Destination: `192.168.223.188`
- Multiple retransmissions observed

**Why This Is Suspicious:**
Retransmissions without successful session establishment can suggest scanning behavior, failed connection attempts, network interference, or probing of closed or filtered ports.

---

## 6. Summary of Suspicious Sources and Flows

| Activity Type                  | Source IP        | Destination IP      | Protocol        |
|--------------------------------|------------------|---------------------|-----------------|
| Large HTTP continuations       | 146.75.90.172    | 192.168.0.166       | HTTP / TCP      |
| Network reconnaissance / scanning     | 146.75.90.172    | 192.168.0.166       | TCP             |
| QUIC traffic with resets       | 34.87.1.8        | 192.168.0.112       | QUIC / TCP RST  |
| Spurious TCP retransmissions   | 192.168.0.112    | 192.168.223.188     | TCP             |

---

### Analyst Assessment
The traffic patterns described above are consistent with reconnaissance activity, abnormal application behavior, or partially blocked communications rather than confirmed exploitation. These indicators support the overall classification of the incident as **low-to-moderate risk**, warranting continued monitoring and preventive hardening rather than immediate containment.
