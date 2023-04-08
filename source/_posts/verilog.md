---
title: verilog
tags: 语言
categories: 语言
abbrlink: 41623
cover: /img/verilog.jpg
date: 2023-03-31 15:06:54
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





## $test$plusargs和$value$plusargs

该函数的调用发生在仿真运行（run）阶段。这样仅需要对设计进行一次编译即可，如果需要改变相应的条件，可以在run的时候动态指定，这样有利于脚本处理进行回归的验证，同时也有利于object的动态construct。

- $test$plusargs

```verilog
test.v
------------------------
initial begin
    if($test$plusargs("test01"))
        $readmemh("test01.dat", mem01);
    if($test$plusargs("test02"))
        $readmemh("test02.dat", mem02);
    if($test$plusargs("test03"))
        $readmemh("test03.dat", mem03);
end 
```

当仿真运行时，$test$plusargs会在命令行中搜索指定的字符，若找到相应字符，在函数返回“1”，否则返回“0”。如果下次仿真时不需要test01时，仅需要将test01从运行命令中删除即可。

命令

```
<run-options>+test01+test02+test03...
```

- $value$plusargs

```verilog
test.v
------------------------
if($value$plusargs("FINISH=%d", stop_clk))begin
    repeat(stop_clk)@(posedge clk);
    $finish
end 
 
if(value$plusargs("TESTNAME=%s", testname))begin
    $display("Running test %0s", testname);
end 
 
if($value$plusargs("FREQ=%0f", frequency))begin
    frequency = 8.333333;
end 
```

若使用的运行命令如下：

```
<run-options>+FINISH=10000+TESTNAME=this_test+FREQ=5.6666
```

则上例的运行结果为：

stop_clk ： 10000

testname：this_test

frequency：5.6666（如果run-options中没有增加“FREQ=5.6666”，那么frequency为8.333333）。

[(55条消息) 详解$test$plusargs和$value$plusargs_test_plus_args_Hyunnnnn的博客-CSDN博客](https://blog.csdn.net/github_33678609/article/details/86575671)
