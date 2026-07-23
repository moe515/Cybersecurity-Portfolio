# Incident Report Analysis: NIST CSF Framework
## DoS Attack - ICMP Flood

---

## Summary

The organization experienced a DoS attack where a malicious actor flooded the internal network with ICMP packets through an unconfigured firewall. This caused all internal network services to stop responding for two hours until the incident was resolved.

---

## Identify

A malicious actor sent a flood of ICMP ping packets through an unconfigured firewall, targeting the company's internal network. This DoS attack affected all internal network services and prevented employees from accessing any network resources for approximately two hours.

**Systems affected:** Entire internal network infrastructure  
**Attack type:** DoS ICMP Flood  
**Vulnerability exploited:** Unconfigured firewall with no ICMP rate limiting

---

## Protect

The team implemented the following protective measures:
- New firewall rule to limit the rate of incoming ICMP packets
- Source IP address verification on the firewall to detect spoofed IP addresses
- Regular firewall configuration reviews should be scheduled
- Employee cybersecurity awareness training should be conducted

---

## Detect

The following detection tools were deployed:
- Network monitoring software to detect abnormal traffic patterns
- IDS/IPS system to filter suspicious ICMP traffic based on known characteristics
- Continuous monitoring of incoming external ICMP packets from non-trusted IP addresses

---

## Respond

During future incidents, the team should:
- Immediately block suspicious IP addresses at the firewall
- Take non-critical services offline to preserve critical operations
- Notify stakeholders about the incident and expected resolution time
- Analyze network logs to determine attack source and scope
- Report findings to direct supervisor and management

---

## Recover

Recovery steps implemented and planned:
- Critical network services were restored first, followed by non-critical services
- Systems restored from clean backups where necessary
- Network integrity verified after restoration
- Lessons learned documented to improve future incident response
- Recovery procedures reviewed and updated based on this incident
