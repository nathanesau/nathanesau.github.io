---
layout: projects/rpackages
---

### m4fe

<a href="https://github.com/nathanesau/m4fe"><img src="../../../assets/images/github-button-blue.png" width="250"/></a>

This project implements some models from [Derivatives Markets](http://fac.ksu.edu.sa/sites/default/files/derivatives_markets_3e_0.pdf) by McDonald.

### Brief User Guide

Install the package as shown below:

```R
devtools::install_github("nathanesau/m4fe")
```

The example below calibrates a BDT tree to a set of yields and volatilities.

```R
yields = c(0.10, 0.11, 0.12, 0.125)
volatilities = c(NA, 0.10, 0.15, 0.14) 
rateTree = bdt.tree(yields, volatilities)
print(rateTree)
```

The output is:

```R
[[1]]
[1] 0.1

[[2]]
[1] 0.1322011 0.1082371

[[3]]
[1] 0.20170244 0.13662290 0.09254136

[[4]]
[1] 0.20028379 0.15683226 0.12280753 0.09616446
```

Multivariate Newtons method is used as the underlying solve algorithm. Note that this output matches Figure 25.5 from the Third Edition of Derivatives Markets. For more information on the package, please see the GitHub page.

This page was last updated on Sept 8, 2019.