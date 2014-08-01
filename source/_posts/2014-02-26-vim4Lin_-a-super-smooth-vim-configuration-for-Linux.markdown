---
layout: post
title: "vim4Lin: a super smooth vim configuration for Linux"
date: 2014-02-26 17:12:15 UTC
updated: 2014-02-26 17:12:15 UTC
comments: true
categories: Vim
---

Recently I forked a project on Github.com, and renamed it to vim4Lin which is a vim configuration. The project can be used to help to synchronize the configuration files of vim on multiple machines. However, I intentionally want to focus its experiences on Linux, such as Ubuntu.
The project you can find in this following url: https://github.com/bfeng/vim4Lin

## Overview
This is another vim configuration, which I normally use under terminal. So default theme is changed to `molokai`, which is optimized for C under terminals.

Vim related settings are in `plugin/settings/Settings.vim`, and other plugins' settings are in `plugin/settings` corresponding directories.

Two vimrc files:

1. `vimrc`, standard version vimrc.

2. `gvimrc`, same as vimrc, but added some features only available in GUI mode.

you can link your `~/.vimrc` to any one of them as you wish :)

It's a screenshot of the up-to-date configuration:

![image](https://github.com/bfeng/vim4Lin/blob/master/screenshots/Screenshot-c.png?raw=true)

![image](https://github.com/bfeng/vim4Lin/blob/master/screenshots/Screenshot-python.png?raw=true)

The content above is from [http://flask.pocoo.org/snippets/5/](http://flask.pocoo.org/snippets/5/)

## Installation and Update

1. BACKUP your `.vim` directory and `.vimrc` first.(IMPORTANT!)

2. `cd ~` to change directory to your home directory.

3. Clone files to your home directory:

        git clone https://github.com/bfeng/vim4Lin.git

4. cd to `vim4Lin` directory and execute the `update.sh` to get latest version modules:

        cd vim4Lin
        ./update.sh

5. make a symbolic link `.vim` to `vim4Lin` that you just cloned, or just rename it to `.vim` also be fine:

        ln -s vim4Lin .vim

6. link the vimrc to

        ln -s .vim/vimrc .vimrc

7. if you use GUI version VIM, such as MacVim or GVim, you can also link to `.gvimrc`:

        ln -s .vim/gvimrc .gvimrc

8. change directory to `~/.vim` and execute `./update.sh` script, it should do all the updates automatically.

## Features and Key Mappings

1. Resize splited windows automatically, so that you  get a bigger editing room if you're working with a smaller screen. (stole from [Gary Bernhardt](https://github.com/garybernhardt))

2. Toggle between working mode and presentation mode by `\``z`, but only work in GUI version Vim. You can check [here](http://blog.eddie.com.tw/2012/03/14/switch-to-presentation-mode/) to see how it looks like. (stolen from [Mike Skalnik](https://github.com/skalnik))

3. some usually used key mappings in normal mode:

    a. `<F1>` to toggle a Calendar window on and off.

    b. `<F2>` to toggle NERDTree on and off.

    c. `<F4>` to toggle Taglist window.

    d. `<F5>` is the script runner, according to it's filetype, it will run Ruby(*.rb) ,Python(*.py) or Javascript(*.js) file(SpiderMonkey is needed), even CoffeeScript(*.coffee, but you may have to install CoffeeScript first). If the filetype is VimScript, `<F5>` will run `:source %` for you.

    e. `<F7>` to switch to previous tab, and `<F8>` to the next tab.

    f. hit `<ctrl>p` will launch a quick window to match keywords from your current working directory, not only file name, but also path name. And `<ctrl>w u` will match from your MRU(Mostly Recent Used) files, which is also frequently used.

    g. hit `\` twice to toggle comment on and off.

    h. `<tab>` and `<shift><tab>` to increase and decrease the syntax indentation. By default, `<tab>` will invoke the code-completion prompt. If you need to input a real `<tab>` into text, hit `<ctrl>v` and `<tab>`.

    i. `\``v` to open `.vimrc` in a new tab.

    j. `\``0` to edit or create `README.md` in current working directory.

4. Remove tailing whitespace automatically while saving.
5. [Exuberant Ctags](http://ctags.sourceforge.net/) is recommended for the executable of ctags.

## Reference
This work was forked from Eddie Kao's [eddie-vim](https://github.com/kaochenlong/eddie-vim). Thanks!
Some modules, such as which support `flex` and css colors, are moved out, and add some modules which support `latex` are added in.
The `molokai` theme is now supported as the main coding theme and `vim-airline` replaces the obsolte `vim-powerline`. Much work were done to focus on the compatibility between the GUI mode and the console mode.

