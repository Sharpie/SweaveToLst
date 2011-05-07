SweaveToLst
===========
*A simple LaTeX package for automagically reformatting Sweave output*


What
----

SweaveToLst (a.k.a Sweave to Listing) is a simple LaTeX style file that
repurposes the `Schunk` environment used by the [Sweave][Sweave] literate
programming system such that it uses the LaTeX `listings` package to
pretty-print R input/output rather than the default setup that uses `fancyvrb`
and two nested environments `Sinput` and `Soutput`. This is accomplished by
using the LaTeX [`xstring`][xstring] package to replace things like
`\begin{Sinput}` with custom delimiters that `listings` can use to format code.

The end result is that a `Schunk` environment containing multiple `Sinput` and
`Soutput` environments is collapsed to a single `Schunk` environment containing
custom delimiters.

This code is released under a [3-clause BSD license][license]. See the
[COPYING][copying] file for formal details.


How
---

SweaveToLst may be used by copying the file `sweavetolst.sty` into the same
directory as the vignette of an R package or other file to be processed by
Sweave. In order to activate the package, the following two lines must be added
to the preamble of the `.Rnw` file:

    \usepackage{Sweave} % To prevent Sweave from automagically inserting it
    \usepackage{sweavetolst}

The style used by `listings` to format Sweave code chunks may be adjusted by
editing the definition of `sweavechunk` at the beginning of `sweavetolst.sty`.


Why
---

This style file was created to support the vignette of the
[tikzDevice][tikzDevice] package. For reasons I won't go into here, tikzDevice
requires all Sweave output to be contained within a single environment.
Previously, a rather ugly hack was used to achieve this effect by re-writing
the output routines of the Sweave driver while it processed the package
vignette. This hack required maintenance with ever major R release and so
SweaveToLst was created to provide a light-weight alternative that attacked the
problem from the LaTeX side.

SweveToLst is recommended for any R package authors who want more control over
the way code chunks are formatted in their vignettes. It is lightweight and
requires no external dependencies which plays nicely with the automated build
process used by CRAN.


Why Not
-------

There are several options that provide more detailed control over Sweave output
formatting that are more appropriate for reports or vignette writers who are
not afraid of setting up additional dependencies. Some of these options are:

  - [SweaveListingUtils][SweaveLstUtils]: An R package that also uses
    `listings` to format Sweave code chunks. Provides more detailed control.

  - [pgfSweave][pgfSweave] provides an alternate Sweave driver that uses the
    [highlight][highlight] package to pretty print Sweave code chunks.


Thanks
------

Many thanks to the community at [tex.stackexchange.com][texexchange],
especially those who provided answers to [this question][texexchange-question].
This input helped shape the package implementation.


  [Sweave]: http://www.stat.uni-muenchen.de/~leisch/Sweave
  [license]: http://opensource.org/licenses/bsd-license
  [copying]: http://github.com/Sharpie/SweaveToLst/blob/master/COPYING
  [xtring]: http://ctan.org/pkg/xstring
  [tikzDevice]: http://github.com/Sharpie/RTikZDevice
  [SweaveLstUtils]: http://cran.r-project.org/web/packages/SweaveListingUtils/index.html
  [pgfSweave]: http://cran.r-project.org/web/packages/pgfSweave/index.html
  [highlight]: http://cran.r-project.org/web/packages/highlight/index.html
  [texexchange]: http://tex.stackexchange.com
  [texexchange-question]: http://tex.stackexchange.com/questions/16299/search-and-replace-in-a-verbatim-token-list
