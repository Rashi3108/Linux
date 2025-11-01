
# Linux Text Processing & Search Commands Lab
This lab covers five essential Linux commands used for searching, filtering, and transforming data in files or output streams:
- **grep**
- **sed**
- **awk**
- **find**
- **cut**

Each section includes explanations, syntax, and hands-on examples.

---

## 1. grep (Global Regular Expression Print)
Used to search text patterns in files or output.

### Syntax
```bash
grep [options] PATTERN [FILE...]
```

### Common Options
| Option | Description |
|--------|--------------|
| `-i` | Ignore case |
| `-v` | Invert match (show non-matching lines) |
| `-n` | Show line numbers |
| `-r` | Recursive search in directories |
| `-E` | Use extended regex (like `egrep`) |

### Examples
```bash
# Find lines containing 'error' in a log file
grep "error" /var/log/syslog

# Case-insensitive search for 'failed'
grep -i "failed" auth.log

# Show line numbers
grep -n "bash" /etc/passwd

# Show lines that do NOT contain 'root'
grep -v "root" /etc/passwd
```

---

## 2. sed (Stream Editor)
Used to modify or transform text in a stream or file.

### Syntax
```bash
sed [options] 'command' [file]
```

### Common Uses
| Command | Description |
|----------|--------------|
| `s/pattern/replacement/` | Substitute first match in line |
| `s/pattern/replacement/g` | Substitute all matches |
| `d` | Delete matching lines |
| `p` | Print lines (used with `-n`) |

### Examples
```bash
# Replace the first occurrence of 'foo' with 'bar' in each line
echo "foo test foo" | sed 's/foo/bar/'

# Replace all occurrences
echo "foo test foo" | sed 's/foo/bar/g'

# Delete lines containing 'root' in /etc/passwd
sed '/root/d' /etc/passwd

# Print only lines containing 'bash'
sed -n '/bash/p' /etc/passwd
```

---

## 3. awk (Pattern Scanning & Processing)
`awk` is a powerful tool for processing text files, particularly for structured data like CSV.

### Syntax
```bash
awk 'pattern { action }' [file]
```

### Key Concepts
- `$1`, `$2`, `$3` → represent first, second, third columns
- `NF` → number of fields in the current line
- `NR` → current line number

### Examples
```bash
# Print first column from /etc/passwd
awk -F: '{print $1}' /etc/passwd

# Print username and shell (1st and 7th columns)
awk -F: '{print $1, $7}' /etc/passwd

# Print lines with more than 5 fields
awk 'NF > 5' /etc/passwd

# Calculate sum of numbers in 2nd column
awk '{sum += $2} END {print sum}' data.txt
```

---

## 4. find (Search for Files/Directories)
Used to locate files in a directory hierarchy based on name, size, time, etc.

###  Syntax
```bash
find [path] [options] [expression]
```

###  Common Examples
```bash
# Find all .txt files in current directory
find . -name "*.txt"

# Find files larger than 10MB
find /home -size +10M

# Find files modified in the last 1 day
find /var/log -mtime -1

# Find and delete .tmp files
find . -name "*.tmp" -delete

# Find and execute a command on results
find . -type f -name "*.log" -exec rm {} \;
```

---

##  5. cut (Extract Specific Columns from Text)
Used to extract specific fields or columns from lines.

###  Syntax
```bash
cut OPTION... [FILE]
```

###  Common Options
| Option | Description |
|--------|--------------|
| `-d` | Specify delimiter |
| `-f` | Select fields |
| `-c` | Select character positions |

###  Examples
```bash
# Extract usernames from /etc/passwd
cut -d: -f1 /etc/passwd

# Extract shell field (7th column)
cut -d: -f7 /etc/passwd

# Extract first 5 characters of each line
cut -c1-5 file.txt
```

---

##  Practice Lab Exercises

### 1. grep
- Find all users using `/bin/bash` in `/etc/passwd`.
- Count how many lines contain the word “error” in `/var/log/syslog`.

### 2. sed
- Replace all “dev” with “developer” in `team.txt`.
- Delete lines containing “test” from `data.txt`.

### 3. awk
- Print usernames and shells from `/etc/passwd`.
- Count total number of users in `/etc/passwd`.
- Calculate total and average from a CSV file `marks.csv` (comma-separated).

### 4. find
- Find all `.log` files in `/var/log` modified in last 2 days.
- Find and delete all `.bak` files in your home directory.

### 5. cut
- Extract first and third columns from a CSV file.
- Display only first 10 characters from each line in `notes.txt`.

---

## Combine commands for more power:
```bash
# Extract usernames and filter by pattern
cut -d: -f1 /etc/passwd | grep "adm"
```
