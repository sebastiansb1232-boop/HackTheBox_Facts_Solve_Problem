
# Facts | Hack The Box Writeup
> A comprehensive technical report for the "Facts" machine on the Hack The Box platform.
# Bandit Level 6 → Level 7 | OverTheWire Writeup
> A detailed technical walkthrough for identifying a specific file based on system ownership and metadata properties.

**Date:** March 1, 2026
**Author:** [Your Name]
**Platform:** OverTheWire
**Challenge:** Bandit Level 6
**Categories:** Linux / File System
**Rating:** 2/10
**Difficulty:** Easy
**Solving Time:** ~10 Minutes

---

## Table of Contents
- [Overview](#overview)
- [Challenge](#challenge)
- [Walkthrough](#walkthrough)

---

## Overview
This level focuses on advanced file system navigation and the use of the `find` command to filter objects based on specific administrative attributes. Unlike previous levels where the target was within a local directory, the password is hidden "somewhere on the server," requiring a global search across the root directory.

## Challenge
The objective is to retrieve the password for **Bandit7**, which is stored in a file with the following unique properties:
* **User Owner:** `bandit7`
* **Group Owner:** `bandit6`
* **File Size:** `33 bytes`

### Available Tools
* `find`: To search for the file using filters.
* `ls`: To verify file attributes.
* `cat`: To read the password once the file is located.

---

## Walkthrough

### 1. Environment Analysis
Upon logging in as `bandit6`, we observe that the home directory does not contain the target file. The challenge description implies the file exists outside the user's immediate scope, necessitating a search starting from the root directory `/`.

### 2. Executing the Search
To find a file matching all three specific criteria, we use the `find` command. To avoid being overwhelmed by "Permission Denied" errors from system folders we cannot access, we redirect the standard error (`stderr`) to `/dev/null`.

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
