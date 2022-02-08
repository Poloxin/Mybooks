# Install Vim-plug

A minimalist Vim plugin manager.

## Installation

You need download plug.vim and put in the `~/.vim/autoload` directory

```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## Configure .vimrc


Add a vim-plug section to your `~/.vimrc`


**NOTE:** open `.vimrc` without `sudo`


1. Begin the section with `call plug#begin([PLUGIN_DIR])`

1. List the plugins with `Plug` commands

1. `call plug#end()` to update `&runtimepath` and initialize plugin system


**Example:**

```vim
"" Start vim-plug section
call plug#begin('~/.vim/plugged')

"" Plugin begin from 'Plug'
Plug 'instant-markdown/vim-instant-markdown', {'for': 'markdown', 'do': 'yarn install'}

"" End vim-plug setion
call plug#end()
```

Reload `.vimrc` and call `:PlugInstall` to install plugins. 
