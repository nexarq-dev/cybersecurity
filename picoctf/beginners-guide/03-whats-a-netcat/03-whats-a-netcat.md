# PicoCTF -- What's a Netcat?

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Connect to a remote server using netcat and retrieve the flag.

---

## Solution

Connected using nc:

    nc fickle-tempest.picoctf.net 61700

The server responded immediately with the flag:

    You're on your way to becoming the net cat master
    picoCTF{nEtCat_Mast3ry_f20a728c}

---

## Concepts Learned

Netcat (nc) is a raw TCP/UDP connection tool. Unlike SSH which provides an encrypted shell session, netcat makes a direct connection to any port on any server. Security researchers use it for:

- Connecting to challenge servers
- Testing open ports
- Setting up listeners
- Debugging network services

The command structure is:

    nc hostname port

---

## Key Takeaway

Netcat is one of the most versatile tools in a security researcher's toolkit. Where SSH is for authenticated shell sessions, netcat is for raw connections. Understanding the difference between the two is foundational for network-level security work.

---

## Flag

picoCTF{nEtCat_Mast3ry_f20a728c}
