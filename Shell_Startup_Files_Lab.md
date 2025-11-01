# Lab: Understanding Shell Startup Files (.profile, .bashrc, .shrc)

## Objective
By the end of this lab, you will:
1. Understand what `.profile`, `.bashrc`, and `.shrc` do.  
2. See when each file executes.  
3. Learn how login and non-login shells differ.  
4. Make persistent environment changes visible across shell sessions.

---

## Environment
- Works on both **Ubuntu** and **macOS**
- Shells used:
  - `/bin/bash` (default for Ubuntu)
  - `/bin/zsh` or `/bin/bash` (macOS default is `zsh`, but `bash` is also available)
  - `/bin/sh` (POSIX shell)

---

## Section 1: Preparation

### Step 1. Identify your default shell
```bash
echo $SHELL
```

Expected output examples:
- Ubuntu: `/bin/bash`
- macOS: `/bin/zsh` or `/bin/bash`

### Step 2. List your shell startup files
```bash
ls -a ~ | grep profile
ls -a ~ | grep bash
```

Expected output (may vary):
```
.bash_profile
.bashrc
.profile
```

---

## Section 2: The `.profile` File (for login shells)

`.profile` is executed **once when you log in** — like via SSH or a new terminal login.

### Step 1. Open `.profile`
```bash
nano ~/.profile
```

### Step 2. Add these lines at the end:
```bash
echo " .profile executed for user: $USER"
export PROFILE_VAR="This variable came from .profile"
```

Save and exit (`Ctrl + O`, `Enter`, `Ctrl + X`).

### Step 3. Test `.profile`
```bash
bash --login
```

Expected output:
```
.profile executed for user: yourusername
```

---

## Section 3: The `.bashrc` File (for interactive shells)

`.bashrc` is executed **every time** you open a new interactive Bash shell.

### Step 1. Edit `.bashrc`
```bash
nano ~/.bashrc
```

Add:
```bash
echo "🌀 .bashrc executed for user: $USER"
export BASHRC_VAR="This variable came from .bashrc"
```

Save and exit.

### Step 2. Run new shell
```bash
bash
```

Expected:
```
🌀 .bashrc executed for user: yourusername
```

Check:
```bash
echo $BASHRC_VAR
```

Output:
```
This variable came from .bashrc
```

---

### Step 3. Compare behavior

| Action | Expected File Executed | Command |
|---------|------------------------|----------|
| Login shell | `.profile` | `bash --login` |
| Interactive shell | `.bashrc` | `bash` |
| Non-login script shell | none | `bash script.sh` |

---

##  Section 4: The `.shrc` File (for `sh` / POSIX shell)

By default, `/bin/sh` does **not** have a startup rc file.  
We can create one and source it manually via `.profile`.

### Step 1. Create a `.shrc`
```bash
echo 'echo " .shrc executed"' > ~/.shrc
echo 'export SHRC_VAR="This variable came from .shrc"' >> ~/.shrc
```

### Step 2. Edit `.profile` to source `.shrc`
```bash
echo 'if [ -f ~/.shrc ]; then . ~/.shrc; fi' >> ~/.profile
```

### Step 3. Start a login shell with `sh`
```bash
sh --login
```

Expected output:
```
 .profile executed for user: yourusername
 .shrc executed
```
