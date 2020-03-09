---
layout: post
title: VIM插件管理
category: VIM
---

# {{ page.title }}

# vim-plug介绍

A minimalist Vim plugin manager. See [git repo](https://github.com/junegunn/vim-plug).

# vim-plug的安装

Download [plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim) and put it in the ".vim/autoload" directory.

# 插件的安装

Add a vim-plug section to your `~/.vimrc`

1. Begin the section with `call plug#begin()`;

2. List the plugins with `Plug` commands;

3. `call plug#end()` to update &runtimepath and initialize plugin system.

Example
~~~
call plug#begin('~/.vim/plugged')
Plug 'scrooloose/nerdtree'
call plug#end()
~~~

Commands                            |   Command	Description
-                                   |   -
PlugInstall [name ...] [#threads]   |   Install plugins
PlugUpdate [name ...] [#threads]	|   Install or update plugins
PlugClean[!]	                    |   Remove unlisted plugins (bang version will clean without prompt)
PlugUpgrade	                        |   Upgrade vim-plug itself
PlugStatus	                        |   Check the status of plugins
PlugDiff	                        |   Examine changes from the previous update and the pending changes
PlugSnapshot[!] [output path]	Generate script for restoring the current snapshot of the plugins

