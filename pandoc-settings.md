---
title: Notes
author: "Ayush Kumar Shah"
toc: True
numbersections: true
autoEqnLabels: true
geometry:
- top=30mm
- left=30mm
- right=30mm
- bottom=30mm
header-includes: |
  \usepackage{float}
  \let\origfigure\figure
  \let\endorigfigure\endfigure
  \renewenvironment{figure}[1][2] {
    \expandafter\origfigure\expandafter[H]
    }{
    \endorigfigure
    }
---
