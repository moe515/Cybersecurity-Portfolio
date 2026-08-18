# Python Advanced Functions Lab: Built-in Functions and Login Analysis

**Language:** Python 3  
**Context:** Analyzing failed login attempts and detecting suspicious activity

---

## Project Description

In this lab, I used built-in Python functions to analyze a list of failed login attempts per month, and defined a custom `analyze_logins()` function that compares a user's current login attempts to their daily average. The final version uses a `return` statement and a conditional to automatically trigger a security alert when login activity is abnormally high.

---

## Task 1: Sorting with sorted()

```python
failed_login_list = [119, 101, 99, 91, 92, 105, 108, 85, 88, 90, 264, 223]

print(sorted(failed_login_list))
```

**Output:** `[85, 88, 90, 91, 92, 99, 101, 105, 108, 119, 223, 264]`

**Q1:** Two values stand out as outliers — **223** and **264** — significantly higher than the rest (85–119). These likely correspond to November and December and warrant further investigation as potential indicators of malicious activity.

---

## Task 2: Finding the Maximum with max()

```python
failed_login_list = [119, 101, 99, 91, 92, 105, 108, 85, 88, 90, 264, 223]

print(max(failed_login_list))
```

**Output:** `264`

**Q2:** The highest number of failed login attempts is 264 — occurring in November. This month should be investigated first as it represents the most significant spike in activity.

---

## Task 3 & 4: Defining and Calling analyze_logins() — 2 Parameters

```python
def analyze_logins(username, current_day_logins):
    print("Current day login total for", username, "is", current_day_logins)

analyze_logins("ejones", 9)
```

**Output:** `Current day login total for ejones is 9`

**Q3:** The function displays a personalized message per user. Yes, the output varies — different usernames and login counts produce different messages.

---

## Task 5: Adding a Third Parameter

```python
def analyze_logins(username, current_day_logins, average_day_logins):
    print("Current day login total for", username, "is", current_day_logins)
    print("Average logins per day for", username, "is", average_day_logins)

analyze_logins("ejones", 9, 3)
```

**Output:**
```
Current day login total for ejones is 9
Average logins per day for ejones is 3
```

---

## Task 6: Calculating Login Ratio

```python
def analyze_logins(username, current_day_logins, average_day_logins):
    print("Current day login total for", username, "is", current_day_logins)
    print("Average logins per day for", username, "is", average_day_logins)

    login_ratio = current_day_logins / average_day_logins

    print(username, "logged in", login_ratio, "times as much as they do on an average day.")

analyze_logins("ejones", 9, 3)
```

**Output:**
```
Current day login total for ejones is 9
Average logins per day for ejones is 3
ejones logged in 3.0 times as much as they do on an average day.
```

**Q4:** This version calculates and displays how many times more than usual the user logged in — a key metric for detecting anomalous behavior.

---

## Task 7: Adding a return Statement

```python
def analyze_logins(username, current_day_logins, average_day_logins):
    print("Current day login total for", username, "is", current_day_logins)
    print("Average logins per day for", username, "is", average_day_logins)

    login_ratio = current_day_logins / average_day_logins

    return login_ratio

login_analysis = analyze_logins("ejones", 9, 3)
print("ejones", "logged in", login_analysis, "times as much as they do on an average day.")
```

**Output:**
```
Current day login total for ejones is 9
Average logins per day for ejones is 3
ejones logged in 3.0 times as much as they do on an average day.
```

**Q5:** The `return` statement sends `login_ratio` back to the caller, storing it in `login_analysis`. This makes the value reusable outside the function — enabling further logic like conditionals and alerts.

---

## Task 8: Triggering a Security Alert with a Conditional

```python
def analyze_logins(username, current_day_logins, average_day_logins):
    print("Current day login total for", username, "is", current_day_logins)
    print("Average logins per day for", username, "is", average_day_logins)
    login_ratio = current_day_logins / average_day_logins
    return login_ratio

login_analysis = analyze_logins("ejones", 9, 3)

if login_analysis >= 3:
    print("Alert! This account has more login activity than normal.")
```

**Output:**
```
Current day login total for ejones is 9
Average logins per day for ejones is 3
Alert! This account has more login activity than normal.
```

The function returns a ratio, which is then used in a conditional to automatically trigger a security alert — fully automated threat detection.

---

## Security Application Summary

| Tool | Purpose | Security Use |
|---|---|---|
| `sorted()` | Sort a list | Order login attempt data for pattern analysis |
| `max()` | Find the largest value | Identify the most suspicious month |
| `analyze_logins()` | Custom function | Detect abnormal login activity per user |
| `return` statement | Send value back | Enable reuse of calculated ratio in alerts |
| `if login_ratio >= 3` | Conditional alert | Auto-trigger investigation on anomalous logins |

---

## Key Takeaways

- Built-in functions like `sorted()` and `max()` simplify data analysis without writing custom code
- User-defined functions with parameters allow flexible, reusable logic across multiple users and datasets
- `return` statements make function output reusable — essential for chaining operations in security scripts
- Combining functions with conditionals creates fully automated alert systems
- A login ratio ≥ 3x average is a strong indicator of suspicious activity worth investigating
