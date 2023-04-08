---
title: cmake
tags:
  - 工具
categories:
  - 工具
cover: /img/cmake.png
abbrlink: 24935
date: 2023-03-28 15:16:00
---

# Cmake

## 流程

```cmake
PROJECT  (HELLO)
SET (SRC_LIST main.c)  
MESSAGE (STATUS "This is BINARY dir" ${HELLO_BINARY_DIR})
MESSAGE (STATUS "This is SOURCE dir" ${HELLO_SOURCE_DIR})
ADD_EXECUTABLE(hello ${SRC_LIST})
```

可简化为

```cmake
PROJECT(HELLO)
ADD_EXECUTABLE(hello main.c)
```



使用${}方式来取得变量中的值，而在IF语句中则直接使用变量名。

可以使用双引号“”将源文件包含起来。处理特别难处理的名字比如fun c.c，则使用`SET(SRC_LIST "fun c.c")`可以防止报错。

可以使用make clean清理makefile产生的中间的文件，但是，不能使用make distclean清除cmake产生的中间件。如果需要删除cmake的中间件，可以采用rm -rf ***来删除中间件。

在目录下建立一个build文件用来存储cmake产生的中间件，不过需要使用cmake …来运行。其中外部编译，PROJECT_SOURCE_DIR仍然指代工程路径，即**/backup/cmake/t1**，而PROJECT_BINARY_DIR指代编译路径，即**/backup/cmake/t1/build**。

## 一些命令

cmake -D宏定义

[cmake常用命令的一些整理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/315768216)
