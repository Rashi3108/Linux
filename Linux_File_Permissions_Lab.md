
#  Linux Lab: Understanding File Permissions

## Objective
By the end of this lab, students should be able to:
- Read and interpret file permissions.
- Modify permissions using `chmod`.
- Change ownership and groups with `chown` and `chgrp`.
- Identify and solve permission-related errors.

---

## Part 1: Explore Current Permissions

### Step 1: Create Sample Files and Directories
```bash
mkdir ~/permissions_lab
cd ~/permissions_lab
touch file1.txt file2.sh
mkdir scripts data
ls -l
```

**Observation:**  
Check the first column of `ls -l` output (e.g. `-rw-r--r--`).  
That shows:
- File type (`-` for file, `d` for directory)
- Owner permissions (rwx)
- Group permissions (rwx)
- Others permissions (rwx)

---

## Part 2: Modify Permissions

### Step 1: Symbolic Method
```bash
chmod u+x file2.sh
chmod g+w file1.txt
chmod o-r file1.txt
ls -l
```

**Question:**  
What permission changes do you observe for `file1.txt` and `file2.sh`?

---

### Step 2: Numeric (Octal) Method
```bash
chmod 644 file1.txt
chmod 755 file2.sh
ls -l
```

**Breakdown Reminder:**

| Octal | Binary | Permission | Meaning |
|--------|---------|------------|----------|
| 7 | 111 | rwx | read, write, execute |
| 6 | 110 | rw- | read, write |
| 5 | 101 | r-x | read, execute |
| 4 | 100 | r-- | read only |

**Task:**  
1. Give everyone full access to `data` folder → ?  
2. Give only owner full access, group read-only, others no access → ?

---

##  Part 3: Ownership & Groups

### Step 1: Change File Ownership
```bash
sudo chown student file1.txt
sudo chgrp developers file1.txt
```

**Questions:**
1. What does `chown student file1.txt` do?  
2. How can you change both owner and group at once?  
3. How to recursively change ownership for a directory?

---

## Part 4: Practice Challenges (Quiz-Style)

### Identify the Permissions
You run:
```bash
ls -l file1.txt
```
Output:
```
-rw-r-x---
```

**Question:**  
1. Who can execute this file?  
2. Can “others” read this file?  
3. What is the numeric equivalent?  

---

###  Modify the Permissions

#### Q1:
Make `file2.sh` executable for everyone but writable **only** by the owner.  
Expected final: `-rwxr-xr-x`

#### Q2:
Remove all permissions for “others” from `data/` directory.  
Hint: use `chmod o-rwx data`

#### Q3:
Give read-only permission to everyone for `notes.txt`.  
Expected: `-r--r--r--`

---

##  Part 5: Permission Error Simulation
```bash
cd ~/permissions_lab
chmod 000 file1.txt
cat file1.txt
```
**Question:**  
What happens? Why?  

Then fix it:
```bash
chmod 644 file1.txt
```

---

## Part 6: Special Permissions (Optional Advanced)

| Type | Symbol | Purpose | Example |
|------|---------|----------|----------|
| SUID | `s` on user | Run file as file owner | `/usr/bin/passwd` |
| SGID | `s` on group | Run as group | shared project dirs |
| Sticky bit | `t` | Prevent file deletion by others | `/tmp` |

Try:
```bash
chmod +t data
ls -ld data
```

---

## Part 7: Reflection & Discussion

1. Why is it dangerous to give `777` to files or directories?  
2. How does file ownership affect collaboration in teams?  
3. When would you use `chmod -R`?  
4. What happens if a directory lacks execute (`x`) permission?

---

## Cleanup
```bash
cd ~
rm -r ~/permissions_lab
```

---
