* [Latest updates](#latest-updates)
* [Short video introduction](#short-video-introduction)
* [Helpfile examples](#helpfile-examples)
* [Overview](#overview)
* [Installing and updating mrrobust](#installing-and-updating-mrrobust)
* [Code testing](#code-testing)
* [Authors](#authors)
* [How to cite the mrrobust package](#how-to-cite-the-mrrobust-package)
* [References](#references)
* [Collaboration](#collaboration)
* [Acknowledgements](#acknowledgements)

## Latest updates

* December 2018: 
  - Improved compatibility with the [`github` package](https://haghish.github.io/github/), i.e. mrrobust and its dependencies can be installed simply by issuing: `gitget mrrobust` , assuming that you have the `github` package installed. [See below for instructions](#2-use-the-github-package).
  - `mrdeps` command added for conveniently installing dependencies.
* November 2018: Example showing the use of `TwoSampleMR` and `mrrobust` in the same Rmarkdown script (`.Rmd` file) is [here](https://remlapmot.github.io/mrrobust/docs/rmarkdown-call-stata-example).
* November 2018: Example showing the use of `TwoSampleMR` and `mrrobust` in the same Stata Markdown script (`.stmd` file) is [here](https://remlapmot.github.io/mrrobust/docs/markstat-call-R-example).
* September 2018: IJE paper published online <https://doi.org/10.1093/ije/dyy195>.
* August 2018: [Click here for the example code and output from our IJE article](https://remlapmot.github.io/mrrobust/docs/spiller-ije-2018-examples).
* May 2018: [Click here for code and output from the examples in the helpfiles](https://remlapmot.github.io/mrrobust/docs/mrrobust-examples).
* May 2018: This page is now on GitHub Pages <https://remlapmot.github.io/mrrobust/>.
* April 2018: `mregger` now has option `radial` which implements the radial formulation of the MR-Egger model, and of the IVW model when used with option `ivw`.

## Short video introduction
[Click here for a short video demonstrating the use of the package.](https://drive.google.com/open?id=0B1owQlNgzNcPY0lMSGk0SnFfQWs)

[<img src="./img/mrconf2017_video_mrforest_screenshot.png" width="528" height="300">](https://drive.google.com/open?id=0B1owQlNgzNcPY0lMSGk0SnFfQWs)

## Helpfile examples
[Click here for some of the code and output from the examples in the helpfiles.](https://remlapmot.github.io/mrrobust/docs/mrrobust-examples)

Once the package is installed, there is a summary helpfile which can be viewed in Stata with:
```
help mrrobust
```
This has links to the helpfile for each command, which has an example near the bottom. In these examples you can click on the code to run it.

## Overview
The mrrobust package is a collection of commands for performing two-sample Mendelian randomization analyses using summary data of genotype-phenotype and genotype-outcome associations. 

Such data can be obtained from repositories such as MR-Base <http://www.mrbase.org> (Hemani et al. 2016).

The package contains the following commands:

 - `mrdeps` installs dependencies for the package.
 - `mrratio` implements the standard instrumental variable ratio (Wald) estimate with a choice of standard errors/confidence intervals.
 - `mrivests` automates calling `mrratio` on all the selected genotypes in your dataset.
 - `mregger` implements the IVW and MR-Egger regression approaches introduced in Bowden et al. 2015.
 - `mreggersimex` implements the simulation extrapolation algorithm for the MR-Egger model.
 - `mreggerplot` implements a scatter plot with fitted line (either from IVW, MR-Egger, or weighted median estimators) and confidence interval.
 - `mrmedian` and `mrmedianobs` implement the unweighted, weighted, and penalized weighted median IV estimators robust to 50% invalid instruments in Bowden et al. 2016.
 - `mrmodal` implements the zero modal estimator of Hartwig et al. 2017.
 - `mrmodalplot` plot of density used in modal estimator.
 - `mrforest` implements a forest plot of genotype specific IV estimates and estimates from models (e.g. IVW and MR-Egger).
 - `mrfunnel` funnel plot of genotype specific IV estimates.

## Installing and updating mrrobust
To install mrrobust in Stata versions 13 and later you have two choices.

### 1. Use `net install`

```
net install mrrobust, from(https://raw.github.com/remlapmot/mrrobust/master/) replace
mrdeps
```
In this code `mrdeps` installs the dependencies. These are `addplot`, `kdens`, and `moremata` packages (all by Ben Jann), the `heterogi` command (Orsini et al.), the `metan` command (Harris et al.), and the `grc1leg` command (Wiggins).

If you have previously installed the package and the `net install` command above fails with an error message that there are two copies of the package installed simply run `adoupdate`.

To check if there is an update available to any of your user-written Stata packages run `adoupdate`. To update mrrobust run:
```
adoupdate mrrobust, update
```

To uninstall mrrobust, issue in Stata:
```
ado uninstall mrrobust
```
If this fails with an error message mentioning that you have "multiple citations/instances of the package installed" simply issue `adoupdate mrrobust` which should leave you with the most recent version of the package you previously installed. You can then run `ado uninstall mrrobust`.

### 2. Use the `github` package

```
net install github, from("https://haghish.github.io/github/")
gitget mrrobust
```
This automatically installs the dependencies.

To update the package issue:
```
github update mrrobust
```

To uninstall mrrobust issue:
```
github uninstall mrrobust
```

### Installation for Stata version 12 and earlier versions
The `net install` syntax for installing `mrrobust` does not work under Stata version 12 and earlier because this webpage has an address starting with https rather than http. In such cases you need to do a manual installation.

To download and install mrrobust manually:

* click the green "Clone or download" button at the top of the GitHub repository [here](https://github.com/remlapmot/mrrobust) and download as a zip archive.
* On your computer, extract the zip archive and move the extracted files to your `adopath` 
* Typing `adopath` in Stata shows you the folders where the Stata programs, ado-files, are saved. Save the mrrobust files in the folder marked PERSONAL. If the folder Stata is pointing to does not exist simply make it, e.g. using Windows Explorer.

The installation commands for the other dependencies should work. However, if you want to install them manually: 

 * the `moremata` package is available as a zip file here <http://fmwww.bc.edu/repec/bocode/m/moremata.zip>. 
 * the `addplot` package is available here <http://fmwww.bc.edu/repec/bocode/a/addplot.zip>. 
 * the `heterogi` command is available here <https://ideas.repec.org/c/boc/bocode/s449201.html>.
 * the `kdens` package is available here <http://fmwww.bc.edu/repec/bocode/k/kdens.zip>.
 * the `metan` command is available here <https://ideas.repec.org/c/boc/bocode/s456798.html>.
 * the `grc1leg` ado-file is here <http://www.stata.com/users/vwiggins/grc1leg/grc1leg.ado> and the helpfile is here <http://www.stata.com/users/vwiggins/grc1leg/grc1leg.hlp>
 
Extract the zip archives and save all files on your `adopath`.

To uninstall a manual installation simply delete the files that you placed on your adopath.

## Code testing
As far as I know, and unlike R which has the `testthat` package, there is no recognised standard for writing unit tests for Stata commands. However, StataCorp refer to such do-files as cscripts (certification scripts). If you are interested I publish my cscripts (and their log files of output) in the cscripts directory in the GitHub repository. 

## Authors
Tom Palmer <tom.palmer@lancaster.ac.uk>, Wesley Spiller, Neil Davies

## How to cite the mrrobust package
Spiller W, Davies NM, Palmer TM. Software Application Profile: mrrobust - A tool for performing two-sample summary Mendelian randomization analyses. International Journal of Epidemiology, published online 12th September 2018. <https://doi.org/10.1093/ije/dyy195>

## Collaboration
If you would like to extend the code or add new commands I am open to receiving pull requests on GitHub or send me an email.

## References

 * Bowden J, Davey Smith G, Burgess S. Mendelian randomization with invalid instruments: effect estimation and bias detection through Egger regression. International Journal of Epidemiology, 2015, 44, 2, 512-525. <http://dx.doi.org/10.1093/ije/dyv080>
 * Bowden J, Davey Smith G, Haycock PC, Burgess S. Consistent estimation in Mendelian randomization with some invalid instruments using a weighted median estimator. Genetic Epidemiology, published online 7 April 2016. <http://dx.doi.org/10.1002/gepi.21965>
 * Hartwig FP, Davey Smith G, Bowden J. Robust inference in two-sample Mendelian randomisation via the zero modal pleiotropy assumption. bioRxiv. <http://dx.doi.org/10.1101/126102>
 * Hemani G et al. MR-Base: a platform for systematic causal inference across the phenome using billions of genetic associations. bioRxiv, 2016. <https://doi.org/10.1101/078972>

## Acknowledgements
Thanks to Michael Holmes, Caroline Dale, Amy Taylor, Rebecca Richmond, Judith Brand, Yanchun Bao, Kawthar Al-Dabhani, Michalis Katsoulis, and Ghazaleh Fatemifar for helpful feedback and suggestions.
