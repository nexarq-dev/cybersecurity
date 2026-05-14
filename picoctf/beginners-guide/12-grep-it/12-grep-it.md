# PicoCTF -- Grep It

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find the flag hidden inside a large file without manually reading through it.

---

## Solution

Downloaded the file:

    wget [url]/file

Used grep to search for the flag pattern:

    grep "picoCTF" file

Output:

    picoCTF{grep_is_good_to_find_things_e3C4b360}

---

## Concepts Learned

grep searches through text for a specified pattern and prints matching lines. When given a large file with thousands of lines of random characters, grep finds the flag instantly rather than requiring manual inspection.

The basic syntax is:

    grep "searchterm" filename

For searching across multiple files recursively:

    grep -r "searchterm" directory/

Using less with search is an alternative for interactive exploration:

    less file
    /picoCTF    (then press Enter to jump to the match)

---

## Key Takeaway

grep is one of the most powerful and frequently used tools in Linux. In security work it is used to search log files for suspicious activity, find credentials in source code, locate specific strings in large datasets, and filter command output. Mastering grep -- including its -r, -i, -n, and -l flags -- is essential for efficient security analysis.

---

## Flag

picoCTF{grep_is_good_to_find_things_e3C4b360}
