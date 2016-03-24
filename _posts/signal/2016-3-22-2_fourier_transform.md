---
layout: post
title: 信号处理之浅见（二）：傅里叶变换
category: 信号处理
---

# {{ page.title }}

## 连续时间周期信号的傅里叶级数(FS, Fourier Series)

对于任意一个满足一定条件的时间上连续的周期信号，都可以表示为无穷多个复指数信号之和。若其周期为T0，角频率为Ω0，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{jk\Omega_0t}">

上式两边同时乘以<img src="http://www.forkosh.com/mathtex.cgi?\ e^{-jr\Omega_0t}">，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)e^{-jr\Omega_0t}=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{jk\Omega_0t} \cdot e^{-jr\Omega_0t}">

上式两边同时在一个信号周期内积分，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-jr\Omega_0t}dt=\int_0^{T_0} \sum_{k=-\infty}^{+\infty} a_k \cdot e^{jk\Omega_0t} \cdot e^{-jr\Omega_0t}dt">

交换积分和求和的顺序并化简，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-jr\Omega_0t}dt=\sum_{k=-\infty}^{+\infty} a_k \int_0^{T_0}e^{j(k-r)\Omega_0t}dt">

由于上式右侧积分号内的复指数周期为<img src="http://www.forkosh.com/mathtex.cgi?\ T_0/(k-r)">，且在一个周期内对其积分，结果为零，所以有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0}e^{j(k-r)\Omega_0t}dt=\begin{cases} T_0,k=r\\ 0,k\not=r \end{cases}">

因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-jr\Omega_0t}dt=a_k|_{k=r} T_0=a_rT_0">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(k\Omega_0)=\frac{1}{T_0}\int_0^{T_0} x(t)e^{-jk\Omega_0t}dt">

则

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\sum_{k=-\infty}^{+\infty} X(k\Omega_0) \cdot e^{jk\Omega_0t}">

上述两式互为傅立叶级数对。

## 连续时间非周期信号的傅里叶变换(FT, Fourier Transform)

对于非周期信号x(t)，我们只关注0~T0之间的信号x'(t)，然后在坐标系上延拓，便形成了周期为T0的周期信号x''(t)。由之前的分析可知：


<img src="http://www.forkosh.com/mathtex.cgi?\ x''(t)=\sum_{k=-\infty}^{+\infty} X''(k\Omega_0) \cdot e^{jk\Omega_0t}">

其中

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(k\Omega_0)=\frac{1}{T_0}\int_0^{T_0} x''(t)e^{-jk\Omega_0t}dt">

因为在0~T0区间内x(t)=x''(t)，其余区间内x(t)=0，因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(k\Omega_0)=\frac{1}{T_0}\int_{-\infty}^{+\infty} x(t)e^{-jk\Omega_0t}dt">


将上式代入第一个公式，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x''(t)=\sum_{k=-\infty}^{+\infty} \frac{1}{T_0}\int_{-\infty}^{+\infty} x(t)e^{-jk\Omega_0t}dt \cdot e^{jk\Omega_0t}">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\sum_{k=-\infty}^{+\infty} \int_{-\infty}^{+\infty} x(t)e^{-jk\Omega_0t}dt \cdot e^{jk\Omega_0t} \cdot \Omega_0">

因为：

<img src="http://www.forkosh.com/mathtex.cgi?\ \lim_{T_0 \rightarrow +\infty}x''(t)=\lim_{\Omega_0 \rightarrow 0}x''(t)=x(t)">

所以根据积分的定义，将求和转换为积分形式：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\lim_{\Omega_0 \rightarrow 0} \frac{1}{2\pi}\sum_{k=-\infty}^{+\infty} \int_{-\infty}^{+\infty} x(t)e^{-jk\Omega_0t}dt \cdot e^{jk\Omega_0t} \cdot \Omega_0">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} x(t)e^{-j\Omega t}dt \cdot e^{j\Omega t}d\Omega">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(\Omega)=\int_{-\infty}^{+\infty} x(t)e^{-j\Omega t}dt">

则：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\frac{1}{2\pi}\int_{-\infty}^{+\infty} X(j\Omega) e^{\Omega t}d\Omega">

上述两式互为傅立叶变换对。

## 离散时间周期信号的傅里叶级数(DFS, Discrete Fourier Series)
分析离散周期信号的傅里叶级数之前不妨回顾一下连续时间的情况，根据之前的分析，连续时间周期信号x(t)可以分解成无穷多个复指数信号的和：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{jk\Omega_0t}">

那么离散周期信号是不是也可以分解成无穷多个复指数的和呢？对于离散信号而言，若采样率为Fs，一个信号周期内采样点为N，那么k次谐波对应复指数如下：

<img src="http://www.forkosh.com/mathtex.cgi?\ e^{jk\Omega_0t}|_{t=nT_s}=e^{jk\Omega_0nF_s}=e^{jk\frac{2\pi}{N}n}">

先看看连续信号的情况，k+N次谐波对应的复指数如下：

<img src="http://www.forkosh.com/mathtex.cgi?\ e^{j(k+N)\Omega_0t}">

显然对于连续信号而言，复指数并非周期出现的，也就是说k次谐波复指数信号与k+N次谐波复指数并不相同。再来看看离散信号：

<img src="http://www.forkosh.com/mathtex.cgi?\ e^{j(k+N)\frac{2\pi}{N}n}=e^{jk\frac{2\pi}{N}n}e^{jN\frac{2\pi}{N}n}=e^{jk\frac{2\pi}{N}n}e^{j2n\pi}=e^{jk\frac{2\pi}{N}n}">

显然，对于离散信号而言，复指数信号是周期出现的，周期是N，也就是说只有N中不同频率的复指数，并非连续信号那样有无数种！这是怎么造成的？看看下图应该就明白了：

![2-1](http://ceohs.img47.wal8.com/img47/536944_20160203171046/145881588141.png)

图中上部分是k次谐波对应的复指数（只看实部），下部分是k+N次谐波对应的复指数，不难看出对于连续信号，频率增加了N倍，而对于离散信号，因为一个基波周期内采样点个数有限，所以恰好k次和k+N次谐波的采样点重合，也就是说分不清二者有什么区别。

那离散周期信号是否可以表示成这有限几个复指数的和呢？即：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\sum_{k=0}^{N-1} a_k \cdot e^{jk\frac{2\pi}{N}n}">





若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(k)=\sum_{n=0}^{N-1} x(n)e^{-jk\omega_0n}">

则

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\frac{1}{N}\sum_{k=0}^{N-1} X(k) \cdot e^{jk\omega_0n}">

上述两式互为傅立叶级数对。

观察X(k)不难发现其周期性，周期为N：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(k+N)=\sum_{k=0}^{N-1} x(n)e^{-jk\frac{2\pi}{N}n} \cdot e^{-jN\frac{2\pi}{N}n}=\sum_{k=0}^{N-1} x(n)e^{-jk\frac{2\pi}{N}n}=X(k)">

## 离散时间非周期信号的傅里叶级数(DTFT, Discrete Time Fourier Transform)

对于非周期信号x(n)，我们只关注0~N-1之间的信号x'(n)，然后在坐标系上延拓，便形成了周期为N的周期信号x''(n)。由之前的分析可知：

<img src="http://www.forkosh.com/mathtex.cgi?\ x''(n)=\frac{1}{N}\sum_{k=0}^{N-1} X''(k) \cdot e^{jk\omega_0n}">

其中

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(k)=\sum_{n=0}^{N-1} x''(n)e^{-jk\omega_0n}">

因为在0~N-1区间内x(n)=x''(n)，其余区间内x(n)=0，因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(k)=\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\omega_0n}">

将上式代入第一个公式，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x''(n)=\frac{1}{N}\sum_{k=0}^{N-1} (\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\omega_0n}) \cdot e^{jk\omega_0n}">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\sum_{k=0}^{N-1} (\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\omega_0n}) \cdot e^{jk\omega_0n} \cdot \omega_0">

因为：

<img src="http://www.forkosh.com/mathtex.cgi?\ \lim_{N \rightarrow +\infty}x''(n)=\lim_{\omega_0 \rightarrow 0}x''(n)=x(n)">

所以根据积分的定义，将求和转换为积分形式：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\lim_{\omega_0 \rightarrow 0} \frac{1}{2\pi}\sum_{k=0}^{N-1} (\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\omega_0n}) \cdot e^{jk\omega_0n} \cdot \omega_0">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\int_{0}^{2\pi} (\sum_{n=-\infty}^{+\infty} x(n)e^{-j\omega n})e^{j\omega n}d\omega">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(\omega)=\sum_{n=-\infty}^{+\infty} x(n)e^{-j\omega n}">

则：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\frac{1}{2\pi}\int_{0}^{2\pi} X(\omega)e^{j\omega n}d\omega">

同样的，离散非周期信号的傅里叶变换也是周期的，周期为2pi。
