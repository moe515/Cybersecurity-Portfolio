# Python Conditional Statements Lab: Access Control Automation

**Language:** Python 3  
**Context:** Automating OS update checks and device login verification

---

## Project Description

In this lab, I practiced writing conditional statements in Python to automate two security tasks: checking if a user's operating system requires an update, and verifying whether login attempts were made by approved users during organization hours. Conditional statements are essential for automating security decisions without manual intervention.

---

## Task 1-2: OS Update Check (if statement)

```python
system = "OS 2"

if system == "OS 2":
    print("no update needed")
```

**Output:** `no update needed`

**Q1:** When OS 2 is running, "no update needed" is displayed. When OS 1 is running, nothing is displayed — the condition evaluates to `False` so no output is produced.

---

## Task 3: Adding else (if/else)

```python
system = "OS 3"

if system == "OS 2":
    print("no update needed")
else:
    print("update needed")
```

**Output:** `update needed`

**Q2:** When OS 2 is running → "no update needed". When any other OS is running → "update needed". The `else` block handles all cases where the `if` condition is `False`.

---

## Task 4: Adding elif (if/elif/elif)

```python
system = "OS 3"

if system == "OS 2":
    print("no update needed")
elif system == "OS 1":
    print("update needed")
elif system == "OS 3":
    print("update needed")
```

**Q3:**
- OS 2 → "no update needed"
- OS 1 → "update needed"
- OS 3 → "update needed"
- Any other value (e.g. "OS 4") → nothing displayed (no matching condition)

---

## Task 5: Using OR to Combine elif Statements

```python
system = "OS 2"

if system == "OS 2":
    print("no update needed")
elif system == "OS 1" or system == "OS 3":
    print("update needed")
```

**Q4:** The `or` operator combines two conditions into one `elif` — making the code more concise. The result is the same as Task 4 but with fewer lines.

---

## Task 6: User Access Check (Two Users)

```python
approved_user1 = "elarson"
approved_user2 = "bmoreno"
username = "bmoreno"

if username == approved_user1 or username == approved_user2:
    print("This user has access to this device.")
else:
    print("This user does not have access to this device.")
```

**Output:** `This user has access to this device.`

---

## Task 7: Using a List and the `in` Operator

```python
approved_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
username = "bmoreno"

if username in approved_list:
    print("This user has access to this device.")
else:
    print("This user does not have access to this device.")
```

**Q5:** Approved users → "This user has access to this device." Unapproved users → "This user does not have access to this device." Using `in` with a list is more scalable than comparing individual variables.

---

## Task 8: Organization Hours Check

```python
organization_hours = True

if organization_hours == True:
    print("Login attempt made during organization hours.")
else:
    print("Login attempt made outside of organization hours.")
```

**Q6:** `True` → "Login attempt made during organization hours." `False` → "Login attempt made outside of organization hours."

---

## Task 9: Combined Access and Hours Check

```python
approved_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
username = "bmoreno"
organization_hours = True

if username in approved_list:
    print("This user has access to this device.")
else:
    print("This user does not have access to this device.")

if organization_hours == True:
    print("Login attempt made during organization hours.")
else:
    print("Login attempt made outside of organization hours.")
```

**Q7:** Two separate checks run independently — one for the username, one for the time. Both messages display regardless of each other's result.

---

## Task 10: Combined Condition with AND

```python
approved_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
username = "bmoreno"
organization_hours = True

if username in approved_list and organization_hours == True:
    print("Login attempt made by an approved user during organization hours.")
else:
    print("Username not approved or login attempt made outside of organization hours.")
```

**Q8:** Both conditions must be `True` for access to be granted. If either the username is unapproved OR the time is outside organization hours → access denied message. The `and` operator enforces both conditions simultaneously.

---

## Security Logic Summary

| Scenario | Output |
|---|---|
| Approved user + organization hours | ✅ "Login attempt made by an approved user during organization hours." |
| Approved user + outside hours | ❌ "Username not approved or login attempt made outside of organization hours." |
| Unapproved user + organization hours | ❌ "Username not approved or login attempt made outside of organization hours." |
| Unapproved user + outside hours | ❌ "Username not approved or login attempt made outside of organization hours." |

---

## Key Takeaways

- `if/elif/else` statements automate decision-making in security scripts without manual checks
- The `in` operator efficiently checks membership in a list — ideal for allowlists of approved users
- Logical operators (`and`, `or`) combine multiple conditions — `and` requires all conditions to be true, `or` requires at least one
- Boolean variables (`True`/`False`) are perfect for representing binary security states like login status or organization hours
- Conditional statements are foundational for building automated access control systems in Python
