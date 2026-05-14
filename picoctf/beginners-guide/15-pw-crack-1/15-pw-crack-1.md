# PicoCTF -- PW Crack 1

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Crack the password to decrypt the flag by reading the Python source code.

---

## Solution

Downloaded the files:

    wget [url]/level1.py
    wget [url]/level1.flag.txt.enc

Read the script:

    cat level1.py

The password was hardcoded in plain text inside the checkPassword function:

    if( user_pw == "8713"):

Ran the script and entered the password:

    python3 level1.py
    8713

Output:

    picoCTF{545h_r1ng1ng_1b2fd683}

---

## Concepts Learned

Hardcoded credentials are passwords, API keys, or secrets stored directly in source code. This is one of the most common and critical vulnerability classes in real-world security audits. Anyone with access to the source code can read the credential instantly.

This is why source code repositories should never contain credentials. Secrets belong in environment variables, secret management systems, or dedicated credential stores -- never in code.

---

## Key Takeaway

Always read the source code before running a program. Hardcoded credentials are a top finding in real security audits and appear in every language. Searching source code for patterns like password =, secret =, key =, and token = is one of the first steps in a code review.

---

## Flag

picoCTF{545h_r1ng1ng_1b2fd683}
