---
title: Insert missing periods into python docstrings using regex
date: 2025-08-08
draft: false
---

The first line of python docstrings is meant to always end with a period: [PEP 257](https://peps.python.org/pep-0257/)

As I only learned of this recently I tried to fix it in my existing code.
Tools like ruff can do that partially for function and class docstrings, but I also regularly use attribute docstrings.

Therefore I used a vim regex:

```:%s/^\(\s*\)"""\(\(\s*[^."]\+\)\+\)\("""\)\?\s*$/\1"""\2.\4/g```

