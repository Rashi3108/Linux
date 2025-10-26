
# Linux Basics Lab Guide

## Objective
To help students understand how to navigate the Linux filesystem and use basic Linux commands effectively — including `/`, `~`, `.`, and `..`.

---

## Part 1: Understanding the Linux Filesystem

### Key Concepts

| Symbol | Meaning | Example |
|---------|----------|----------|
| `/` | Root directory (topmost folder) | `/home/student` |
| `~` | Home directory for the logged-in user | `cd ~` |
| `.` | Current directory | `cd ./folder` |
| `..` | Parent directory (one level up) | `cd ..` |

---

## Part 2: Basic Linux Commands Overview

| Command | Description | Example |
|----------|--------------|----------|
| `pwd` | Print current working directory | `pwd` |
| `ls` | List files and directories | `ls -l` |
| `cd` | Change directory | `cd /home` |
| `mkdir` | Create directory | `mkdir test` |
| `rmdir` | Remove empty directory | `rmdir test` |
| `touch` | Create empty file | `touch file.txt` |
| `cp` | Copy files/directories | `cp file1 file2` |
| `mv` | Move or rename files | `mv file1 newname.txt` |
| `rm` | Remove files | `rm file.txt` |
| `cat` | View file content | `cat file.txt` |
| `more` / `less` | View long files | `less file.txt` |
| `head` / `tail` | View beginning/end of file | `head -5 file.txt` |
| `echo` | Print text to terminal | `echo "Hello Linux"` |
| `find` | Search for files | `find /home -name file.txt` |
| `grep` | Search text in files | `grep "word" file.txt` |
| `man` | Show manual/help for command | `man ls` |
| `history` | Show previously executed commands | `history` |

---

## Part 3: Lab — Navigating the Filesystem

### Step 1: Explore the Root `/` and Home `~`
```bash
cd /
pwd
ls
cd ~
pwd
ls
```

**Question:** What’s the difference between `/` and `~`?

---

### Step 2: Create Practice Folders
```bash
cd ~
mkdir -p nav_lab/{projects/{frontend,backend},notes/{class,personal},tmp}
tree ~/nav_lab
```

**Structure:**
```
~/nav_lab
├── projects
│   ├── frontend
│   └── backend
├── notes
│   ├── class
│   └── personal
└── tmp
```

---

### Step 3: Navigate Using `cd`
```bash
cd ~/nav_lab
cd projects
cd frontend
cd ..
cd ../notes/personal
cd ../../tmp
cd ~
```

**Task:** Write the shortest `cd` command to go from `~/nav_lab/notes/personal` to `~/nav_lab/projects/backend`.

---

### Step 4: Use Shortcuts and Special Paths
```bash
cd /         # go to root
cd ~         # go to home
cd -         # go back to previous directory
cd .         # stay in current directory
cd ..        # go one level up
cd ../..     # go two levels up
```

**Challenge:** From `/home/student/nav_lab/notes/class`, move to `/tmp` in a single command.

---

## Part 4: Exploring with ls, pwd, and tree

```bash
pwd
ls
ls -l
ls -a
ls ~/nav_lab/projects
tree ~/nav_lab
```

**Questions:**
1. What does `ls -a` show that `ls` doesn’t?
2. What is the difference between `ls -l` and `ls`?
3. Which directory are you currently in?

---

## Part 5: Bonus Exercises

1. Create a file called `test.txt` inside `~/nav_lab/tmp`
   ```bash
   cd ~/nav_lab/tmp
   touch test.txt
   ```

2. Copy it to the `notes` folder:
   ```bash
   cp test.txt ~/nav_lab/notes/class/
   ```

3. Rename it:
   ```bash
   mv ~/nav_lab/notes/class/test.txt ~/nav_lab/notes/class/final.txt
   ```

4. Delete it:
   ```bash
   rm ~/nav_lab/notes/class/final.txt
   ```

---

## Cleanup (Optional)
```bash
rm -r ~/nav_lab
```

---
