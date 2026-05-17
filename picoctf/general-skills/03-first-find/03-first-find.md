# First Find

**Category:** General Skills
**Difficulty:** Easy
**Author:** LT 'syreal' Jones

---

## Challenge

Unzip an archive and find a file named `uber-secret.txt` hidden somewhere inside.

---

## Solution

**Step 1 -- Download and unzip the archive**

```bash
wget https://artifacts.picoctf.net/c/502/files.zip
unzip files.zip
```

**Step 2 -- Find the file**

```bash
find . -name "uber-secret.txt"
```

Output:
./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
The file is buried several directories deep inside a hidden folder (`.secret`).

**Step 3 -- Read the file**

```bash
cat ./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

---

## Flag

`picoCTF{f1nd_15_f457_ab443fd1}`

---

## Key Takeaways

- `find . -name "filename"` searches recursively from the current directory for a file by name
- Hidden directories start with `.` -- they don't appear with a plain `ls` but `find` still searches them
- `find` is faster and more reliable than manually navigating a deep directory tree
