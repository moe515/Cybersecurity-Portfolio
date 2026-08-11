# Python Loops Lab: Automating Security Tasks with Iteration

**Language:** Python 3  
**Context:** Automating network connection monitoring, IP allowlist checking, and employee ID generation

---

## Project Description

In this lab, I practiced writing `for` and `while` loops in Python to automate repetitive security tasks. These included displaying network connection attempt messages, checking IP addresses against an allowlist, and generating employee IDs for a Sales department.

---

## Task 1: for Loop with range()

```python
for i in range(3):
    print("Connection could not be established.")
```

**Output:**
```
Connection could not be established.
Connection could not be established.
Connection could not be established.
```

---

## Task 2: for Loop with a Variable

```python
connection_attempts = 3

for i in range(connection_attempts):
    print("Connection could not be established.")
```

Using a variable makes the loop flexible — changing `connection_attempts` adjusts how many times the message displays.

---

## Task 3: while Loop

```python
connection_attempts = 0

while connection_attempts < 3:
    print("Connection could not be established.")
    connection_attempts = connection_attempts + 1
```

**Q1 — Difference between for and while:**
- `for` loop: runs a fixed number of times defined by `range()` — best when the number of iterations is known
- `while` loop: runs until a condition becomes `False` — best when the number of iterations is unknown (e.g., keep trying until connected)

---

## Task 4: Iterating Over a List of IP Addresses

```python
ip_addresses = ["192.168.142.245", "192.168.109.50", "192.168.86.232",
                "192.168.131.147", "192.168.205.12", "192.168.200.48"]

for i in ip_addresses:
    print(i)
```

**Output:** Prints each IP address on a separate line.

---

## Task 5: IP Allowlist Check

```python
allow_list = ["192.168.243.140", "192.168.205.12", "192.168.151.162",
              "192.168.178.71", "192.168.86.232", "192.168.3.24",
              "192.168.170.243", "192.168.119.173"]

ip_addresses = ["192.168.142.245", "192.168.109.50", "192.168.86.232",
                "192.168.131.147", "192.168.205.12", "192.168.200.48"]

for i in ip_addresses:
    if i in allow_list:
        print("IP address is allowed", i)
    else:
        print("IP address is not allowed", i)
```

**Output:**
```
IP address is not allowed 192.168.142.245
IP address is not allowed 192.168.109.50
IP address is allowed 192.168.86.232
IP address is not allowed 192.168.131.147
IP address is allowed 192.168.205.12
IP address is not allowed 192.168.200.48
```

---

## Task 6: Using break to Stop on Suspicious IP

```python
for i in ip_addresses:
    if i in allow_list:
        print("IP address is allowed", i)
    else:
        print("IP address is not allowed. Further investigation of login activity required", i)
        break
```

**Output:**
```
IP address is not allowed. Further investigation of login activity required 192.168.142.245
```

The `break` keyword immediately stops the loop when an unauthorized IP is detected — triggering further investigation.

---

## Task 7: Employee ID Generator

```python
i = 5000

while i <= 5150:
    print(i)
    i = i + 5
```

Generates all employee IDs divisible by 5 between 5000 and 5150 (inclusive).

---

## Task 8: Adding an Alert with if Inside while

```python
i = 5000

while i <= 5150:
    print(i)
    if i == 5100:
        print("Only 10 valid employee ids remaining")
    i = i + 5
```

**Q2 — Why is `print(i)` before the conditional?**
Because we want to display every ID including 5100 itself. If `print(i)` were inside the `if`, it would only print when `i == 5100`. Placing it before ensures all IDs are displayed, and the alert message appears only once at the right point.

---

## Security Application Summary

| Loop Type | Task | Security Use |
|---|---|---|
| `for` + `range()` | Display connection messages | Alert on repeated failed connections |
| `for` + list | Iterate IP addresses | Check each login attempt |
| `for` + `if` + `in` | Allowlist check | Approve/deny network access |
| `for` + `break` | Stop on unauthorized IP | Trigger investigation immediately |
| `while` | Generate IDs | Automate employee provisioning |
| `while` + `if` | ID generator with alert | Notify when resources are running low |

---

## Key Takeaways

- `for` loops are ideal when the number of iterations is known (e.g., checking a fixed list of IP addresses)
- `while` loops are ideal when iterations depend on a condition (e.g., keep retrying until connected)
- The `break` keyword stops a loop immediately — critical for halting execution when a security threat is detected
- Combining loops with `if` statements and the `in` operator creates powerful automated security checks
- Python loops eliminate the need to manually check each item in large security datasets
