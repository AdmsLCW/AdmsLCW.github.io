---
title: RI5CY
date: 2023-03-28 20:06:50
tags:
  - RSIC-V
categories:
  - RISC-V
cover: img/RISCY.png
---

# RI5CY

支持：RV32I、RV32C、RV32M、扩展指令集（算术指令集扩展、硬件循环、地址自增的访存指令、乘累加指令、向量操作）

寻址方式：4种。立即数寻址、寄存器寻址、Load指令的基地址寻址、分支跳转的PC相对寻址。

![image-20230328200918392](I:\Github\Blogroot\blog\source\img\RISC-V\image-20230328200918392.png)

四级流水：取值、译码、执行、回写。

结构冒险：指令接口取指令，数据接口取数据，数据和地址分开，采用哈佛结构，防止了结构冒险/相关。

数据冒险：解决方法（1）Forward电路，数据前推；（2）Bypass电路；（3）流水线停顿。

指令预取buffer：队列buffer、FIFO；cache方式，位于多核共享指令缓存和处理器和之间。
