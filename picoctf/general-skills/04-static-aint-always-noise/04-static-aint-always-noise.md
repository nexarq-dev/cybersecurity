# Static ain't always noise

**Category:** General Skills
**Difficulty:** Easy
**Author:** syreal

---

## Challenge

Analyse a binary file and extract the flag from it using a provided bash script.

---

## Solution

**Step 1 -- Download both files**

```bash
wget https://challenge-files.picoctf.net/c_wily_courier/.../static
wget https://challenge-files.picoctf.net/c_wily_courier/.../ltdis.sh
```

**Step 2 -- Read the script**

```bash
cat ltdis.sh
```

The script does two things:
- Disassembles the binary using `objdump -Dj .text`
- Extracts all strings from the binary using `strings -a -t x`

**Step 3 -- Run the script**

```bash
chmod +x ltdis.sh
./ltdis.sh static
```

This produces two files:
- `static.ltdis.x86_64.txt` -- disassembly
- `static.ltdis.strings.txt` -- all strings with file offsets

**Step 4 -- Search for the flag**

```bash
grep "picoCTF" static.ltdis.strings.txt
```

Output:
3020 picoCTF{d15a5m_t34s3r_20335e41}
---

## Flag

`picoCTF{d15a5m_t34s3r_20335e41}`

---

## Key Takeaways

- `strings` extracts all human-readable strings from a binary file
- `strings -a -t x` includes all sections and prints file offsets in hex
- `grep` filters output for a specific pattern -- use it to find flags quickly
- Binaries often contain embedded strings including flags, version info, and debug messages
- `objdump` disassembles a binary into assembly instructions -- useful for reverse engineering
