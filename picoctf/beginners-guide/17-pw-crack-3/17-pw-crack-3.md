# PicoCTF -- PW Crack 3

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Crack the password by identifying which of seven candidates matches the stored MD5 hash.

---

## Solution

Downloaded the files and read the script:

    cat level3.py

The script stores an MD5 hash of the correct password and compares it against the hash of user input. Seven candidate passwords were listed at the bottom of the script.

Wrote a Python one-liner to hash each candidate and compare against the stored hash:

    python3 -c "
    import hashlib
    correct = open('level3.hash.bin', 'rb').read()
    for pw in ['6997', '3ac8', 'f0ac', '4b17', 'ec27', '4e66', '865e']:
        h = hashlib.md5(pw.encode()).digest()
        if h == correct:
            print('Correct password:', pw)
    "

Output:

    Correct password: 865e

Ran the script and entered the password:

    python3 level3.py
    865e

Output:

    picoCTF{m45h_fl1ng1ng_2b072a90}

---

## Concepts Learned

MD5 is a hashing algorithm that produces a fixed-length digest from any input. Hashing is one-way -- you cannot reverse a hash to get the original input. However, if you have a list of candidates, you can hash each one and compare against the stored hash. This is called a dictionary attack.

Real password storage should use MD5 hash with salt at minimum, but modern systems use bcrypt, scrypt, or Argon2 which are designed to be slow and resistant to brute force.

---

## Key Takeaway

Hashing passwords is better than storing them in plain text, but it is not enough on its own. A list of candidates reduces the search space from infinite to finite. With only seven candidates, the correct password was found instantly. This is why password lists and wordlists are so powerful in real attacks against leaked hash databases.

---

## Flag

picoCTF{m45h_fl1ng1ng_2b072a90}
