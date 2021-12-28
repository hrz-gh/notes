# 谱分析

## 1. 实验项目名称

谱分析

## 2.实验目的

研究不同类型的窗函数，研究一些不同的方法来测试窗的性能；专注于有关窄带信号的几个不同的情形，要求合组讨论、单独实验，2学时。

## 3. 实验内容与步骤

实验内容：
信号是无限长的，而在进行信号处理时只能采用有限长信号，所以需要将信号“截断”。在信号处理中，“截断”被看成是用一个有限长的“窗口”看无限长的信号，或者从分析的角度是无限长的信号x(t)乘以一个有限长的窗函数w(t)，由傅里叶变换性质可知

$$x(t)\Leftrightarrow \frac{1}{2\pi}X(j\omega)W(j\omega)$$

如果是x(t)是频宽有限信号，而w(t)是频宽无限函数，截断后的信号也必是频宽无限信号，从而产生所谓的频谱泄露。频谱泄露是不可避免的，但要尽量减小，因此设计了不同的窗函数满足不同用途的要求。从能量的角度，频谱泄露也是能量泄露，因为加窗后，使原来的信号集中在窄带内的能量分散到无限的频宽范围。
Matlab中提供了8种窗函数：矩形窗、汉宁窗、汉明窗、巴特利特窗、布莱克曼、triang窗、kaiser窗、切比雪夫窗
各种窗函数的幅频响应都存在明显的主瓣和旁瓣，主瓣频宽与旁瓣频宽的特性决定窗函
数的应用。不同的窗函数在这两方面的特点是不相同的。如blcakman窗具有最宽的主瓣，而chebyshev窗具有最窄的主瓣等。
主瓣的频宽还与窗的长度N有关，增加窗长度N将缩小窗函数主瓣宽度，但不能减小旁瓣幅值衰减相对值（分贝数），这个值是由窗函数决定的。
1.	用Matlab编程绘制各种窗函数的形状。
2.	用Matlab编程绘制各种窗函数的幅频响应。
3.	绘制矩形窗的幅频相应，窗长度分别为：N=10，N=20，N=50，N=100。
4.	已知周期信号

$$x(t)=0.75+3.4cos(2\pi ft)+2.7cos(4\pi ft)+1.5sin(3.5\pi ft)+2.5sin(7\pi ft)$$

其中，$f=\frac{25}{16}$Hz，若截断的时间长度分别为信号周期的0.9倍和1.1倍，试绘制和比
较采用下面窗函数提取的x(t)的频谱。
(1)矩形窗 (2)汉宁窗 (3)汉明窗 (4)巴特利特窗 (5)布莱克曼窗 (6)triang窗 (7)kaiser窗
(8)切比雪夫窗

## 4. 实验环境

MATLAB R2019b

## 5. 实验过程与分析程序文本

### 1. 用Matlab编程绘制各种窗函数的形状

```matlab
N=100;
w1=boxcar(N);
figure(1);
stem(w1);
title('图1.1：矩形窗boxcar');
xlabel('n'),ylabel('w1');
w2=hanning(N);
figure(2);
stem(w2);
title('图1.2：汉宁窗Hanning');
xlabel('n'),ylabel('w2');
w3=hamming(N);
figure(3);
stem(w3);
title('图1.3：汉明窗Hamming');
xlabel('n'),ylabel('w3');
w4=bartlett(N);
figure(4);
stem(w4);
title('图1.4：巴特利特窗bartlett');
xlabel('n'),ylabel('w4');
w5=blackman(N);
figure(5);
stem(w5);
title('图1.5：布莱克曼窗blackman');
xlabel('n'),ylabel('w5');
w6=triang(N);
figure(6);
stem(w6);
title('图1.6：triang窗');
xlabel('n'),ylabel('w6');
w7=kaiser(N);
figure(7);
stem(w7);
title('图1.7：kaiser窗');
xlabel('n'),ylabel('w7');
w8=chebwin(N);
figure(8);
stem(w8);
title('图1.8：切比雪夫窗chebwin');
xlabel('n'),ylabel('w8');
```

结果如图1.1-1.8

### 2. 用Matlab编程绘制各种窗函数的幅频响应

```matlab
clear;
N=100;%选择窗函数的长度
subplot(421);
[H W]=dtft(boxcar(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.1：boxcar的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(422);
[H W]=dtft(hanning(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.2：Hanning的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(423);
[H W]=dtft(hamming(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.3：Hamming的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(424);
[H W]=dtft(bartlett(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.4：bartlett的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(425);
[H W]=dtft(blackman(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.5：blackman的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(426);
[H W]=dtft(triang(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.6：triang的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(427);
[H W]=dtft(kaiser(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.7：kaiser的幅频响应');
xlabel('w'),ylabel('幅度');
subplot(428);
[H W]=dtft(chebwin(N),1024);%DTFT
plot(W/pi,abs(H));
title('图2.8：hebwin的幅频响应');
xlabel('w'),ylabel('幅度'); 
```

结果如图2.1-2.8

### 3. 绘制矩形窗的幅频相应

```matlab
clear;
N=[10,20,50,100];
w1=boxcar(N(1));
subplot(411);
[H,W]=dtft(w1,1024);
plot(W/pi,abs(H));
title('图3.1：长度为10的矩形窗幅频特响应');
xlabel('频率（单位：pi）'),ylabel('幅度');
w2=boxcar(N(2));
subplot(412);
[H,W]=dtft(w2,1024);
plot(W/pi,abs(H));
title('图3.2：长度为20的矩形窗幅频特响应');
xlabel('频率（单位：pi）'),ylabel('幅度');
w3=boxcar(N(3));
subplot(413);
[H,W]=dtft(w3,1024);
plot(W/pi,abs(H));
title('图3.3：长度为50的矩形窗幅频特响应');
xlabel('频率（单位：pi）'),ylabel('幅度');
w4=boxcar(N(4));
subplot(414);
[H,W]=dtft(w4,1024);
plot(W/pi,abs(H));
title('图3.4：长度为100的矩形窗幅频特响应');
xlabel('频率（单位：pi）'),ylabel('幅度');
```

四种长度分别对应图3.1-3.4

### 4. 绘制和比较采用各种窗函数提取的x(t)的频谱

令1/f=T,则4个正弦分量的周期分别为T，1/2T，4/7T和2/7T，
则x（t）的基本周期为14T，

```matlab
clear;
f=25/16;        %实验信号的周期为25/16
T=14*(1/f);
fs=100;         %采样频率
f1=round(0.9*T*fs);
f2=round(1.1*T*fs);
t1=0:f1-1;
t2=0:f2-1;
xt1=0.75+3.4*cos(2*pi*f.*t1/fs)+2.7*cos(4*pi*f.*t1/fs)+1.5*sin(3.5*pi*f.*t1/fs)+2.5*sin(7*pi.*t1/fs);
xt2=0.75+3.4*cos(2*pi*f.*t2/fs)+2.7*cos(4*pi*f.*t2/fs)+1.5*sin(3.5*pi*f.*t2/fs)+2.5*sin(7*pi.*t2/fs);
figure(1);
subplot(211),grid;
w11=boxcar(f1);
x1=w11.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.1.1：0.9T0矩形窗boxcar的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
w12=boxcar(f2);
x2=w12.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.1.2：1.1T0矩形窗boxcar的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(2);
w21=hanning(f1);
w22=hanning(f2);
subplot(211),grid;
x1=w21.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.2.1：0.9T0汉宁窗Hanning的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w22.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.2.2：1.1T0汉宁窗Hanning的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(3);
w31=hamming(f1);
w32=hamming(f2);
subplot(211),grid;
x1=w31.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.3.1：0.9T0汉明窗Hamming的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w32.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.3.2：1.1T0汉明窗Hamming的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(4);
w41=bartlett(f1);
w42=bartlett(f2);
subplot(211),grid;
x1=w41.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.4.1：0.9T0巴特利特窗bartlett的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w42.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.4.2：1.1T0巴特利特窗bartlett的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(5);
w51=blackman(f1);
w52=blackman(f2);
subplot(211),grid;
x1=w51.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.5.1：0.9T0布莱克曼窗blackman的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w52.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.5.2：1.1T0布莱克曼窗blackman的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(6);
w61=triang(f1);
w62=triang(f2);
subplot(211),grid;
x1=w61.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.6.1：0.9T0的triang窗的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w62.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.6.2：1.1T0的triang窗的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(7);
w71=kaiser(f1);
w72=kaiser(f2);
subplot(211),grid;
x1=w71.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.7.1：10.9T0的kaiser窗的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w72.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.7.2：1.1T0的kaiser窗的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
figure(8);
w81=chebwin(f1);
w82=chebwin(f2);
subplot(211),grid;
x1=w81.*xt1'; 
[H,W]=dtft(x1,1024);
plot(W/pi,abs(H));
title('图4.8.1：0.9T0切比雪夫窗chebwin的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
subplot(212),grid;
x2=w82.*xt2'; 
[H,W]=dtft(x2,1024);
plot(W/pi,abs(H));
title('图4.8.2：1.1T0切比雪夫窗chebwin的频谱'),xlabel('频率：（单位：pi）'),ylabel('幅度');
```

结果如图4.1.1-4.8.2

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_3.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_4.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_5.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_6.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_7.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_1_8.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_3.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_1.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_2.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_3.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_4.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_5.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_6.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_7.png)

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/5_4_8.png)

</center>

## 7. 结果分析

绘制了8种窗函数的形状，在绘制周期函数时，无论0.9还是1.1T都发生了频谱泄露现象，推测只要不是整数倍都会有频谱泄露现象的发生

## 8.心得体会

1. 动手实现了8种窗函数的形状，对其形状加深了印象。
2. 了解到了窗函数会导致频谱泄露现象。