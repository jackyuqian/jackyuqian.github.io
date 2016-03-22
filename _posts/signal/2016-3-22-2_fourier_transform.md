---
layout: post
title: 信号处理之浅见（二）：傅里叶变换
category: 信号处理
---

# {{ page.title }}

## 傅里叶级数(FS, Fourier Series)

对于任意一个满足一定条件的时间上连续的周期信号，都可以表示为若干复指数信号之和。若其周期为T0，角频率为w0，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\sum_{k=-\infty}^{-\infty} a_k \cdot e^{j\omega_0kt}">

上式两边同时乘以<img src="http://www.forkosh.com/mathtex.cgi?\ e^{-j\omega_0rt}">，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)e^{-j\omega_0rt}=\sum_{k=-\infty}^{-\infty} a_k \cdot e^{j\omega_0kt} \cdot e^{-j\omega_0rt}">

上式两边同时在一个信号周期内求积分，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-j\omega_0rt}dt=\int_0^{T_0} \sum_{k=-\infty}^{-\infty} a_k \cdot e^{j\omega_0kt} \cdot e^{-j\omega_0rt}dt">

交换积分和求和的顺序并化简，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-j\omega_0rt}dt=\sum_{k=-\infty}^{-\infty} a_k \int_0^{T_0}e^{j\omega_0(k-r)t}dt">

由于上式右侧积分号内的复指数周期为<img src="http://www.forkosh.com/mathtex.cgi?\ T_0/(k-r)">，且在一个周期内对其积分，结果为零，所以有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0}e^{j\omega_0(k-r)t}dt=\begin{cases} T_0,k=r\\ 0,k\not=r \end{cases}">

因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-j\omega_0rt}dt=a_k T_0">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(jw_0)=\int_0^{T_0} x(t)e^{-j\omega_0rt}dt">

则

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\frac{1}{T_0}\sum_{k=-\infty}^{-\infty} X(jw_0) \cdot e^{j\omega_0kt}">

上述两式互为傅立叶级数对。