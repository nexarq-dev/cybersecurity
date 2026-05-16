# Nice netcat...

**Category:** General Skills
**Difficulty:** Easy
**Points:** 15
**Author:** syreal

---

## Challenge

Connect to a server using netcat and retrieve the flag.

nc wily-courier.picoctf.net 59982
---

## What the Server Returns

A list of decimal numbers, one per line:
112
105
99
111
Each number is an ASCII decimal value representing a character.

---

## Manual Approach

Using the ASCII anchor points:
- 48 = 0
- 65 = A
- 97 = a

Count up from the nearest anchor to find each character. For example:
- 112 = 97(a) + 15 = p
- 105 = 97(a) + 8 = i
- 99 = 97(a) + 2 = c
- 111 = 97(a) + 14 = o

---

## Solution

Pipe the netcat output directly through Python to convert all decimal values to ASCII in one step:

```bash
nc -w 2 wily-courier.picoctf.net 53619 | python3 -c "import sys; print(''.join(chr(int(n)) for n in sys.stdin.read().split()))"
```

**How it works:**
- `nc -w 2` connects and closes after 2 seconds of inactivity
- `|` pipes the output to Python
- `sys.stdin.read().split()` splits the numbers into a list
- `chr(int(n))` converts each decimal number to its ASCII character
- `''.join(...)` joins all characters into one string

---

## Flag

`picoCTF{g00d_k1tty!_n1c3_k1tty!_a94e7}`

---

## Key Takeaway

When a server returns a list of decimal numbers, they are almost always ASCII values. Pipe directly through Python's `chr()` function rather than converting manually.
