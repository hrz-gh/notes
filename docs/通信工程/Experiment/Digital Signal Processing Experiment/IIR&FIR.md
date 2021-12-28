# 离散时间滤波器设计

## 1. 实验项目名称

离散时间滤波器设计

## 2.实验目的

设计和分析一组滤波器，获得对设计过程的深入认识，并且掌握几种标准设计方法的特点，要求合组讨论，单独实验，2学时。

## 3. 实验内容与步骤

### IIR数字滤波器的设计
1. 脉冲响应不变法变换原理：
脉冲相应不变法将模拟滤波器的$s$平面变换成数字滤波器的$z$平面，从而将模拟滤波器映射成数字滤波器
IIR数字滤波器设计的重要环节是模拟低通滤波器的设计，典型的模拟低通滤波器由巴特沃思和切比雪夫(Ⅰ型和Ⅱ型)等滤波器。由模拟低通滤波器经过相应的复频率转换为$H(s)$，由$H(s)$经过脉冲相应不变法就得到了所需要的IIR数字滤波器$H(z)$。

2. 双线性变换法原理
为克服脉冲响应不变法产生频率相应的混叠失真，可以采用非线性频率压缩方法，使s平面与z平面建立了一一对应的单值关系，消除了多值变换性，也就消除了频谱混叠现象，这就是双线性变换法。

3. 实验内容：
    1. 要求通带截止频率$f_p = 3kHz$，通带最大衰减$a_p = 1dB$，阻带截止频率$f_s = 4.5kHz$，阻带最小衰减$a_s = 15dB$，采样频率$f_c = 30kHz$，用脉冲响应不变法设计一个切比雪夫数字低通滤波器，并图示滤波器的振幅特性，检验$\omega_p$，$\omega_s$对应的衰减。

    2. 用双线性变换法设计一个切比雪夫Ⅰ型数字高通滤波器。技术指标为:采样频率$f_c = 2kHz$，通带截止频率$f_p = 700Hz$，通带最大衰减$a_p \le 1dB$；阻带边缘频率$f_s = 500Hz$，最带最小衰减$a_s \ge 32dB$。

### 窗函数法设计FIR数字滤波器

1. 设计原理
FIR滤波器的设计问题，就是要是所设计的FIR滤波器的频率响应$H(e^{j\omega})$逼近所要求的理想滤波器的频率响应$H_d(e^{j\omega})$。逼近可在时域进行，也可在频域进行。窗函数法设计FIR数字滤波器实在时域进行的，用窗函数截取无限长的$h_d(n)$，这样得到的频率响应$H(e^{j\omega})$逼近于理想的频率响应$H_d(e^{j\omega})$。

2. 实验内容：
    1. 根据下列指标采用窗函数法设计低通数字滤波器，通带截止频率$\omega_p = 0.2\pi$，阻带截至频率$\omega_s = 0.3\pi$，通带最大衰减$0.25dB$，阻带最小衰减$50dB$。
    (1)分别利用汉明窗、布莱克曼窗和凯泽窗设计该滤波器，且滤波器具有线性相位。汇出脉冲相应h(n)及滤波器的频率响应。
    (2)增加N，观察过渡带和最大肩峰值的变化。

    2. 利用汉明窗设计数字微分器，
    $$H_d(\omega) = \begin{cases}
    j\omega ,& 0 < \omega \le \pi \\
    -j\omega ,& -\pi < \omega < 0   
    \end{cases}$$
    要求N=21，且滤波器具有线性相位。

## 4. 实验环境


MATLAB R2019b

## 5. 实验过程与分析程序文本

### IIR数字滤波器的设计

要求通带截止频率$f_p = 3kHz$，通带最大衰减$a_p = 1dB$，阻带截止频率$f_s = 4.5kHz$，阻带最小衰减$a_s = 15dB$，采样频率$f_c = 30kHz$，用脉冲响应不变法设计一个切比雪夫数字低通滤波器，并图示滤波器的振幅特性，检验$\omega_p$，$\omega_s$对应的衰减。

```matlab
clear;
wp = 2*pi*3*10^3;
ws = 2*pi*4.5*10^3;
ap = 1;
as = 15;
Fs = 30*10^3;                           %采样频率
wp1 = wp/Fs;
ws1 = ws/Fs;                            %数字频率
[N,WC] = cheb1ord(wp,ws,ap,as,'s');     %确切比雪夫低通阶数截止频率
[b,a] = cheby1(N,ap,WC,'low','s');      %调用函数设计多项式系数
[bz,az] = impinvar(b,a,Fs);             %脉冲响应不变法实现数字低通
w0 = [wp1,ws1];
Hx = freqz(bz,az,w0);                   %返回特定的的频率响应特性
[H,W] = freqz(bz,az);                   %得到bz到az完整的频率响应特性
dbHx = -20*log10(abs(Hx)/max(abs(H)))   %求wp,ws对应的衰减
plot(W,abs(H));
title('图1.1：切比雪夫数字低通滤波器');
xlabel('相对频率');ylabel('幅频');
grid on;
```

输出：

```
dbHx =
    1.0005   21.5790
```

结果如图1.1

用双线性变换法设计一个切比雪夫Ⅰ型数字高通滤波器。技术指标为:采样频率$f_c = 2kHz$，通带截止频率$f_p = 700Hz$，通带最大衰减$a_p \le 1dB$；阻带边缘频率$f_s = 500Hz$，最带最小衰减$a_s \ge 32dB$。

```matlab
fp=700;fs=500;ap=1;as=32;
wp=2*pi*fp;
ws=2*pi*fs;
Fc=2000;
wp1=wp/Fc;ws1=ws/Fc;
omp1=2*Fc*tan(wp1/2);
omps=2*Fc*tan(ws1/2);
[N,WC]=cheb1ord(omp1,omps,ap,as,'s');
[b,a]=cheby1(N,ap,WC,'high','s');
[bz,az]=bilinear(b,a,Fc);
w0=[wp1,ws1];
Hx=freqz(bz,az,w0);
[H,W]=freqz(bz,az);
dbHx=-20*log10(abs(Hx)/max(abs(H)))
plot(W,abs(H));
title('图1.2：切比雪夫1型高通滤波器')
xlabel('相对频率'),ylabel('幅频');
grid on;
```

输出：

```
dbHx =
    1.0000   33.1098
```

结果如图1.2

### 窗函数法设计FIR数字滤波器

根据下列指标采用窗函数法设计低通数字滤波器，通带截止频率$\omega_p = 0.2\pi$，阻带截至频率$\omega_s = 0.3\pi$，通带最大衰减$0.25dB$，阻带最小衰减$50dB$。
    
(1)分别利用汉明窗、布莱克曼窗和凯泽窗设计该滤波器，且滤波器具有线性相位。汇出脉冲相应h(n)及滤波器的频率响应。

$$N = \frac{4\pi}{\omega_s - \omega_p} = 40$$

```matlab
N=40;
wc=0.3;
figure(1)
subplot(211);
h=fir1(N-1,wc,'low',hamming(N));
stem(h);
title('图2.1.1：汉明窗低通滤波器的脉冲响应'),grid;
xlabel('n'),ylabel('幅度h(n)');
subplot(212);
[H,W]=freqz(h,1);
plot(W/pi,abs(H));
title('图2.1.2：汉明窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
figure(2)
subplot(211);
h=fir1(N-1,wc,'low',blackman(N));
stem(h);
title('图2.1.3：布莱克曼窗低通滤波器的脉冲响应'),grid;
xlabel('n'),ylabel('幅度h(n)');
subplot(212);
[H,W]=freqz(h,1);
plot(W/pi,abs(H));
title('图2.1.4：布莱克曼窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
figure(3)
subplot(211);
h=fir1(N-1,wc,'low',kaiser(N));
stem(h);
title('图2.1.5：凯泽窗低通滤波器的脉冲响应'),grid;
xlabel('n'),ylabel('幅度h(n)');
subplot(212);
[H,W]=freqz(h,1);
plot(W/pi,abs(H));
title('图2.1.6：凯泽窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
```

结果如图2.1.1-2.1.6

(2)增加N，观察过渡带和最大肩峰值的变化。

```matlab
N=51;
wc=0.3;
figure(1)
h=fir1(N-1,wc,'low',hamming(N));
[H,W]=freqz(h,1);
subplot(211);
plot(W/pi,abs(H));
title('图2.2.1：N=51时汉明窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
N=101;
h=fir1(N-1,wc,'low',hamming(N));
[H,W]=freqz(h,1);
subplot(212);
plot(W/pi,abs(H));
title('图2.2.2：N=101汉明窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
N=51;
figure(2)
h=fir1(N-1,wc,'low',blackman(N));
[H,W]=freqz(h,1);
subplot(211);
plot(W/pi,abs(H));
title('图2.2.3：N=51布莱克曼窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
N=101;
h=fir1(N-1,wc,'low',blackman(N));
[H,W]=freqz(h,1);
subplot(212);
plot(W/pi,abs(H));
title('图2.2.4：N=101布莱克曼窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
N=51;
figure(3)
h=fir1(N-1,wc,'low',kaiser(N));
[H,W]=freqz(h,1);
subplot(211);
plot(W/pi,abs(H));
title('图2.2.5：N=51凯泽窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
N=101;
h=fir1(N-1,wc,'low',kaiser(N));
[H,W]=freqz(h,1);
subplot(212);
plot(W/pi,abs(H));
title('图2.2.6：N=101凯泽窗低通振幅特性'),grid;
xlabel('相对频率'),ylabel('H(w)');
```

结果如图2.2.1-2.1.6

利用汉明窗设计数字微分器，

$$H_d(\omega) = \begin{cases}
j\omega ,& 0 < \omega \le \pi \\
-j\omega ,& -\pi < \omega < 0   
\end{cases}$$
要求N=21，且滤波器具有线性相位。

```matlab
clear;
dt = 1;
N = 21;
x_t = 0:dt:N-dt;
h1 = (-1+exp(1j.*pi.*x_t).*(1-1j.*pi.*x_t))./(x_t.^2)+(-1+exp(-1j.*pi.*x_t).*(1+1j.*pi.*x_t))./(x_t.^2);
h1(1)=10;
w=hamming(N/dt);
h=h1.*w';
figure(1)
subplot(311);
stem(x_t,h);
title('图2.3.1汉宁窗单位脉冲响应');
[H, W]=dtft(h,512);%DTFT
subplot(312);
plot(W/pi,abs(H));
title('图2.3.2：幅频特性');
xlabel('w'),ylabel('幅度');
subplot(313);
plot(W/pi,angle(H));
title('图2.3.3：幅频特性');
xlabel('w'),ylabel('弧度');
```

## 6. 实验结果总结

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_1_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_1_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_1_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_1_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_1_3.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_2_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_2_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_2_3.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab6/6_2_3.png)

</center>

## 7. 结果分析

### IIR数字滤波器的设计

1. `dbHx`中1.0005与21.5790为$w_p$，$w_s$处的衰减。$a_p = 1.0005$近似等于1，$a_s = 21.5790 > 15$故满足要求。
2. 双线性变换法设计一个切比雪夫Ⅰ型数字高通滤波器，`dbHx`中1.0000与33.1098为$w_p$，$w_s$处的衰减。$a_p = 1.0000$等于1，$as = 33.1098 > 32$故满足要求。

### 窗函数法设计FIR数字滤波器

1. 当增大$N$值时，振幅特性曲线过渡带的衰减将会变大，而最大肩峰值基本保持不变。
2. 由
   
   $$\frac{1}{2\pi}(\int_{-\pi}^{0} -j\omega e^{j\omega n} \mathrm{d} \omega + \int_{0}^{\pi} j\omega e^{j\omega n} \mathrm{d} \omega) = \frac{-1 + e^{j\pi n}(1 - j\pi n)}{n^2} + \frac{-1 + e^{-j\pi n}(1 + j\pi n)}{n^2}$$

   得到$h(n)$，再DTFT，最后得到图形，但微分器应该不具有线性相位，所以这道题没看懂，以后再说。

## 8.心得体会

1. 学会了用matlab函数设计数字滤波器。

2. 对IIR和FIR滤波器原理有更好的理解。