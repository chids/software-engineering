# Vim

* Use Vundle to manage plugins.
* iTerm set to 256 colors.
* Don't use prepackaged vim config. But take a look at square/maximum-awesome
* key bindings - (mode)map <key> <command>
* <leader> to trigger keys
* grammar - `[register][num/range]<verb><motion|(i|a)<text object>>` e.g. 4fa, ciw, de
* magic key - `.` (repeat last action)
* `brew install vim` for system clipboard support.
```  
   $ vim --version | grep clipboard  
   +clipboard  
```

## Resources for learning.

* https://github.com/shawncplus/vim-classes
* :help (everything) - shorthand :h
* vimtutor (comes with vim)
* http://vimcast.org, also "Practical Vim" book.
* http://vim-adventures.com/ (game)
* http://vimgolf.com
* Sublime vintage mode.
* https://github.com/lunixbochs/actualvim
* Practical Vim - https://github.com/gitig/Practical-Vim-Notes 
* https://learn.thoughtbot.com/vim
* https://github.com/Gonzih/vim-keymap

## Modes

* Normal
  * `/` or `?` to search, `n` next , `shift+n` previous.
  * `shift+}` `shift+{` block
  * `%s/oldword/newworld/gc` - substitute, global, confirmation
  * `i`, `a`, `I`, `A`, `o`, `O`
  * `r` - replace
  * `ciw` change in word
  * `shift+h`, `shift+l`, `shift+m`, `zz`
* Insert
  * `ctrl+n` autocomplete
  * `ctrl+o` to goto normal mode for just one command
* Command
* Visual
  * `ctrl+v` block
  * `shift+v` line
  * `viw ` word, `vap` paragraph

## Registers

`:reg` - lists all registers

`"0p` - to paste from `0` register

`set clipboard=unnamed` - yank and paste with the system clipboard

Insert mode - `ctrl-r + # of register` to paste.

## Buffers

* `:ls` - show buffers
* `:b # of buffer` - go to buffer
* `:copen` - Quickfix list - syntax errors, search in project
* `ctrl+o`, `ctrl+i` to jump between last jumps. `g,`, `g;` - change lists

## Ctags

* `ctrl+]` - jump into tag, `ctrl+o` to jump back
* `brew install ctags`, `ctags -R`, `gem install gem-ctags`, `gem ctags` - generate ctags for all gems
* `tpope/vim-bundler` - will be aware of all tags from all gems in bundle.

### Macro

TBA

### Dispatch in background 

`:!`
e.g. `:!rspec spec/model/user.rb`

or `ctrl-z` to put vim in background, do your thing and `fg` to resume

__Mac OS X__
> If you have administrator privileges, you must fix an Apple-introduced problem in Mac OS X 10.5 Leopard by executing the following command, or BASH and Zsh will have the wrong PATH when executed non-interactively.

`sudo chmod ugo-x /usr/libexec/path_helper`

### Protip

__Esc key timeout__
* vimrc `set timeoutlen=1000 ttimeoutlen=0`
* zsh # 10ms for key sequences `KEYTIMEOUT=1`
* tmux `set -sg escape-time 0`

__folding__
```
set foldmethod=syntax
set nofoldable
```

__marks__ http://vim.wikia.com/wiki/Using_marks
```
ma - marks a marker at a
'a or `a - jumps to mark a
:marks - lists markers
:delmarks a - delete marker a
'. - jumps to last edit
```
__scroll__
```
ctrl-e up
ctrl-y down
ctrl-d page-down
ctrl-u page-up
zl scroll right
zL scroll half page right
zh, zH scroll left
```

Quick zoom in pane
https://coderwall.com/p/qqz1lq/vim-zoom-restore-window
