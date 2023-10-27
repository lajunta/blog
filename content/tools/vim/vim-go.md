---
title: "vim go config"
date: 2021-04-04T23:56:54+08:00
draft: false
tags: ["vim","golang"]
---
VIM-GO PLUGIN
===

### Install Vim-Pathogen

```bash
mkdir -p ~/.vim/autoload ~/.vim/bundle && \
curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```

* Modify .vimrc

```bash
execute pathogen#infect()
syntax on
filetype plugin indent on
```


### Install Nerdtree

```bash
git clone https://github.com/preservim/nerdtree.git ~/.vim/bundle/nerdtree
```

### Install vim-go

```bash
git clone https://github.com/fatih/vim-go.git ~/.vim/bundle/vim-go
```