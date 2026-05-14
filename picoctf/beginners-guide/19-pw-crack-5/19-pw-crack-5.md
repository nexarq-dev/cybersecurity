# PicoCTF -- PW Crack 5

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Crack the password by finding the matching MD5 hash from a dictionary file containing 65,536 candidate passwords.

---

## Solution

Downloaded the files:

    wget [url]/level5.py
    wget [url]/level5.flag.txt.enc
    wget [url]/level5.hash.bin
    wget [url]/dictionary.txt

Checked the size of the dictionary:

    wc -l dictionary.txt
    65536 dictionary.txt

Read the script -- same MD5 hash comparison structure as levels 3 and 4, but with no hardcoded candidate list. The password must come from dictionary.txt.

Wrote a Python one-liner to read the dictionary file and find the matching hash:

    python3 -c "
    import hashlib
    correct = open('level5.hash.bin', 'rb').read()
    for pw in open('dictionary.txt').read().splitlines():
        pw = pw.strip()
        h = hashlib.md5(pw.encode()).digest()
        if h == correct:
            print('Correct password:', pw)
    "

Output:

    Correct password: eee0

Ran the script and entered the password:

    python3 level5.py
    eee0

Output:

    picoCTF{h45h_sl1ng1ng_1e4c0d1f}

---

## Concepts Learned

Reading from a file in Python uses open('filename').read(). The splitlines() method splits the text into a list of lines. The strip() method removes whitespace including newline characters from each line before hashing -- essential because a trailing newline would produce a different hash.

65,536 passwords is far too many to test manually. The same script that worked on 7 and 100 candidates works on 65,536 without modification -- only the data source changed from a hardcoded list to a file.

---

## Key Takeaway

Real password cracking uses wordlists -- files containing millions of common passwords, dictionary words, and known leaked passwords. The rockyou.txt wordlist alone contains 14 million entries. Tools like hashcat can test billions of hashes per second against such lists. The defence is not a stronger hash algorithm alone but combining hashing with salting and using algorithms designed to be slow like bcrypt or Argon2.

---

## Flag

picoCTF{h45h_sl1ng1ng_1e4c0d1f}
