---
title: Test note 1
author: "Ayush Kumar Shah"
date: "2021-01-09"
toc: True
numbersections: true
autoEqnLabels: true
tags: [test, markdown]
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

# Title

## Subtitle

### Sub sub title 1

My name is Ayush Kumar Shah.

I like:

- football
- basketball
- travelling
- hiking
- photography

![My profile](/Users/ayushkumarshah/Desktop/ProfilePictures/pro_pic_new.jpg)

### Sub sub title 2

I am a Computer Engineer.

## Subtitle 2

I am a student of RIT

# Title 2

This is empty.

Good bye.

<hr>


