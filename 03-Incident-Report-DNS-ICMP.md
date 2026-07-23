# Cybersecurity Incident Report: Network Traffic Analysis
## DNS/ICMP Traffic Analysis

---

## Part 1: Summary of the Problem

The UDP protocol was used to send DNS requests to port 53 of the DNS server, which were unsuccessful. Network analysis using tcpdump showed that the ICMP echo reply returned the error message: "udp port 53 unreachable."

Port 53 is used for DNS service. The most likely issue is that the DNS server is not responding, which is preventing users from accessing www.yummyrecipesforme.com.

---

## Part 2: Analysis and Cause

**Time incident occurred:** 1:24 PM (13:24:32)

**How the IT team became aware:** Several customers reported being unable to access www.yummyrecipesforme.com and receiving a "destination port unreachable" error message.

**Actions taken:** The IT department used tcpdump to analyze network traffic while attempting to load the website.

**Key findings:** UDP packets sent to DNS server (203.0.113.2) on port 53 received ICMP error responses three consecutive times, indicating port 53 is unreachable.

**Likely cause:** The DNS server is down, or its firewall is blocking port 53, possibly due to a Denial of Service (DoS) attack or a misconfiguration, making it impossible to resolve the domain name.

**Next steps:** Investigate whether the DNS server is functioning properly and check firewall settings to determine if port 53 traffic is being blocked.
