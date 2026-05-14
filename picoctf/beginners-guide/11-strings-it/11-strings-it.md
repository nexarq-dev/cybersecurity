# PicoCTF -- Strings It

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find the flag in a binary file without running it.

---

## Solution

Downloaded the binary:

    wget [url]/strings

Used the strings command to extract readable text, piped through grep:

    strings strings | grep picoCTF

Output:

    picoCTF{5tRIng5_1T_47948C73}

---

## Concepts Learned

The strings command extracts all human-readable text from any file -- compiled binaries, firmware, malware samples. Binaries often contain readable strings such as function names, error messages, URLs, and sometimes credentials or flags left by developers.

Piping strings output through grep filters the results to show only matching lines. Without grep, strings on a large binary produces hundreds of lines. With grep, you get exactly what you need in one step.

---

## Key Takeaway

strings is one of the first tools used when analysing an unknown binary. It gives a quick overview of what the program might do and what data it contains before deeper analysis. In real security work it is used to find hardcoded credentials, URLs, and configuration data in compiled applications.

---

## Flag

picoCTF{5tRIng5_1T_47948C73}
