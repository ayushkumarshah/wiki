# PDF Character and Line Extraction with SymbolScraper

## Summary

### Introduction
- character locations are represented
by positions on provided writing lines, along with character codes
and font sizes. This presents an opportunity to recover symbol
identities and locations directly from PDFs, without the need for
OCR software
- symbol layout information for graphics extraction (e.g., for mathematical
    formulas or text
search
- other techniques - return position but not enough to locate characters due to
    varying sizes and font styles
- locates precise character boundaries by using the character outlines (glyphs) provided
by font profiles embedded in PDF files.

### Working
- First by PDFBOX
- Individual characters represented by:
  - Unicode
  - (x, y) position
  - font metrics
  - glyphs 
      - (vector-based representations of
        how characters are drawn using a series of lines, arcs, and ‘pen’
        up/down/move operations)
      - represented by a set of coordinates with winding rules (commands) used
        to draw the outline of a character
- glyph plus font scaling information used
- 
