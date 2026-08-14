# Python Functions Lab: Defining and Calling Functions for Security Tasks

**Language:** Python 3  
**Context:** Automating security alerts and converting username lists to strings

---

## Project Description

In this lab, I practiced defining and calling user-defined functions in Python. I built a security alert function and a username list converter function — both common tasks for security analysts who need to automate repetitive processes and manipulate data structures efficiently.

---

## Task 1 & 2: Defining and Calling alert()

```python
# Define the function
def alert():
    print("Potential security issue. Investigate further.")

# Call the function
alert()
```

**Output:** `Potential security issue. Investigate further.`

**Q1:** The `alert()` function, when called, prints a security warning message to the screen.

**Q2 — Advantages of using a function:**
- Reusability — call `alert()` anywhere in the code without rewriting the logic
- Maintainability — update the message in one place and it applies everywhere
- Readability — descriptive function names make code easier to understand

---

## Task 3: alert() with a for Loop

```python
def alert():
    for i in range(3):
        print("Potential security issue. Investigate further.")

alert()
```

**Output:**
```
Potential security issue. Investigate further.
Potential security issue. Investigate further.
Potential security issue. Investigate further.
```

**Q3:** This version displays the alert 3 times instead of once. The `for` loop is embedded inside the function — showing that functions can contain any Python structure including loops and conditionals.

---

## Task 4 & 5: list_to_string() — Iterating Through Usernames

```python
def list_to_string():
    username_list = ["elarson", "bmoreno", "tshah", "sgilmore",
                     "eraab", "gesparza", "alevitsk", "wjaffrey"]

    for i in username_list:
        print(i)

list_to_string()
```

**Output:**
```
elarson
bmoreno
tshah
sgilmore
eraab
gesparza
alevitsk
wjaffrey
```

**Q4:** Each username in the list is printed on a separate line. The function encapsulates the list and the loop, making it reusable.

---

## Task 6: String Concatenation

```python
def list_to_string():
    username_list = ["elarson", "bmoreno", "tshah", "sgilmore",
                     "eraab", "gesparza", "alevitsk", "wjaffrey"]

    sum_variable = ""

    for i in username_list:
        sum_variable = sum_variable + i

    print(sum_variable)

list_to_string()
```

**Output:** `elarsonbmorenotshahsgilmoreeraabgesparzaalevitskwjaffrey`

**Q5:** All usernames are joined into one continuous string. The `+` operator concatenates each username to `sum_variable`. The result is hard to read because there are no separators between names.

---

## Task 7: Adding Separators for Readability (Corrected)

```python
def list_to_string():
    username_list = ["elarson", "bmoreno", "tshah", "sgilmore",
                     "eraab", "gesparza", "alevitsk", "wjaffrey"]

    sum_variable = ""

    for i in username_list:
        sum_variable = sum_variable + i + ", "

    print(sum_variable)

list_to_string()
```

**Output:** `elarson, bmoreno, tshah, sgilmore, eraab, gesparza, alevitsk, wjaffrey,`

**Q6:** Adding `", "` after each username makes the output much more readable. Each username is now clearly separated by a comma and space — making this string suitable for writing to a text file or log entry.

---

## Security Application Summary

| Function | Purpose | Security Use |
|---|---|---|
| `alert()` | Display a security warning | Notify analysts of potential threats |
| `alert()` with loop | Repeat alert multiple times | Emphasize critical security issues |
| `list_to_string()` | Convert username list to string | Format allowlists for logging or file export |

---

## Key Takeaways

- Functions allow reusable, maintainable code — critical for security automation at scale
- Functions can contain any Python structure: loops, conditionals, variables
- String concatenation with `+` joins multiple strings into one — useful for formatting security reports
- Adding separators like `", "` improves readability of concatenated output
- Security analysts regularly define custom functions to automate alert systems, data formatting, and log processing
