# 离散傅里叶变换

## 1. 实验项目名称

离散傅里叶变换

## 2.实验目的

加深对DFT性质的理解，拓展它们在DSP中的使用，要求1人1组，2学时。

## 3. 实验内容与步骤

实验内容：
1. 由DFT定义式：$X(k)=DFT[x(t)]=\sum_{n=0}^{N-1}x(n)W_N^{kn}$
将其写成矩阵方程表示为： $X=W_Nx$
其中，

$$x=\begin{bmatrix}
  x(0)\\
  x(1)\\
  \vdots\\
  x(N-1)
  \end{bmatrix}\ 
X=\begin{bmatrix}
  X(0)\\
  X(1)\\
  \vdots\\
  X(N-1)
\end{bmatrix}$$

$$W_N=\begin{bmatrix}
  1 & 1 & 1 & \dotsb & 1\\
  1 & W_N^1 & W_N^2 & \dotsb & W_N^{N-1}\\
  1 & W_N^2 & W_N^4 & \dotsb & W_N^{2(N-1)}\\
  \vdots & \vdots & \vdots & \ddots & \vdots\\
  1 & W_N^{(N-1)} & W_N^{2(N-1)} & \dotsb & W_N^{(N-1)\times(N-1)}
\end{bmatrix}$$

利用Matlab的矩阵运算功能，可编写出计算DFT的函数文件。

```matlab
function [ Xk ] = dft( xn,N )
%DFT Xk = dft(xn,N)
%Xk = 在0<=k<=N-1 间的DFT系数数组
%xn = N点有限长度序列
%N = DFT的长度
n = [0:1:N-1];
k = [0:1:N-1];		
WN = exp(-j*2*pi/N);
nk = n'*k;
WNnk = WN.^nk;			
Xk = xn * WNnk;			
```

请编写计算离散傅里叶反变换的函数文件。

2. 利用DFT做连续信号的频谱分析
DFT(实际中用FFT计算)可用来对连续信号和数字信号进行谱分析。在实际分析过程中，要对连续信号采样和截断，由此可能引起分析误差。

   1. 混叠效应
对连续信号进行频谱分析时，首先要对其采样，变成时域离散信号后才能用DFT（FFT）进行谱分析。采样速率fs必须满足采样定理，否则会在w=$\pi$（对应模拟频率f=fs/2）附近发生频谱混叠现象。

   2. 截断效应
处理实际信号序列x(n)时，一般总要将它截断为一有限长序列，长为N点，相当于乘以一个矩形窗形成有限长序列y(n)=x(n)w(n)。矩形窗函数其频谱有主瓣，也许许多副瓣，窗口越大，主瓣越窄，当窗口趋于无穷大时，就是一个冲击函数。时域的乘积对应于频域的卷积，所以，加窗后的频域实际是原信号频谱与矩形窗函数频谱的卷积，卷积的结果使频谱延伸到了主瓣以外，且一直延时到无穷。当窗口无穷大时，与冲击函数的卷积才是其本身，这时无畸变。这种差别表现对频谱分析的影响主要表现在如下两个方面：
频谱泄露:原来序列x(n)的频谱是离散谱线，经截断后，原来离散谱线向附近展宽泄露。显然，泄露使频谱变模糊，使谱分辨率降低。
谱间干扰:主谱线两边又很多旁谱，引起不同频率分量间干扰，这使谱分析产生较大偏差。程度与窗函数幅度谱主瓣宽度直接相关。

   3. 栅栏效应
我们知道，N点DFT是频率区间[0,2π]上对时域离散信号的频谱进行N点等间隔采样，而采样点之间的频谱函数是看不见的。


## 4. 实验环境

MATLAB R2019b

## 5. 实验过程与分析程序文本

### 1. IDFT函数

```matlab
function [ xn ] = idft( Xk,N )
%xn = N点有限长度序列
%N = DFT的长度
n = [0:1:N-1];              %n的行向量
k = [0:1:N-1];              %k的行向量
WN = exp(j*2*pi/N);         %Wn因子
nk = n'*k;                  %产生一个含nk值的N乘N维矩阵
WNnk = WN.^nk;              %IDFT矩阵
xn = 1/N*Xk * WNnk;
```
### 2. 利用DFT做连续信号的频谱分析

1. 已知连续周期信号$x(t)=cos(10\pi t)+2sin(18\pi t)$
   1. 确定信号的基频$\Omega$和基本周期
   基频为$\Omega=2\pi$ rad/s，基本周期为$2\pi/2\pi = 1$s

   2. 分析长度分别取$0.5T_p,1.5T_p,2T_p$时，利用FFT计算其幅度谱：对所得结果进行比较，总结应如何选取分析长度。

      ```matlab
      f1 = 5;%cos函数的频率
      f2 = 9;%sin函数的频率
      dt=1/100;
      t=[0:dt:1];
      x1=cos(2*pi*f1*t)+2*sin(2*pi*f2*t);
      figure(1)
      subplot(211);
      plot(t,x1);%样本信号的周期为1
      title('图1.1：实验样本信号');
      xlabel('时间（单位：秒）'),ylabel('幅度');
      subplot(212);
      xk1 = fft(x1); %FFT算法求得解
      stem(2*t,abs(xk1));
      title('1Tp分析长度时的FFT幅度谱');
      xlabel('频率(单位：pi)');ylabel('幅度');
      fs=10*f2;%以最大频率的10倍作为采样频率
      n0=0.5,n1=1.5,n2=2;%设定分析长度
      figure(2);
      L = fs*n0;
      n = 0:L-1;
      x = cos(2*pi*n*f1/fs)+2*sin(2*pi*n*f2/fs); 
      xk1 = fft(x); %FFT算法求得解
      subplot(211);
      stem(n/fs,x);
      title('图1.2：0.5Tp分析长度时的采样结果'),xlabel('时间（单位：秒）');
      subplot(212);
      stem(2*n/L,abs(xk1));
      title('0.5Tp分析长度时的FFT幅度谱');
      xlabel('频率(单位：pi)');ylabel('幅度');
      figure(3);
      L = fs*n1;
      n = 0:L-1;
      x = cos(2*pi*n*f1/fs)+2*sin(2*pi*n*f2/fs); 
      xk1 = fft(x); %FFT算法求得解
      subplot(211);
      stem(n/fs,x);
      title('图1.3：1.5Tp分析长度时的采样结果'),xlabel('时间（单位：秒）');
      subplot(212);
      stem(2*n/L,abs(xk1));
      title('1.5Tp分析长度时的FFT幅度谱');
      xlabel('频率(单位：pi)');ylabel('幅度');
      figure(4);
      L = fs*n2;
      n = 0:L-1;
      x = cos(2*pi*n*f1/fs)+2*sin(2*pi*n*f2/fs); 
      xk1 = fft(x); %FFT算法求得解
      subplot(211);
      stem(n/fs,x);
      title('图1.4：2Tp分析长度时的采样结果'),xlabel('时间（单位：秒）');
      subplot(212);
      stem(2*n/L,abs(xk1));
      title('2Tp分析长度时的FFT幅度谱');
      xlabel('频率(单位：pi)');ylabel('幅度');
      ```

    结果如图1.1-1.4.

2. 对模拟信号$x_a(t)=2sin(4\pi t)+5cos(8\pi t)$,以采样T=0.01秒采样，分别选取N=40，N=50，N=60得到x(n),用N点DFT得到对$x_a(t)$幅度谱的估计并比较结果。

```matlab
dt=1/100;
t=[0:dt:0.5];%样本信号的周期为1
f1=2;
f2=4;
xt=2*sin(2*pi*f1*t)+5*cos(2*pi*f2*t);
%画布分割
figure(1);
stem(t,xt)
title('图2.1：采样信号信号');
xlabel('时间（单位：秒）'),ylabel('幅度');
%画布分割
figure(2);
subplot(311);
xk1 = fft(xt,40); %FFT算法求得解
n=[0:1:40-1]
L=length(n);
stem(n/L,abs(xk1));
title('图2.2.1：40个采样点的DFT幅度谱');
xlabel('频率(单位：pi)');ylabel('幅度');
subplot(312);
xk1 = fft(xt,50); %FFT算法求得解
n=[0:1:50-1]
L=length(n);
stem(n/L,abs(xk1));
title('图2.2.2：50个采样点的DFT幅度谱');
xlabel('频率(单位：pi)');ylabel('幅度');
subplot(313);
xk1 = fft(xt,60); %FFT算法求得解
n=[0:1:60-1]
L=length(n);
stem(n/L,abs(xk1));
title('图2.2.3：60个采样点的DFT幅度谱');
xlabel('频率(单位：pi)');ylabel('幅度');
```
结果如图2.1-2.2

## 6. 实验结果总结

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/4_1_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/4_1_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/4_1_3.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/4_1_4.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/4_2_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/4_2_2.png)

</center>

## 7. 结果分析

### 1. IDFT函数

只需要在DFT函数基础上把单位复数根改为`wN=exp(1j*2*pi/N)`，最后结果再乘1/N。

### 2. 利用DFT做连续信号的频谱分析

1. 当截取长度为$1T_p$与$2T_p$时，可得到单一谱线的频谱，而长度为$0.5T_p$和$1.5T_p$时出现了频谱泄漏现象。因而当分析长度不为样本周期的整数倍时，将会出现频率泄露现象，无法得到单一谱线的频谱。

2. 只有当截断点数为样本信号完整周期的采样点数的整数倍时，才不会发生频率泄露现象，而本题的基本周期为$T=0.5s$，所以只有当$N=50$时，所得频谱图像为单一的谱线。

## 8.心得体会

1. 动手实现了IDFT，对其记忆加深。
   
2. 了解到了频谱泄露现象，以及避免其发生的方法。