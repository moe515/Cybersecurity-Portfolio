# Update a File Through a Python Algorithm

**Language:** Python 3  
**Type:** Official Portfolio Activity  
**Context:** Automating IP allowlist management by removing unauthorized addresses

---

## Project Description

In this activity, I developed a Python algorithm that automates the process of updating an IP address allowlist. The algorithm reads a text file containing approved IP addresses, removes addresses that should no longer have access, and rewrites the updated list back to the file. This type of automation is critical for maintaining accurate access control in a security environment.

---

## Scenario

As a security analyst, I'm responsible for maintaining an allowlist (`allow_list.txt`) of IP addresses permitted to access restricted content. When users no longer need access, their IP addresses must be removed from this file. Python automates this process, eliminating manual errors and saving time.

---

## Complete Algorithm

```python
# Define a function that updates the allow list by removing specified IP addresses
def update_file(import_file, remove_list):

    # Read the current contents of the file
    with open(import_file, "r") as file:
        ip_addresses = file.read()

    # Convert the string to a list for easier manipulation
    ip_addresses = ip_addresses.split()

    # Loop through each IP address and remove it if it's in the remove list
    for element in ip_addresses:
        if element in remove_list:
            ip_addresses.remove(element)

    # Convert the updated list back to a string with spaces between entries
    ip_addresses = " ".join(ip_addresses)

    # Write the updated list back to the file (overwrites previous content)
    with open(import_file, "w") as file:
        file.write(ip_addresses)


# Call the function with the file name and list of IPs to remove
update_file("allow_list.txt", ["192.168.25.60", "192.168.140.81", "192.168.203.198"])

# Verify the file was updated correctly
with open("allow_list.txt", "r") as file:
    text = file.read()

print(text)
```

---

## Step-by-Step Breakdown

### Step 1: Open and Read the File

```python
with open(import_file, "r") as file:
    ip_addresses = file.read()
```

The `with` statement opens the file in read mode (`"r"`) and automatically closes it afterward. `.read()` imports the entire file as a single string.

### Step 2: Convert String to List

```python
ip_addresses = ip_addresses.split()
```

`.split()` converts the string into a list where each IP address is a separate element — enabling iteration and removal.

**Before:** `"192.168.25.60 192.168.205.12 192.168.97.225..."`  
**After:** `['192.168.25.60', '192.168.205.12', '192.168.97.225', ...]`

### Step 3: Remove Unauthorized IP Addresses

```python
for element in ip_addresses:
    if element in remove_list:
        ip_addresses.remove(element)
```

The loop iterates through each IP address. If it's in `remove_list`, the `.remove()` method deletes it from `ip_addresses`.

### Step 4: Convert List Back to String

```python
ip_addresses = " ".join(ip_addresses)
```

`.join()` converts the updated list back to a string with spaces between entries, making it ready to write back to the file.

### Step 5: Write Updated List to File

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

Opening with `"w"` overwrites the original file content with the updated allowlist.

---

## Sample Input and Output

**Original `allow_list.txt`:**
```
ip_address
192.168.25.60
192.168.205.12
192.168.97.225
192.168.6.9
192.168.52.90
192.168.158.170
192.168.90.124
...
```

**remove_list:**
```python
["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]
```

**Updated `allow_list.txt`:**
```
ip_address 192.168.25.60 192.168.205.12 192.168.6.9 192.168.52.90
192.168.90.124 192.168.186.176 192.168.133.188 192.168.203.198
192.168.218.219 192.168.52.37 192.168.156.224 192.168.60.153 192.168.69.116
```

The 4 unauthorized IP addresses have been successfully removed.

---

## Q3: Benefits of Using a Function

Encapsulating the algorithm in `update_file()` provides several key benefits:

- **Reusability** — the function can be called with any file name and any remove list without rewriting the code
- **Scalability** — easily handles large allowlists and long remove lists
- **Maintainability** — fixing a bug or updating the logic only requires changing the function definition once
- **Readability** — the function call `update_file("allow_list.txt", remove_list)` clearly communicates intent

---

## Key Takeaways

- File handling with `open()`, `.read()`, and `.write()` enables Python to automate log and allowlist management
- `.split()` and `.join()` convert between strings and lists — essential for processing file contents
- Combining loops, conditionals, and file I/O creates a complete automated access control workflow
- Wrapping the algorithm in a function makes it reusable across different files and remove lists
- This type of automation reduces human error in access management — a critical security practice
