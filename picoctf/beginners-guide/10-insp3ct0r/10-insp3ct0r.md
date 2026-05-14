# PicoCTF -- Insp3ct0r

**Platform:** PicoCTF / CyLab Security Academy
**Category:** Web Exploitation
**Difficulty:** Easy
**Status:** Completed

---

## Objective

Find a flag split across three parts hidden in the HTML, CSS, and JavaScript source of a web page.

---

## Solution

Opened the challenge URL in the browser and used developer tools (F12) to inspect the source.

Part 1 found in HTML comment:

    <!-- Html is neat. Anyways have 1/3 of the flag: picoCTF{tru3_d3 -->

Part 2 found in CSS file (mycss.css):

    /* You need CSS to make pretty pages. Here's part 2/3 of the flag: t3ct1ve_0r_ju5t */

Part 3 found in JavaScript file (myjs.js):

    /* Javascript sure is neat. Anyways part 3/3 of the flag: _lucky?302945a7} */

Full flag assembled:

    picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?302945a7}

---

## Concepts Learned

Web pages are built from three layers -- HTML (structure), CSS (styling), and JavaScript (behaviour). Developers sometimes accidentally leave sensitive information in comments across all three files. Browser developer tools give full access to all three layers without needing any special software.

The Sources tab in developer tools lists all files loaded by the page. Clicking each file reveals its full contents including comments that are not visible in the rendered page.

---

## Key Takeaway

Inspecting page source is one of the first steps in web application security assessment. Comments, hidden fields, and disabled UI elements often contain information the developer did not intend to expose publicly.

---

## Flag

picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?302945a7}
