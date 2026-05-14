# PicoCTF -- Obedient Cat

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find the flag hidden in plain text inside a downloaded file.

---

## Solution

Downloaded the file using wget:

    wget https://challenge-files.picoctf.net/.../flag

Read the contents using cat:

    cat flag

Output:

    picoCTF{s4n1ty_v3r1f13d_9b8fa0bc}

---

## Concepts Learned

wget downloads files from the internet to your current directory. cat prints the contents of a file to the terminal. These are two of the most frequently used commands in CTF work and general Linux usage.

---

## Key Takeaway

Before reaching for complex tools, check if the answer is visible in plain text. Many early CTF challenges hide the flag in clear sight inside a downloadable file.

---

## Flag

picoCTF{s4n1ty_v3r1f13d_9b8fa0bc}
