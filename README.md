# Bandit Level 7 → Level 8 | OverTheWire Write-Up

> A practical exploration of efficient text filtering, Linux pipelines, and command-line data extraction.

**Date:** 1 March 2026  
**Platform:** OverTheWire  
**Challenge:** Bandit Level 7  
**Category:** Linux / Text Processing  
**Difficulty:** Easy (3/10)  
**Estimated Solving Time:** ~5 minutes  

---

## Table of Contents
- [Overview](#overview)
- [Challenge Description](#challenge-description)
- [Environment Setup](#environment-setup)
- [Step-by-Step Walkthrough](#step-by-step-walkthrough)
- [Command Breakdown & Functional Analysis](#command-breakdown--functional-analysis)
- [Optimised Alternative Approach](#optimised-alternative-approach)
- [Final Password](#final-password)
- [Key Takeaways](#key-takeaways)

---

## Overview

In cybersecurity engineering, the ability to extract specific information from large datasets is essential. Whether analysing server logs (e.g. Apache or Nginx), reviewing application output, or searching for exposed credentials, text-processing tools are indispensable.

This level of Bandit simulates a realistic scenario:

> A specific piece of information (the password) is hidden within a large file, and only a keyword clue is provided.

To solve it efficiently, we rely on standard Linux command-line utilities, particularly `grep`, combined with shell pipelines.

---

## Challenge Description

The goal is to retrieve the password for **Bandit Level 8**.

### Provided Information

- The password is stored in a file named `data.txt`
- The password is located **on the same line as the word `"millionth"`**
- The file is large enough that manual inspection is impractical

### Technical Details

- **Source File:** `~/data.txt`
- **Search Keyword:** `millionth`
- **Expected Output:** 32-character alphanumeric password string

---

## Environment Setup

### 1. Establish SSH Connection

We begin by connecting to the Bandit server using SSH:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

After entering the password from Level 6, we gain access to the remote environment.

---

### 2. Verify File Presence and Size

Before attempting extraction, it is good practice to confirm the file exists and inspect its size:

```bash
ls -lh data.txt
```

The `-lh` flags mean:

- `-l` → long listing format  
- `-h` → human-readable file size  

The output confirms that `data.txt` is relatively large, making manual inspection inefficient and unnecessary.

---

## Step-by-Step Walkthrough

### Step 1 — Understanding the Objective

We know:
- The password appears next to the word `millionth`
- The file is too large to inspect manually
- We need a filtering approach

This makes `grep` the ideal tool.

---

### Step 2 — Filtering the File with `grep`

We execute:

```bash
cat data.txt | grep "millionth"
```

### Command Execution

```bash
bandit7@bandit:~$ cat data.txt | grep "millionth"
```

### Output

```
millionth   dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

The password is the alphanumeric string following the keyword.

---

## Command Breakdown & Functional Analysis

To understand why this works, let us examine each component.

---

### `cat data.txt`

**Purpose:**  
Displays the contents of a file.

**Role in this context:**  
Acts as the data source, sending the file's entire contents to standard output (stdout).

---

### `|` (Pipe Operator)

**Purpose:**  
Connects two commands.

**How it works:**  
The pipe redirects the standard output (stdout) of the command on the left to the standard input (stdin) of the command on the right.

This allows commands to work together in a data-processing chain.

---

### `grep "millionth"`

**Meaning:**  
Global Regular Expression Print.

**Function:**  
Searches input line by line for a pattern match.

**Role here:**  
Filters the incoming data stream and prints only the line containing the word `"millionth"`.

---

## Optimised Alternative Approach

Although the pipeline works perfectly, it is not strictly necessary to use `cat` here. A more efficient command is:

```bash
grep "millionth" data.txt
```

This avoids spawning an additional process and directly instructs `grep` to read from the file.

Both approaches produce identical output, but the second is considered cleaner and more efficient in Unix philosophy.

---

## Final Password

The password for **Bandit Level 8** is:

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

## Key Takeaways

- Efficient text filtering is a fundamental cybersecurity skill.
- `grep` is one of the most powerful and commonly used tools in Linux environments.
- Understanding pipelines (`|`) enables modular and readable command chaining.
- Avoid unnecessary use of `cat` when a command can read directly from a file.
- Even simple challenges reinforce essential real-world command-line techniques.

---

### Closing Thoughts

While this level is relatively straightforward, it reinforces an important mindset:

> Never process data manually when automation can do it faster, cleaner, and more reliably.

Mastery of small utilities like `grep`, `awk`, and `sed` forms the backbone of efficient system analysis and security operations.

Onwards to Level 8.
