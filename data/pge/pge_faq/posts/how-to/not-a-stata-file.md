---
categories:
- howto
title: I'm using an older version of Stata, and it won’t open the file. How can I
  use the PGE data?
---

Stata 13 introduced a new file format which older versions of Stata can’t open. Fortunately, there’s an easy fix: the `use13` command. In the command window, first type `ssc install use13` to install it. Then you can type `use13 pge1_0.dta, clear` (change the version number as necessary, ofc) to load the PGE data.
