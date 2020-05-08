# manage_frac

`manage_frac` is an R function to calculate the management fraction of employment in a population of firms.  It is based on a model first proposed by Herbert Simon (see reference below). In this model, firms are hierarchically organized with a fixed 'span of control'. This means that each superior commands the same number of subordinates, with the number of subordinates equal to the span of control. See Simon's paper for more details:

* Simon, H. A. (1957). The compensation of executives. Sociometry, 20(1), 32-35.

Managers are defined as all individuals in and above some arbitrary hierarchical rank *n*, where *n* is you choice of integer.

### Inputs

* `firm_vec` = a vector of firm sizes (number of members in the firm)
* `span` =  the span of control in the firms (number of subordinates controlled by each superior). `span` must be greater than 1.
* `manage_rank_thresh` = the rank in and above which all individuals are classified as managers.

### Output
`manage_frac` a decimal indicating the management fraction of employment


### Example:

```R
library(RcppArmadillo)
library(Rcpp)

sourceCpp("manage_frac.cpp")

# vector of firm sizes (number of employees)
firm_vec = c(1, 1, 2, 5, 10, 100)

# span of control in each firm
span = 3

# hierarchical rank defining managers
manage_rank_thresh = 3

# management fraction
manager_frac(firm_vec, span, manage_rank_thresh)

[1] 0.07563025
```

For a given size distribution of firms, a greater span of control increase the number of managers. Conversely, a greater management rank threshold decreases the number of managers. 

For an application of the model (and an explanation of the underlying math) see this paper and the accompanying appendix:

* Fix, B. (2017). [Energy and institution size](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0171823). PloS one, 12(2).



### Installation
To use `manage_frac`, install the following R packages:
 * [Rcpp](https://cran.r-project.org/web/packages/Rcpp/index.html) 
 * [RcppArmadillo](https://cran.r-project.org/web/packages/RcppArmadillo/index.html) 

Put the source code (`hierarchy_fix_span.h` and `manage_frac.cpp`) in the directory of your R script. Then source it with the command `sourceCpp('manage_frac.cpp')`.








