# PicoCTF -- Enhance

**Platform:** PicoCTF / CyLab Security Academy
**Category:** Forensics
**Difficulty:** Medium
**Status:** Completed

---

## Objective

Find the flag hidden inside an SVG image file.

---

## Solution

Downloaded the file:

    wget [url]/drawing.flag.svg

Read the raw file contents:

    cat drawing.flag.svg

Found flag characters split across multiple tspan elements with font size 0.00352781px -- invisible when rendered but present in the XML:

    <tspan>p </tspan>
    <tspan>i </tspan>
    <tspan>c </tspan>
    <tspan>o </tspan>
    <tspan>C </tspan>
    <tspan>T </tspan>
    <tspan>F{3nh4n</tspan>
    <tspan>c3d_aab729dd}</tspan>

Assembled the flag:

    picoCTF{3nh4nc3d_aab729dd}

---

## Concepts Learned

SVG files are XML text files, not binary image formats. Any text editor or the cat command reveals the full file contents including hidden elements. Data can be hidden in SVG files by setting text colour to match the background, scaling text to microscopic size, setting opacity to zero, or placing elements outside the visible viewport.

In forensics, always read the raw file rather than just viewing the rendered output. The rendered image showed nothing. The raw XML contained the flag.

---

## Key Takeaway

File formats that are text-based -- SVG, HTML, XML, JSON, CSS -- can hide data in plain sight within their structure. Rendering hides the data visually but cat, strings, or a text editor reveals everything. In real forensic investigations, examining raw file contents rather than relying on application rendering is standard practice.

---

## Flag

picoCTF{3nh4nc3d_aab729dd}
