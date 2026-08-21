# Python Algorithm Lab: Developing a User-Device Authentication System

**Language:** Python 3  
**Context:** Building an automated login verification algorithm for device access control

---

## Project Description

In this lab, I developed a complete Python algorithm that automates the process of verifying whether a user is authorized to access a system and whether they have brought their assigned device. The algorithm uses synchronized lists, list methods (`.append()`, `.remove()`, `.index()`), conditional statements, and a user-defined function to create a fully automated authentication system.

---

## Task 1: Synchronized Lists

```python
approved_users = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
approved_devices = ["8rp2k75", "hl0s5o1", "2ye3lzg", "4n482ts", "a307vir"]

print(approved_users[0])   # elarson
print(approved_devices[0]) # 8rp2k75
```

**Q1:** The lists are synchronized — the user at index 0 (`elarson`) is assigned the device at index 0 (`8rp2k75`). Changing the index retrieves the corresponding user and device pair at that position.

---

## Task 2: Adding a New User with .append()

```python
new_user = "gesparza"
new_device = "3rcv4w6"

approved_users.append(new_user)
approved_devices.append(new_device)

print(approved_users)
print(approved_devices)
```

**Output:**
```
['elarson', 'bmoreno', 'tshah', 'sgilmore', 'eraab', 'gesparza']
['8rp2k75', 'hl0s5o1', '2ye3lzg', '4n482ts', 'a307vir', '3rcv4w6']
```

**Q2:** Both new entries appear at the end of their respective lists, maintaining synchronization. `.append()` adds elements to the end of a list.

---

## Task 3: Removing a Departing Employee with .remove()

```python
removed_user = "tshah"
removed_device = "2ye3lzg"

approved_users.remove(removed_user)
approved_devices.remove(removed_device)

print(approved_users)
print(approved_devices)
```

**Output:**
```
['elarson', 'bmoreno', 'sgilmore', 'eraab', 'gesparza']
['8rp2k75', 'hl0s5o1', '4n482ts', 'a307vir', '3rcv4w6']
```

**Q3:** `tshah` and their device `2ye3lzg` are both removed. Revoking access requires removing from both lists simultaneously to maintain synchronization.

---

## Task 4: Checking User Authorization

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
username = "sgilmore"

if username in approved_users:
    print("The username", username, "is approved to access the system.")
else:
    print("The username", username, "is not approved to access the system.")
```

**Output:** `The username sgilmore is approved to access the system.`

**Q4:** Since `"sgilmore"` is in `approved_users`, the `if` condition is `True` and the approval message displays.

---

## Task 5: Finding the User's Index with .index()

```python
ind = approved_users.index("sgilmore")
print(ind)
```

**Output:** `2`

**Q5:** `"sgilmore"` is at index 2 in `approved_users`. This index is used to find the corresponding device in `approved_devices`.

---

## Task 6: Retrieving the Assigned Device

```python
ind = approved_users.index(username)
print(approved_devices[ind])
```

**Output:** `4n482ts`

**Q6:** Using the same index (`ind = 2`) on `approved_devices` retrieves `"sgilmore"`'s assigned device `"4n482ts"` — the synchronized list relationship in action.

---

## Task 7: Verifying Username AND Device

```python
username = "sgilmore"
device_id = "4n482ts"
ind = approved_users.index(username)

if username in approved_users and device_id == approved_devices[ind]:
    print("The user", username, "is approved to access the system.")
    print(device_id, "is the assigned device for", username)
```

**Output:**
```
The user sgilmore is approved to access the system.
4n482ts is the assigned device for sgilmore
```

**Q7:** Both conditions are `True` — the username is approved AND the device matches — so full access is granted.

---

## Task 8: Handling Wrong Device with elif

```python
if username in approved_users and device_id == approved_devices[ind]:
    print("The user", username, "is approved to access the system.")
    print(device_id, "is the assigned device for", username)
elif username in approved_users:
    print("The user", username, "is approved to access the system, but", device_id, "is not their assigned device.")
```

**Q8:** When the correct device `"4n482ts"` is used, the `if` block runs. If a wrong device is entered, the `elif` block warns the user their device doesn't match.

---

## Task 9: Complete login() Function (Final Algorithm)

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

def login(username, device_id):
    if username in approved_users:
        print("The user", username, "is approved to access the system.")
        ind = approved_users.index(username)
        if device_id == approved_devices[ind]:
            print(device_id, "is the assigned device for", username)
        else:
            print(device_id, "is not their assigned device.")
    else:
        print("The username", username, "is not approved to access the system.")

# Test cases
login("sgilmore", "4n482ts")    # Approved user, correct device
login("sgilmore", "8rp2k75")    # Approved user, wrong device
login("jsmith", "4n482ts")     # Unapproved user
```

**Output:**
```
The user sgilmore is approved to access the system.
4n482ts is the assigned device for sgilmore

The user sgilmore is approved to access the system.
8rp2k75 is not their assigned device.

The username jsmith is not approved to access the system.
```

**Q9:** When the device ID is correct → confirms device assignment. When incorrect → warns about device mismatch. The nested conditional handles all three scenarios automatically.

---

## Algorithm Logic Flow

```
login(username, device_id)
        │
        ▼
Is username in approved_users?
    │               │
   YES              NO
    │               │
    ▼               ▼
"Approved"    "Not approved"
    │
    ▼
Does device_id match approved_devices[ind]?
    │               │
   YES              NO
    │               │
    ▼               ▼
"Correct       "Wrong device"
 device"
```

---

## Key Takeaways

- Synchronized lists allow linking user data (username ↔ device ID) using shared indices
- `.append()` and `.remove()` automate user provisioning and deprovisioning — critical for access management
- `.index()` bridges two synchronized lists — finding a value in one list and retrieving the corresponding value in another
- Nested conditionals handle multiple security scenarios in one function
- Encapsulating the algorithm in a `login()` function makes it reusable across the entire security system
- This algorithm mirrors real-world IAM (Identity and Access Management) systems used in enterprise security
