# File Permissions in Linux

---

## Project Description

This project demonstrates the use of Linux commands to check, interpret, and modify file and directory permissions to ensure proper access control on a research team's file system. I reviewed existing permissions in the `/home/researcher2/projects` directory, identified misconfigurations that violated the organization's policy of disallowing write access for others, and used `chmod` to correct them.

---

## Check File and Directory Details

```
ls -la
```

This command lists all files and directories in long format (`-l`), including hidden files (`-a`) such as `.project_x.txt`. The output displays permissions, owner, group, size, and modification date for each item.

**Example output:**
```
-rw-rw-rw- 1 researcher2 research 0 Jun 1 10:00 project_k.txt
-rw-r----- 1 researcher2 research 0 Jun 1 10:00 project_m.txt
-rw-rw-r-- 1 researcher2 research 0 Jun 1 10:00 project_r.txt
-rw-rw-r-- 1 researcher2 research 0 Jun 1 10:00 project_t.txt
-rw--w---- 1 researcher2 research 0 Jun 1 10:00 .project_x.txt
drwxr-x--- 2 researcher2 research 4096 Jun 1 10:00 drafts
```

---

## Describe the Permissions String

Using `project_k.txt` as the example: `-rw-rw-rw-`

This 10-character string represents the file type and permissions:
- **Character 1 (`-`):** File type — a dash means it's a regular file (a `d` would indicate a directory)
- **Characters 2-4 (`rw-`):** User (owner) permissions — read and write, no execute
- **Characters 5-7 (`rw-`):** Group permissions — read and write, no execute
- **Characters 8-10 (`rw-`):** Other permissions — read and write, no execute

---

## Change File Permissions

`project_k.txt` grants "Other" both read and write access, which violates the organization's policy that others should not have write access to any files.

```
chmod o-w project_k.txt
```

This removes the write permission from the "Other" category while leaving User and Group permissions unchanged.

**Result:**
```
-rw-rw-r-- 1 researcher2 research 0 Jun 1 10:00 project_k.txt
```

---

## Change File Permissions on a Hidden File

`.project_x.txt` is a hidden file (research has been archived) that currently has User=read/write, Group=write only, Other=none. It needs to be updated so no one has write access, while User and Group can read it.

```
chmod 440 .project_x.txt
```

This sets User=read only, Group=read only, and Other=no permissions.

**Result:**
```
-r--r----- 1 researcher2 research 0 Jun 1 10:00 .project_x.txt
```

---

## Change Directory Permissions

The `drafts` directory currently grants Group execute access, but only researcher2 should be able to access the directory and its contents.

```
chmod g-x drafts
```

This removes the execute permission from Group, leaving only the owner (researcher2) with access.

**Result:**
```
drwx------ 2 researcher2 research 4096 Jun 1 10:00 drafts
```

---

## Summary

In this project, I used the `ls -la` command to check existing file and directory permissions, including hidden files, in the `/home/researcher2/projects` directory. I identified that `project_k.txt` and the `drafts` directory had overly permissive access for Group and Other, which violated organizational policy. I used `chmod` to remove unauthorized write access from `project_k.txt`, restrict the hidden file `.project_x.txt` to read-only access for the User and Group, and limit the `drafts` directory to researcher2 only. These changes ensure that only authorized users have appropriate access to sensitive research files.
