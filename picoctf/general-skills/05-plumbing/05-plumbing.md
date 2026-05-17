# Plumbing

**Category:** General Skills
**Difficulty:** Medium
**Author:** Alex Fulton/Danny Tunitis

---

## Challenge

A program outputs a large amount of data over netcat. Find the flag hidden somewhere in the output.

---

## Solution

The server sends a large stream of output. Scrolling through it manually is impractical. Instead pipe the output directly to `grep` to filter for the flag format:

```bash
nc fickle-tempest.picoctf.net 49418 | grep "picoCTF"
```

**How it works:**
- `nc` connects to the server and receives the output stream
- `|` pipes that output to `grep`
- `grep "picoCTF"` filters and prints only lines containing the flag format

---

## Flag

`picoCTF{digital_plumb3r_A01Bc3eC}`

---

## Key Takeaways

- The `|` pipe operator passes the output of one command as input to another
- `grep` filters lines matching a pattern -- essential for finding flags in large output streams
- You never need to save data to a file just to search it -- pipe directly
- This pattern (`command | grep "pattern"`) is one of the most used in CTF general skills challenges
