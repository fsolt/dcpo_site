---
categories:
- howto
title: How can I use the PGE data to make my own graphs?
---

The [PGE download](../../../pge_downloads.qmd) contains files pre-formatted for use with the tools for analyzing multiply-imputed data and other data measured with uncertainty in Stata (e.g., `pge1_0.dta`) or R (e.g., `pge1_0.rda`). This is meant to "set the default" in a way that encourages researchers to take into account the uncertainty in the PGE estimates.  This uncertainty is considerable in many countries, and the tools available in both software packages can now handle pretty much any analysis one may desire (for details, read the documents `R_pge.pdf` and `stata_pge.pdf` in the PGE download). But this format does not lend itself to graphing.  For this purpose, use the summary file (e.g., `pge1_0_summary.csv`), which presents the PGE estimates in mean-plus-standard-error summary format.

In Stata:

```
import delimited "pge1_0_summary.csv", clear

// A silly example
gen name_length = length(country)
gen first_letter = substr(country, 1, 1)
keep if year==2010 & first_letter=="S" /*2010 for Senegal, Serbia, . . .*/

// A scatterplot with 95% uncertainty intervals
twoway rspike p2_5 p97_5 name_length, lstyle(ci) || ///
    scatter pge name_length, msize(small) ///
    legend(order(2 "PGE Public Gender Equality")) 
```

In R: 

```R
llibrary(tidyverse)

# Load the PGE
load("pge1_0.rda")

# Plot PGE estimates for the United States
pge_summary %>% 
    filter(country == "United States") %>% 
    ggplot(aes(x=year, y=pge)) + 
    geom_line() +
    geom_ribbon(aes(ymin = pge-1.96*pge_se,
                    ymax = pge+1.96*pge_se, 
                    linetype=NA), alpha = .25) +
    scale_x_continuous(breaks=seq(1970, 2020, 5)) +
    theme_bw() + 
    labs(x = "Year", 
         y = "PGE: Public Gender Egalitarianism",
         title = "Public gender egalitarianism in the United States")
```
      
