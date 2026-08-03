# Suricata IDS Lab: Alerts, Logs, and Rules

**Tool:** Suricata (Open-source IDS/IPS/Network Analysis)
**Environment:** Linux Bash Shell

---

## Project Description

In this lab, I configured and used Suricata, an open-source intrusion detection system, to monitor network traffic and generate alerts based on custom rules. I analyzed both fast.log and eve.json output files to investigate network activity and understand how IDS alerts are structured and interpreted.

---

## Task 1: Examine a Custom Rule

Displayed the contents of the custom rules file:

```bash
cat custom.rules
```

**Rule examined:**
```
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"GET on wire"; flow:established,to_server; content:"GET"; http_method; sid:12345; rev:3;)
```

**Rule breakdown:**

| Component | Value | Description |
|---|---|---|
| Action | `alert` | Triggers an alert when conditions are met |
| Protocol | `http` | Applies only to HTTP traffic |
| Source | `$HOME_NET any` | Any port from the home network |
| Direction | `->` | Traffic flowing outbound |
| Destination | `$EXTERNAL_NET any` | Any external network/port |
| msg | `"GET on wire"` | Alert message displayed in logs |
| flow | `established,to_server` | Matches packets from client to server |
| content | `"GET"` | Looks for GET in the HTTP method |
| sid | `12345` | Unique signature ID |
| rev | `3` | Revision version of the rule |

---

## Task 2: Trigger the Custom Rule

**Listed log directory before running Suricata (empty):**
```bash
ls -l /var/log/suricata
```

**Ran Suricata against the sample packet capture:**
```bash
sudo suricata -r sample.pcap -S custom.rules -k none
```

| Flag | Purpose |
|---|---|
| `-r sample.pcap` | Input file to simulate network traffic |
| `-S custom.rules` | Custom rules file to apply |
| `-k none` | Disable checksum validation |

**Listed log directory after running Suricata:**
```bash
ls -l /var/log/suricata
# Output: fast.log, eve.json, stats.log, suricata.log
```

**Examined fast.log output:**
```bash
cat /var/log/suricata/fast.log
```

**Output:**
```
11/23/2022-12:38:34.624866 [**] [1:12345:3] GET on wire [**] [Classification: (null)] [Priority: 3] {TCP} 172.21.224.2:49652 -> 142.250.1.139:80
11/23/2022-12:38:58.958203 [**] [1:12345:3] GET on wire [**] [Classification: (null)] [Priority: 3] {TCP} 172.21.224.2:58494 -> 142.250.1.139:80
```

Two alerts were generated, both triggered by outbound HTTP GET requests from the home network.

---

## Task 3: Examine eve.json Output

**Displayed raw eve.json:**
```bash
cat /var/log/suricata/eve.json
```

**Used jq to format the output in a readable way:**
```bash
jq . /var/log/suricata/eve.json | less
```

**Extracted specific fields from the log:**
```bash
jq -c "[.timestamp,.flow_id,.alert.signature,.proto,.dest_ip]" /var/log/suricata/eve.json
```

**Output:**
```
["2022-11-23T12:38:34.624866+0000",14500150016149,"GET on wire","TCP","142.250.1.139"]
["2022-11-23T12:38:58.958203+0000",1647223379236084,"GET on wire","TCP","142.250.1.102"]
```

**Queried logs for a specific flow_id:**
```bash
jq "select(.flow_id==14500150016149)" /var/log/suricata/eve.json
```

---

## Key Findings

| Field | Value |
|---|---|
| Alert signature | GET on wire |
| Severity | 3 |
| Protocol | TCP/HTTP |
| Source IP | 172.21.224.2 |
| Destination IPs | 142.250.1.139, 142.250.1.102 |
| Destination Port | 80 |
| Timestamp | 2022-11-23 12:38 |

---

## Summary

In this lab, I gained hands-on experience with Suricata by examining, triggering, and analyzing IDS rules and alert logs. I learned how to write and interpret Suricata rules, run Suricata against packet capture files, and use the `jq` tool to parse and filter JSON log output from the eve.json file. These skills are essential for network traffic monitoring and threat detection in a SOC environment.
