# 抽样

## 1. 实验项目名称

抽样

## 2. 实验目的

研究抽样过程，分析产生混叠效应的原因，实现不同重建方案，要求1人1组，2学时。

## 3. 实验内容与步骤

1. 抽样引起的混叠

    对连续正弦信号考虑下面表示式：

    $$x(t)=sin(2\pi f_0+\phi)$$

    可以按抽样频率$f_s=1/T_s$对x(t)抽样来获得离散时间信号

    $$x[n]=x(t)|_{t=nT_s}=x(t)|_{t=n/f_s}=sin(2\pi\frac{f_0}{f_S}n+\phi)$$

    $f_0$= 500Hz,  分别取100Hz,1KHz,10KHz,绘出x[n]及其DTFT

2. 抽样的频域视图

   a. $x_a(t)=e^{-1000|t|}$, 求出并绘制其傅里叶变换

   b. 以5000HZ和1000HZ分别对其采样得到x1(n),x2(n);画出他们的DTFT并与$x_a(j\Omega)$比较

3. 从样本重建信号

   (1)拟合为正弦波

    假设三个抽样样本符合下列形式的正弦波形：

    $$x(t)=Acos(\omega t+\phi)$$

    已知x(0)、x(1)和x(2)，这些信息足以确定$A,\omega,\phi$吗？能建立有关的方程吗？总能解出这些方程吗？如果不能，给出不能求解处的具体数值。

    (2)线性与多项式内插

    a．使用matlab,用直线段连接样本。在间隔0.01秒的细密网格上绘出结果，解释plot指令将会如何自动的绘出这一结果。
   
    b．将三角形冲激响应与三个样本进行卷积，但首先要在每两个样本之间插入四个零点，并令冲激响应为0.2，0.4，0.6，0.8，1.0，0.8，0.6，0.4，0.2。证明如果假设在t=-1和t=3的样本为零，上面的结果与线性插值相同。

    c. 使用MATLAB,将这三个数据点拟合为二阶多项式(见polyfit与polyval指令)。以细密网格对$-5\le t\le 5$绘出这个多项式。在实际意义上，这一曲线是否可实现？它是否能很好地在$0\le t\le 2$区间以外扩展信号值？

    (3)	理想低通滤波器

    a.假设只有有限数量的样本是非零值，且只需在有限时间区间上进行信号重建，写出sinc内插表达式。

    b.对t=0处的数值为1的单点样本进行插值，绘出大约从-5到+5的结果。它应该与sinc函数形状一致。

    c.现在对sinc函数内插及实验内容1中的三点情形进行插值，将其结果与拟合为正弦波的结果相比较

4.	设定带宽的选择

    带限于某频率$f_B$的信号可以用$f_S=2f_B$进行抽样，并可以由截止频率为$f_B$的理想低通重建滤波器恢复，此结论对于带限于$fb$的第二个信号同样成立，其中$f_b$小于$f_B$,这是因为带限于$f_b$ 的信号也带限于$f_B$。同样，带限于$f_b$的信号也可以用$f_S$ 抽样并由截止频率为$f_b$ 的理想低通重建滤波器恢复，该理想低通重建滤波器的冲激响应（sinc函数）比截止频率为$f_B=f_S/2$的理想低通重建滤波器的冲激响应更宽。能否使用截止频率为$f_b < f_S/2$的理想低通重建滤波器的重建响应对带限于$f_b$并以$f_S$抽样得到的信号样本进行插值？

## 4. 实验环境

MATLAB R2019b

## 5. 实验过程与分析程序文本

### 1. 抽样引起的混叠

实验内容：

$f_0$=500Hz,$f_s$分别取100Hz,1KHz,10KHz,绘出x[n]及其DTFT

```matlab
%100HZ抽样结果
clear;
fs=100;%采样频率
f0=500;
dt=1/fs;
w0=0;%初始相位
t=0:dt:15/500;
xt=sin(2*pi*f0*t+w0);%函数表达式
subplot(311);
stem(t,xt);
grid on;
xlabel('时间/秒'),ylabel(' 幅度'); 
title('以100HZ抽样所得信号');
[X,W]=dtft(xt,1000);%dtft变换
subplot(312);
plot(W/2/pi,abs(X));
grid,title('抽样信号的响应')
xlabel('频率/2pi）'),ylabel('幅度');
subplot(313);
plot(W/2/pi,180/pi*angle(X));
grid,title('抽样信号的相位')
xlabel('频率/2pi）'),ylabel('相位/度）');
```

同理，当$f_s$分别取1KHz,10KHz时，把代码中`fs=100`分别改为`fs=1000`和`fs=10000`即可。

结果如图1.1.1 ,1.1.2 ,1.1.3所示。

### 2. 抽样的频域视图

a. $x_a(t)=e^{-1000|t|}$, 求出并绘制其傅里叶变换

```matlab
dt=1/10000;
t=-0.05:dt:0.05;
xt=exp(-1000*abs(t));
figure(1);
subplot(211);
plot(t,xt),grid on;
title('样本信号'),xlabel('时间/秒'),ylabel('幅度');
subplot(212);
fmagplot(xt,dt);
```

结果如图2.1

b. 以5000HZ和1000HZ分别对其采样得到x1(n),x2(n);画出他们的DTFT并与$x_a(j\Omega)$比较

```matlab
%5khz抽样所得的信号
figure(1);
fs=5000;
dt=1/fs;
t=-0.05:dt:0.05;%5khz抽样的时间范围
xt=exp(-1000*abs(t));
subplot(311),stem(t,xt),grid on;
xlabel('时间/秒'),ylabel('幅度'); 
title('以5KHZ抽样的信号');
[X,W]=dtft(xt,10000);
subplot(312);
plot(W/2/pi,abs(X));
grid,title('幅频特性曲线')
xlabel('频率/2pi'),ylabel('幅度');
subplot(313);
plot(W/2/pi,180/pi*angle(X),'r');
grid,title('Xa的相频特性曲线')
xlabel('频率/2pi'),ylabel('相位/度');
```

对于1Khz的采样把`fs=5000`改为`fs=1000`即可。

结果如图2.2.1 ,2.2.2

### 3. 从样本重建信号

#### 1. 拟合为正弦波

假设三个抽样样本符合下列形式的正弦波形：

$$x(t)=Acos(\omega t+\phi)$$

已知x(0)、x(1)和x(2)，这些信息足以确定$A,\omega,\phi$吗？能建立有关的方程吗？总能解出这些方程吗？如果不能，给出不能求解处的具体数值。

能，直接解方程，然后画图，使用书中的情形：

$$x(0)=2,x(1)=1,x(2)=-1$$

```matlab
y = [2,1,-1];
xdata = [0,1,2];
syms A omega phi
%三元方程组
eq1 = A*cos(omega*xdata(1)+phi)-y(1);
eq2 = A*cos(omega*xdata(2)+phi)-y(2);
eq3 = A*cos(omega*xdata(3)+phi)-y(3);
[A ,omega ,phi] = solve(eq1 ,eq2 ,eq3);
dt = 1/1000;
x = (xdata(1):dt:xdata(length(xdata)));
%循环，有几个解画几张图
for i = 1:length(A)
   figure(i);
   plot(x,A(i)*cos(omega(i).*x+phi(i))),grid on;
   %添加注释，显示三个参数值
   text(0.05,0,'omega=');
   text(0.05,-0.15,'A=');
   text(0.05,-0.3,'phi=');
   text(0.3,0,char(omega(i)));
   text(0.3,-0.15,char(A(i)));
   text(0.3,-0.3,char(phi(i)));
end 
```

共有4组解，结果如图3.1.1 ,3.1.2 ,3.1.3 ,3.1.4

#### 2. 线性与多项式内插

a．使用matlab,用直线段连接样本。在间隔0.01秒的细密网格上绘出结果，解释plot指令将会如何自动的绘出这一结果。

```matlab
clear;
x0=2,x1=1,x2=-1;%题目提供的三个样本点
y=zeros(1,201);
y(1:101)=(x0:-0.01:x1);
y(101:201)=(x1:-0.02:x2);
t=(0:0.01:2);
plot(t,y);
grid on;
xlabel('时间/秒'),ylabel('幅度'),title('线性内插');
```
结果如图3.2.1

b．将三角形冲激响应与三个样本进行卷积，但首先要在每两个样本之间插入四个零点，并令冲激响应为0.2，0.4，0.6，0.8，1.0，0.8，0.6，0.4，0.2。证明如果假设在t=-1和t=3的样本为零，上面的结果与线性插值相同。

```matlab
clear;
dt=1/5;%每五个点代表长度1
n=[0,0.2,0.4,0.6,0.8,1.0,0.8,0.6,0.4,0.2,0];%三角冲激响应
x=[2,0,0,0,0,1,0,0,0,0,-1];
y=conv(n,x);%卷积运算
subplot(2,1,1)
n=(-1:dt:3);
stem(n,y),grid on;
title('三角形冲激响应卷积内插');
subplot(2,1,2)
y2=[0,2,1,-1,0];
x2=(-1:3);%依据样本点创建的横纵序列
plot(x2,y2);
grid on;
title('线性内插');
```
结果如图3.2.2

c. 使用MATLAB,将这三个数据点拟合为二阶多项式(见polyfit与polyval指令)。以细密网格对$-5\le t\le 5$绘出这个多项式。在实际意义上，这一曲线是否可实现？它是否能很好地在$0\le t\le 2$区间以外扩展信号值？

```matlab
x0=2,x1=1,x2=-1;%题目所提供的三个样本点
y=[x0,x1,x2];
x=[0,1,2];
t=(-5:0.1:5);
C=polyfit(x,y,2);
Z=polyval(C,t);
plot(x,y,'r*',t,Z,'b'),grid on;
xlabel('时间/秒'),ylabel('幅度'),title('二阶多项式拟合内插');
```

结果如图3.2.3

#### 3. 理想低通滤波器

a.假设只有有限数量的样本是非零值，且只需在有限时间区间上进行信号重建，写出sinc内插表达式。

设有限样本函数长度为N，

$$x_a(t)=\sum_{n=0}^{N-1}x_a(t)\frac{sin(\pi(t-nT_s/T_s))}{\pi(t-nT_s/T_s)}$$

b.对t=0处的数值为1的单点样本进行插值，绘出大约从-5到+5的结果。它应该与sinc函数形状一致。

```matlab
clear;
T=1;
dt=0.01;
t= (-5:dt:5);
x=1;
sinc = (sin(pi.*t./T))./(pi.*t./T);%sinc内插表示式
x_a=conv(x,sinc);
plot(t,x_a),grid on;
title('插值重建结果'),xlabel('x'),ylabel('y');
```

结果如图3.3.1

c.现在对sinc函数内插及实验内容1中的三点情形进行插值，将其结果与拟合为正弦波的结果相比较

```matlab
clear;
x0=2;x1=1;x2=-1;
x=[x0,x1,x2];
T=1;
dt=0.01;
t= (-5:dt:5);
x_a=zeros(1,1201);%移位相加共1201个点
sinc = (sin(pi.*t./T))./(pi.*t./T);
for n = 0:2%移位相加
   x_a((1+n*100):(1+n*100+1000))=\
   x_a((1+n*100):(1+n*100+1000))+x(n+1)*(sin(pi.*t./T))./(pi.*t./T);
end
x_a=x_a(501:701);%截取t=0到2对应的值
t_a=(0:dt:2);
plot(t_a,x_a),grid on;
title('插值重建结果'),xlabel('x'),ylabel('y');
```

结果如图3.3.2

#### 4. 设定带宽的选择

解决下面的问题：带限于某频率$f_B$的信号可以用$f_S=2f_B$进行抽样，并可以由截止频率为$f_B$的理想低通重建滤波器恢复，此结论对于带限于$fb$的第二个信号同样成立，其中$f_b$小于$f_B$,这是因为带限于$f_b$ 的信号也带限于$f_B$。同样，带限于$f_b$的信号也可以用$f_S$ 抽样并由截止频率为$f_b$ 的理想低通重建滤波器恢复，该理想低通重建滤波器的冲激响应（sinc函数）比截止频率为$f_B=f_S/2$的理想低通重建滤波器的冲激响应更宽。能否使用截止频率为$f_b < f_S/2$的理想低通重建滤波器的重建响应对带限于$f_b$并以$f_S$抽样得到的信号样本进行插值？

可以，截至频率fb 小于采样频率fS一半，频域无混叠现象，因此可以使用截止频率为fb < fS /2的理想低通重建滤波器的重建响应对带限于fb 并以fS 抽样得到的信号样本进行插值。

## 6. 实验结果总结

<center>

![图1.1.1](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_1_1_1.png)

图1.1.1

![图1.1.2](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_1_1_2.png)

图1.1.2

![图1.1.3](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_1_1_3.png)

图1.1.3

![图2.1](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_2_1.png)

图2.1

![图2.2.1](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_2_2_1.png)

图2.2.1

![图2.2.2](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_2_2_2.png)

图2.2.2

![图3.1.1](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_1_1.png)

图3.1.1

![图3.1.2](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_1_2.png)

图3.1.2]

![图3.1.3](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_1_3.png)

图3.1.3

![图3.1.4](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_1_4.png)

图3.1.4

![图3.2.1](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_2_1.png)

图3.2.1

![图3.2.2](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_2_2.png)

图3.2.2

![图3.2.3](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_2_3.png)

图3.2.3

![图3.3.1](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_1.png)

图3.3.1

![图3.3.2](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab3/3_3_3_2.png)

图3.3.2

</center>

## 7. 结果分析

### 1. 抽样引起的混叠

只有当(采样频率$\ge$样本频率的2倍)时，才能较好的还原信号。100HZ时无法重现信号，1KHZ时能重现样本信号的局部关系，10KHZ时能较完整的重现样本信号。

### 2. 抽样的频域视图

***a.*** 偶函数，在$|\Omega|>4000\pi$时，幅值几乎为零。

***b.*** 不同采样频率的DTFT与$X(j\Omega)$比较，它们仅在幅值上有差异，这是因为采样点数增加，序列长度增加，幅值增加。

### 3. 从样本重建信号

#### 1. 拟合为正弦波

能求出解，三个未知数，三个方程，只不过有4组解，利用matlab解方程组，结果如图3.1.1 ,3.1.2 ,3.1.3 ,3.1.4

#### 2. 线性与多项式内插

***a.*** plot指令通过把每两个点连成一条直线，绘出结果。

***b.*** 通过三角冲激后，和线性插值结果相同。

***c.*** 三个点刚好能唯一确定一个二阶多项式，实际中不能实现这种信号，只能无限接近，且不能很好在$0\le t\le 2$扩展信号值，（衰减迅速）。
#### 3. 理想低通滤波器

***c.*** 插值结果接近正弦波。

#### 4. 设定带宽的选择

可以，截至频率fb 小于采样频率fS一半，频域无混叠现象。

## 8.心得体会

1. 对于采样频率增加，DTFT结果幅度增加的现象有了理解。

2. 对不同方式的插值方法重建信号结果进行了分析，加深了理解。
   
3. 直接用for循环写了卷积，认识到其实质为移位不同权值相加。