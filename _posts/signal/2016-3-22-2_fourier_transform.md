---
layout: post
title: 信号处理之浅见（二）：傅里叶变换
category: 信号处理
---

# {{ page.title }}

## 连续时间周期信号的傅里叶级数(FS, Fourier Series)

对于任意一个满足一定条件的时间上连续的周期信号，都可以表示为若干复指数信号之和。若其周期为T0，角频率为w0，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{j\omega_0kt}">

上式两边同时乘以<img src="http://www.forkosh.com/mathtex.cgi?\ e^{-j\omega_0rt}">，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)e^{-j\omega_0rt}=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{j\omega_0kt} \cdot e^{-j\omega_0rt}">

上式两边同时在一个信号周期内积分，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-j\omega_0rt}dt=\int_0^{T_0} \sum_{k=-\infty}^{+\infty} a_k \cdot e^{j\omega_0kt} \cdot e^{-j\omega_0rt}dt">

交换积分和求和的顺序并化简，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-j\omega_0rt}dt=\sum_{k=-\infty}^{+\infty} a_k \int_0^{T_0}e^{j\omega_0(k-r)t}dt">

由于上式右侧积分号内的复指数周期为<img src="http://www.forkosh.com/mathtex.cgi?\ T_0/(k-r)">，且在一个周期内对其积分，结果为零，所以有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0}e^{j\omega_0(k-r)t}dt=\begin{cases} T_0,k=r\\ 0,k\not=r \end{cases}">

因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ \int_0^{T_0} x(t)e^{-j\omega_0rt}dt=a_k|_{k=r} T_0=a_rT_0">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(kw_0)=\frac{1}{T_0}\int_0^{T_0} x(t)e^{-j\omega_0kt}dt">

则

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\sum_{k=-\infty}^{+\infty} X(kw_0) \cdot e^{j\omega_0kt}">

上述两式互为傅立叶级数对。

## 连续时间非周期信号的傅里叶变换(FT, Fourier Transform)

对于非周期信号x(t)，我们只关注0~T0之间的信号x'(t)，然后在坐标系上延拓，便形成了周期为T0的周期信号x''(t)。由之前的分析可知：


<img src="http://www.forkosh.com/mathtex.cgi?\ x''(t)=\sum_{k=-\infty}^{+\infty} X''(kw_0) \cdot e^{j\omega_0kt}">

其中

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(kw_0)=\frac{1}{T_0}\int_0^{T_0} x''(t)e^{-j\omega_0kt}dt">

因为在0~T0区间内x(t)=x''(t)，其余区间内x(t)=0，因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(kw_0)=\frac{1}{T_0}\int_{-\infty}^{+\infty} x(t)e^{-j\omega_0kt}dt">


将上式代入第一个公式，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x''(t)=\sum_{k=-\infty}^{+\infty} \frac{1}{T_0}\int_{-\infty}^{+\infty} x(t)e^{-j\omega_0kt}dt \cdot e^{j\omega_0kt}">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\sum_{k=-\infty}^{+\infty} \int_{-\infty}^{+\infty} x(t)e^{-j\omega_0kt}dt \cdot e^{j\omega_0kt} \cdot \omega_0">

因为：

<img src="http://www.forkosh.com/mathtex.cgi?\ \lim_{T_0 \rightarrow +\infty}x''(t)=\lim_{\omega_0 \rightarrow 0}x''(t)=x(t)">

所以根据积分的定义，将求和转换为积分形式：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\lim_{\omega_0 \rightarrow 0} \frac{1}{2\pi}\sum_{k=-\infty}^{+\infty} \int_{-\infty}^{+\infty} x(t)e^{-j\omega_0kt}dt \cdot e^{j\omega_0kt} \cdot \omega_0">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} x(t)e^{-j\omega t}dt \cdot e^{j\omega t}d\omega">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(\omega)=\int_{-\infty}^{+\infty} x(t)e^{-j\omega t}dt">

则：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(t)=\frac{1}{2\pi}\int_{-\infty}^{+\infty} X(j\omega) e^{\omega t}d\omega">

上述两式互为傅立叶变换对。

## 离散时间周期信号的傅里叶级数(DFS, Discrete Fourier Series)

对一个连续时间的周期信号采样后的信号即为离散时间周期信号，若采样周期为Ts，则该离散信号为：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=x(nT_s)=x(t)|_{t=nT_s}=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{j\omega_0knT_s}">

若一个信号周期内共有N个采样点，用每采样一次转过的角度来表示离散信号的角频率，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \Omega_0=\frac{2\pi}{N}=\omega_0T_s">

带入上式则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{jk\Omega_0n}">

上式两边同时乘以<img src="http://www.forkosh.com/mathtex.cgi?\ e^{-jrn\Omega_0}">，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)e^{-jr\Omega_0n}=\sum_{k=-\infty}^{+\infty} a_k \cdot e^{jk\Omega_0n} \cdot e^{-jr\Omega_0n}">

上式两边同时在一个信号周期内求和，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \sum_{n=0}^{N-1} x(n)e^{-jr\Omega_0n}=\sum_{n=0}^{N-1} \sum_{k=-\infty}^{+\infty} a_k \cdot e^{j(k-r)\Omega_0n}">

交换求和的顺序并化简，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \sum_{k=0}^{N-1} x(n)e^{-jr\Omega_0n}=\sum_{k=-\infty}^{+\infty} a_k \sum_{n=0}^{N-1} e^{j(k-r)\Omega_0n}">

由于上式右侧求和号内的复指数周期为<img src="http://www.forkosh.com/mathtex.cgi?\ N/(k-r)">，且在一个周期内对其积分，结果为零，所以有：

<img src="http://www.forkosh.com/mathtex.cgi?\ \sum_{n=0}^{N-1} e^{j(k-r)\Omega_0n}=\begin{cases} N,k=r\\ 0,k\not=r \end{cases}">

因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ \sum_{n=0}^{N-1} x(n)e^{-jr\Omega_0n}=a_k|_{k=r}N=a_rN">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(k)=\sum_{n=0}^{N-1} x(n)e^{-jk\Omega_0n}">

则

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\frac{1}{N}\sum_{k=-\infty}^{+\infty} X(k) \cdot e^{jk\Omega_0n}">

上述两式互为傅立叶级数对。

观察X(k)不难发现其周期性，周期为N：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(k+N)=\sum_{k=0}^{N-1} x(n)e^{-jk\frac{2\pi}{N}n} \cdot e^{-jN\frac{2\pi}{N}n}=\sum_{k=0}^{N-1} x(n)e^{-jk\frac{2\pi}{N}n}=X(k)">

## 离散时间非周期信号的傅里叶级数(DTFT, Discrete Time Fourier Transform)

对于非周期信号x(n)，我们只关注0~N-1之间的信号x'(n)，然后在坐标系上延拓，便形成了周期为N的周期信号x''(n)。由之前的分析可知：

<img src="http://www.forkosh.com/mathtex.cgi?\ x''(n)=\frac{1}{N}\sum_{k=0}^{N-1} X''(k) \cdot e^{jk\Omega_0n}">

其中

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(k)=\sum_{n=0}^{N-1} x''(n)e^{-jk\Omega_0n}">

因为在0~N-1区间内x(n)=x''(n)，其余区间内x(n)=0，因此：

<img src="http://www.forkosh.com/mathtex.cgi?\ X''(k)=\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\Omega_0n}">

将上式代入第一个公式，则有：

<img src="http://www.forkosh.com/mathtex.cgi?\ x''(n)=\frac{1}{N}\sum_{k=0}^{N-1} (\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\Omega_0n}) \cdot e^{jk\Omega_0n}">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\sum_{k=0}^{N-1} (\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\Omega_0n}) \cdot e^{jk\Omega_0n} \cdot \Omega_0">

因为：

<img src="http://www.forkosh.com/mathtex.cgi?\ \lim_{N \rightarrow +\infty}x''(n)=\lim_{\Omega_0 \rightarrow 0}x''(n)=x(n)">

所以根据积分的定义，将求和转换为积分形式：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\lim_{\Omega_0 \rightarrow 0} \frac{1}{2\pi}\sum_{k=0}^{N-1} (\sum_{n=-\infty}^{+\infty} x(n)e^{-jk\Omega_0n}) \cdot e^{jk\Omega_0n} \cdot \Omega_0">

<img src="http://www.forkosh.com/mathtex.cgi?\ =\frac{1}{2\pi}\int_{0}^{2\pi} (\sum_{n=-\infty}^{+\infty} x(n)e^{-j\Omega n})e^{j\Omega n}d\Omega">

若记：

<img src="http://www.forkosh.com/mathtex.cgi?\ X(\Omega)=\sum_{n=-\infty}^{+\infty} x(n)e^{-j\Omega n}">

则：

<img src="http://www.forkosh.com/mathtex.cgi?\ x(n)=\frac{1}{2\pi}\int_{0}^{2\pi} X(\Omega)e^{j\Omega n}d\Omega">

同样的，离散非周期信号的傅里叶变换也是周期的，周期为2pi。
