---
title: "计算机组成原理 — 计算机系统概述"
subtitle: "基础不牢，地动山摇！"
layout: post
author: "luobr"
header-style: text
tags:
  - 计算机组成原理
  - 笔记
---


## 计算机系统概述

### 计算机系统简介

#### 计算机系统

计算机系统由**硬件**和**软件**两大部分组成

![image-20230623125741365](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230623125741365.png)

#### 计算机软硬件机器

微程序机器M0、实际机器M1 归属于硬件 ；虚拟机M2、M3、M4归属于软件

![image-20230622094955297](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622094955297.png) 

#### 计算机体系结构和计算机组成区别

计算机体系结构：程序员所见到的计算机系统的属性概念性的结构与功能特性（指令系统、数据类型、寻址技术、I/O机理等）类似定义接口的概念

计算机组成：实现计算机系统结构所体现的属性（具体指令的实现）类似接口实现的概念

举例说明：一台机器是否具有某一项功能是计算机体系结构的问题，以至于这项功能是怎么实现得就是计算机组成的问题



### 计算机的基本组成

#### 冯.诺伊曼计算机的特点

1、五大部件组成（控制器、运算器、存储器、输入设备、输出设备）

2、指令和数据以相同的地位存储在存储器中，可按地址进行寻访

3、指令由操作码和地址码组成

4、指令和数据以二进制的形式表示

5、以运算器为中心

6、指令在存储器内按顺序存放

#### 存储器的基本组成

主要介绍存储体、存储器地址寄存器 MAR、存储器数据寄存器 MDR

![image-20230622150559063](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622150559063.png) 

#### 运算器的基本组成

主要介绍算数逻辑运算单元 ALU、累加器 ACC、乘商寄存器 MQ、操作数寄存器 X

![image-20230622132557894](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622132557894.png) 

#### 控制器的基本组成

主要介绍控制单元 CU、程序计数器 PC、指令寄存器 IR

![image-20230622135326640](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622135326640.png)

#### 主机完成一条指令的过程

**以取数指令为例**

指令包含两部分：一个是指令码（决定进行什么操作，比如是取数操作）；另一个是地址码（存放数据的地址）

步骤1：取**取数指令**到指令寄存器 IR （绿线）

![image-20230622142251410](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622142251410.png) 

步骤2：分析指令码以及执行指令操作（红线）

![image-20230622143704305](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622143704305.png) 

**以存数指令为例**

步骤1：取**存数指令**到指令寄存器 IR （如上图取取数指令步骤1）

步骤2：分析指令码以及执行指令操作（橙线）

![image-20230622144324986](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622144324986.png) 



### 计算机硬件的主要技术指标

![image-20230622150434734](https://use-typora.oss-cn-hangzhou.aliyuncs.com/image-20230622150434734.png)

