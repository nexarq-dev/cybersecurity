# PicoCTF -- 2Warm

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Convert the number 42 from decimal (base 10) to binary (base 2).

---

## Solution

Manual conversion by repeated division by 2:

    42 / 2 = 21 remainder 0
    21 / 2 = 10 remainder 1
    10 / 2 = 5  remainder 0
    5  / 2 = 2  remainder 1
    2  / 2 = 1  remainder 0
    1  / 2 = 0  remainder 1

Reading remainders from bottom to top: 101010

Verified using bc:

    echo "obase=2; 42" | bc
    101010

---

## Concepts Learned

Binary is base 2, using only 0 and 1. Every number can be expressed as a sum of powers of 2. Converting from decimal to binary uses repeated division by 2, collecting remainders from bottom to top.

Binary is the fundamental language of computing. Understanding it is essential for reading memory dumps, analysing file headers, working with bitwise operations in smart contracts, and understanding how data is stored at the lowest level.

---

## Key Takeaway

Binary conversion is foundational. In smart contract security, bitwise operations and binary representations appear in low-level EVM work and storage layout analysis. Being fluent in base conversion across decimal, hex, and binary is a core skill.

---

## Flag

picoCTF{101010}
