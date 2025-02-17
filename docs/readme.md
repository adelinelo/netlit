# Replication files 

This document is available online at https://judgelord.github.io/netlit/readme

All of the data and code required to reproduce the figures in the body and supplements are available on the github repository for the `netlit` package ([github.com/judgelord/netlit](https://judgelord.github.io/netlit/)) as described below. 
Clone a copy of all replication data and code on the command line with: 

```git clone github.com/judgelord/netlit```

The package will soon be on CRAN. Until then, install the package in R: 

```devtools::install_github("judgelord/netlit")```

Because live package vignettes may change in the future, we have archived submission versions of the data in `/replication_data/` and submission versions of the vignettes in `/docs/`. 

---

## Body text

Figures 2 and 3 are generated by the main [netlit vignette](https://judgelord.github.io/netlit/articles/netlit.html), with the submission version archived as [netlit-replication.Rmd](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication.Rmd). 

- **data:** [/replication_data/](https://github.com/judgelord/netlit/tree/main/replication_data)
   - /replication_data/literature.rda 
   - /replication_data/node_attributes.rda
 
- **code:** /docs/netlit-replication.Rmd
  - live: https://judgelord.github.io/netlit/netlit-replication
  - raw: https://github.com/judgelord/netlit/blob/main/docs/netlit-replication.Rmd

- **output figures:** [/docs/netlit-replication_files/figure-html/](https://github.com/judgelord/netlit/tree/main/docs/netlit-replication_files/figure-html)
  - Figure 2: [ggraph-1.png](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication_files/figure-html/ggraph-1.png) and [figure2.pdf](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication_files/figure-html/figure2.pdf)
  - Figure 3a: [ggraph-subset1.png](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication_files/figure-html/ggraph-subset-1.png) or [figure3a.pdf](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication_files/figure-html/figure3a.pdf)
  - Figure 3b: [ggraph-subset2.png](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication_files/figure-html/ggraph-subset-2.png) or [figure3b.pdf](https://github.com/judgelord/netlit/blob/main/docs/netlit-replication_files/figure-html/figure3b.pdf)

***Note: The body of the paper includes hand-cropped versions of Figures 3a and 3b that focus on the key part of the network.**
  
---

## Supplements

### Simulating Biased Literature Reviews Supplement

All the figures in the **Simulating Biased Literature Reviews Supplement** are created by /docs/vignette-bias.Rmd

- **data:** [/replication_data/](https://github.com/judgelord/netlit/tree/main/replication_data)
  - /replication_data/literature.rda
  - /replication_data/literature_metadata.rda
  
- **code:** /docs/vignette-bias.Rmd
   - live: https://judgelord.github.io/netlit/vignette-bias
   - raw: https://github.com/judgelord/netlit/blob/main/docs/vignette-bias.Rmd

- **output figures:** [/docs/vignette-bias_files/figure-html/](https://github.com/judgelord/netlit/tree/main/docs/vignette-bias_files/figure-html)

---

### Applied Researcher Experiment Supplement

All the figures in the **Applied Researcher Experiment Supplement** are created by /docs/vignette-IR.Rmd

- **data:** [/replication_data/](https://github.com/judgelord/netlit/tree/main/replication_data) 
   - /replication_data/IR_evaluations.rda
   - /replication_data/IR_original_networks.rda

- **code:** /docs/vignette-IR.Rmd
  - live: https://judgelord.github.io/netlit/vignette-IR
  - raw: https://github.com/judgelord/netlit/blob/main/docs/vignette-IR.Rmd

- **output figures:** [/docs/vignette-IR_files/figure-html/](https://github.com/judgelord/netlit/tree/main/docs/vignette-IR_files/figure-html)

