# Cybersecurity Incident Report: SYN Flood Attack

---

## Section 1: Type of Attack

One potential explanation for the website's connection timeout error is a DoS SYN flood attack.

The logs show that a large number of TCP SYN requests were sent from a single IP address (203.0.113.0) to the web server (192.0.2.1) at an abnormally rapid pace.

This is a direct Denial of Service (DoS) SYN flood attack, since all malicious traffic originated from one source.

---

## Section 2: How the Attack Caused the Malfunction

**Three-way handshake process:**
1. Client sends a SYN packet to the server requesting a connection
2. Server responds with a SYN-ACK packet, reserving system resources for the connection
3. Client sends an ACK packet to confirm the connection is established

**Impact of the attack:**  
When a malicious actor sends a large number of SYN packets without completing the handshake, the server keeps reserving resources for each request while waiting for the final ACK that never arrives. This exhausts the server's resources.

**Log findings:**  
The Wireshark logs show the server becoming overwhelmed — legitimate employees started receiving 504 Gateway Timeout errors and RST-ACK packets, meaning the server could no longer handle real traffic. From log entry 125 onward, the server stopped responding to all legitimate traffic.

**Immediate actions taken:**
- Server taken offline temporarily to recover
- Firewall configured to block the attacking IP address (203.0.113.0)

**Recommended next steps:**
- Implement rate limiting on SYN packets
- Deploy SYN cookies to prevent resource exhaustion
- Consider upgrading to DDoS protection services
