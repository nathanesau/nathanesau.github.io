---
layout: projects/rpackages
---

### Makehams

<a href="https://github.com/nathanesau/makehams"><img src="../../../assets/images/github-button-blue.png" width="250"/></a>

This project was created to re-produce life tables show in [Actuarial Mathematics for Life Contingent Risks](https://www.amazon.ca/Actuarial-Mathematics-Life-Contingent-Risks/dp/1107044073). A PDF of the textbook can be found [here](https://fac.ksu.edu.sa/sites/default/files/actuarial-mathematics-for-life-contingent-risks.pdf).

### Brief User Guide

The model used is from Example 3.13 in the textbook. Assume that the force of mortality follows Makeham's law $u_{x} = A + Bc^{x}$. First, install the package with 

```R
devtools::install_github("nathanesau/makehams")
```

Then, load the package in ``R`` with 

```R
library(makehams)

makehams(A=0.00022, B=2.7e-06, c=1.124, w=131, radix=1e+05)
head(createLifeTable(x=20))

#x   l[x]+0   l[x]+1      lx+2 x+2
#1 NA       NA       NA 100000.00  20
#2 NA       NA       NA  99975.04  21
#3 20 99995.08 99973.75  99949.71  22
#4 21 99970.04 99948.40  99923.98  23
#5 22 99944.63 99922.65  99897.79  24
#6 23 99918.81 99896.43  99871.08  25
```

This matches the textbook calculations. For more information, please see the GitHub page.

This page was last updatd on Sept 7, 2019.