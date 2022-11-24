# pastclim <img src="./man/figures/logo.png" align="right" alt="" width="150" />

<!-- badges: start -->
[![CircleCI](https://circleci.com/gh/EvolEcolGroup/pastclim/tree/master.svg?style=shield&circle-token=928bdbe8f065e17b22642f66a8b9c13f29f2e3fb)](https://circleci.com/gh/EvolEcolGroup/pastclim/tree/master)
[![codecov](https://codecov.io/gh/EvolEcolGroup/pastclim/branch/master/graph/badge.svg?token=NflUsWlnQR)](https://codecov.io/gh/EvolEcolGroup/pastclim)
<!-- badges: end -->

<!---
comment out the githubactions as they can't cope with downgrading terra
[![R-CMD-check](https://github.com/EvolEcolGroup/pastclim/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/EvolEcolGroup/pastclim/actions/workflows/R-CMD-check.yaml)
--->

This `R` library is designed to provide an easy way to extract and manipulate paleoclimate
reconstructions for ecological and anthropological analyses. 

A paper
describing the functionality of `pastclim` can be found on [bioRxiv](https://www.biorxiv.org/content/10.1101/2022.05.18.492456v1). Please cite it if you
use `pastclim` in your research.

## Install the library

You will need to install the library from Github. For this step, you will need to
use `devtools` (if you haven't done so already, install it from CRAN with `install.packages("devtools")`.
Once you have `devtools`, simply use:
```
devtools::install_github("EvolEcolGroup/pastclim")
```

## Overview of functionality

On its dedicated website [website](https://evolecolgroup.github.io/pastclim), you can find
Articles giving you a step-by-step ([overview of the package](https://evolecolgroup.github.io/pastclim/articles/a0_pastclim_overview.html), and how
to build and use [custom datasets](https://evolecolgroup.github.io/pastclim/articles/a2_custom_datasets.html). There is also a [cheatsheet](https://evolecolgroup.github.io/pastclim/pastclim_cheatsheet.pdf). 

Pastclim currently includes data from Beyer et al 2020, a reconstruction of climate based on the HadCM3 
model for the last 120k years, and Krapp et al 2021, which covers the last 800k years.
The reconstructions are bias-corrected and downscaled to 0.5 degree. More details on these datasets
can be found [here](https://evolecolgroup.github.io/pastclim/articles/a1_available_datasets.html).

You can also build the vignettes when installing 
`pastclim` (note that you will need to have the necessary tools to build vignettes already installed;
requirements depend on your OS):
```
devtools::install_github("EvolEcolGroup/pastclim", build_vignette = TRUE)
```
If you built the vignettes, you can read them directly in R. For example, the overview can be
obtained with:
```
vignette("pastclim_overview", package = "pastclim")
```

---

## Current issues

If something does not work, check the [issues on Github](https://github.com/EvolEcolGroup/pastclim/issues) to see whether the problem
has already been reported. If not, feel free to create an new issue. Please make sure you provide
[a reproducible example](https://stackoverflow.com/questions/5963269/how-to-make-a-great-r-reproducible-example) for the developers to investigate the issue.


### Error in x\$.self\$finalize()

`pastclim` relies on `terra` to process rasters. There is a known bug in
`terra` that leads to the occasional message: 
```
"Error in x$.self$finalize() : attempt to apply non-function"
```
This is an error related to garbage collection, which does not 
affect the script being correctly executed, so it can be ignored. More discussion
of this issue can be found on [stack**overflow**](https://stackoverflow.com/questions/61598340/why-does-rastertopoints-generate-an-error-on-first-call-but-not-second)

---

### terra without NETCDF driver for OSX

A number of versions of `terra` available as binaries for OSX on CRAN (including the latest one) have
been compiled without a NETCDF driver. This prevents `pastclim`, which relies on `terra`, from 
correctly reading files. When loaded, `pastclim` checks if the driver is available; in case of
a missing driver, you will get the error:

```
error: the R library terra currently installed relies on a version of gdal
that does not support reading netcdf files. You will need to reinstall
terra, possibly from source, if there isn't a version with netcdf 
support on CRAN."
```

To install `terra` from source, see instructions [here](https://github.com/rspatial/terra).


