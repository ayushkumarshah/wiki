# NeoVim + Vimtex + Skim for forward and backward search

## Forward search:

### Config required

```vim
let g:vimtex_latexmk_continuous = 1
let g:vimtex_compiler_progname = 'nvr'
let g:vimtex_view_method = 'skim'
let g:vimtex_view_skim_activate = 1
let g:vimtex_view_skim_reading_bar = 1
```

### Usage:

Run :VimtexView

## Backward Search:

For `neovim`, select the `Custom` preset from the drop-down list and set:

- Command: nvr
- Args: --remote-silent +"%line" "%file"
 
Please ensure that you have the `nvr` (neovim-remote) utility and the
`pynvim` Python module available.

Q: Does Vimtex work with neovim?

A: Yes, but backward sync requires the `neovim-remote` utility. It may be
   installed and used by vimtex as follows:

1. Install the `pynvim` and `neovim-remote` modules for python3 (e.g.,
  using `pip3 install --user pynvim neovim-remote`; if `python3 -c
  "import pynvim"` returns without error and `nvr` starts neovim from
  the command line, everything should be good to go).

1. Configure your viewer to use `nvr --remote +"%line" "%file"` for
  backward sync.

   See https://github.com/mhinz/neovim-remote for more information on `nvr`.


### Usage:

Shift + Cmd + Double click

## Alternative: Zathura (in Mac)

Backward search works but forward search does not work in Mac (dbus issues)

### Installation

```zsh
$ brew install zathura --with-synctex
$ brew install xdotool
$ brew install zathura-pdf-poppler

$ mkdir -p $(brew --prefix zathura)/lib/zathura
$ ln -s $(brew --prefix zathura-pdf-poppler)/libpdf-poppler.dylib $(brew --prefix zathura)/lib/zathura/libpdf-poppler.dylib
```

### Backward search usage:

Ctrl + click
