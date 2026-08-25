# Python File Handling Lab: Importing and Parsing Security Log Files

**Language:** Python 3  
**Context:** Importing security logs, appending missing entries, and creating IP allowlist files

---

## Project Description

In this lab, I practiced reading, writing, and appending text files in Python — essential skills for security analysts who work with log files daily. I imported a security log file, parsed its contents, appended a missing log entry, and created a new text file containing an IP allowlist for restricted access control.

---

## Task 1 & 2: Opening and Reading a Log File

```python
import_file = "login.txt"

with open(import_file, "r") as file:
    text = file.read()

print(text)
```

**Output (excerpt):**
```
username,ip_address,time,date
tshah,192.168.92.147,15:26:08,2022-05-10
dtanaka,192.168.98.221,9:45:18,2022-05-09
tmitchel,192.168.110.131,14:13:41,2022-05-11
...
jsoto,192.168.25.60,5:09:21,2022-05-09
```

The `with` statement automatically closes the file after reading — preventing resource leaks. The `"r"` parameter opens the file in read mode. `.read()` imports the entire file as one string.

---

## Task 3: Splitting the Log into Lines

```python
with open(import_file, "r") as file:
    text = file.read()

print(text.split())
```

**Output:** A Python list where each element is one log entry (e.g., `'tshah,192.168.92.147,15:26:08,2022-05-10'`).

**Q1:** Before `.split()`, the output is one long string with newlines. After `.split()`, it becomes a list of strings — one string per log entry. This makes individual entries easier to process and analyze programmatically.

---

## Task 4: Appending a Missing Entry

```python
import_file = "login.txt"
missing_entry = "jrafael,192.168.243.140,4:56:27,2022-05-09"

# Append missing entry
with open(import_file, "a") as file:
    file.write(missing_entry)

# Read and display updated file
with open(import_file, "r") as file:
    text = file.read()

print(text)
```

**Q2:** The missing entry `jrafael,192.168.243.140,4:56:27,2022-05-09` is appended at the end of the file. The `"a"` parameter opens the file in append mode — adding content without overwriting existing data.

---

## Task 5: Creating an IP Allowlist File

```python
import_file = "allow_list.txt"
ip_addresses = "192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246"

print(import_file)
print(ip_addresses)
```

**Output:**
```
allow_list.txt
192.168.218.160 192.168.97.225 192.168.145.158 ...
```

---

## Task 6: Writing to the Allowlist File

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

The `"w"` parameter opens the file in write mode — creating it if it doesn't exist or overwriting it if it does. This is used when creating a fresh allowlist from scratch.

---

## Task 7: Reading Back the Allowlist

```python
with open(import_file, "r") as file:
    text = file.read()

print(text)
```

**Output:**
```
192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153
192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246
```

---

## File Mode Summary

| Mode | Parameter | Use |
|---|---|---|
| Read | `"r"` | Open existing file to read its contents |
| Write | `"w"` | Create new file or overwrite existing file |
| Append | `"a"` | Add content to the end of an existing file |

---

## Security Application Summary

| Task | Operation | Security Use |
|---|---|---|
| Import log file | `open("r")` + `.read()` | Load security logs for analysis |
| Parse log entries | `.split()` | Separate individual login records |
| Add missing entry | `open("a")` + `.write()` | Maintain complete audit logs |
| Create allowlist | `open("w")` + `.write()` | Document approved IP addresses |
| Read allowlist | `open("r")` + `.read()` | Verify allowlist contents |

---

## Key Takeaways

- The `with` statement automatically closes files after use — preventing data corruption and resource leaks
- `.read()` imports the entire file as a single string; `.split()` converts it into a list for easier processing
- `"r"` for reading, `"w"` for writing (overwrites), `"a"` for appending — choosing the wrong mode can destroy log data
- File handling in Python is fundamental for security analysts who work with log files, allowlists, and audit trails
- Appending (`"a"`) is safer than writing (`"w"`) when updating existing logs — it preserves all previous entries
