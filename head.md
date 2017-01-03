
---
# Copyright (C) 2017 Anthony DeDominic
#
# Permission is granted to copy, distribute and/or modify this document
# under the terms of the GNU Free Documentation License, Version 1.3
# or any later version published by the Free Software Foundation;
# with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
# A copy of the license is included in the section entitled "GNU
# Free Documentation License".

# The build requires the following dependencies:
#    TeXLive
#    pandoc 
#    pandoc-citeproc

title: "undecided"
abstract: |
    *To be written.*

papersize: letter
geometry: margin=2cm
fontfamily: mathpazo
fontsize: 12pt
header-includes:
- \hyphenpenalty 10000
- \usepackage{fancyhdr}
- \pagestyle{fancy}
- \fancyfoot[L]{DeDominic - undet}
- \fancyfoot[C]{Independent Study - \the\year}
- \fancyfoot[R]{\thepage}
- \author{DeDominic, Anthony\\Eastern Connecticut State University\\Willimantic, USA\\dedominica@my.easternct.edu}

link-citations: Yes
references:
- title: 'Caml-Shcaml: An OCaml Library for UNIX Shell Programming'
  DOI: 10.1145/1411304.1411316
  publisher: ACM
  author:
  - family: Heller
    given: Alec
  - family: Tov
    given: Jesse
  id: shcaml
  type: article-journal
  issued:
    year: 2008

- title: Monad Manifesto
  URL: http://www.jsnover.com/Docs/MonadManifesto.pdf
  publisher: Microsoft
  author:
  - family: Snover
    given: Jeffrey
  issued:
    month: Aug
    year: 2002
  id: monadshell
---
