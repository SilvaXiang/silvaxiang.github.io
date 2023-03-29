---
layout: post
title: Machine Learning Compilation
categories: [Course]
---
## 机器学习编译中的问题
机器学习部署问题和数据库查询优化问题很像。在机器学习/深度学习模型和部署环境之间存在巨大的Gap，这些Gap包括硬件结构不同，操作系统的不同，容器环境的不同，运行时依赖的不同等等等等，所以机器学习部署应运而生

Machine Learning Compilation is the process to transform and optimize machine learning execution from its development form to deployment form

## 机器学习编译的目标

#### 1.Integration and Dependency Minimization

Integrate Libraries together and only incorporate necessary ones

即，最小化的集成和依赖。简单来说，运行ResNet模型只需要一些conv2d,softmax,relu算子，并不需要NLP的一些算子，所以就只需要将必须的组件集成即可。
#### 2.Leverage hardware naive acceleration
在部署中，利用好特殊硬件对AI模型的加速，比如Intel的AVX512, GPU等

## Keys elements in 机器学习编译
1. Tensor: Tensor是模型执行中用于保存数据的多维数组，用于存储输入、输入以及大量的中间数据
2. Tensor Functions：Tensor Function是对Tensor的操作，类似于数据库中的算子。Tensor Function可由多个操作/算子结合，即从Input Tensor到OutPut Tensor之间的所有Function，都可以当作一个Tensor Function

机器学习编译主要是对Tensor Function做变换，这点很像数据库查询优化器中对Query Tree做变换。比如算子融合。
### 抽象和实现
在模型的推理中，抽象表示不同的方法来代表相同的系统推理过程。比如linear+relu，可以被抽象为两个算子（linear, relu），也可也被抽象为一个算子（linear_relu）。
在实际中，一般用More Specialized Version表示一个抽象的不同实现
### Four Categories of Abstractions
1. Computation Graph: 计算图是对模型的高度抽象的表示，它允许我们对其进行改写和优化
2. Tensor Program：Tensor Program允许我们进行数据Layout的转换和算子的融合
3. Libraries and Runtimes
4. Hardware Primitives

## Primitive Tensor Function
Primitive Tensor Function，原语张量函数，即在计算图中的一个基本计算单元，比如Linear，Relu等等
相同的Primitive Tensor Function抽象能有不同的实现，比如普通的实现，利用SIMD等等。在实际上，相同的算子抽象可以用*pybind11*绑定到不同的算子实现后端

## Tensor Program Abstarction
Tensor Program抽象主要是对Tensor进行操作，因为Tensor是一个多维的数组/矩阵，所以对其进行处理时，循环的方式，以及数据的Layout都会对性能造成很大的影响。
### Key elements of a Tensor Program
Tensor Program Abstraction主要是对循环方式、数据Layout、以及循环中进行的计算过程进行抽象。

这种抽象，本质上是对高性能实现方式转换的规则定义，比如对于一个Naive的多重循环，我们可以定义一些规则（抽象），比如循环的重排（内循环和外循环的顺序调换）、数据处理在某个线程上的绑定等等等等

Naive Implementation Code ---- Transformation Rules ---> High Proformance Implementation Code

这点很像数据库查询优化器中对Query Tree的变换规则定义，比如Filter下推、连接顺序重排、Top-N转Limit等等

Most of the machine learning compilation process can be viewed as tranformations amoung computation graphs and tensor program in model executions

