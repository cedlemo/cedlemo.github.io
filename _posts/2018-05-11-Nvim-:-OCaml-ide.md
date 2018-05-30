---
layout: post
title: Nvim OCaml ide
categories: nvim OCaml
---

How to configure/extend vim/nvim in order to write OCaml code.

## Install a plugin loader
 * [vim-plug](https://github.com/junegunn/vim-plug), a simple one.

 ```
 mkdir ~/.config/nvim/autoload
 curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

in the *~/.config/nvim/init.vim* :

```vim
" Specify a directory for plugins
" - For Neovim: ~/.local/share/nvim/plugged
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.local/share/nvim/plugged')
" - call your plugin here
call plug#end
```

### Some vim-plug commands

-  PlugInstall  Install plugins
-  PlugUpdate 	Install or update plugins
-  PlugClean[!]	Remove unused directories (bang version will clean without prompt)
-  PlugUpgrade	Upgrade vim-plug itself
-  PlugStatus	Check the status of plugins

Check the Readme of the github repository for more information.

## Add the vim-sensible plugin
This plugin add the configuration that everybody agree on.

```vim
call plug#begin('~/.local/share/nvim/plugged')
  Plug 'https://github.com/tpope/vim-sensible'
call plug#end
```

Reload the .vimrc and run in command mode (`:`) `PlugInstall`.
## Merlin

Install Merlin with (/!\ Merlin depends on `python-neovim`):

```
opam install merlin
```
then in *~/.config/nvim/init.vim* append this to add merlin in neovim's
runtime-path:

```
let g:opamshare = substitute(system('opam config var share'),'\n$','','''')
execute "set rtp+=" . g:opamshare . "/merlin/vim"
```

Finaly, run the following line in vim to index the documentation:

```
:execute "helptags " . g:opamshare . "/merlin/vim/doc"
```

### Some Merlin commands:

- Error reporting with `:MerlinErrorCheck`
- Completion with `<C-x><C-o>`
- Extracting type informations `:MerlinTypeOf`
- Source browsing
    * `:MerlinLocate`
    * `:ML ModuleName` or `:MLI ModuleName`

### Merlin file
Merlin uses .merlin files in order to know about your current project. Jbuilder
(Dune) create those files automatically. For more information see https://github.com/ocaml/merlin/wiki/project-configuration.

## Ocp-indent

* https://www.typerex.org/ocp-indent.html
* https://github.com/OCamlPro/ocp-indent
* https://www.systutorials.com/5212/auto-indenting-for-ocaml-code-in-vim-with-ocp-indent/

### Installation

Via opam : `opam install ocp-indent`

In the neovim configuration file :

```
execute "set rtp^=" . g:opamshare . "/ocp-indent/vim"
```

### Usage:

On a line or a selection of lines, juste use `==`.

In order to have automatic indentation after hitting Enter of after an `if`
for example, it exists a plugin:

* https://github.com/let-def/ocp-indent-vim

with *vim-plug* :

```vim
call plug#begin('~/.local/share/nvim/plugged')
  Plug 'https://github.com/tpope/vim-sensible'
  Plug 'https://github.com/let-def/ocp-indent-vim'
call plug#end()
```

## Asynchronous Lint Engine

It provides linting while editing. ALE uses Merlin for OCaml files.
* https://github.com/w0rp/ale.git

### Installation:

```vim
call plug#begin('~/.local/share/nvim/plugged')
  Plug 'https://github.com/tpope/vim-sensible'
  Plug 'https://github.com/let-def/ocp-indent-vim'
  Plug 'https://github.com/w0rp/ale.git'
call plug#end()
```
Reload the neovim configuration file and run in command mode : `PlugUpdate`.

### Commands:

* `:help ALE` vim documentation of ALE.
* `:help ale-ocaml-merlin`
* `:ALENext` go to next lint error.
* `:ALEPrevious` go to previous lint error.
* `:ALEFirst` `:ALELast` go to first or last lint error.
* `:ALEToggle` enable or disable ALE.
* `:ALEInfoToClipboard` copy ALEInfor to clipboard.

## Deoplete

It provides an extensible and asynchronous completion framework for neovim/vim8.
As ALE, this framework is not specific to OCaml but works with the plugin
`deoplete-ocaml` to offer OCaml completion and ocamldoc viewing .

* https://github.com/Shougo/deoplete.nvim
* https://github.com/copy/deoplete-ocaml

### Installation:

Install the related plugins:

```vim
call plug#begin('~/.local/share/nvim/plugged')
  Plug 'https://github.com/tpope/vim-sensible'
  Plug 'https://github.com/let-def/ocp-indent-vim'
  Plug 'https://github.com/w0rp/ale.git'
  Plug 'Shougo/deoplete.nvim', { 'do': ':UpdateRemotePlugins' }
  Plug 'https://github.com/copy/deoplete-ocaml'
call plug#end()
```

```
" enable deoplete
let g:deoplete#enable_at_startup = 1
```

see `:help deoplete` for more information.

## Neoformat

It is as ALE and deoplete, a generic plugin (ie: not specific to OCaml)
for vim8/neovim that helps you to format your code.

### Installation:

```
call plug#begin('~/.local/share/nvim/plugged')
  Plug 'https://github.com/tpope/vim-sensible'
  Plug 'https://github.com/let-def/ocp-indent-vim'
  Plug 'https://github.com/w0rp/ale.git'
  Plug 'Shougo/deoplete.nvim', { 'do': ':UpdateRemotePlugins' }
  Plug 'https://github.com/copy/deoplete-ocaml'
  Plug 'https://github.com/sbdchd/neoformat'
call plug#end()
```

### Commands:

* `:Neoformat` : format all the buffer or the selection
* `:help neoformat` : get access to the documentation of the neovim plugin.


## user-setup

Automatic configuration, when you do not want to bother to modify you vim/neovim
configuration file.

* https://github.com/OCamlPro/opam-user-setup

### Installation and usage:

```
# if your editor environment variable is set
opam user-setup install
# if you want to specify one or more editor.
opam user-setup install --editors=vim
```

The generated file for vim :

```
" sensible.vim - Defaults everyone can agree on
" Maintainer:   Tim Pope <http://tpo.pe/>
" Version:      1.1

if &compatible
  finish
else
  let g:loaded_sensible = 1
endif

if has('autocmd')
  filetype plugin indent on
endif
if has('syntax') && !exists('g:syntax_on')
  syntax enable
endif

" Use :help 'option' to see the documentation for the given option.

set autoindent
set backspace=indent,eol,start
set complete-=i
set smarttab

set nrformats-=octal

set ttimeout
set ttimeoutlen=100

set incsearch
" Use <C-L> to clear the highlighting of :set hlsearch.
if maparg('<C-L>', 'n') ==# ''                                                                                                                       [67/921]
  nnoremap <silent> <C-L> :nohlsearch<CR><C-L>
endif

set laststatus=2
set ruler
set showcmd
set wildmenu

if !&scrolloff
  set scrolloff=1
endif
if !&sidescrolloff
  set sidescrolloff=5
endif
set display+=lastline

if &encoding ==# 'latin1' && has('gui_running')
  set encoding=utf-8
endif

if &listchars ==# 'eol:$'
  set listchars=tab:>\ ,trail:-,extends:>,precedes:<,nbsp:+
endif

if v:version > 703 || v:version == 703 && has("patch541")
  set formatoptions+=j " Delete comment character when joining commented lines
endif

if has('path_extra')
  setglobal tags-=./tags tags^=./tags;
endif
if &shell =~# 'fish$'
  set shell=/bin/bash
endif

set autoread
set fileformats+=mac

if &history < 1000
  set history=1000
endif
if &tabpagemax < 50
  set tabpagemax=50
endif
if !empty(&viminfo)
  set viminfo^=!
endif
set sessionoptions-=options

" Allow color schemes to do bright colors without forcing bold.
if &t_Co == 8 && $TERM !~# '^linux'
  set t_Co=16
endif

" Load matchit.vim, but only if the user hasn't installed a newer version.
if !exists('g:loaded_matchit') && findfile('plugin/matchit.vim', &rtp) ==# ''
  runtime! macros/matchit.vim
endif

inoremap <C-U> <C-G>u<C-U>
" ## added by OPAM user-setup for vim / base ## 93ee63e278bdfc07d1139a748ed3fff2 ## you can edit, but keep this line
let s:opam_share_dir = system("opam config var share")
let s:opam_share_dir = substitute(s:opam_share_dir, '[\r\n]*$', '', '')
let s:opam_configuration = {}                                                                                                                         [1/921]

function! OpamConfOcpIndent()
  execute "set rtp^=" . s:opam_share_dir . "/ocp-indent/vim"
endfunction
let s:opam_configuration['ocp-indent'] = function('OpamConfOcpIndent')

function! OpamConfOcpIndex()
  execute "set rtp+=" . s:opam_share_dir . "/ocp-index/vim"
endfunction
let s:opam_configuration['ocp-index'] = function('OpamConfOcpIndex')

function! OpamConfMerlin()
  let l:dir = s:opam_share_dir . "/merlin/vim"
  execute "set rtp+=" . l:dir
endfunction
let s:opam_configuration['merlin'] = function('OpamConfMerlin')

let s:opam_packages = ["ocp-indent", "ocp-index", "merlin"]
let s:opam_check_cmdline = ["opam list --installed --short --safe --color=never"] + s:opam_packages
let s:opam_available_tools = split(system(join(s:opam_check_cmdline)))
for tool in s:opam_packages
  " Respect package order (merlin should be after ocp-index)
  if count(s:opam_available_tools, tool) > 0
    call s:opam_configuration[tool]()
  endif
endfor
" ## end of OPAM user-setup addition for vim / base ## keep this line
" ## added by OPAM user-setup for vim / ocp-indent ## 30625c6cd28cfaded2318243c9f88ff8 ## you can edit, but keep this line
if count(s:opam_available_tools,"ocp-indent") == 0
  source "/home/cedlemo/.opam/default/share/vim/syntax/ocp-indent.vim"
endif
" ## end of OPAM user-setup addition for vim / ocp-indent ## keep this line

```
Links:

* https://discuss.ocaml.org/t/whats-your-setup-for-ocaml-development/1784/27
* https://www.systutorials.com/5212/auto-indenting-for-ocaml-code-in-vim-with-ocp-indent/
* https://github.com/OCamlPro/opam-user-setup
