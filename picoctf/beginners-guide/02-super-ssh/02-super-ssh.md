# PicoCTF -- Super SSH

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Connect to a remote server using SSH and retrieve the flag.

---

## Solution

Connected using the provided credentials:

    ssh ctf-player@titan.picoctf.net -p 64817

Accepted the fingerprint prompt with yes, entered the password f3b61b38, and the flag was printed on login:

    Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_3e293eea}

---

## Concepts Learned

SSH (Secure Shell) is the standard protocol for connecting securely to remote servers. The command structure is:

    ssh username@hostname -p port

The -p flag specifies a non-standard port. When connecting to a server for the first time, SSH asks you to verify the server fingerprint -- typing yes adds it to your known hosts file.

---

## Key Takeaway

SSH is a foundational tool in security work. Remote server access, cloud infrastructure management, and CTF challenge environments all use SSH. Understanding the command structure and how fingerprint verification works is essential.

---

## Flag

picoCTF{s3cur3_c0nn3ct10n_3e293eea}
