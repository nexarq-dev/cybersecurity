# PicoCTF -- Keygenme-py

**Platform:** PicoCTF / CyLab Security Academy
**Category:** Reverse Engineering
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Reverse engineer a key validation algorithm to generate a valid licence key.

---

## Solution

Downloaded and read the script:

    wget [url]/keygenme-trial.py
    cat keygenme-trial.py

The key structure was visible in the globals:

    key_part_static1_trial = "picoCTF{1n_7h3_kk3y_of_"
    key_part_dynamic1_trial = "xxxxxxxx"
    key_part_static2_trial = "}"

The check_key function revealed the dynamic part was constructed from specific indexes of the SHA256 hash of the username BENNETT:

    if key[i] != hashlib.sha256(username_trial).hexdigest()[4]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[5]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[3]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[6]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[2]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[7]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[1]: return False
    if key[i] != hashlib.sha256(username_trial).hexdigest()[8]: return False

Generated the dynamic part:

    python3 -c "
    import hashlib
    h = hashlib.sha256(b'BENNETT').hexdigest()
    print(h[4]+h[5]+h[3]+h[6]+h[2]+h[7]+h[1]+h[8])
    "
    08c46aa4

Full flag:

    picoCTF{1n_7h3_kk3y_of_08c46aa4}

---

## Concepts Learned

A keygen challenge requires reconstructing a key generation algorithm by reading the validation logic in reverse. The validator tells you exactly what a valid key must look like -- reading it carefully gives you everything needed to generate one.

SHA256 produces a deterministic 64-character hex digest from any input. Given the same input, it always produces the same output. Because the username was fixed and known, the hash was fixed and the key derivation was fully predictable.

---

## Key Takeaway

Licence key validation algorithms are only as secure as their secrecy. If an attacker has access to the validation source code, they can reconstruct the generation logic and produce valid keys for any input. This appears in real software piracy and is why modern licence systems use server-side validation rather than client-side algorithms.

---

## Flag

picoCTF{1n_7h3_kk3y_of_08c46aa4}
