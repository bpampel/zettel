---
title: inkscape_embedded_image_transparency
date: 2021-12-10 12:07
---

When using inkscape to edit pdf files that have embedded images, the exported pdf sometimes does not render the embedded image anymore.

Personally, I encountered this when plotting 2D plots with gnuplot via pdfcairo.
Importing them into an inkscape drawing worked fine, but when exporting to pdf again, the 2D images were simply not shown.

Saving to inkscape svg and then converting via rsvg-convert solves the issue!

    rsvg-convert -f pdf input.svg > output.pdf
