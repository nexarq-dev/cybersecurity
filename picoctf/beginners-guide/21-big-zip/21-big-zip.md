# PicoCTF -- Big Zip

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find the flag hidden somewhere inside a large zip archive with many nested directories.

---

## Solution

Downloaded and unzipped the archive:

    wget [url]/big-zip-files.zip
    unzip big-zip-files.zip

Used grep recursively to search all files in all subdirectories:

    grep -r "picoCTF" big-zip-files/

Output:

    big-zip-files/folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:...picoCTF{gr3p_15_m4g1c_ef8790dc}

---

## Concepts Learned

The -r flag makes grep recursive -- it searches every file in every subdirectory automatically, no matter how deep the structure goes. Without it, grep only searches the specified file or the immediate directory.

The archive contained four levels of nested directories with random names. Manual navigation would have required dozens of ls and cd commands with no guarantee of finding the right file. grep -r found it in one command.

---

## Key Takeaway

grep -r is one of the most useful command combinations in Linux. When you need to find something across a large file structure -- source code repositories, log directories, forensic images -- grep -r "searchterm" directory/ is the answer. The -l flag can be added to show only filenames rather than matching lines, useful when there are many matches.

---

## Flag

picoCTF{gr3p_15_m4g1c_ef8790dc}
