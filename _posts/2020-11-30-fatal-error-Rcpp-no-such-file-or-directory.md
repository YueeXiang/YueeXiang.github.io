---
layout:     post
title:      Error in sourceCpp('xx.cpp') : Error 1 occurred building shared library.
subtitle:   我差点因为这个bug换题，真实bug可能是'fatal error: Rcpp: no such file or directory'
date:       2020-11-30
author:     Yue
header-img: img/sweet.jpg
catalog: true
tags:
    - rcpp
    - debug	
---

## debug的心路历程

### 太长不看版：

删去.cpp文件中的`#include <Rcpp>`

### 还是看看我的碎碎念吧：

老师让我试着复现论文，论文代码有是有（用rcpp写的），但在sourceCpp这一步就卡了，开始以为是安装Rtools或者rcpp的时候环境或者路径没设置好（我对环境/路径一窍不通），把Rtools和rcpp都重装了几次，还是同一个bug；以为是源代码有问题，问了师兄才知道我那个bug还没开始编译，根本不是人家代码的问题。那就是我的问题惹。中午的时候好绝望，师兄当场跑出来了，我都想换电脑了（贫穷。

代码：

```
> source('.../sample.R')
```

报错：

```
"C:/rtools40/mingw64/bin/"g++  -std=gnu++11 -I"E:/r/R-4.0.3/include" -DNDEBUG -I../inst/include -fopenmp  -I"E:/r/R-4.0.3/library/Rcpp/include" -I"E:/r/R-4.0.3/library/RcppArmadillo/include" -I"E:/{文件路径}"        -O2 -Wall  -mfpmath=sse -msse2 -mstackrealign -c code.cpp -o code.o
code.cpp:1:10: fatal error: Rcpp: No such file or directory
 #include <Rcpp>
          ^~~~~~
compilation terminated.
make: *** [E:/r/R-4.0.3/etc/x64/Makeconf:229: admmmcp_code.o] Error 1
Error in sourceCpp("code.cpp") : 
  Error 1 occurred building shared library.
WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/
```

开始以为主要bug是

```
Error in sourceCpp("code.cpp") : 
  Error 1 occurred building shared library.
```

这个bug非常难找解决方案，包括stackoverflow在内的所有网站基本都是同一个人问的问题，并且方案对我不适用（基本都是说让test一下Rtools的路径对不对，但是我安装Rtools的时候已经勾选了添加路径，已经自动配好了，不需要我自己配；我用下面几行代码test了，结果完全没问题）

```
find_rtools(T)
Sys.which("gcc.exe")
writeLines('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', con = "~/.Renviron")
Sys.which("make")
system('g++ -v')
Rcpp::evalCpp("2 + 2")
```

这几行代码几乎是全网Rtools安装和这个bug相关的代码，我跑出来的test结果完全没问题。。

经过师兄提醒我开始仔细看那个bug，也就是“error”前面还说了一大堆话，这个过程中搜到一个说需要在cpp文件中加上`#include <Rcpp.h>`，我就加上看看，结果bug变了，提示让我删去这句话，有`#include <RcppArmadillo.h>`就够了。这个时候我都有点崩溃了，从一个bug变成另一个bug。。我也没抱啥希望就把那句话删了，结果？？？好了？？？就是这么神奇。我这就是运气好把这个bug给de出来了。谁让我不好好听课不好好学rcpp呢？

解决了就好，终于可以安心看论文看理论了，我真的真的很不喜欢（害怕）写代码。
