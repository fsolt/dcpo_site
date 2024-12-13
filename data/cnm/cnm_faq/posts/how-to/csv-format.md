---
categories:
- howto
title: I imported the cnm_summary.csv file, and the data for some countries seem to be greater than one, when the CNM supposedly ranges only from zero to one. How can I interpret these data?
---

The issue here is that the cnm_summary.csv file is saved using [RFC 4180 csv conventions](https://en.wikipedia.org/wiki/Comma-separated_values), that is, with a dot marking the decimal and a comma separating values.  If you are in a locale that observes different conventions---many countries use commas to indicate the decimal and semicolons to separate values---your software's default settings may not read the data correctly.  Be sure to specify the decimal marker and value delimiter appropriately when loading the file: all CNM values fall between zero and one. 
