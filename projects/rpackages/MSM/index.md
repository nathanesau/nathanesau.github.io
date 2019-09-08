---
layout: projects/rpackages
---

### MSM

<a href="https://github.com/nathanesau/MSM"><img src="../../../assets/images/github-button-blue.png" width="250"/></a>

This project was created to re-produce results related to multiple state models in [Actuarial Mathematics for Life Contingent Risks](https://www.amazon.ca/Actuarial-Mathematics-Life-Contingent-Risks/dp/1107044073). A PDF of the textbook can be found [here](https://fac.ksu.edu.sa/sites/default/files/actuarial-mathematics-for-life-contingent-risks.pdf).

### Brief User Guide

First install the package as shown below:

```R
devtools::install_github("nathanesau/MSM")
```

The example below uses the model from Exercise 8.7 of the textbook (2nd edition). There are 4 states (healthy, sick, dead and critical ill). The transition intensities are:

$$\mu_{x}^{01} = a_{1} + b_{1} e^{c_{1} * x}$$
$$\mu_{x}^{02} = a_{2} + b_{2} e^{c_{2} * x}$$
$$\mu_{x}^{12} = \mu_{x}^{02}$$
$$\mu_{x}^{10} = 0.1\mu_{x}^{01}$$
$$\mu_{x}^{03} = 0.05\mu_{x}^{01}$$
$$\mu_{x}^{13} = \mu_{x}^{03}$$

where $a_{1} = 4e-04$, $b_{1} = 3.5e-06$, $c_{1} = 0.14$, $a_{2} = 5e-04$, $b_{2} = 7.6e-05$, $c_{2} = 0.09$.

To calculate ${}_{t}p_{30}^{00}$ for $t = 0, 1/12, 2/12, ...$ the code below can be used:

```R
library(MSM)

mod_dm <- new("msm", name="Modified disability model",
              states = c("Healthy", "Sick", "Permanently disabled", "Dead"),
              Qxt = Qxt.diag(matrix(nrow=4, ncol=4, data=c(
                  uxt00 = function(t=0, x=0)0
                , uxt01 = function(t=0, x=0) 0.0068*t^0
                , uxt02 = function(t=0, x=0) 0.05 * 0.0068*t^0
                , uxt03 = function(t=0, x=0, a=5e-04, b=7.6e-05, c=0.09) a + b*exp(c*(x+t))
                , uxt10 = function(t=0, x=0) 0.1 * 0.0068 * t^0
                , uxt11 = function(t=0, x=0) 0
                , uxt12 = function(t=0, x=0) 0.05 * 0.0068*t^0
                , uxt13 = function(t=0, x=0, a=5e-04, b=7.6e-05, c=0.09) a + b*exp(c*(x+t))
                , uxt20 = function(t=0, x=0) 0 * t
                , uxt21 = function(t=0, x=0) 0 * t
                , uxt22 = function(t=0, x=0) 0
                , uxt23 = function(t=0, x=0, a=5e-04, b=7.6e-05, c=0.09) 1.2*(a + b*exp(c*(x+t)))
                , uxt30 = function(t=0, x=0) 0 * t
                , uxt31 = function(t=0, x=0) 0 * t 
                , uxt32 = function(t=0, x=0) 0 * t
                , uxt33 = function(t=0, x=0) 0))))

print(mod_dm)
```

This gives the following output:

```
Name     =  Modified disability model 
States   =  [0] Healthy [1] Sick [2] Permanently disabled [3] Dead 
Qx+t     = -vx+t1   ux+t01  ux+t02  ux+t03  
            ux+t10 -vx+t2   ux+t12  ux+t13  
            ux+t20  ux+t21 -vx+t3   ux+t23  
            ux+t30  ux+t31  ux+t32 -vx+t4   
-vx+t1  
 ux+t01  = 0.0068 * t^0
 ux+t02  = 0.05 * 0.0068 * t^0
 ux+t03  = a + b * exp(c * (x + t))
 ux+t10  = 0.1 * 0.0068 * t^0
-vx+t2  
 ux+t12  = 0.05 * 0.0068 * t^0
 ux+t13  = a + b * exp(c * (x + t))
 ux+t20  = 0 * t
 ux+t21  = 0 * t
-vx+t3  
 ux+t23  = 1.2 * (a + b * exp(c * (x + t)))
 ux+t30  = 0 * t
 ux+t31  = 0 * t
 ux+t32  = 0 * t
-vx+t4 
```

Then calculate the probabilities:

```R
# obtain probabilities using kolmogorov's forward equations
P10 <- tPx(object=mod_dm, t=10, x=30, h=1/12, all=TRUE)
t <- c(0, 1/12, 2/12, 5, 9+11/12)

for(e in t) {
  index = e * 12 + 1
  cat(format(round(e, 3), nsmall=3), "p30_00: ", format(round(P10[[index]][1,1], 5), nsmall=5))
}
```

Which gives the following output:

```
0.000p30_00: 1.00000
0.083p30_00: 0.99927
0.167p30_00: 0.99854
5.000p30_00: 0.95574
9.917p30_00: 0.91064
```

The ``tPx`` function and ``msm`` class shown in the demo are just two of the examples of what the package can do. For more info, please see the GitHub repository for this project.

This page was last updated on Sept 7, 2019.
