---
categories:
- howto
title: How can I merge my other data into the PGE using ISO or other country codes?
---

First, add whatever country codes are needed to the PGE data: there are routines for both Stata ([kountry](http://www.stata-journal.com/article.html?article=dm0038); type `findit kountry` in Stata’s command window to install) and R ([countrycode](http://cran.r-project.org/web/packages/countrycode/countrycode.pdf), on CRAN) to generate many commonly used country codes. Then follow the instructions for merging data into the PGE found in the "stata_pge.pdf" or "R_pge.pdf" files included in the data download.
