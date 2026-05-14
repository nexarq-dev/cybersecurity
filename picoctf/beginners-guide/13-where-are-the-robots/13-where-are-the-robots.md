# PicoCTF -- Where are the Robots

**Platform:** PicoCTF / CyLab Security Academy
**Category:** Web Exploitation
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find the flag hidden in a page listed in the site's robots.txt file.

---

## Solution

Navigated to the robots.txt file of the challenge site:

    http://fickle-tempest.picoctf.net:58028/robots.txt

Contents:

    User-agent: *
    Disallow: /cc6b1.html

Navigated directly to the disallowed page:

    http://fickle-tempest.picoctf.net:58028/cc6b1.html

The flag was displayed on the page:

    picoCTF{ca1cu1at1ng_Mach1n3s_cc6b1}

---

## Concepts Learned

robots.txt is a file that websites use to tell search engine crawlers which pages not to index. It is publicly readable by anyone. Security researchers always check it during web reconnaissance because developers sometimes list sensitive or hidden pages there -- ironically making them easy to find.

The Disallow directive tells crawlers not to visit a path. It does not restrict human access -- any browser can navigate directly to a disallowed URL.

---

## Key Takeaway

robots.txt is one of the first files checked during web application reconnaissance. Pages listed as Disallow are often administrative interfaces, backup files, staging environments, or other sensitive content the developer wanted to hide from search engines but not actually protect. Always check it.

---

## Flag

picoCTF{ca1cu1at1ng_Mach1n3s_cc6b1}
