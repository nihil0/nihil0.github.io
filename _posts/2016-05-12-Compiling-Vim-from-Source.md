---
layout: post
title: How to build Vim from source without root access. 
---

This post builds on the process described [here](https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source). However, in my case, I did not have root access, so `sudo` commands
don't work. However, I realized I can still install software using Ubuntu Software Center. Also, this was the first step to building a highly portable Python development environment. 


### System

1. OS: Ubuntu 14.04 
2. Arch: x86_64
3. Compiler: gcc 4.8.4


### Prerequisites

Make sure you have the required dependencies installed. If you have root access to your machine, you can do this by running 

```
sudo apt-get build-dep vim-gtk
```

or

Here is a list of dependencies I installed. This is by no means an exhaustive list, but it worked for me. 

```
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
libgtk2.0-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev 
```

### Method

Step 1: If you have previously built Vim from source, go to your source folder `/something/vim/src`, run `make uninstall` and then `make distclean`.

Step 2: Make sure python libraries are installed first. the packages are `python-dev` and `python3-dev`. The config directories for python need to be given as input to
the build config script. The variables are `--with-python-config-dir` and `--with-python-config-dir`. You can get these by running `python-config --configdir` and `python3-config --configdir`, respectively. 

Step 3: Configure the build.

```
./configure --with-features=huge --enable-multibyte --enable-pythoninterp --enable-python3interp\
 --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
 --with-python3-config-dir=/usr/lib/python3.4/config-3.4m-x86_64-linux-gnu \
 --enable-gui \
 --prefix=$HOME/vim
```

Step 4: The final step is to run 

```
make && make install 
```

