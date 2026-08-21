# Python Regular Expressions Lab: Extracting Patterns from Security Logs

**Language:** Python 3  
**Module:** `re` (Regular Expressions)  
**Context:** Extracting device IDs and IP addresses from security logs

---

## Project Description

In this lab, I used Python's `re` module to write regular expressions that extract security-relevant patterns from log files. I extracted device IDs requiring OS updates and identified valid IP addresses from a network log — then compared them against a list of flagged addresses for further investigation.

---

## Task 1: Import the re Module

```python
import re
```

The `re` module must be imported before using any regular expression functions.

---

## Task 2 & 3: Extracting Device IDs Starting with "r15"

**Device log:**
```
r262c36 67bv8fy 41j1u2e r151dm4 1270t3o 42dr56i r15xk9h 2j33krk 253be78 ac742a1 r15u9q5 zh86b2l ii286fq 9x482kt 6oa6m6u x3463ac i4l56nq g07h55q 081qc9t r159r1u
```

```python
target_pattern = "r15\w+"
```

**Q1 — Pattern breakdown:**

| Symbol | Meaning | If missing |
|---|---|---|
| `r15` | Literal characters to match at start | Would match ALL device IDs |
| `\w` | Any alphanumeric character or underscore | Would only match "r15" exactly |
| `+` | One or more of the preceding character | Would match only one character after "r15" |

---

## Task 4: Applying re.findall() for Device IDs

```python
devices = "r262c36 67bv8fy 41j1u2e r151dm4 1270t3o 42dr56i r15xk9h 2j33krk 253be78 ac742a1 r15u9q5 zh86b2l ii286fq 9x482kt 6oa6m6u x3463ac i4l56nq g07h55q 081qc9t r159r1u"

target_pattern = "r15\w+"
print(re.findall(target_pattern, devices))
```

**Output:** `['r151dm4', 'r15xk9h', 'r15u9q5', 'r159r1u']`

These 4 devices are running outdated OS and need updates.

---

## Task 6: Building an IP Address Pattern (Exact 3 Digits)

```python
pattern = "\d\d\d\.\d\d\d\.\d\d\d\.\d\d\d"
```

| Symbol | Meaning |
|---|---|
| `\d` | Any digit (0-9) |
| `\d\d\d` | Exactly three digits |
| `\.` | Literal period (escaped) |

---

## Task 7: Extracting IPs with Exact 3 Digits

```python
print(re.findall(pattern, log_file))
```

**Output:** `['192.168.152.148', '192.168.190.178', '192.168.213.128', '192.168.247.153', '192.168.174.117', '192.168.148.115', '192.168.168.144']`

**Q2:** Some valid IPs like `192.168.22.115` (has a 2-digit segment) were NOT extracted. The pattern was too strict — requiring exactly 3 digits per segment.

---

## Task 8: Flexible Pattern with \d+

```python
pattern = "\d+\.\d+\.\d+\.\d+"
print(re.findall(pattern, log_file))
```

**Q3:** Now extracts more IPs including those with 1-2 digit segments, but also pulls invalid IPs like `1923.1689.3.24` with segments over 3 digits.

---

## Task 9: Valid IP Pattern with Curly Brackets {1,3}

```python
pattern = "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

valid_ip_addresses = re.findall(pattern, log_file)
print(valid_ip_addresses)
```

**Output:**
```
['192.168.152.148', '192.168.22.115', '192.168.190.178', '192.168.213.128',
 '192.168.96.200', '192.168.247.153', '192.168.174.117', '192.168.148.115',
 '192.168.103.106', '192.168.168.144']
```

**Q4:** `{1,3}` means 1, 2, or 3 digits per segment — extracting all valid IPs while excluding those with 4+ digit segments like `1923.1689.3.24`.

---

## Task 10 & 11: Comparing Against Flagged IP List

```python
flagged_addresses = ["192.168.190.178", "192.168.96.200", "192.168.174.117", "192.168.168.144"]

for address in valid_ip_addresses:
    if address in flagged_addresses:
        print("The IP address", address, "has been flagged for further analysis.")
    else:
        print("The IP address", address, "does not require further analysis.")
```

**Output (flagged entries):**
```
The IP address 192.168.190.178 has been flagged for further analysis.
The IP address 192.168.96.200 has been flagged for further analysis.
The IP address 192.168.174.117 has been flagged for further analysis.
The IP address 192.168.168.144 has been flagged for further analysis.
```

---

## Regex Pattern Summary

| Pattern | Use | Security Application |
|---|---|---|
| `r15\w+` | Device IDs starting with "r15" | Find devices needing OS update |
| `\d\d\d\.\d\d\d\.\d\d\d\.\d\d\d` | Exact 3-digit IP segments | Strict IP matching |
| `\d+\.\d+\.\d+\.\d+` | Variable-length IP segments | Flexible IP extraction |
| `\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}` | Valid IPs (1-3 digits per segment) | Extract only valid IPs from logs |

---

## Key Takeaways

- `re.findall()` returns all matches of a pattern in a string — perfect for log analysis
- `\w` matches any alphanumeric character; `\d` matches any digit; `\.` matches a literal period
- `+` means one or more; `{1,3}` means between 1 and 3 repetitions — controlling match precision
- Regular expressions are essential for parsing large log files that can't be searched manually
- Combining regex extraction with list-based flagging creates a powerful automated threat detection pipeline
