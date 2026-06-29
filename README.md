# 🚩 OverTheWire Bandit — The Complete Walkthrough (All 34 Levels)

> **Professional, Beginner-Friendly, Fully Commented — Every Command Explained**
>
> 📅 Last Updated: 29 June 2026
>
> 🔗 **Official Site:** [https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)
>
> ⭐ **Found this helpful?** Give it a star on GitHub and share it with fellow learners!

---

<p align="center">
  <img src="https://overthewire.org/img/domokitten.png" alt="OverTheWire Bandit" width="200"/>
</p>

---

## 📖 What Is This?

**OverTheWire: Bandit** is the ultimate wargame for anyone who wants to **actually learn Linux** — not just read about it, but *live it*. Over 34 increasingly challenging levels, you'll SSH into remote servers, hunt for hidden passwords, and pick up real-world skills that every security professional, developer, and sysadmin needs.

This writeup is your companion. Every command is **commented line-by-line**. Every concept is explained as if you're hearing it for the first time. No assumptions. No "obviously." Just clear, patient, professional teaching.

> 🎯 **Who is this for?** Absolute beginners who want to learn Linux the hands-on way, and intermediate users who want a reference they can trust.

---

## 📑 Table of Contents

| # | Level | Difficulty | Core Skill |
|---|-------|------------|------------|
| 0 | [Level 0 → Level 1](#level-0--level-1) | ⭐ | SSH & `cat` basics |
| 1 | [Level 1 → Level 2](#level-1--level-2) | ⭐ | Dashed filenames (`-`) |
| 2 | [Level 2 → Level 3](#level-2--level-3) | ⭐ | Filenames with spaces |
| 3 | [Level 3 → Level 4](#level-3--level-4) | ⭐ | Hidden files (`.`) |
| 4 | [Level 4 → Level 5](#level-4--level-5) | ⭐⭐ | `file` type detection |
| 5 | [Level 5 → Level 6](#level-5--level-6) | ⭐⭐ | `find` with multiple filters |
| 6 | [Level 6 → Level 7](#level-6--level-7) | ⭐⭐ | System-wide search |
| 7 | [Level 7 → Level 8](#level-7--level-8) | ⭐ | `grep` |
| 8 | [Level 8 → Level 9](#level-8--level-9) | ⭐⭐ | `sort` + `uniq` |
| 9 | [Level 9 → Level 10](#level-9--level-10) | ⭐⭐ | `strings` |
| 10 | [Level 10 → Level 11](#level-10--level-11) | ⭐ | `base64` |
| 11 | [Level 11 → Level 12](#level-11--level-12) | ⭐⭐ | ROT13 cipher |
| 12 | [Level 12 → Level 13](#level-12--level-13) | ⭐⭐⭐ | Hexdump + multi-layer decompression |
| 13 | [Level 13 → Level 14](#level-13--level-14) | ⭐⭐ | SSH private key |
| 14 | [Level 14 → Level 15](#level-14--level-15) | ⭐⭐ | `nc` (netcat) |
| 15 | [Level 15 → Level 16](#level-15--level-16) | ⭐⭐ | SSL/TLS with `openssl` |
| 16 | [Level 16 → Level 17](#level-16--level-17) | ⭐⭐⭐ | `nmap` + port scanning |
| 17 | [Level 17 → Level 18](#level-17--level-18) | ⭐ | `diff` |
| 18 | [Level 18 → Level 19](#level-18--level-19) | ⭐⭐ | SSH inline commands |
| 19 | [Level 19 → Level 20](#level-19--level-20) | ⭐⭐ | `setuid` binaries |
| 20 | [Level 20 → Level 21](#level-20--level-21) | ⭐⭐ | `nc` listener + setuid |
| 21 | [Level 21 → Level 22](#level-21--level-22) | ⭐⭐ | `cron` jobs |
| 22 | [Level 22 → Level 23](#level-22--level-23) | ⭐⭐ | `cron` + `md5sum` |
| 23 | [Level 23 → Level 24](#level-23--level-24) | ⭐⭐⭐ | Writing shell scripts |
| 24 | [Level 24 → Level 25](#level-24--level-25) | ⭐⭐⭐ | Brute-force attack |
| 25 | [Level 25 → Level 26](#level-25--level-26) | ⭐⭐⭐ | `more` → `vim` escape |
| 26 | [Level 26 → Level 27](#level-26--level-27) | ⭐⭐ | setuid after escape |
| 27 | [Level 27 → Level 28](#level-27--level-28) | ⭐⭐ | `git clone` |
| 28 | [Level 28 → Level 29](#level-28--level-29) | ⭐⭐ | `git log` / history |
| 29 | [Level 29 → Level 30](#level-29--level-30) | ⭐⭐ | `git branch` |
| 30 | [Level 30 → Level 31](#level-30--level-31) | ⭐⭐ | `git tag` |
| 31 | [Level 31 → Level 32](#level-31--level-32) | ⭐⭐⭐ | `git push` + server hook |
| 32 | [Level 32 → Level 33](#level-32--level-33) | ⭐⭐⭐ | Uppercase shell escape (`$0`) |
| 33 | [Level 33 → Level 34](#level-33--level-34) | 🏁 | The finale |

---

## 🛠️ Prerequisites

| Tool | Why You Need It | How to Get It |
|------|-----------------|---------------|
| **SSH Client** | To connect to the Bandit servers | Built-in on Linux/macOS; on Windows use **Command Prompt**, **WSL**, or **Git Bash** |
| **Internet** | To reach `bandit.labs.overthewire.org` | You already have this 🙂 |
| **Curiosity** | The most important tool | Comes pre-installed in every human |

---

## Level 0 → Level 1

### 📋 Level Goal

> The password for the next level is stored in a file called **readme** located in the **home directory**. Use this password to log into `bandit1` using SSH.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect to the Bandit server as user "bandit0"
#   ssh  : Secure Shell — the tool to connect to remote servers
#   -p   : specifies the port number (Bandit uses port 2220, not the default 22)
ssh bandit0@bandit.labs.overthewire.org -p 2220
#   When prompted, enter the password: bandit0

# Step 2: List the files in the current directory
#   ls   : "list" — shows you what files and folders are here
ls
#   Output: readme    ← there's our target file!

# Step 3: Read the contents of the file "readme"
#   cat  : "concatenate" — prints the contents of a file to the screen
cat readme
#   Output: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If   ← this is the password!
```

### 🔑 Password for Level 1

```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

> ⚠️ **Important:** Passwords change periodically. Copy the one that appears on **your** screen, not the example above.

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `ssh user@host -p port` | Connect to a remote server securely |
| `ls` | List files and folders in the current directory |
| `cat filename` | Print the contents of a file to the terminal |

This is the simplest level — a warm-up to make sure you can connect and read files. The `cat` command will be your best friend throughout this entire wargame.

### 🚀 Onward to Level 1!

```bash
# Exit the current session
exit

# Connect as bandit1 using the password you just found
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

---

## Level 1 → Level 2

### 📋 Level Goal

> The password for the next level is stored in a file called **`-`** located in the home directory.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit1 (use the password from the previous level)
ssh bandit1@bandit.labs.overthewire.org -p 2220

# Step 2: List files to confirm the dash file exists
ls
#   Output: -    ← yep, that's the filename — a single dash!

# Step 3: Try the naive approach (THIS WILL FAIL — but let's understand why)
cat -
#   This FREEZES! You'll need to press Ctrl+C to escape.
#   WHY? In Linux, the dash "-" means "read from standard input (keyboard)".
#   So "cat -" is waiting for you to type something, not reading a file!

# Step 4: The CORRECT way — use "./" to force the shell to treat it as a filename
#   ./   : means "in the current directory"
#   ./-   : means "the file named '-' located in the current directory"
cat ./-
#   Output: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx   ← password for Level 2!
```

### 🔑 Password for Level 2

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `-` as a special character | In Linux, `-` often means **stdin/stdout** (standard input/output), not a filename |
| `./` prefix | Forces the shell to interpret what follows as a **file path**, not a special flag |
| Alternative: `cat /home/bandit1/-` | Using the **absolute path** also works — no ambiguity! |
| Alternative: `cat -- -` | `--` signals "end of options" — everything after is a filename |

> 💡 **Pro Tip:** This is a common gotcha in Linux. If a filename starts with `-`, always prefix it with `./` or use the full path. You'll see this trick again in the real world when dealing with weirdly named files.

### 🚀 Onward to Level 2!

```bash
exit
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

---

## Level 2 → Level 3

### 📋 Level Goal

> The password for the next level is stored in a file called **spaces in this filename** located in the home directory.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit2
ssh bandit2@bandit.labs.overthewire.org -p 2220

# Step 2: List files
ls
#   Output: spaces in this filename    ← a file with spaces in its name!

# Step 3: Try reading it WITHOUT quotes (THIS WILL FAIL)
cat spaces in this filename
#   cat thinks "spaces", "in", "this", "filename" are FOUR separate files!
#   It will complain: "No such file or directory" for each word.

# Step 4: The CORRECT way — wrap the filename in quotes
#   "spaces in this filename"   : the quotes tell the shell: "this is ONE thing"
cat "spaces in this filename"
#   Output: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx   ← password for Level 3!
```

### 🔑 Password for Level 3

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| Spaces in filenames | The shell uses spaces to separate **arguments**. Quotes (`"..."`) group words together. |
| `"file name"` | Double quotes preserve spaces as part of the filename |
| Alternative: `cat spaces\ in\ this\ filename` | Backslash `\` "escapes" the next space — also works but is harder to type |

> 💡 **Pro Tip:** In the real world, avoid creating files with spaces. Use `snake_case` or `kebab-case` instead. But when you encounter them, quotes are your friend!

### 🚀 Onward to Level 3!

```bash
exit
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

---

## Level 3 → Level 4

### 📋 Level Goal

> The password for the next level is stored in a **hidden file** in the **inhere** directory.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit3
ssh bandit3@bandit.labs.overthewire.org -p 2220

# Step 2: List files — notice the "inhere" directory
ls
#   Output: inhere

# Step 3: Move into the "inhere" directory
#   cd   : "change directory" — move into a folder
cd inhere

# Step 4: Try a regular ls... nothing shows up!
ls
#   Output: (empty — no output at all!)

# Step 5: List ALL files, INCLUDING hidden ones
#   -a   : "all" — show hidden files too (files starting with a dot)
#   -l   : "long" — show details like permissions, size, date
ls -la
#   Output: ...Hiding-From-You    ← there it is! The dots mean it's hidden.

# Step 6: Read the hidden file
cat ...Hiding-From-You
#   Output: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ   ← password for Level 4!
```

### 🔑 Password for Level 4

```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

### 🧠 What You Learned

| Command/Flag | What It Does |
|-------------|-------------|
| `cd <dir>` | Change into a directory |
| `ls -a` | Show **all** files, including hidden ones (`.`) |
| `ls -l` | Show **long** format with permissions, size, owner, date |
| `ls -la` | Combine both flags — show all files in long format |
| `.filename` | Files starting with `.` are **hidden** by default in Linux |

> 💡 **Pro Tip:** Configuration files (like `.bashrc`, `.gitconfig`, `.ssh/`) are hidden so they don't clutter your normal view. `ls -la` is the first command many professionals run when entering a new directory.

### 🚀 Onward to Level 4!

```bash
exit
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

---

## Level 4 → Level 5

### 📋 Level Goal

> The password for the next level is stored in the **only human-readable file** in the **inhere** directory. Tip: if your terminal is messed up, try the "reset" command.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit4
ssh bandit4@bandit.labs.overthewire.org -p 2220

# Step 2: Navigate into "inhere"
cd inhere

# Step 3: List files — there are 10 files, all named "-file0X"
ls
#   Output: -file00  -file01  -file02  ...  -file09

# Step 4: Check the TYPE of each file
#   file    : tells you what kind of data is inside a file
#   ./*     : means "every file in the current directory"
file ./*
#   Output: ...most are "data" (binary), but ONE is "ASCII text"!

# Step 5: Read the ASCII text file (let's say it's -file07)
#   Remember: use "./" because the filename starts with "-"!
cat ./-file07
#   Output: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw   ← password for Level 5!
```

### 🔑 Password for Level 5

```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `file <filename>` | Identifies the type of a file (text, binary, image, archive, etc.) |
| `./*` | A wildcard meaning "all files in the current directory" |
| Binary vs ASCII | Binary files contain non-human-readable data; ASCII files are plain text |

> 💡 **Pro Tip:** `file` is one of the most underrated commands. It looks at the **magic bytes** (first few bytes) of a file to determine its type, regardless of the file extension. Always use it before `cat` on unknown files!

### 🚀 Onward to Level 5!

```bash
exit
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

---

## Level 5 → Level 6

### 📋 Level Goal

> The password is stored in a file somewhere under the **inhere** directory with these properties:
> - **human-readable**
> - **1033 bytes** in size
> - **not executable**

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit5
ssh bandit5@bandit.labs.overthewire.org -p 2220

# Step 2: Use find to hunt for the file matching ALL three criteria
#   find inhere          : start searching from the "inhere" directory
#   -type f              : only look for regular FILES (not directories)
#   -size 1033c          : exactly 1033 bytes (c = bytes)
#   ! -executable        : NOT executable (the "!" means "not")
#   -exec file {} \;     : run the "file" command on each result
#   | grep ASCII         : filter the output to show only human-readable (ASCII) files
find inhere -type f -size 1033c ! -executable -exec file {} \; | grep ASCII
#   Output: inhere/maybehere07/.file2: ASCII text

# Step 3: Read the file that matched
cat inhere/maybehere07/.file2
#   Output: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG   ← password for Level 6!
```

### 🔑 Password for Level 6

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

### 🧠 What You Learned

| `find` Flag | What It Does |
|------------|-------------|
| `-type f` | Match only regular files (not directories, symlinks, etc.) |
| `-size 1033c` | Match files exactly 1033 bytes (`c` = bytes, `k` = kilobytes, `M` = megabytes) |
| `! -executable` | The `!` means **NOT** — exclude files that have execute permission |
| `-exec file {} \;` | Run `file` on each matched file; `{}` is a placeholder for the filename |
| `| grep ASCII` | Pipe the output into `grep` to show only lines containing "ASCII" |

> 💡 **Pro Tip:** `find` is one of the most powerful commands in Linux. You can filter by name, size, owner, permissions, modification time, and even run commands on results. Master it — it'll save you hours.

### 🚀 Onward to Level 6!

```bash
exit
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

---

## Level 6 → Level 7

### 📋 Level Goal

> The password is stored **somewhere on the server** with these properties:
> - owned by user **bandit7**
> - owned by group **bandit6**
> - **33 bytes** in size

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit6
ssh bandit6@bandit.labs.overthewire.org -p 2220

# Step 2: Search the ENTIRE filesystem from root "/"
#   find /                : start from the ROOT of the filesystem (EVERYTHING!)
#   -type f               : only regular files
#   -user bandit7         : owned by user "bandit7"
#   -group bandit6        : owned by group "bandit6"
#   -size 33c             : exactly 33 bytes
#   2>/dev/null           : redirect error messages (like "Permission denied") to /dev/null
#                           (2 = stderr, > /dev/null = throw them away)
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
#   Output: /var/lib/dpkg/info/bandit7.password    ← found it!

# Step 3: Read the file
cat /var/lib/dpkg/info/bandit7.password
#   Output: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj   ← password for Level 7!
```

### 🔑 Password for Level 7

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `find /` | Search starting from the root — the **entire filesystem** |
| `-user` / `-group` | Filter by file ownership |
| `2>/dev/null` | `2` = stderr (error output), `> /dev/null` = discard it. This silences "Permission denied" errors. |
| `/dev/null` | A special "black hole" file — anything written to it disappears forever |

> 💡 **Pro Tip:** `2>/dev/null` is essential when doing system-wide searches as a non-root user. Without it, your screen would be flooded with thousands of "Permission denied" messages.

### 🚀 Onward to Level 7!

```bash
exit
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

---

## Level 7 → Level 8

### 📋 Level Goal

> The password for the next level is stored in the file **data.txt** next to the word **millionth**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit7
ssh bandit7@bandit.labs.overthewire.org -p 2220

# Step 2: Use grep to find the line containing "millionth"
#   grep   : "global regular expression print" — searches for patterns in text
#   "millionth"          : the pattern we're looking for
#   data.txt             : the file to search in
grep "millionth" data.txt
#   Output: millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
#           ^^^^^^^^    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#           the word    the password is right next to it!
```

### 🔑 Password for Level 8

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `grep "pattern" file` | Search for lines containing a pattern in a file |
| `grep` | One of the most-used commands in Linux — it's a search engine for text |

> 💡 **Pro Tip:** `grep` is pronounced "g-rep" (not "grep" like "grape"). It stands for **G**lobal **R**egular **E**xpression **P**rint. It's older than most of us and still essential.

### 🚀 Onward to Level 8!

```bash
exit
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

---

## Level 8 → Level 9

### 📋 Level Goal

> The password for the next level is stored in the file **data.txt** and is the **only line of text that occurs only once**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit8
ssh bandit8@bandit.labs.overthewire.org -p 2220

# Step 2: Sort the file, then find the unique line
#   sort data.txt        : sort all lines alphabetically (groups duplicates together)
#   |                    : pipe — send the output of "sort" into "uniq"
#   uniq -u              : print only lines that appear EXACTLY ONCE (-u = unique)
sort data.txt | uniq -u
#   Output: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM   ← the only unique line = password!
```

### 🔑 Password for Level 9

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `sort` | Sorts lines alphabetically/numerically |
| `uniq -u` | Prints only the lines that appear **exactly once** |
| `\|` (pipe) | Takes the output of one command and feeds it as input to the next |

> 💡 **Pro Tip:** `sort | uniq -u` is a classic combo. `uniq` only detects adjacent duplicates, so you MUST sort first. Without `sort`, `uniq` would miss duplicates that aren't next to each other.

### 🚀 Onward to Level 9!

```bash
exit
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

---

## Level 9 → Level 10

### 📋 Level Goal

> The password is stored in the file **data.txt** in one of the few human-readable strings, preceded by several `=` characters.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit9
ssh bandit9@bandit.labs.overthewire.org -p 2220

# Step 2: Extract readable strings, then filter for "="
#   strings data.txt     : extract printable character sequences from a binary file
#   |                    : pipe the readable strings into grep
#   grep "="             : show only lines that contain "=" (the password marker)
strings data.txt | grep "="
#   Output: ========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
#           ^^^^^^^^^^ the "=" signs    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ ← password!
```

### 🔑 Password for Level 10

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `strings` | Extracts human-readable text from binary files (minimum 4 printable characters by default) |
| `grep "="` | Filters lines containing the `=` character |

> 💡 **Pro Tip:** `strings` is a reverse-engineering staple. When you have a compiled binary or unknown file, `strings` is often the first tool to reveal embedded text, URLs, or even passwords.

### 🚀 Onward to Level 10!

```bash
exit
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

---

## Level 10 → Level 11

### 📋 Level Goal

> The password is stored in the file **data.txt**, which contains **base64 encoded** data.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit10
ssh bandit10@bandit.labs.overthewire.org -p 2220

# Step 2: Decode the base64 data
#   base64         : the base64 encoding/decoding tool
#   -d             : "decode" — convert from base64 back to the original text
#   data.txt       : the file to decode
base64 -d data.txt
#   Output: The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
#                                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ← password!
```

### 🔑 Password for Level 11

```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `base64` | Encode or decode data in Base64 format |
| `base64 -d` | `-d` = **decode**: convert Base64 back to the original text |
| `base64` (no flag) | **Encode**: convert text to Base64 |

> 💡 **Pro Tip:** Base64 is an **encoding**, not encryption. It's designed to safely transport binary data in text-only mediums (email, JSON, URLs). Anyone can decode it — never use it to hide secrets!

### 🚀 Onward to Level 11!

```bash
exit
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

---

## Level 11 → Level 12

### 📋 Level Goal

> The password is stored in **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been **rotated by 13 positions** (ROT13 cipher).

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit11
ssh bandit11@bandit.labs.overthewire.org -p 2220

# Step 2: Decode the ROT13 cipher
#   cat data.txt                            : read the encoded file
#   |                                       : pipe it into tr
#   tr 'A-Za-z' 'N-ZA-Mn-za-m'             : translate (rotate) the letters
#
#   HOW ROT13 WORKS:
#     A → N, B → O, C → P ... M → Z
#     N → A, O → B, P → C ... Z → M
#     (same for lowercase: a → n, b → o ...)
#
#   HOW tr WORKS:
#     SET1 = 'A-Za-z'     (all uppercase + lowercase letters)
#     SET2 = 'N-ZA-Mn-za-m' (letters shifted by 13)
#     tr replaces each character from SET1 with the corresponding character from SET2
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
#   Output: The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
#                                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ← password!
```

### 🔑 Password for Level 12

```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| ROT13 | A Caesar cipher that shifts letters by 13 positions. Since the alphabet has 26 letters, applying ROT13 twice gives you back the original text. |
| `tr SET1 SET2` | "Translate" — replaces characters in SET1 with the corresponding characters in SET2 |
| `'A-Za-z'` | All uppercase letters A-Z, then all lowercase a-z |
| `'N-ZA-Mn-za-m'` | N to Z then A to M (uppercase), then n to z then a to m (lowercase) |

> 💡 **Pro Tip:** ROT13 is the classic "I'm not really hiding this" cipher. It's used in online forums for spoilers, puzzle answers, and jokes. `tr` is a text-processing Swiss Army knife — learn it well.

### 🚀 Onward to Level 12!

```bash
exit
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

---

## Level 12 → Level 13

### 📋 Level Goal

> The password is stored in **data.txt**, which is a **hexdump** of a file that has been **repeatedly compressed**. Create a working directory under `/tmp`, copy the file, reverse the hexdump, and decompress layer by layer.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit12
ssh bandit12@bandit.labs.overthewire.org -p 2220

# Step 2: Create a temporary working directory
#   mktemp -d        : create a temporary directory with a random name (safer!)
#                      Alternatively: mkdir /tmp/mywork
cd /tmp
mktemp -d
#   Output: /tmp/tmp.XXXXXXXXXX
cd /tmp/tmp.XXXXXXXXXX   # use the directory name printed on your screen

# Step 3: Copy the data file to your workspace
#   cp SOURCE DEST   : "copy" — makes a duplicate
cp ~/data.txt .
#   ~/data.txt    : the original file in your home directory ("~" = home)
#   .             : copy it here (the current directory)

# Step 4: Reverse the hexdump → binary file
#   xxd -r          : "reverse" — convert a hexdump back to binary
#   data.txt        : the hexdump input
#   > data          : redirect output to a new file called "data"
xxd -r data.txt > data

# Step 5: Check what kind of file "data" is
file data
#   Output: data: gzip compressed data ...   (example — yours may differ)

# Step 6: Rename based on the compression type and decompress
#   mv data data.gz    : rename the file to have the correct extension
#   gunzip data.gz     : decompress gzip

# OR if it's bzip2:
#   mv data data.bz2
#   bunzip2 data.bz2

# OR if it's tar:
#   tar -xf data       : extract tar archive

# Step 7: REPEAT steps 5-6 until the file is ASCII text
file data          # check the type
# decompress with the appropriate tool
file data          # check again
# keep going...

# Step 8: When file says "ASCII text", read it!
cat data
#   Output: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn   ← password for Level 13!
```

### 🔑 Password for Level 13

```
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `mktemp -d` | Creates a temporary directory with a random, unique name |
| `cp ~/file .` | Copy a file from home (`~`) to the current directory (`.`) |
| `xxd -r` | Reverse a hexdump — convert hex back to raw binary |
| `file` | Identify the type of compression used |
| `gunzip` | Decompress `.gz` files |
| `bunzip2` | Decompress `.bz2` files |
| `tar -xf` | Extract `.tar` archives |

> 💡 **Pro Tip:** This level teaches the **"onion peeling"** approach — keep checking the type with `file` and decompressing until you hit plain text. This is exactly how malware analysts and CTF players handle multi-layered obfuscation.

### 🚀 Onward to Level 13!

```bash
exit
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

---

## Level 13 → Level 14

### 📋 Level Goal

> The password is stored in `/etc/bandit_pass/bandit14` and can only be read by user **bandit14**. You don't get the password — you get a **private SSH key** to log in as bandit14.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit13
ssh bandit13@bandit.labs.overthewire.org -p 2220

# Step 2: See what's in the home directory
ls
#   Output: sshkey.private    ← an SSH private key!

# Step 3: View the key and copy it
cat sshkey.private
#   Output: -----BEGIN RSA PRIVATE KEY-----
#           (long key content)
#           -----END RSA PRIVATE KEY-----

# Step 4: Exit and save the key LOCALLY on your machine
exit
#   On YOUR machine:
nano bandit14.key
#   Paste the key content, save, and exit

# Step 5: Set proper permissions on the key file
#   chmod 600    : read+write for the owner ONLY (required by SSH, or it will refuse!)
#   bandit14.key : the key file
chmod 600 bandit14.key

# Step 6: Log in as bandit14 using the private key
#   -i bandit14.key    : "identity file" — use this private key for authentication
ssh -i bandit14.key bandit14@bandit.labs.overthewire.org -p 2220

# Step 7: Now logged in as bandit14 — read the password!
cat /etc/bandit_pass/bandit14
#   Output: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS   ← password for Level 14!
```

### 🔑 Password for Level 14

```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| SSH Private Key | A cryptographic key used for passwordless authentication — more secure than passwords |
| `ssh -i keyfile` | Use a specific private key for authentication |
| `chmod 600` | Set permissions so ONLY the owner can read/write. SSH requires this for keys. |
| `/etc/bandit_pass/` | The directory where all Bandit passwords are stored (readable only by their respective users) |

> 💡 **Pro Tip:** SSH keys are the standard for server authentication in the real world. `chmod 600` is critical — if your key is readable by others, SSH will refuse to use it with a "permissions are too open" error.

### 🚀 Onward to Level 14!

```bash
exit
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

---

## Level 14 → Level 15

### 📋 Level Goal

> The password can be retrieved by submitting the current level's password to **port 30000 on localhost**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit14
ssh bandit14@bandit.labs.overthewire.org -p 2220

# Step 2: Send the password to port 30000 using netcat
#   echo "PASSWORD"       : print the password
#   |                     : pipe it into netcat
#   nc localhost 30000    : "netcat" — open a TCP connection to localhost on port 30000
#   nc = the "Swiss Army knife" of networking — it can connect, listen, send, receive
echo "MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS" | nc localhost 30000
#   Output: Correct!
#           8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo   ← password for Level 15!
```

### 🔑 Password for Level 15

```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `nc` (netcat) | Creates TCP/UDP connections — reads and writes data over the network |
| `echo "text"` | Prints text to stdout (the terminal) |
| `\|` (pipe) | Sends one command's output as another command's input |
| `localhost` | The current machine (127.0.0.1) — "this computer" |

> 💡 **Pro Tip:** `nc` is one of the most versatile tools in a hacker's toolkit. It can be a client, a server, a port scanner, a file transfer tool, and even a backdoor. Learning `nc` is learning networking from the command line.

### 🚀 Onward to Level 15!

```bash
exit
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

---

## Level 15 → Level 16

### 📋 Level Goal

> The password can be retrieved by submitting the current level's password to **port 30001 on localhost** using **SSL/TLS encryption**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit15
ssh bandit15@bandit.labs.overthewire.org -p 2220

# Step 2: Connect to the SSL/TLS service
#   openssl s_client    : OpenSSL's SSL/TLS client — like nc but with encryption
#   -connect            : specify the host and port to connect to
#   localhost:30001     : the server and port
openssl s_client -connect localhost:30001
#   (TLS handshake happens — you'll see certificate info, then a prompt)

# Step 3: Type the password and press Enter
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
#   Output: Correct!
#           kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx   ← password for Level 16!
```

### 🔑 Password for Level 16

```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `openssl s_client` | A command-line SSL/TLS client — creates encrypted connections |
| `-connect host:port` | Specifies the server and port to connect to |
| SSL/TLS | Protocols that encrypt network traffic (the "S" in HTTPS) |

> 💡 **Pro Tip:** `openssl s_client` is invaluable for debugging TLS issues, checking certificates, and testing encrypted services. If you see "DONE", "RENEGOTIATING", or "KEYUPDATE" — those are normal TLS protocol messages, ignore them.

### 🚀 Onward to Level 16!

```bash
exit
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

---

## Level 16 → Level 17

### 📋 Level Goal

> Submit the current password to a port on localhost in the range **31000-32000**. First find the open ports, then find which ones speak SSL/TLS. Only one server returns the credentials.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit16
ssh bandit16@bandit.labs.overthewire.org -p 2220

# Step 2: Scan ports 31000-32000 on localhost
#   nmap                  : "Network Mapper" — the industry-standard port scanner
#   -p 31000-32000        : scan only ports in this range (the -p flag specifies ports)
#   localhost             : scan the local machine
nmap -p 31000-32000 localhost
#   Output: Several ports are open — 31046, 31518, 31691, 31790, 31960

# Step 3: Test each open port with openssl to find the TLS-enabled one
#   echo "PASSWORD"                           : send the password
#   | openssl s_client -connect localhost:PORT -quiet   : connect with TLS
#   -quiet                                    : suppress verbose TLS handshake output
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31790 -quiet
#   Output: -----BEGIN RSA PRIVATE KEY-----
#           (SSH private key for bandit17!)
#           -----END RSA PRIVATE KEY-----

# Step 4: Save the private key locally
exit
nano bandit17.key
#   Paste the SSH key, save, and exit

# Step 5: Set permissions and connect
chmod 600 bandit17.key
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220

# Step 6: Read the password file
cat /etc/bandit_pass/bandit17
#   Output: EReVavePLFHtFlFsjn3hyzMlvSuSAcRD   ← password for Level 17!
```

### 🔑 Password for Level 17

```
EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `nmap -p` | Scan specific ports to see which are open/listening |
| Port scanning | Systematically checking which network ports are accepting connections |
| TLS discrimination | Testing each open port to find the one that speaks SSL/TLS vs plain TCP |
| Multi-step recon | First scan, then probe each candidate — a real-world pentesting workflow |

> 💡 **Pro Tip:** This level mirrors a real penetration testing scenario: scan → identify services → interact with the right one. `nmap` is the first tool any pentester reaches for. The `-quiet` flag on `openssl s_client` is new and cleaner than the older approach of piping and ignoring errors.

### 🚀 Onward to Level 17!

```bash
exit
ssh bandit17@bandit.labs.overthewire.org -p 2220
```

---

## Level 17 → Level 18

### 📋 Level Goal

> There are two files: **passwords.old** and **passwords.new**. The password is in **passwords.new** and is the only line that changed between the two files.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit17
ssh bandit17@bandit.labs.overthewire.org -p 2220

# Step 2: Compare the two files
#   diff               : "difference" — compares two files line by line
#   passwords.old      : the old version
#   passwords.new      : the new version
diff passwords.old passwords.new
#   Output: 42c42
#           < (old line)
#           ---
#           > x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO   ← the changed line = password!
```

### 🔑 Password for Level 18

```
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `diff file1 file2` | Compares two files and shows what lines differ between them |
| `42c42` | Line 42 in file1 was **c**hanged to line 42 in file2 |
| `<` | Lines from the first file (passwords.old) |
| `>` | Lines from the second file (passwords.new) |

> 💡 **Pro Tip:** `diff` is essential for code reviews, configuration changes, and debugging. The output format (`<`, `>`, `---`) is standardized and used by version control systems like Git.

### 🚀 Onward to Level 18!

```bash
exit
ssh bandit18@bandit.labs.overthewire.org -p 2220
```

---

## Level 18 → Level 19

### 📋 Level Goal

> The password is stored in a file **readme** in the home directory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: The trick — pass a command directly to SSH
#   Normally, ssh gives you an interactive shell.
#   But you can also pass a command that runs IMMEDIATELY, before .bashrc kicks in.
#
#   ssh user@host -p port "command"  : runs "command" and exits, no interactive shell
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
#   Output: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8   ← password for Level 19!
#
#   WHY THIS WORKS:
#   .bashrc only runs when you get an INTERACTIVE shell.
#   When you pass a command directly, SSH runs it non-interactively
#   and exits BEFORE .bashrc can log you out.
```

### 🔑 Password for Level 19

```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `.bashrc` | A script that runs every time you start an interactive Bash shell |
| SSH inline commands | `ssh user@host "command"` runs a single command without a shell |
| Interactive vs non-interactive | `.bashrc` only triggers for interactive shells — inline commands bypass it |

> 💡 **Pro Tip:** This is a common "escape hatch" technique. If a server's shell is broken or hostile, pass your command directly. You can also use `ssh user@host /bin/bash --norc` to skip `.bashrc` entirely.

### 🚀 Onward to Level 19!

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

---

## Level 19 → Level 20

### 📋 Level Goal

> Use the **setuid binary** in the home directory to gain access as bandit20. Execute it without arguments to learn how to use it.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit19
ssh bandit19@bandit.labs.overthewire.org -p 2220

# Step 2: List files — there's a special binary
ls
#   Output: bandit20-do    ← notice the different color? It's an executable!

# Step 3: Run it without arguments to see usage
#   ./bandit20-do    : run the binary ("./" means "in the current directory")
./bandit20-do
#   Output: Run a command as another user.
#           Example: ./bandit20-do id

# Step 4: Verify it runs as bandit20
#   whoami    : "who am I?" — prints the current username
./bandit20-do whoami
#   Output: bandit20    ← confirmed! It runs commands as bandit20!

# Step 5: Use it to read the password file
#   We run "cat" as bandit20, so we can read bandit20's password file!
./bandit20-do cat /etc/bandit_pass/bandit20
#   Output: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO   ← password for Level 20!
```

### 🔑 Password for Level 20

```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `setuid` (SUID) | A special permission bit: when executed, the program runs with the **owner's** privileges, not the runner's |
| `./binary` | Execute a binary in the current directory (Linux doesn't look in `.` by default) |
| `whoami` | Prints the effective username — useful for confirming setuid works |
| `/etc/bandit_pass/` | The password directory — each user's password file is readable only by that user |

> 💡 **Pro Tip:** `setuid` is a powerful (and dangerous) Linux feature. Classic examples: `passwd` (lets you change your password, which requires writing to protected files) and `sudo` (runs commands as root). Misconfigured setuid binaries are a common privilege escalation vector.

### 🚀 Onward to Level 20!

```bash
exit
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

---

## Level 20 → Level 21

### 📋 Level Goal

> There is a setuid binary that connects to localhost on a port you specify. It reads a line from the connection and compares it to the bandit20 password. If correct, it transmits the bandit21 password.

### 💻 Commands — With Line-by-Line Comments

```bash
# ⚠️ You need TWO terminal sessions for this level! (or use tmux/screen)

# ===== TERMINAL 1: Set up a listener =====
ssh bandit20@bandit.labs.overthewire.org -p 2220

# Start a netcat listener on port 1337 (or any port you like)
#   nc -l 1337    : "listen" on port 1337 — waits for an incoming connection
nc -l 1337
#   (Terminal 1 now waits for a connection...)

# ===== TERMINAL 2: Connect with the setuid binary =====
ssh bandit20@bandit.labs.overthewire.org -p 2220

# Run the setuid binary, telling it to connect to port 1337
#   ./suconnect 1337   : run the binary, connecting to port 1337
./suconnect 1337
#   (Terminal 2 now connects to Terminal 1)

# ===== BACK TO TERMINAL 1: Send the password =====
#   Type the bandit20 password and press Enter:
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
#   Output: Correct!
#           EeoULMCra2q0dSkYj561DX7s1CpBuOBt   ← password for Level 21!
```

### 🔑 Password for Level 21

```
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `nc -l PORT` | Netcat in **listen** mode — creates a simple TCP server |
| Two-terminal workflow | Using multiple SSH sessions to simulate a client-server interaction |
| setuid + networking | Combining setuid binaries with network connections for inter-user communication |

> 💡 **Pro Tip:** This level simulates a simple client-server authentication protocol. This is essentially how many network services work — a client sends credentials, the server validates them and returns a token. `nc -l` is your quick-and-dirty server for testing.

### 🚀 Onward to Level 21!

```bash
exit
ssh bandit21@bandit.labs.overthewire.org -p 2220
```

---

## Level 21 → Level 22

### 📋 Level Goal

> A program is running automatically at regular intervals from **cron**. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit21
ssh bandit21@bandit.labs.overthewire.org -p 2220

# Step 2: Navigate to the cron configuration directory
#   /etc/cron.d/    : where system cron job definitions live
cd /etc/cron.d/

# Step 3: List the cron job files
ls
#   Output: cronjob_bandit22  ...    ← there's our target!

# Step 4: Read the cron job definition
cat cronjob_bandit22
#   Output: * * * * * bandit22 /usr/bin/cronjob_bandit22.sh
#           ^^^^^^^^^ the schedule     ^^^^^^^^^^^^^^^^^^^^^^^ the script it runs
#   Translation: Run this script EVERY MINUTE as user bandit22

# Step 5: Read the script to see what it does
cat /usr/bin/cronjob_bandit22.sh
#   Output: #!/bin/bash
#           chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
#           cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
#   Translation: Copy the password to a file in /tmp and make it readable!

# Step 6: Read the password file in /tmp
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
#   Output: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q   ← password for Level 22!
```

### 🔑 Password for Level 22

```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `cron` | The Linux time-based job scheduler — runs commands on a schedule |
| `/etc/cron.d/` | Directory for system cron job definitions |
| `* * * * *` | Cron schedule: every minute (minute, hour, day, month, weekday) |
| Cron job anatomy | `schedule user command` — when to run, as whom, what to run |
| `chmod 644` | Set file permissions: owner read+write, group read, others read |

> 💡 **Pro Tip:** Cron jobs are a goldmine in CTFs and pentesting. They often run as privileged users and write to world-readable locations. Always check `/etc/cron.d/`, `crontab -l`, and `/var/spool/cron/` when looking for privilege escalation paths.

### 🚀 Onward to Level 22!

```bash
exit
ssh bandit22@bandit.labs.overthewire.org -p 2220
```

---

## Level 22 → Level 23

### 📋 Level Goal

> Another cron job. This time the script uses `md5sum` to generate the filename in `/tmp`. You need to reproduce the hash to find the file.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit22
ssh bandit22@bandit.labs.overthewire.org -p 2220

# Step 2: Read the cron job definition
cd /etc/cron.d/
cat cronjob_bandit23
#   Output: * * * * * bandit23 /usr/bin/cronjob_bandit23.sh

# Step 3: Read the script
cat /usr/bin/cronjob_bandit23.sh
#   Output: #!/bin/bash
#           myname=$(whoami)                          # gets "bandit23"
#           mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
#                                                      # generates an MD5 hash
#           cat /etc/bandit_pass/$myname > /tmp/$mytarget
#                                                      # copies password to /tmp/<hash>

# Step 4: Reproduce the hash locally
#   echo "I am user bandit23"    : the string being hashed (from the script)
#   | md5sum                     : compute the MD5 hash
#   | cut -d ' ' -f 1            : extract only the hash (first field, space-delimited)
echo "I am user bandit23" | md5sum | cut -d ' ' -f 1
#   Output: 8ca319486bfbbc3663ea0fbe81326349   ← this is the filename in /tmp!

# Step 5: Read the file
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
#   Output: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga   ← password for Level 23!
```

### 🔑 Password for Level 23

```
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `md5sum` | Computes the MD5 hash of input (128-bit fingerprint) |
| `cut -d ' ' -f 1` | Splits text by the delimiter (space) and takes the first field |
| `$(...)` | Command substitution — runs the command and inserts its output |
| Reproducing hashes | If you know the input, you can recompute the hash to find the filename |

> 💡 **Pro Tip:** MD5 is cryptographically broken (don't use it for security), but it's still widely used for checksums and filename generation. The `cut` command is a text-processing workhorse — learn `-d` (delimiter) and `-f` (field).

### 🚀 Onward to Level 23!

```bash
exit
ssh bandit23@bandit.labs.overthewire.org -p 2220
```

---

## Level 23 → Level 24

### 📋 Level Goal

> A cron job executes scripts from `/var/spool/bandit24/foo`. Create your own shell script to extract the password.

> ⚠️ **NOTE:** This is your first shell script — a big milestone! Be proud.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit23
ssh bandit23@bandit.labs.overthewire.org -p 2220

# Step 2: Read the cron job to understand the mechanism
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
#   The script: cd /var/spool/bandit24/foo
#               for each file owned by bandit23: execute it, then delete it

# Step 3: Go to the spool directory
cd /var/spool/bandit24/foo

# Step 4: Create a directory to store the output (where bandit23 can write)
mkdir /tmp/bandit23_output

# Step 5: Write your shell script
#   nano myscript.sh    : open nano text editor
nano myscript.sh
```

Inside `nano`, write this script:

```bash
#!/bin/bash
#   ^^^^^^^^^^^^  The "shebang" — tells Linux this is a Bash script
#   Copy the password to a file we can read
cat /etc/bandit_pass/bandit24 > /tmp/bandit23_output/password.txt
#   ^^^  reads the password         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  writes to our file
#   Make it readable
chmod 644 /tmp/bandit23_output/password.txt
#   ^^^  change permissions         ^^^  owner:rw, group:r, others:r
```

```bash
# Step 6: Make your script executable
chmod +x myscript.sh
#   +x   : add execute permission

# Step 7: Wait one minute for cron to run...
#   (grab a coffee ☕)

# Step 8: Read the result!
cat /tmp/bandit23_output/password.txt
#   Output: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8   ← password for Level 24!
```

### 🔑 Password for Level 24

```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `#!/bin/bash` | The **shebang** — tells the system which interpreter to use |
| Writing a shell script | Your first program! Scripts automate repetitive tasks |
| `chmod +x` | Make a file executable |
| Cron execution model | Scripts in `/var/spool/bandit24/foo` are executed as bandit24, then deleted |
| Privilege escalation via cron | A script owned by you, executed by a privileged user, writing to your directory |

> 🎉 **Congratulations!** You just wrote your first shell script. This is a huge step. Every sysadmin, developer, and hacker writes scripts. You've joined the club.

### 🚀 Onward to Level 24!

```bash
exit
ssh bandit24@bandit.labs.overthewire.org -p 2220
```

---

## Level 24 → Level 25

### 📋 Level Goal

> A daemon listens on port 30002. It gives you the bandit25 password if you provide the bandit24 password **plus a secret 4-digit PIN**. There's no way to retrieve the PIN except by trying all 10,000 combinations — **brute force**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit24
ssh bandit24@bandit.labs.overthewire.org -p 2220

# Step 2: Brute-force ALL 10,000 PINs in a single connection
#   for i in $(seq -w 0000 9999); do    : loop through 0000, 0001, ... 9999
#       echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
#                                         : print password + PIN
#   done                                  : end the loop
#   | nc localhost 30002                  : pipe all attempts into ONE netcat connection
#   | grep -v "Wrong"                     : filter OUT lines with "Wrong" (show only success)
for i in $(seq -w 0000 9999); do
  echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
done | nc localhost 30002 | grep -v "Wrong"
#   Output: Correct!
#           The password of bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
#                                     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ← password!

#   HOW THE LOOP WORKS:
#   seq -w 0000 9999  → generates: 0000\n0001\n0002\n...\n9999
#   -w = equal width (pad with leading zeros: 0001 not 1)
#   for i in $(...)   → iterate over each number
#   echo "password $i" → format: "gb8KRRC... 0000", "gb8KRRC... 0001", etc.
```

### 🔑 Password for Level 25

```
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| Brute-force attack | Systematically trying all possible combinations |
| `seq -w 0000 9999` | Generate a sequence of zero-padded numbers |
| `for` loop in Bash | Iterate over a list of items |
| Single-connection brute-force | Keeping the TCP connection open for all attempts (much faster than reconnecting) |
| `grep -v "pattern"` | `-v` = invert — show lines that do NOT match the pattern |

> 💡 **Pro Tip:** Brute-force is the simplest attack — and often the slowest. The key insight here is keeping the connection open (piping into one `nc` call, not calling `nc` 10,000 times). This is the difference between seconds and minutes. Always optimize your brute-force loops!

### 🚀 Onward to Level 25!

```bash
exit
ssh bandit25@bandit.labs.overthewire.org -p 2220
```

---

## Level 25 → Level 26

### 📋 Level Goal

> Logging in to bandit26 should be fairly easy... The shell for bandit26 is **not /bin/bash** but something else. Find out what it is, how it works, and how to break out of it.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit25
ssh bandit25@bandit.labs.overthewire.org -p 2220

# Step 2: Check what shell bandit26 uses
#   cat /etc/passwd       : the system user database
#   | grep bandit26       : filter for bandit26's entry
cat /etc/passwd | grep bandit26
#   Output: bandit26:x:11026:11026:...:/home/bandit26:/usr/bin/showtext
#                                                     ^^^^^^^^^^^^^^^^^
#   The shell is /usr/bin/showtext — NOT /bin/bash!

# Step 3: Investigate what showtext does
cat /usr/bin/showtext
#   Output: #!/bin/sh
#           more ~/text.txt
#           exit 0
#   It runs "more" to display ~/text.txt, then exits!

# Step 4: Get the SSH key for bandit26
ls
#   Output: bandit26.sshkey
cat bandit26.sshkey
#   Copy this key to your local machine
exit

# Step 5: Save the key locally
nano bandit26.key
#   Paste the key, save, exit
chmod 600 bandit26.key

# Step 6: THE TRICK — make your terminal window VERY SMALL before connecting!
#   Shrink the terminal window to just a few lines tall.
#   WHY? When the window is too small for "more" to display all the text,
#   it PAUSES and waits for you — giving you control!

# Step 7: Connect with the key
ssh -i bandit26.key bandit26@bandit.labs.overthewire.org -p 2220
#   You should see "more" paused with "--More--(XX%)" at the bottom

# Step 8: Break out of "more" into "vim"
#   Press "v" (lowercase v)
#   This opens the current file in vim!

# Step 9: From vim, change the shell and spawn bash
#   Type exactly:
:set shell=/bin/bash
#   Press Enter
:shell
#   Press Enter
#   You are now in a real Bash shell as bandit26!

# Step 10: Get the password
cat /etc/bandit_pass/bandit26
#   Output: s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ   ← password for Level 26!
```

### 🔑 Password for Level 26

```
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `/etc/passwd` | The user database — contains username, UID, home directory, and shell |
| Non-standard shells | A user's shell doesn't have to be `/bin/bash` — it can be any program |
| `more` pager | Displays text one screen at a time; pauses when the terminal is too small |
| `v` in `more` | Opens the current file in `vim` (the text editor) |
| `:set shell=/bin/bash` | In vim, change the shell used by the `:shell` command |
| `:shell` | In vim, spawn a shell |
| Restricted shell escape | Breaking out of a limited environment into a full shell |

> 💡 **Pro Tip:** This is one of the most creative levels in Bandit. The "make the terminal tiny" trick is a classic restricted-environment escape. Always check `/etc/passwd` when something seems off — the shell field is the first thing to inspect.

### 🚀 Onward to Level 26!

```bash
exit
ssh bandit26@bandit.labs.overthewire.org -p 2220
```

---

## Level 26 → Level 27

### 📋 Level Goal

> Good job getting a shell! Now hurry and grab the password for bandit27!

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Repeat the escape from Level 25 → 26 to get a shell as bandit26
#   (Shrink terminal, ssh -i bandit26.key, press v, :set shell=/bin/bash, :shell)

# Step 2: List files in the home directory
ls
#   Output: bandit27-do    ← another setuid binary!

# Step 3: Use the setuid binary to read the password
#   ./bandit27-do    : runs commands as bandit27
#   cat /etc/bandit_pass/bandit27   : read the password file
./bandit27-do cat /etc/bandit_pass/bandit27
#   Output: upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB   ← password for Level 27!
```

### 🔑 Password for Level 27

```
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| Combining techniques | Shell escape + setuid binary = privilege escalation chain |
| Quick win | After a complex escape, sometimes the next level is a simple reward |

> 💡 **Pro Tip:** This level is a "bonus round" — you already did the hard work escaping the restricted shell. Now you just apply the same setuid technique from Level 19. In real pentesting, chaining exploits together is how you go from low-privilege to root.

### 🚀 Onward to Level 27!

```bash
exit
ssh bandit27@bandit.labs.overthewire.org -p 2220
```

---

## Level 27 → Level 28

### 📋 Level Goal

> There is a **Git repository** at `ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo` via port 2220. The password for `bandit27-git` is the same as for `bandit27`. Clone the repository and find the password.

### 💻 Commands — With Line-by-Line Comments

```bash
# ⚠️ FROM LEVEL 27 TO 31: Clone the repos on YOUR LOCAL MACHINE, not the Bandit server!

# Step 1: Clone the Git repository
#   git clone URL          : download a copy of the repository
#   ssh://bandit27-git@... : the repository address (SSH protocol, port 2220)
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
#   When prompted for password: use the bandit27 password

# Step 2: Enter the cloned repository
cd repo

# Step 3: List files
ls
#   Output: README

# Step 4: Read the README file
cat README
#   Output: The password to the next level is: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
#                                               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  ← password!
```

### 🔑 Password for Level 28

```
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `git clone <url>` | Downloads (clones) a remote Git repository to your local machine |
| SSH-based Git | Git can use SSH for authentication — same port, same keys |
| Repository structure | A Git repo is a directory with a `.git/` folder tracking all history |

> 💡 **Pro Tip:** Git is the backbone of modern software development. This is the first of several Git-based levels. The key skill: Git stores ALL history. Even if something is deleted now, it might still exist in an older commit.

### 🚀 Onward to Level 28!

```bash
ssh bandit28@bandit.labs.overthewire.org -p 2220
```

---

## Level 28 → Level 29

### 📋 Level Goal

> Clone the Git repository at `ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo`. The password is hidden in the commit history.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Clone the repository
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
cd repo

# Step 2: Read the current README
cat README.md
#   Output: # Bandit Notes
#           credentials for bandit29
#           - username: bandit29
#           - password: xxxxxxxxxx    ← REDACTED! Someone hid the password...

# Step 3: Check the commit history
#   git log    : shows all commits, newest first, with author, date, and message
git log
#   Output: commit d0cf2ab7dd7ebc6075b59102a980155268f0fe8f  ← "add missing data"
#           commit 1234567890...                              ← "fix info leak"
#           commit abcdef1234...                              ← "initial commit"
#   The "add missing data" commit looks suspicious!

# Step 4: Inspect the suspicious commit
#   git show COMMIT_HASH    : display the full changes introduced by a commit
git show d0cf2ab7dd7ebc6075b59102a980155268f0fe8f
#   Output: - password: xxxxxxxxxx
#           + password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7    ← password revealed!
```

### 🔑 Password for Level 29

```
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `git log` | Shows the commit history of the repository |
| `git show <hash>` | Displays the full diff of a specific commit |
| Commit hashes | Every commit has a unique SHA-1 hash identifier |
| Git history is permanent | Deleting data in a new commit doesn't erase it from old commits |

> 💡 **Pro Tip:** NEVER commit secrets (passwords, API keys, tokens) to Git. Even if you "remove" them later, the history is still there. This is one of the most common security mistakes in the real world. Use `.gitignore` and environment variables instead.

### 🚀 Onward to Level 29!

```bash
ssh bandit29@bandit.labs.overthewire.org -p 2220
```

---

## Level 29 → Level 30

### 📋 Level Goal

> Clone the repository. The password is hidden in a different **branch**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Clone the repository
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
cd repo

# Step 2: Check the current README
cat README.md
#   Output: # Bandit Notes
#           no passwords in production!    ← no password on the master branch

# Step 3: List ALL branches (including remote ones)
#   git branch -a    : show all branches (-a = all, including remote)
git branch -a
#   Output: * master
#             remotes/origin/HEAD -> origin/master
#             remotes/origin/dev       ← interesting! A "dev" branch!
#             remotes/origin/master
#             remotes/origin/sploits

# Step 4: Switch to the "dev" branch
#   git checkout dev    : switch to the dev branch (Git auto-detects the remote branch)
git checkout dev
#   Output: Branch 'dev' set up to track remote branch 'dev' from 'origin'.

# Step 5: Read the README on the dev branch
cat README.md
#   Output: # Bandit Notes
#           credentials for bandit30
#           - username: bandit30
#           - password: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL    ← password!
```

### 🔑 Password for Level 30

```
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `git branch -a` | List all local and remote branches |
| `git checkout <branch>` | Switch to a different branch |
| `master` vs `dev` | Common branch naming: `master`/`main` for production, `dev` for development |
| Remote branches | Branches stored on the server (prefixed with `remotes/origin/`) |

> 💡 **Pro Tip:** In real projects, the `dev` branch often contains features not yet ready for production — and sometimes, accidentally committed secrets. Always check all branches during a security audit.

### 🚀 Onward to Level 30!

```bash
ssh bandit30@bandit.labs.overthewire.org -p 2220
```

---

## Level 30 → Level 31

### 📋 Level Goal

> Clone the repository. The password is hidden in a **tag**.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Clone the repository
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
cd repo

# Step 2: Check the README — nothing useful
cat README.md
#   Output: just an epmty file... muahaha    ← the author is taunting us!

# Step 3: Check commits (nothing), branches (nothing)... what about TAGS?
#   git tag    : list all tags in the repository
git tag
#   Output: secret    ← a tag named "secret"!

# Step 4: Show the contents of the tag
#   git show secret    : display the tag's message and associated commit
git show secret
#   Output: fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy    ← password!
```

### 🔑 Password for Level 31

```
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `git tag` | Lists all tags in the repository |
| `git show <tag>` | Displays the contents associated with a tag |
| Git tags | Markers for specific commits — often used for releases (v1.0, v2.0, etc.) |
| Hidden in plain sight | Tags are visible but easily overlooked — always check them! |

> 💡 **Pro Tip:** Tags are the third place to check in Git (after commits and branches). Tags can have their own messages separate from commit messages. In CTFs and audits, always run `git tag` — you might find something interesting.

### 🚀 Onward to Level 31!

```bash
ssh bandit31@bandit.labs.overthewire.org -p 2220
```

---

## Level 31 → Level 32

### 📋 Level Goal

> Clone the repository. This time, you need to **push** a specific file to the remote. The server-side hook will reveal the password.

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Clone the repository
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
cd repo

# Step 2: Read the instructions
cat README.md
#   Output: This time your task is to push a file to the remote repository.
#           Details:
#           File name: key.txt
#           Content: 'May I come in?'
#           Branch: master

# Step 3: Create the required file
#   echo "TEXT" > filename    : write text to a file (creates it if it doesn't exist)
echo "May I come in?" > key.txt

# Step 4: Check if the file is ignored by Git
cat .gitignore
#   Output: *.txt    ← ALL .txt files are ignored!

# Step 5: Force-add the file (bypass .gitignore)
#   git add -f key.txt    : -f = force — add even if .gitignore says to ignore it
git add -f key.txt

# Step 6: Configure Git identity (required for committing)
#   The identity can be found in the server's .gitconfig
git config user.name "bandit31"
git config user.email "bandit31@overthewire.org"

# Step 7: Commit the file
git commit -m "add key"
#   -m "message"    : the commit message

# Step 8: Push to the remote repository
git push
#   The push is REJECTED, but the server hook prints:
#   Output: remote: Well done! Here is the password for the next level:
#           remote: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K    ← password!
```

### 🔑 Password for Level 32

```
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

### 🧠 What You Learned

| Command | What It Does |
|---------|-------------|
| `git add -f` | Force-add a file even if it's in `.gitignore` |
| `.gitignore` | A file listing patterns that Git should ignore |
| `git config user.name/email` | Set your identity for commits |
| `git push` | Upload your commits to the remote repository |
| Server-side hooks | Scripts that run on the server when you push — can validate, reject, or print messages |

> 💡 **Pro Tip:** This level teaches that Git interactions go both ways. Server-side hooks (pre-receive, post-receive) can run arbitrary code. In the real world, this is used for CI/CD pipelines, code quality checks, and... occasionally... CTF challenges!

### 🚀 Onward to Level 32!

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

---

## Level 32 → Level 33

### 📋 Level Goal

> After all the Git stuff, it's time for another escape. This time you're in an **uppercase shell** — it converts ALL commands to uppercase!

### 💻 Commands — With Line-by-Line Comments

```bash
# Step 1: Connect as bandit32
ssh bandit32@bandit.labs.overthewire.org -p 2220

# You're greeted with:
#   WELCOME TO THE UPPERCASE SHELL
#   >> 
#   Try typing "ls" — it becomes "LS" (which doesn't work!)
#   Try "cat" — becomes "CAT" (nope!)
#   Try "whoami" — becomes "WHOAMI" (nothing!)

# Step 2: THE TRICK — use the special variable $0
#   $0    : a shell variable that contains the name of the current shell/program
#   Typing $0 re-executes the shell itself, but this time WITHOUT the uppercase restriction
#   (because the restriction is in the wrapper program, not the actual shell)
$0
#   Press Enter

# Step 3: You're now in a normal shell!
whoami
#   Output: bandit33    ← we're running as bandit33!

# Step 4: Read the final password
cat /etc/bandit_pass/bandit33
#   Output: tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0    ← the FINAL password!
```

### 🔑 Password for Level 33

```
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

### 🧠 What You Learned

| Concept | Explanation |
|---------|-------------|
| `$0` | A special shell variable — contains the name of the current shell or script |
| Uppercase shell | A restricted environment that converts all input to uppercase |
| Shell re-execution | Running `$0` spawns a new instance of the shell without the wrapper's restrictions |
| Special variables | `$0` (shell name), `$1`-`$9` (arguments), `$?` (exit code), `$$` (PID) |

> 💡 **Pro Tip:** `$0` is one of the most useful special variables. In a restricted environment, always try `$0`, `bash`, `sh`, `/bin/bash`, and `exec /bin/bash`. One of them usually works. The uppercase shell is a classic CTF challenge — now you know the trick!

### 🚀 Onward to the Final Level!

```bash
ssh bandit33@bandit.labs.overthewire.org -p 2220
```

---

## Level 33 → Level 34

### 📋 Level Goal

> **At this moment, level 34 does not exist yet.**

### 💻 Commands

```bash
# Step 1: Connect as bandit33
ssh bandit33@bandit.labs.overthewire.org -p 2220

# Step 2: See what's here
ls
#   Output: README.txt

# Step 3: Read the final message
cat README.txt
#   Output: Congratulations on solving the last level of Bandit!
#           ...
```

### 🔑 Password

```
None — this is the end. 🏁
```

### 🧠 Explanation

Sadly, it ended. But what a journey! From `cat readme` to escaping uppercase shells, from base64 to brute-force, from cron jobs to Git archaeology — you've covered an incredible amount of ground.

---

## 🏁 Conclusion

The **OverTheWire Bandit** wargame is one of the best introductions to Linux, security, and problem-solving you can find. In 34 levels, you've learned:

| Phase | Levels | Skills Acquired |
|-------|--------|-----------------|
| 🟢 **Linux Fundamentals** | 0–3 | `ssh`, `ls`, `cat`, `cd`, special filenames, hidden files |
| 🔵 **File Analysis** | 4–6 | `file`, `find`, multi-criteria search, `2>/dev/null` |
| 🟡 **Text Processing** | 7–11 | `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, ROT13 |
| 🟠 **Decompression** | 12 | `xxd`, `gunzip`, `bunzip2`, `tar`, multi-layer extraction |
| 🔴 **Networking** | 13–16 | SSH keys, `nc`, `openssl s_client`, `nmap`, port scanning |
| 🟣 **Advanced Shell** | 17–20 | `diff`, SSH inline commands, `setuid`, two-terminal workflows |
| 🟤 **Cron & Automation** | 21–24 | `cron`, `md5sum`, shell scripting, brute-force attacks |
| ⚫ **Shell Escapes** | 25–26, 32 | `more` → `vim` escape, restricted shells, `$0` trick |
| 🔷 **Git Mastery** | 27–31 | `clone`, `log`, `show`, `branch`, `checkout`, `tag`, `push`, `.gitignore` |

---

<div align="center">

## 🎉 YOU DID IT! 🎉

### All 34 Levels — Complete!

<p>
  <img src="https://img.shields.io/badge/Levels-34%2F34-brightgreen?style=for-the-badge" alt="34/34 levels completed"/>
  <img src="https://img.shields.io/badge/Difficulty-Increasing-red?style=for-the-badge" alt="Progressively harder"/>
  <img src="https://img.shields.io/badge/Skills-20%2B-blue?style=for-the-badge" alt="20+ skills learned"/>
</p>

---

> *"The quieter you become, the more you can hear."* — Ram Dass

> *"In the world of Linux, there's always another way. Find it."*

---

### 📝 About This Writeup

Every command is commented. Every concept is explained. Built for beginners who want to actually **understand**, not just copy-paste.

### ⭐ Found this helpful?

Share it with a friend. Star it. Use it as a reference. And most importantly — **keep hacking**.

---

**Author:** [B0GYMAN]

**Last Updated:** 29 June 2026

**Official Bandit:** [https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)

---

<p align="center">
  <sub>This writeup is for educational purposes only. All passwords shown are examples and may differ from live server values.</sub>
</p>

</div>
