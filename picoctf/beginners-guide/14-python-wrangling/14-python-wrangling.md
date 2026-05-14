# PicoCTF -- Python Wrangling

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Run a Python script to decrypt an encrypted flag file using a provided password.

---

## Solution

Downloaded all three files:

    wget [url]/ende.py
    wget [url]/password.txt
    wget [url]/flag.txt.en

Read the script to understand its interface:

    cat ende.py

The script accepts -e to encrypt and -d to decrypt. It prompts for a password.

Read the password:

    cat password.txt
    720b6ad346f84cd483c60c7464dd95d4

Ran the decryption:

    python3 ende.py -d flag.txt.en

Entered the password when prompted:

    picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}

---

## Concepts Learned

Python scripts are run with python3 scriptname.py. Reading the script before running it reveals what arguments it accepts and what it does. The -d flag told the script to decrypt rather than encrypt.

The script used Fernet symmetric encryption from the cryptography library. Fernet takes a password, base64 encodes it, and uses it as an encryption key. The same key that encrypts can decrypt -- hence symmetric.

---

## Key Takeaway

Always read a script before running it. cat script.py takes seconds and tells you exactly what the script does, what arguments it accepts, and what dependencies it needs. In security work you constantly encounter unfamiliar scripts -- running them blind is a bad habit.

---

## Flag

picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}
