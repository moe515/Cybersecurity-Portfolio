# Python Debugging Lab: Identifying and Fixing Code Errors

**Language:** Python 3  
**Context:** Debugging security automation scripts

---

## Project Description

In this lab, I practiced identifying and resolving three types of Python errors: syntax errors, exceptions, and logic errors. Debugging is a critical skill for security analysts who develop automation scripts — an undetected error can cause security tools to fail silently, creating vulnerabilities in automated processes.

---

## Types of Errors

| Error Type | Description | Example |
|---|---|---|
| **Syntax Error** | Code violates Python grammar rules | Missing `:`, `,`, or `)` |
| **Exception** | Code is syntactically correct but fails at runtime | Index out of range, wrong method call |
| **Logic Error** | Code runs without errors but produces wrong output | Wrong index used for a list |

---

## Task 1: Missing Colon (Syntax Error)

```python
# BEFORE (error)
for i in range(10)
    print("Connection cannot be established")

# AFTER (fixed)
for i in range(10):    # Added : at the end
    print("Connection cannot be established")
```

**Error:** `SyntaxError: invalid syntax`  
**Fix:** Added `:` at the end of the `for` statement.

---

## Task 2: Missing Comma in List (Syntax Error)

```python
# BEFORE (error)
usernames_list = ["djames", "jpark", "tbailey", "zdutchma" "esmith", ...]

# AFTER (fixed)
usernames_list = ["djames", "jpark", "tbailey", "zdutchma", "esmith", ...]
```

**Error:** `SyntaxError: invalid syntax`  
**Fix:** Added `,` between `"zdutchma"` and `"esmith"`.

---

## Task 3: Missing Closing Parenthesis (Syntax Error)

```python
# BEFORE (error)
print("update needed".upper()

# AFTER (fixed)
print("update needed".upper())    # Added closing )
```

**Error:** `SyntaxError: unexpected EOF while parsing`  
**Fix:** Added the missing closing parenthesis `)`.

---

## Task 4: Three Errors — Typo, Wrong Operator, Indentation

```python
# BEFORE (3 errors)
for name in username_list:       # Error 1: missing 's'
    if name = username:          # Error 2: = should be ==
    print("The user is approved") # Error 3: missing indentation

# AFTER (fixed)
for name in usernames_list:      # Fixed: usernames_list
    if name == username:         # Fixed: == for comparison
        print("The user is an approved user")  # Fixed: indented
```

**Errors:**
1. `username_list` → `usernames_list` (NameError — variable didn't exist)
2. `=` → `==` (SyntaxError — assignment inside condition)
3. Missing indentation for `print()` (IndentationError)

---

## Task 5: Index Out of Range (Exception)

```python
usernames_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
#                  index 0      1          2        3            4

# BEFORE (error)
if username == usernames_list[5]:    # Index 5 doesn't exist!

# AFTER (fixed)
if username == usernames_list[4]:    # Last element is at index 4
```

**Error:** `IndexError: list index out of range`  
**Fix:** Changed `[5]` to `[4]`. Python lists start at index 0, so a 5-element list has indices 0-4.

---

## Task 6: Missing Colon + Wrong Method Syntax (Syntax + Exception)

```python
# BEFORE (2 errors)
with open(import_file, "r") as file    # Error 1: missing :
    ip_addresses = file.read()

ip_addresses = split.ip_addresses()   # Error 2: wrong syntax

# AFTER (fixed)
with open(import_file, "r") as file:  # Fixed: added :
    ip_addresses = file.read()

ip_addresses = ip_addresses.split()   # Fixed: method on variable
```

**Errors:**
1. Missing `:` after `with` statement (SyntaxError)
2. `split.ip_addresses()` → `ip_addresses.split()` (AttributeError — methods are called ON the object)

---

## Task 7: Wrong List Indices (Logic Error)

```python
patch_schedule = ["March 1st", "April 1st", "May 1st"]
#                    index 0       index 1     index 2

# BEFORE (logic error — wrong indices)
if system == "OS 1":
    print("Patch date:", patch_schedule[2])   # Wrong! [2] = May 1st

elif system == "OS 2":
    print("Patch date:", patch_schedule[0])   # Wrong! [0] = March 1st

elif system == "OS 3":
    print("Patch date:", patch_schedule[2])   # Correct — May 1st

# AFTER (fixed)
if system == "OS 1":
    print("Patch date:", patch_schedule[0])   # March 1st

elif system == "OS 2":
    print("Patch date:", patch_schedule[1])   # April 1st

elif system == "OS 3":
    print("Patch date:", patch_schedule[2])   # May 1st
```

**Error:** Logic error — no crash, but wrong output. OS 1 and OS 2 were assigned the wrong patch dates.  
**Fix:** Corrected indices to match the order in `patch_schedule`.

---

## Debugging Summary

| Task | Error Type | Root Cause | Fix |
|---|---|---|---|
| 1 | Syntax | Missing `:` in for loop | Added `:` |
| 2 | Syntax | Missing `,` in list | Added `,` |
| 3 | Syntax | Missing `)` | Added `)` |
| 4 | Syntax + Exception + Indentation | Typo, `=` vs `==`, indentation | Fixed all three |
| 5 | Exception | Index out of range | Changed `[5]` to `[4]` |
| 6 | Syntax + Exception | Missing `:`, wrong method call | Fixed both |
| 7 | Logic | Wrong list indices | Corrected index mapping |

---

## Key Takeaways

- **Syntax errors** prevent code from running — Python catches them immediately
- **Exceptions** occur at runtime — the code runs but crashes on a specific line
- **Logic errors** are the hardest to catch — the code runs but produces wrong results
- Always read error messages carefully — they tell you the line number and type of error
- Fix one error at a time and re-run — multiple errors can cascade and hide each other
- Debugging is a critical security skill — a logic error in access control code could grant or deny access incorrectly
