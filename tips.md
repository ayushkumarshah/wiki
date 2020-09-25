# General Tips and Tricks

## .new shortcut urls

- http://doc.new
- http://sheets.new
- http://repo.new
- http://gist.new
- http://story.new
- http://keep.new
- http://meet.new
- http://cal.new

## Convert md to pdf

### Conversion

```zsh
pandoc --highlight-style zenburn --toc -N Week*.md -o notes.pdf
```
N - subsection number enable

### List styles

```zsh
pandoc --list-highlight-styles
```

### List languages supported

```zsh
pandoc --list-highlight-languages
```

## COnvert rmd to pdf

```zsh
R -e "rmarkdown::render('file.rmd OR file.md', output_file = 'file.pdf')" 
```
