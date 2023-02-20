# NeoVim + Vimtex + Skim for forward and backward search

## Forward search:

### Config required

```vim
let g:vimtex_latexmk_continuous = 1
let g:vimtex_compiler_progname = 'nvr'
let g:vimtex_view_method = 'skim'
let g:vimtex_view_skim_activate = 1
let g:vimtex_view_skim_reading_bar = 1
let g:vimtex_view_skim_sync = 1
let g:vimtex_compiler_latexmk = {
    \ 'build_dir' : 'temp',
    \}
    
function! s:write_server_name() abort
  let nvim_server_file = (has('win32') ? $TEMP : '/tmp') . '/vimtexserver.txt'
  call writefile([v:servername], nvim_server_file)
endfunction

augroup vimtex_common
  autocmd!
  autocmd FileType tex call s:write_server_name()
augroup END

```

### Usage:

Run :VimtexView

## Backward Search:

For `neovim`, select the `Custom` preset from the drop-down list in the Pdf viewer (Skim) and set:

- Command: nvim
- Args: --headless -c "VimtexInverseSearch %line '%file'"


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
