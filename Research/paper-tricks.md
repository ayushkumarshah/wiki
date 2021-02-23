---
title: Writing a Research Paper Tricks
author: "Ayush Kumar Shah"
date: "2021-02-23"
toc: false
numbersections: false
autoEqnLabels: true
tags: []
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
# Tips

- Include a list of research questions and contributions and make sure it is
    visible by using bullet points and including in the Introduction.
- Avoid using stock phrases
- Use simple sentences: sentences that you would use to tell someone about your
    contributions in a conversation or a dialogue.
- Move from general overview to specific points. The reader must know the bigger
    picture or how the whole system or contributions look like before moving on
    to the specifics.
- Avoid orphan terms (a single term in a new line). If there is one, try to
    rewrite the sentences in a shorter simpler way.
- Use word like "include" rather than are when listing items since include means
    it is not limited to the things included and there may be more. Example: The
    primary contributions include:
- Don't use the term major contributions, the reader will decide which
    contributions are major. Use primary contributions or just contributions instead.
- Tell a story using related works. Don't just list the contributions of each
    paper but link them and form a graph and compare them with each other and
    how it is related with your paper.
- Never do spell checks and grammar checks until the paper is complete but never
    forget to do it once the paper is complete.
- Use tekdiff tool (comes with latex installation) to track changes in the latex files
- Use pdfcrop tool (comes with latex installation) to crop the pdf
    automatically.
- Always use vector graphics as images (pdf works well). 
- Use commands like `\trim`, `\scalebox`, `\fbox`, `\mbox`, `\subfigure`

