# PicoCTF -- PW Crack 4

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Crack the password by identifying which of 100 candidates matches the stored MD5 hash.

---

## Solution

Downloaded the files and read the script:

    cat level4.py

Same structure as PW Crack 3 but with 100 candidate passwords listed at the bottom of the script instead of 7.

Used the same approach -- hash each candidate and compare against the stored hash:

    python3 -c "
    import hashlib
    correct = open('level4.hash.bin', 'rb').read()
    pos_pw_list = ['8c86', '7692', 'a519', ...]
    for pw in pos_pw_list:
        h = hashlib.md5(pw.encode()).digest()
        if h == correct:
            print('Correct password:', pw)
    "

Output:

    Correct password: 9f63

Ran the script and entered the password:

    python3 level4.py
    9f63

Output:

    picoCTF{fl45h_5pr1ng1ng_d770d48c}

---

## Concepts Learned

The approach from PW Crack 3 scales to any size candidate list without modification. With 7 passwords, manual testing is possible but tedious. With 100, it becomes impractical. With 10,000 or more, only automation works. The same script handles all cases -- just change the list.

This is exactly how real password cracking tools like hashcat operate. They take a wordlist with potentially millions of entries, hash each one using the target algorithm, and check for matches against leaked databases.

---

## Key Takeaway

Automation scales where manual effort cannot. The habit of writing small scripts to automate repetitive tasks -- hashing, comparing, filtering -- is essential in security work. A task that would take hours manually takes seconds with a well-written one-liner.

---

## Flag

picoCTF{fl45h_5pr1ng1ng_d770d48c}
