---
layout: post
title: Compiling vim with some kind of GUI from source for Python development. 
---
![_config.yml]({{ site.baseurl}}/images/config.png)

# Compiling vim with some kind of GUI from source for Python development. 

This post builds on the process described [here][main_link]. 

## System

1. Ubuntu 14.04 
2. Architecture x86_64


## Method

Make sure you have the required dependencies installed. If you have root access to your machine, you can do this by running 

```
sudo apt-get build-dep vim
```

I do not have root access, so I am using the Ubuntu Software Center to install dependencies manually. Here is a list of dependencies I installed.
This is by no means an exhaustive list, but it worked for me. 


Step 1: If you have previously built Vim from source, go to your source folder `/something/vim/src`, run `make uninstall` and then `make distclean`.

Step 2: Make sure python libraries are installed first. the packages are `python-dev` and `python3-dev` and running `python-config --configdir` and `python3-config --configdir`

Step 3: We need to compile it with python and python3 interpreters enabled so run:
```
./configure --with-features=huge --enable-multibyte --enable-pythoninterp --enable-python3interp --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu --with-python3-config-dir=/usr/lib/python3.4/config-3.4m-x86_64-linux-gnu --enable-gui --prefix=$HOME/vim
```

[main_link] https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source