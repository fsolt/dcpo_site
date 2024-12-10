---
categories:
- howto
title: How can I use the SGR data to make my own graphs?
---

The [SGR download](../../../sgr_downloads.qmd) contains files pre-formatted for use with the tools for analyzing multiply-imputed data and other data measured with uncertainty in Stata (e.g., `sgr1_0.dta`) or R (e.g., `sgr1_0.rda`). This is meant to "set the default" in a way that encourages researchers to take into account the uncertainty in the SGR estimates.  This uncertainty is considerable in many countries, and the tools available in both software packages can now handle pretty much any analysis one may desire (for details, read the documents `R_sgr.pdf` and `stata_sgr.pdf` in the SGR download). But this format does not lend itself to graphing.  For this purpose, use the summary file (e.g., `sgr1_0_summary.csv`), which presents the SGR estimates in mean-plus-standard-error summary format.

In Stata:

```
import delimited "sgr1_0_summary.csv", clear

// A silly example
gen name_length = length(country)
gen first_letter = substr(country, 1, 1)
keep if year==2010 & first_letter=="S" /*2010 for Senegal, Serbia, . . .*/

// A scatterplot with 95% uncertainty intervals
twoway rspike p2_5 p97_5 name_length, lstyle(ci) || ///
    scatter sgr name_length, msize(small) ///
    legend(order(2 "SGR: Support for Gay Rights")) 
```

In R: 

```R
llibrary(tidyverse)

# Load the SGR
load("sgr1_0.rda")

# Plot PGE estimates for the United States
sgr_summary %>% 
    filter(country == "United States") %>% 
    ggplot(aes(x=year, y=sgr)) + 
    geom_line() +
    geom_ribbon(aes(ymin = sgr-1.96*sgr_se,
                    ymax = sgr+1.96*sgr_se, 
                    linetype=NA), alpha = .25) +
    scale_x_continuous(breaks=seq(1970, 2020, 5)) +
    theme_bw() + 
    labs(x = "Year", 
         y = "SGR: Support for Gay Rights",
         title = "Support for Gay Rights in the United States")
```
      
