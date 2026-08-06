# Python Variables Lab: Assigning Values and Data Types

**Language:** Python 3  
**Context:** Automating login attempt analysis for a security device

---

## Project Description

In this lab, I practiced creating and working with Python variables to track security-related information for a device access control system. I assigned values to variables, checked their data types, updated variable values, and worked with Boolean comparisons to determine login attempt validity.

---

## Variables and Code

### Task 1 & 2: Device ID (String)

```python
# Assign device ID
device_id = "72e08x0"
print(device_id)

# Check data type
device_id_type = type(device_id)
print(device_id_type)
```

**Output:**
```
72e08x0
<class 'str'>
```

**Q1:** `device_id` is a string (`str`) because it contains alphanumeric characters enclosed in quotes.

---

### Task 3 & 4: Username List (List)

```python
# Assign approved usernames
username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards"]
print(username_list)

# Check data type
username_list_type = type(username_list)
print(username_list_type)
```

**Output:**
```
['madebowa', 'jnguyen', 'tbecker', 'nhersh', 'redwards']
<class 'list'>
```

**Q2:** `username_list` is a `list` data type because it stores multiple string values enclosed in square brackets.

---

### Task 5: Updating a Variable

```python
# Original list
username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards"]
print(username_list)

# Updated list with new employee
username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards", "lpope"]
print(username_list)
```

**Output:**
```
['madebowa', 'jnguyen', 'tbecker', 'nhersh', 'redwards']
['madebowa', 'jnguyen', 'tbecker', 'nhersh', 'redwards', 'lpope']
```

**Q3:** After reassignment, the variable now contains 6 usernames instead of 5. Variables can be updated by reassigning a new value — the old value is replaced.

---

### Task 6 & 7: Integer Variables

```python
# Maximum login attempts allowed
max_logins = 3
max_logins_type = type(max_logins)
print(max_logins_type)

# Current login attempts
login_attempts = 2
login_attempts_type = type(login_attempts)
print(login_attempts_type)
```

**Output:**
```
<class 'int'>
<class 'int'>
```

**Q4 & Q5:** Both `max_logins` and `login_attempts` are integers (`int`) because they store whole numbers without quotes.

---

### Task 8: Boolean Comparison

```python
max_logins = 3
login_attempts = 2

print(login_attempts <= max_logins)
```

**Output:** `True`

**Q6:** The output is `True` because 2 is less than or equal to 3. This means the user has not exceeded the maximum number of login attempts — access can be granted.

---

### Task 9: Changing Values Changes the Boolean Result

```python
max_logins = 3
login_attempts = 5

print(login_attempts <= max_logins)
```

**Output:** `False`

**Q7:** When `login_attempts` is set to 5 (exceeds `max_logins` of 3), the output changes to `False` — meaning the user has exceeded the allowed attempts and access should be denied.

---

### Task 10: Boolean Variable

```python
login_status = False
login_status_type = type(login_status)
print(login_status_type)
```

**Output:** `<class 'bool'>`

**Q8:** `login_status` is a Boolean (`bool`) data type. Booleans can only be `True` or `False` and are commonly used in security logic to represent on/off states like login status.

---

## Security Application Summary

| Variable | Value | Data Type | Security Use |
|---|---|---|---|
| `device_id` | "72e08x0" | str | Identify the target device |
| `username_list` | ["madebowa", ...] | list | Store approved users |
| `max_logins` | 3 | int | Max allowed login attempts |
| `login_attempts` | 2 | int | Current attempt count |
| `login_status` | False | bool | Track if user is logged in |

---

## Key Takeaways

- Python variables store security-relevant data like device IDs, usernames, and login counts
- The `type()` function identifies a variable's data type — critical for validating input in security scripts
- Lists store multiple values (e.g., an allowlist of usernames) and can be updated when access changes
- Boolean comparisons (`<=`, `==`, `>`) automate security decisions like allowing or denying access
- Variables can be reassigned at any time, allowing security scripts to respond dynamically to changing conditions
