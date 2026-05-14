# PicoCTF -- PW Crack 2

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Crack the password hidden using hex encoding in the Python source code.

---

## Solution

Downloaded the files and read the script:

    cat level2.py

The password was encoded using hex character values:

    if( user_pw == chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36) ):

Decoded the hex values using Python:

    python3 -c "print(chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36))"
    de76

Ran the script and entered the password:

    python3 level2.py
    de76

Output:

    picoCTF{tr45h_51ng1ng_489dea9a}

---

## Concepts Learned

Hex encoding represents characters as their hexadecimal ASCII values. 0x64 is the hex value for the letter d, 0x65 for e, 0x37 for 7, and 0x36 for 6. This is a common obfuscation technique developers use thinking it hides credentials. It does not -- anyone who reads the code can decode hex values in seconds.

Obfuscation is not security. Whether a password is written as de76 or as four chr() calls with hex values, it is still hardcoded and still readable by anyone with access to the source.

---

## Key Takeaway

Recognising common encoding schemes on sight is an important skill. Hex values prefixed with 0x, base64 strings, and ROT13 encoded text are all trivially reversible. When reviewing source code, look beyond the surface representation of any string -- the actual value may be hidden in an encoding layer.

---

## Flag

picoCTF{tr45h_51ng1ng_489dea9a}
