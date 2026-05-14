# PicoCTF -- Wave a Flag

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Invoke the help flag on a downloaded binary to get the flag.

---

## Solution

Downloaded the binary:

    wget [url]/warm

Made it executable:

    chmod +x warm

Ran it with the help flag:

    ./warm -h

Output:

    Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}

---

## Concepts Learned

Downloaded files on Linux are not executable by default. chmod +x grants execute permission before a binary can be run. The -h flag is the standard convention for requesting help from a command-line program. Most tools also support --help.

---

## Key Takeaway

Always check what a binary does before running it blindly. Running with -h or --help is the safest first step -- it reveals the program's intended interface without executing its main logic.

---

## Flag

picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
