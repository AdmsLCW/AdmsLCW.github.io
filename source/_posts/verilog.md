---
title: verilog
date: 2023-03-31 15:06:54
tags: -语言
---

# Verilog

## 延迟语法

*//普通时延，A&B计算结果延时10个时间单位赋值给Z*

```verilog
wire Z, A, B ;
assign #10   Z = A & B ;
```

*//隐式时延，声明一个wire型变量时对其进行包含一定时延的连续赋值。*

```verilog
wire A, B;
wire #10        Z = A & B;
```

//惯性时延

在上述例子中，A 或 B 任意一个变量发生变化，那么在 Z 得到新的值之前，会有 10 个时间单位的时延。如果在这 10 个时间单位内，即在 Z 获取新的值之前，A 或 B 任意一个值又发生了变化，那么计算 Z 的新值时会取 A 或 B 当前的新值。所以称之为惯性时延，即信号脉冲宽度小于时延时，对输出没有影响

[(55条消息) 【Verilog语法009】Verilog 6种延时_verilog延时赋值_qq_1615549892的博客-CSDN博客](https://blog.csdn.net/qq_32752869/article/details/121680766)
