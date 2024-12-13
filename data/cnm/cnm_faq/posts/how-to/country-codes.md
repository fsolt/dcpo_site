---
categories:
- howto
title: How can I merge my other data into the CNM using ISO or other country codes?
---

First, add whatever country codes are needed to the CNM data: there are routines for both Stata ([kountry](http://www.stata-journal.com/article.html?article=dm0038); type `findit kountry` in Stata’s command window to install) and R ([countrycode](http://cran.r-project.org/web/packages/countrycode/countrycode.pdf), on CRAN) to generate many commonly used country codes. Then follow the instructions for merging data into the CNM found in the "stata_cnm.pdf" or "R_cnm.pdf" files included in the data download.
