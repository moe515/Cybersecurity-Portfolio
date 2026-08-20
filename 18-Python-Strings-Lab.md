# Python Strings Lab: Working with String Data for Security Tasks

**Language:** Python 3  
**Context:** Automating employee ID formatting, device ID extraction, and URL parsing

---

## Project Description

In this lab, I practiced working with string data in Python — a critical skill for security analysts who regularly work with employee IDs, device IDs, and network URLs. I used string conversion, concatenation, indexing, slicing, and the `.index()` method to extract and manipulate security-relevant string data.

---

## Task 1: Converting int to str

```python
employee_id = 4186
print(type(employee_id))   # <class 'int'>

employee_id = str(employee_id)
print(type(employee_id))   # <class 'str'>
```

**Output:**
```
<class 'int'>
<class 'str'>
```

**Q1:** The first time, `employee_id` is an integer (`int`). After reassignment using `str()`, it becomes a string (`str`) — enabling string operations like length checking and concatenation.

---

## Task 2: Checking Length with len()

```python
employee_id = str(4186)

if len(employee_id) < 5:
    print("This employee ID has less than five digits. It does not meet length requirements.")
```

**Output:** `This employee ID has less than five digits. It does not meet length requirements.`

The `len()` function returns the number of characters in a string — useful for validating ID formats.

---

## Task 3: Standardizing IDs with Concatenation

```python
employee_id = str(4186)
print(employee_id)

if len(employee_id) < 5:
    employee_id = "E" + employee_id

print(employee_id)
```

**Output:**
```
4186
E4186
```

Concatenating `"E"` in front creates a standardized 5-character employee ID. The `+` operator merges two strings into one.

---

## Task 4: Extracting a Character by Index

```python
device_id = "r262c36"
print(device_id[3])   # Index 3 = 4th character
```

**Output:** `2`

Python string indexing starts at 0. Index 3 gives the 4th character of `"r262c36"`.

---

## Task 5: Slicing the First Three Characters

```python
device_id = "r262c36"
print(device_id[0:3])   # Characters at index 0, 1, 2
```

**Output:** `r26`

String slicing with `[start:end]` extracts a substring. `device_id[0:3]` returns characters at positions 0, 1, and 2 (the end index is exclusive).

---

## Task 6: Extracting the Protocol from a URL

```python
url = "https://exampleURL1.com"
print(url[0:8])
```

**Output:** `https://`

Slicing `url[0:8]` extracts the first 8 characters — the HTTPS protocol and the `://` characters that follow it.

---

## Task 7: Finding the Index of ".com"

```python
url = "https://exampleURL1.com"
print(url.index(".com"))
```

**Output:** `19`

The `.index()` method returns the starting position of a substring within a string. `.com` starts at index 19 in this URL.

---

## Task 8: Storing the Index in a Variable

```python
url = "https://exampleURL1.com"
ind = url.index(".com")
```

Storing the index in `ind` makes it reusable for multiple slicing operations without calling `.index()` repeatedly.

---

## Task 9: Extracting the Domain Extension

```python
url = "https://exampleURL1.com"
ind = url.index(".com")
print(url[ind:ind+4])
```

**Output:** `.com`

**Q2:** `url[ind:ind+4]` extracts 4 characters starting from position 19 — which is exactly `.com`. Using `ind+4` makes the code flexible: if `ind` changes, the slice always captures the 4-character extension.

---

## Task 10: Extracting the Website Name

```python
url = "https://exampleURL1.com"
ind = url.index(".com")
print(url[8:ind])
```

**Output:** `exampleURL1`

`url[8:ind]` slices from character 8 (after `https://`) to the start of `.com` at index 19 — extracting just the website name.

---

## String Operations Summary

| Operation | Syntax | Security Use |
|---|---|---|
| Convert to string | `str(value)` | Standardize ID formats |
| Check length | `len(string)` | Validate ID length requirements |
| Concatenation | `"E" + employee_id` | Pad IDs to meet format standards |
| Index access | `string[3]` | Extract specific character from device ID |
| Slicing | `string[0:3]` | Extract substrings from IDs or URLs |
| Find index | `string.index(".com")` | Locate substrings in URLs or logs |

---

## Key Takeaways

- String indexing starts at 0 — `string[3]` gives the 4th character
- Slicing with `[start:end]` extracts substrings — the end index is excluded
- The `.index()` method locates a substring's starting position — useful for parsing URLs and log entries
- `len()` validates string length — critical for enforcing ID format standards
- String concatenation with `+` builds or modifies identifiers automatically
- These string operations are fundamental for parsing log files, URLs, and security identifiers in Python
