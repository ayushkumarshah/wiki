# Installation

- Download stable nvim.appimage (0.6.1) from github releases:
  ```  
  wget https://github.com/neovim/neovim/releases/download/v0.6.1/nvim.appimage
  chmod u+x nvim.appimage
  ```
  * Set alias of vim and nvim to nvim.appimage
   
- Clone dotfiles-linux
- Run the ln commands in setup.sh
- Run nvim-dependencies.sh
  - install fzf, ripgrep, ranger
  - Mac: 
    - `brew install fzf ranger ripgrep`
    - `$(brew --prefix)/opt/fzf/inst`
- Install python packages
  ```
  conda activate base
  pip install pynvim==0.4.2 jedi==0.17.2
  ```
- For luavim language server:
  * sudo npm i -g pyright
  * sudo npm i -g bash-language-server
  * If doesn't work, comment all lua in init.vim
- :CoCInstall coc-python coc-pyright
- Run .config/nvim/scripts/install_coc_extensions.sh

