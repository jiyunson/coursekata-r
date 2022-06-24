<!-- README.md is generated from README.Rmd. Please edit that file -->

# coursekata <img src='man/figures/logo.png' align="right" height="138.5" />

<!-- badges: start -->
<!-- [![CRAN status](https://www.r-pkg.org/badges/version/coursekata)](https://CRAN.R-project.org/package=coursekata) -->

[![R build
status](https://github.com/UCLATALL/coursekata-r/workflows/R-CMD-check/badge.svg)](https://github.com/UCLATALL/coursekata-r/actions)
[![codecov](https://codecov.io/gh/uclatall/coursekata-r/branch/main/graph/badge.svg?token=HEenoYyHcn)](https://app.codecov.io/gh/uclatall/coursekata-r)

<!-- badges: end -->

## Overview

_CourseKata Statistics and Data Science_, is an innovative interactive
online textbook for teaching introductory statistics and data science in
colleges, universities, and high schools. Part of CourseKata’s _Better
Book_ Project, we are leveraging research and student data to guide
continuous improvement of online learning resources. The **coursekata**
package is designed to make it easy to install and load the packages,
functions, and data used in the book and supplementary materials.

Learn more about CourseKata and its free services and materials at
[CourseKata.org](https://coursekata.org/).

This package makes it easy to install and load all packages and
functions used in CourseKata courses. It additionally provides a handful
of helper functions and augments some generic functions to provide
cohesion between the network of packages. This package was inspired by
the [tidyverse](https://tidyverse.tidyverse.org) meta-package.

## Installation

```r
# Install the development version from GitHub
# install.packages("remotes")
remotes::install_github("UCLATALL/coursekata-r")
```

Note that installing the package will install all of the functions that
are used in the course, but by default a couple of packages will not be
installed: `fivethirtyeight` and `fivethirtyeightdata`. These packages
only contain data, so the R package building process complains when
functions are not imported from them. The first time you call
`library(coursekata)` you will be prompted to install the packages if
they are not already installed.

## Loading Packages Used in CourseKata Courses

`library(coursekata)` will load these core packages in addition to the
[functions and theme](#functions-and-theme) included in the `coursekata`
package:

```r
library(coursekata)
#> ── CourseKata packages ───────────────────────────────────── coursekata 0.3.3 ──
#> ✔ supernova           2.5.1       ✔ fivethirtyeightdata 0.1.0
#> ✔ mosaic              1.8.3       ✔ Lock5withR          1.2.2
#> ✔ lsr                 0.5.2       ✔ dslabs              0.7.4
#> ✔ fivethirtyeight     0.6.2
```

- [supernova](https://github.com/UCLATALL/supernova), for
  - creating ANOVA tables.
  - tools for extracting information from fitted models (`b0()`,
    `b1()`, `PRE()`, `fVal()`)
  - an augmented `print.lm()` which prints the fitted equation as
    well
  - … and more!
- [mosaic](https://projectmosaic.github.io/mosaic/), for a unified
  interface to most statistical tools.
- [ggformula](https://projectmosaic.github.io/ggformula/), for a
  formula interface to ggplot2.
- [dplyr](https://dplyr.tidyverse.org), for data manipulation.

In addition to useful functions, a great deal of data sets are used by
instructors who teach the course. This package installs these:

- [fivethirtyeight and
  fivethirtyeightdata](https://cran.r-project.org/web/packages/fivethirtyeight/vignettes/fivethirtyeight.html)
- [Lock5withR](https://github.com/rpruim/Lock5withR)
- [dslabs](https://github.com/rafalab/dslabs)

## Functions and Theme

This package also comes with a variety of functions useful for teaching
statistics and data science, and it has an automatically set `ggplot2`
theme complete with colorblind-friendly palettes and other improvements
to aid perception and clarity of plots.

### Estimate Extraction (and Bootstrapping)

Extracting an estimate is as easy as passing a fitted linear model to
one of the extraction functions:

```r
fit <- lm(mpg ~ hp, data = mtcars)

# the estimate for β₀, the intercept
b0(fit)
#> [1] 30.09886

# the estimate for β₁, the slope
b1(fit)
#> [1] -0.06822828

# the proportional reduction in error
PRE(fit)
#> [1] 0.6024373

# Fisher's F value
fVal(fit)
#> [1] 45.4598

# the sum of the squared errors from the model
SSE(fit)
#> [1] 447.6743

# the sum of squares model/regression
SSM(fit)
#> [1] 678.3729
```

The estimate extraction functions help to simplify the ability to create
bootstrapped sampling distributions of those estimates. Here is an
example of bootstrapping the slope:

```r
# use mosaic package to repetitively resample to bootstrap a distribution
samp_dist_of_b1 <- do(1000) * b1(lm(mpg ~ hp, data = resample(mtcars)))

# plot the bootstrapped estimates
gf_histogram(~ samp_dist_of_b1$b1)
```

<img src="man/figures/README-samp_dist_of_b1-1.png" width="100%" />

Other estimates and terms can be bootstrapped using the same technique,
but you will need to calculate the values yourself. Here’s an example of
doing that for a term that doesn’t have a dedicated extraction function:

```r
samp_dist_of_hp <- do(1000) * {
  # create a new model from the resampled data
  model <- lm(mpg ~ disp * hp, data = resample(mtcars))

  # extract the desired estimate, here the coefficient for hp
  coef(model)[["hp"]]
}

# plot the bootstrapped estimates
gf_histogram(~ samp_dist_of_hp$result)
```

<img src="man/figures/README-samp_dist_of_hp-1.png" width="100%" />

### Sectioning a Distribution

When teaching about hypothesis testing, _F_, and _p_-value, it is useful
to mark different portions of a distribution as inside or outside the
critical zone. `middle()`, `upper()`, and `lower()` each take a
distribution of values and return whether the value was in, e.g. the
middle 95% of the distribution. Use this with a plotting function to
shade in those areas:

```r
# shade in the middle 80% of the Thumb distribution
gf_histogram(~Thumb, data = Fingers, fill = ~ middle(Thumb, .80))
```

<img src="man/figures/README-shaded_middle-1.png" width="100%" />

### Toggling the Theme

The `ggplot2` theme is loaded by default but can be toggled on and off
via `load_coursekata_themes()` and `restore_default_themes()`. The
actual plot theme and scale components are also provided for advanced
users as `theme_coursekata()` and `scale_discrete_coursekata()`
(`viridis` is used for continuous color scales).

# Contributing

If you see an issue, problem, or improvement that you think we should
know about, or you think would fit with this package, please let us know
on our [issues page](https://github.com/UCLATALL/supernova/issues).
Alternatively, if you are up for a little coding of your own, submit a
pull request:

1.  Fork it!
2.  Create your feature branch: `git checkout -b my-new-feature`
3.  Commit your changes: `git commit -am 'Add some feature'`
4.  Push to the branch: `git push origin my-new-feature`
5.  Submit a [pull request](https://github.com/UCLATALL/supernova/pulls)
    :D
