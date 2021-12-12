
<!-- README.md is generated from README.Rmd. Please edit that file -->

# coursekata <img src='man/figures/logo.png' align="right" height="138.5" />

<!-- badges: start -->
<!-- [![CRAN status](https://www.r-pkg.org/badges/version/coursekata)](https://CRAN.R-project.org/package=coursekata) -->

[![R build
status](https://github.com/UCLATALL/coursekata-r/workflows/R-CMD-check/badge.svg)](https://github.com/UCLATALL/coursekata-r/actions)
[![codecov](https://codecov.io/gh/uclatall/coursekata-r/branch/main/graph/badge.svg?token=HEenoYyHcn)](https://app.codecov.io/gh/uclatall/coursekata-r)
<!-- badges: end -->

## Overview

*CourseKata Statistics and Data Science*, is an innovative interactive
online textbook for teaching introductory statistics and data science in
colleges, universities, and high schools. Part of CourseKata’s *Better
Book* Project, we are leveraging research and student data to guide
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

``` r
# Install the development version from GitHub
# install.packages("remotes")
remotes::install_github("UCLATALL/coursekata-r")
```

## Usage

`library(coursekata)` will load these core packages, including the
functions and themes included in this package:

``` r
library(coursekata)
#> 
#> ── CourseKata course packages ──────────────────────────────────────────────────
#> ✓ supernova           2.4.4       ✓ fivethirtyeightdata 0.1.0
#> ✓ mosaic              1.8.3       ✓ Lock5withR          1.2.2
#> ✓ lsr                 0.5.2       ✓ dslabs              0.7.4
#> ✓ fivethirtyeight     0.6.2
#> 
#> Attaching package: 'coursekata'
#> The following objects are masked _by_ 'package:supernova':
#> 
#>     b0, b1, f, fVal, pre, PRE, sse, SSE, ssm, SSM, ssr, SSR
```

-   [coursekata](https://github.com/UCLATALL/coursekata_core), for
    various helpers like
    -   `middle()`, `upper()`, and `lower()` to facilitate shading
        proportions of plots
    -   tools for extracting information from fitted models (`b0()`,
        `b1()`, `PRE()`, `fVal()`)
    -   an automatically set `ggplot2` theme complete with
        colorblind-friendly palettes and other improvements to aid
        perception and clarity of plots. These are loaded by default but
        can be toggled on and off via `load_coursekata_themes()` and
        `restore_default_themes()`. The actual plot theme and scale
        components are also provided for advanced users as
        `theme_coursekata()` and `scale_discrete_coursekata()`
        (`viridis` is used for continuous color scales).
-   [supernova](https://github.com/UCLATALL/supernova), for
    -   creating ANOVA tables.
    -   an augmented `print.lm()` which prints the fitted equation as
        well
    -   … and more!
-   [mosaic](https://projectmosaic.github.io/mosaic/), for a unified
    interface to most statistical tools.
-   [ggformula](https://projectmosaic.github.io/ggformula/), for a
    formula interface to ggplot2.
-   [dplyr](https://dplyr.tidyverse.org), for data manipulation.

In addition to useful functions, a great deal of data sets are used by
instructors who teach the course. This package installs these:

-   [fivethirtyeight and
    fivethirtyeightdata](https://cran.r-project.org/web/packages/fivethirtyeight/vignettes/fivethirtyeight.html)
-   [Lock5withR](https://github.com/rpruim/Lock5withR)
-   [dslabs](https://github.com/rafalab/dslabs)

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
