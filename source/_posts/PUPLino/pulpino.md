---
title: PULPino-asyn
tags: [RISCV,PULPino]
categories: [PULPino]
cover: /img/pulpino.png
recommend: true
abbrlink: 15180
date: 2023-03-29 15:04:25
---

# PULPino-asyn

项目地址： [AdmsLCW/PULPino-asyn (github.com)](https://github.com/AdmsLCW/PULPino-asyn)

## 基础知识

![image-20230329150817712](https://326-adms-1305022140.cos.ap-nanjing.myqcloud.com/images/Pulpino1.png)

</br> PULPino的结构</br> </br> 从图中可以发现PULPino有如下一些特点：</br> （1）采用的是指令RAM、数据RAM分开的哈佛结构；</br> （2）增加了一个Boot ROM，其中可以存储启动代码，利用该启动代码可以加载连接至SPI接口的Flash中的程序。</br> （3）采用的AXI4、APB两级总线结构。</br> （4）具有外设接口，包括GPIO、UART、I2C、SPI等。</br> （5）含有一个SoC Controll模块，其作用是整个SoC平台的控制信息，包括：是否使能时钟门、设置启动地址、架构信息等。</br> （6）提供了一个Advanced Debug Unit，提供了标准调试JTAG接口，使得调试器可以访问指令RAM、数据RAM、处理器内部寄存器，以及外设对应的控制寄存器等。</br> （7）提供了一个SPI Slave接口，直接连接在AXI互连总线上，可以通过该接口在不影响处理器的情况下，访问指令RAM、数据RAM、处理器内部寄存器，以及外设对应的控制寄存器等。</br> 图8-2中各模块的详细功能、寄存器作用可以。</br>

## 工程解读

PULPino SoC 平台是开源发布的， 包括了 RTL 源代码， 所有 IP， RISCY 核心和 ZERO RISCY 核心， RTL 模拟环境代码以及 FPGA 构建流程的相关代码等。具体的代码结构为：

**ci**:该文件夹用于存放各种脚本的归类文件夹；

**doc**:该文件夹包含了对于 PULPino 的介绍文档，主要是 datasheet 文件夹，其中有对该平台的详细介绍；

**fpga**：该文件夹包含了在 ZedBoard 或者 ZYBO FPGA 开发板综合和运行的文件；

**ips**：该文件夹包含了 PULPino 需要的外设以及总线模型的 IP 复用模块。adv_dbg_if、 apb、 axi、 fpu、 RISCY 以及 ZERO RISCY 这些 IP；

**ipstools**:该文件夹用于更新复用 IP 的组件和脚本；

**rtl**：该文件夹是用于存放 HDL 源代码的，主要包含 PULPino SoC 平台搭建的相关代码；

**sw**：该文件夹用于软件模拟，包括应用的源代码和配置的脚本等。其中 build文件夹包含了编译器以及模拟器的输出文件，并且 RTL 软件模拟将在这里运行；

**tb**:该文件夹包含用于测试的相关文件，包括测试用的 mem 和 jtag 的直接程序接口；

**vsim**:该文件夹包含了用于编译模拟的脚本以及库文件。 modelsim_lib 包含了用于 ModelSim 模拟验证的所有库文件。 tcl_files 是用于 ModelSim 模拟的 tcl脚本文件夹。vcompile 用于存放所有 RLT 代码的编译脚本。 wave 文件夹用于存放模拟时产生的波形文件。 work 为 ModelSim 模拟时建立的默认 work 库。

------

