---
layout: post
title: VAR-SD-MSE-COV!
subheading: Introduction of variance, Standard Deviation, Meas Squre Error and Covariance.
author: Jeffrey
categories: jekyll
banner:
  video: https://vjs.zencdn.net/v/oceans.mp4
  loop: true
  volume: 0.8
  start_at: 8.5
  image: https://bit.ly/3xTmdUP
  opacity: 0.618
  background: "#000"
  height: "100vh"
  min_height: "38vh"
  heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
  subheading_style: "color: gold"
tags: Variance Standard_Deviation Meas_Squre_Error Covariance
sidebar: []
---

# 数学基础概念

## 方差：

$$
S^2=\frac{\sum^{n}_{i=1}{x_{i}-x}}{n-1}
$$

在概率论和统计**方差**是衡量随机变量或一组数据时离散程度的度量。**概率论中方差**用来度量随机变量和其数学期望（即均值）之间的偏离程度。**统计中的方差（**样本方差）是各个样本数据和平均数之差的 平方和 的平均数。在许多实际问题中，研究方差即偏离程度有着重要意义。

## 标准差(又称为均方差)：

$$
{S}=\sqrt {\frac {\sum ^{n}_{i=1} {({X}_{i}-\bar {X}{)}^{2}}} {n-1}}
$$

标准差是**方差**的平方根，标准差优势：
1、表示离散程度的数字和样本数据点的数量级一致，更适合对数据样本形成感性认知。
2、表示离散程度的数字单位与样本数据的单位一致，更方便做后续分析运算

![image-20220210180632727](D:\所有笔记\图片目录\image-20220210180632727.png)

3、在样本数据大致符合正态分布的情况下，标准差具有方便估算的特性66.7%的数据点落在平均值前后1个标准差的范围内、95%的数据点落在平均值前后2个标准差的范围内，而99%的数据点将会落在平均值前后3个标准差的范围内。

## 均方误差（Mean Squre Error）

MSE是各数据偏离**真实值**差值的平方和的平均数，方差是偏离**平均值**差值的平方和的平均数

## 协方差

**协方差**（Covariance）在概率论和统计学中用于衡量两个变量的总体误差。而方差是协方差的一种特殊情况，即当两个变量是相同的情况。

协方差表示的是两个变量的总体的误差，这与只表示一个变量误差的方差不同。如果两个变量的变化趋势一致，也就是说如果其中一个大于自身的期望值，另外一个也大于自身的期望值，那么两个变量之间的协方差就是正值。如果两个变量的变化趋势相反，即其中一个大于自身的期望值，另外一个却小于自身的期望值，那么两个变量之间的协方差就是负值。
$$
Cov(X,Y)=E[(X-\mu_x)(Y-\mu_y)]
$$
简单来说就是看两个变量之间的变化趋势，他们是同向还是反向的，同向的程度或反向的程度是怎么样的。
