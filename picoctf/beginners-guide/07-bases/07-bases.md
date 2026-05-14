# PicoCTF -- Bases

**Platform:** PicoCTF / CyLab Security Academy
**Category:** General Skills
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Decode a base64-encoded string to find the flag.

---

## Solution

The encoded string was:

    bDNhcm5fdGgzX3IwcDM1

Decoded using base64:

    echo "bDNhcm5fdGgzX3IwcDM1" | base64 -d
    l3arn_th3_r0p35

Flag:

    picoCTF{l3arn_th3_r0p35}

---

## Concepts Learned

Base64 encodes binary data as printable ASCII text using 64 characters (A-Z, a-z, 0-9, +, /). It is not encryption -- it provides no security. It is used to safely transmit binary data over text-based protocols.

Base64 appears constantly in real security work:

- JWT tokens are base64-encoded
- Email attachments use base64 encoding
- Web attack payloads are often base64-encoded to bypass filters
- On-chain calldata sometimes uses base64 encoding

The base64 -d flag decodes. Without -d it encodes.

In CyberChef, the From Base64 operation decodes base64 strings instantly.

---

## Key Takeaway

Recognising base64 on sight is an important skill. Base64 strings typically end with = or == padding characters and use only alphanumeric characters plus + and /. Any time you see a string matching this pattern in a CTF or real investigation, try base64 decoding it first.

---

## Flag

picoCTF{l3arn_th3_r0p35}
