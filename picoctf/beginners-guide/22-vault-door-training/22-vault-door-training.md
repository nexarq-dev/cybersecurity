# PicoCTF -- Vault Door Training

**Platform:** PicoCTF / CyLab Security Academy
**Category:** Reverse Engineering
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find the password hardcoded in Java source code to open the vault door.

---

## Solution

Downloaded and read the source code:

    wget [url]/VaultDoorTraining.java
    cat VaultDoorTraining.java

Found the password hardcoded in the checkPassword function:

    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_000wYdiGTvt");
    }

The main function strips picoCTF{ from the start and } from the end before checking. So the full flag is:

    picoCTF{w4rm1ng_Up_w1tH_jAv4_000wYdiGTvt}

The developer even left a comment admitting it was a bad idea:

    // The password is below. Is it safe to put the password in the source code?
    // What if somebody stole our source code? Then they would know what our
    // password is. Hmm... I will think of some ways to improve the security
    // on the other doors.
    // -Minion #9567

---

## Concepts Learned

Hardcoded credentials appear in every programming language -- Python, Java, C, JavaScript, Solidity. The language does not change the vulnerability. Anyone with access to the source code can read the credential instantly.

In real security audits, searching source code for patterns like .equals(", == ", password =, and secret = is one of the first steps in a code review. Automated tools like truffleHog, gitleaks, and GitHub Secret Scanning detect hardcoded credentials in repositories.

---

## Key Takeaway

The developer in this challenge knew the password was insecure and left a comment saying so -- then shipped it anyway. This is a common pattern in real codebases. Time pressure, convenience, and the assumption that source code will stay private lead to credentials remaining in code long after they should have been removed. Source code escapes -- through leaks, open source releases, or disgruntled employees. Credentials in code must be treated as compromised.

---

## Flag

picoCTF{w4rm1ng_Up_w1tH_jAv4_000wYdiGTvt}
