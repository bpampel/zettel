---
title: Running difference in gnuplot
date: 2021-04-12 12:54
draft: false
tags: ["awk" "gnuplot" "difference" "columns"]
---

## Problem

I wanted to plot some statistics with gnuplot.
The program puts out the _total_ statistics over time, not just the new ones since the last write.
So to get the statistics for in between the writes I needed to calculate the differences between the current value and the previous one on the fly.

There is an [example for plotting running averages with gnuplot](http://gnuplot.sourceforge.net/demo/running_avg.html) in their demos which I thought I could easily adapt.

Sadly this doesn't work for plotting multiple running differences as this reuses the old variables and I found no way to reinitialize within a `plot for [x in y]` loop.


## Solution

Instead I opted to let awk do the calculations and plot the results on the fly.

The following command does what I want (choosing the 2nd column, ignoring lines starting with '#'):

```
  awk '/^[^#]/ {print $2-a}{a=$2}' filename
```


So I put these into two gnuplot function (for a single and two columns, because I also want to calculate ratios):

```
  running_diff(filename, col) = sprintf("< awk '/^[^#]/ {print $1,$%d-a}{a=$%d}' %s", col, col, filename)
  running_diff_2col(filename, col1, col2) = sprintf("< awk '/^[^#]/ {print $1,$%d-a,$%d-b}{a=$%d;b=$%b}' %s", col1, col2, col1, col2, filename)
```
