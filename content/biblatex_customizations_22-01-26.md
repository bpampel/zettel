---
title: biblatex_customizations
date: 2022-01-26 19:55
draft: false
tags: ["latex", "biblatex", "bibliography"]
---

## Biblatex: citenum command, papers under preparation, and no ISBN/ISSN if DOI present

For my PhD thesis I used biblatex with the biber backend to generate the citations and bibliography automatically in the "numeric" style.

I encountered three small problems:
1. The \citenum command from natbib (to have in-text citations like `In Ref. 3`) does not exist in biblatex
2. The bibliography style for @article prefixes the journal title with "In: ", but I have some papers under preparation that do not have a journal title set.
3. Because I generated most of the bib entries automatically with zotero, often both ISBN/ISSN and DOI are set. I don't want to lengthen the bibliography entries by including both, but by default you can only remove the identifiers unconditionally.


### adding a citenum command

A simple implementation of the \citenum command is found in [this StackExchange answer](https://tex.stackexchange.com/a/249123):

    \DeclareCiteCommand{\citenum}%
      {\usebibmacro{cite:init}%
       \usebibmacro{prenote}}
      {\usebibmacro{citeindex}%
       \usebibmacro{cite:comp}}
      {}
      {\usebibmacro{cite:dump}%
       \usebibmacro{postnote}}


### Removing the "In :" prefix for papers under preparation

The numeric biblatex style for @article entries looks like this (simplified):

  > First1 Last1, First2 Last2, and First3 Last3. “Title of paper.” In: *Jornal title* vol.issue (year)

I had some papers that were under preparation at the time of finishing the thesis that I wanted to include nevertheless.
Using a @article entry without journal information and `date = {under preparation}` does not work out of the box: the prefix `In: ` is added even if no journal title is set.

To remove it, the `in:` command is modified:

    \renewbibmacro*{in:}{
      \iffieldundef{journaltitle}
        {}
        {\bibstring{in}\printunit{\intitlepunct}}
    }


### Show ISBN/ISSN only if DOI is not set

    \AtEveryBibitem{
      \iffieldundef{doi}
        {}
        {\clearfield{issn}%
         \clearfield{isbn}}%
    }
