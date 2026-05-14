# PicoCTF -- Warmed Up

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Convert 0x3D from hexadecimal (base 16) to decimal (base 10).

---

## Solution

Manual conversion:

    0x3D = (3 x 16) + 13 = 48 + 13 = 61

Verified using bc:

    echo "obase=10; ibase=16; 3D" | bc
    61

Flag format requires wrapping the answer:

    picoCTF{61}

---

## Concepts Learned

Hexadecimal is base 16, using digits 0-9 and letters A-F. The 0x prefix indicates a hex value. Converting to decimal requires multiplying each digit by its positional power of 16.

The bc command is a command-line calculator that supports base conversion. obase sets the output base, ibase sets the input base.

In CyberChef, the From Hex operation converts hex values.

---

## Key Takeaway

Number base conversion -- between decimal, hexadecimal, binary, and octal -- is a constant requirement in CTFs and security work. Memory addresses, colour codes, file headers, and network data are all commonly expressed in hex. Being comfortable with manual conversion and knowing the right tools speeds up analysis significantly.

---

## Flag

picoCTF{61}
