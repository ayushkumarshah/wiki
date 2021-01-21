# Pandoc

## Useful flags

|Flag|Description|
|----|----|
|-s|By default, pandoc produces a document fragment. To produce a standalone document (e.g. a valid HTML file including <head> and <body>), use the -s or --standalone flag|
|-f FORMAT|Specify format of input eg: html, latex, markdown|
|-t FORMAT|Specify format of output eg: html, latex, markdown|
|-o output_file.extension|Produces output in the specified file. Default - stdout

Example:

```zsh
pandoc -s -f html input.html -t latex 
pandoc -s input.html -t latex 
pandoc -s input.html -o output.tex 
pandoc input.html -o output.tex 
```

- If no input files specified, input is read from stdin. So, we can use `cat file | pandoc -t latex`

## Math Rendering in HTML

The default is to render TeX math as far as possible using Unicode characters. Formulas are put inside a span with class="math", so that they may be styled differently from the surrounding text if needed. However, this gives acceptable results only for basic math, usually you will want to use --mathjax or another of the following options.

- --mathjax[=URL]: <br>Use MathJax to display embedded TeX math in HTML output. TeX math will be put between \(...\) (for inline math) or \[...\] (for display math) and wrapped in <span> tags with class math. Then the MathJax JavaScript will render it. The URL should point to the MathJax.js load script. If a URL is not provided, a link to the Cloudflare CDN will be inserted.

- --mathml
<br> Convert TeX math to MathML (in epub3, docbook4, docbook5, jats, html4 and html5). This is the default in odt output. Note that currently only Firefox and Safari (and select e-book readers) natively support MathML.

- --webtex[=URL]
<br>Convert TeX formulas to <img> tags that link to an external script that converts formulas to images. The formula will be URL-encoded and concatenated with the URL provided. For SVG images you can for example use --webtex https://latex.codecogs.com/svg.latex?. If no URL is specified, the CodeCogs URL generating PNGs will be used (https://latex.codecogs.com/png.latex?). Note: the --webtex option will affect Markdown output as well as HTML, which is useful if you’re targeting a version of Markdown without native math support.

- --katex[=URL]
<br>Use KaTeX to display embedded TeX math in HTML output. The URL is the base URL for the KaTeX library. That directory should contain a katex.min.js and a katex.min.css file. If a URL is not provided, a link to the KaTeX CDN will be inserted.

- --gladtex
<br> Enclose TeX math in <eq> tags in HTML output. The resulting HTML can then be processed by GladTeX to produce images of the typeset formulas and an HTML file with links to these images.

Usage:

```zsh
pandoc [-s] --mathjax -o output.[html|tex|..]
```
