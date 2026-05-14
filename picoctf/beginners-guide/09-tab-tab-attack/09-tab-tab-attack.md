# PicoCTF -- Tab Tab Attack

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Navigate a deeply nested directory structure using tab completion to find and read the flag.

---

## Solution

Downloaded and unzipped the archive:

    wget [url]/Addadshashanammu.zip
    unzip Addadshashanammu.zip

Used tab completion to navigate seven levels deep:

    cat Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet.c

Output:

    #include <stdio.h>
    int main(){
    printf("*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}\n");
    }

---

## Concepts Learned

Tab completion automatically completes file and directory names when you press Tab after typing the first few characters. When navigating deeply nested structures, typing the first two or three characters of each folder name and pressing Tab saves significant time and eliminates typing errors.

There were two files in the final folder -- fang-of-haynekhtnamet (compiled binary) and fang-of-haynekhtnamet.c (source code). The .c file is human readable. The binary contains machine code that is largely unreadable without tools.

---

## Key Takeaway

Tab completion is one of the most productive habits in Linux. In security work you navigate complex directory structures constantly -- log files, source repositories, forensic images. Tab completion makes this fast and accurate.

---

## Flag

picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}
