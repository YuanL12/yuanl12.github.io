---
title: 'How to run BATS in Mac'
date: 2021-08-15
permalink: /posts/2021/08/How-to-run-BATS-in-Mac/
tags:
  - cool posts
  - category1
  - category2
---

In order to compile it 
### manually in **linux**, use the flag '-fopenmp'
```
g++ -o hello_omp.out hello_omp.cpp -fopenmp
```

### in **Mac**:
```
g++-10 -o hello_omp.out hello_omp.cpp -fopenmp
```

> **_Attention_**:
> If you use `g++ -o hello_omp.out hello_omp.cpp -fopenmp` in Mac, it will return an error like `clang: error: unsupported option '-fopenmp'`, and this is because g++ in Mac is default to use clang like `Apple clang version 12.0.0 (clang-1200.0.32.29)` in my case. You will need Homebrew to install GCC. The details of installation is listed below:
- Install gcc by Homebrew
```
brew install gcc
```
- Find the location of the newly installed gcc. Brew appends the version number to gcc so that it does not conflict with the one installed by Command Line Tools. You will find it in usr/local/bin. In my case it's usr/local/bin/gcc-10.

- Now you need to tell your system about it. When calling a compiler your bash will look into `/usr/bin` by default and not in `/usr/local/bin`. You need to add this directory to your `$PATH`. This can be easily done with the command:

```
vim ~/.zshrc
```
ann then change 
```
export PATH=/usr/local/bin:$PATH
```

Next in Makefile, change all CXX flags into CXX = g++-10.
