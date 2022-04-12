---
title: Latex beamer with enumitem
date: 2022-04-12 17:37
draft: false
tags: ['tex', 'beamer', 'presentation', 'latex', 'enumerate']
---

It is not recommended to use the `enumitem` package with a `beamer` document class in TeX.
When trying without any further ado (just `\usepackage{enumitem}`) in a beamer document it will result in an error: `! TeX capacity exceeded, sorry [grouping levels=255].`

The reason is that `enumitem` assums that the document class defines the `\labelenumi` command, but `beamer` doesn't!
Manually defining it is not recommended: the `beamer` class (re-)defines the commands and environments, loading `enumitem` would then result in these being overwritten.
[This stackoverflow answer](https://tex.stackexchange.com/a/31524) provides a fix, but the generel consensus is to better not use `enumitem` if one doesn't strictly need it.
