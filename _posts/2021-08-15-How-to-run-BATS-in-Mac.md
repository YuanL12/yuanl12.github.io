---
title: 'How to run BATS in Mac'
date: 2021-08-15
permalink: /posts/2021/08/How-to-run-BATS-in-Mac/
tags:
  - BATS
  - C++
---

Run BATS in linux is easy, but on Mac is hard. This blog will help you install that on Mac.

If you use Linux OS, then simply run use the flag '-fopenmp' like
```
g++ -o hello_omp.out hello_omp.cpp -fopenmp
```

If you use Mac OS, then run the following might work depends on your g++ setting: 
```
g++-10 -o hello_omp.out hello_omp.cpp -fopenmp
```
However, it probably cause some problems, if your g++ is not the correction version. If so, please see below.

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
and then in the almost end of that file, change 
```
export PATH=/usr/local/bin:$PATH
```

Now, you are free to compile it. 
Finally, in order to use makefile, change CXX flags into `CXX = g++-10`.

