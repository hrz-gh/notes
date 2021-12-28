# 基于51的定时闹钟

## 《单片机应用设计》课程设计总结报告

</center>

**课程设计名称**：定时闹钟
**学生姓名**： **班级**： **学号**：

### 研究意义和实现功能指标

#### 研究意义

随着人们物质生活水平的提高，各种智能家居进入人们的日常生活当中。在日常生活当中，我们不仅需要闹钟给我们定时提醒，还需要使用作为定时器控制一些不具备定时功能的家电的使用，从而提高生活的便利性，这样的研究是具有意义的。

#### 课程设计要求

1. 利用3个按键调整现在时间，闹铃时间以及闹钟的开关。
2. 使用LCD12864显示现在时间，闹铃时间以及闹钟的状态。
3. 喇叭播放闹铃音乐，继电器定时控制家电的开关。

#### 设计特色分析

1. 灵活性好，可移植性高，只需要经过极少量的改动，可适应大多数传统家电的智能化使用。
2. 具有实时显示，夜间使用的能力。
3. 喇叭可自定义音乐播放。
4. 成本极低。

#### 使用方法

程序执行后工作指示灯LED闪动，表示程序开始执行，现在和闹铃时间都显示为“00：00”，按下操作键K1-K3动作如下：
1. K1—设置现在的时间。
2. K2—设置闹铃的时间。
3. K3—闹铃ON/OFF的状态设置，闹钟响铃时，可通过此按键关闭。
   

当设置时间时，闹钟暂停计时，设置当前时间或闹铃时间如下。
1. K1—时调整。
2. K2—分调整。
3. K3—设置完成


#### 技术指标

1. 时间准确度
2. 电路功耗，电池续航能力

#### 总设计框图

按照系统设计功能的要求，确定系统由6个模块组成：主控制器、闹铃电路、电源电路、按键电路、显示电路和继电器开关电路，结构框图如图所示。

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/总设计框图.png)

</center>

#### LCD1264说明

其中LCD12864使用ST7920控制器，自带中文字库，可显示汉字及图形，内置8192个中文汉字（16X16点阵）、128个字符（8X16点阵）及64X256点阵显示RAM（GDRAM）。
主要技术参数和显示特性:
电源：VDD 3.3V~+5V(内置升压电路，无需负压)；
显示内容：128列× 64行
显示颜色：黄绿
LCD类型：STN
与MCU接口：8位或4位并行/3位串行
配置LED背光
多种软件功能：光标显示、画面移位、自定义字符、睡眠模式等

##### 并行写时序

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/12864write.png)

##### 并行读时序

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/12864read.png)

##### GDRAM地址

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/12864position.png)

### 硬件电路设计实现

#### 原理图

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/principle.bmp)

</center>

#### 模块说明

##### 按键模块

按键K1-K3分别连接至P3.0-P3.2口，然后并联接地，每当相应按键按下时，对应I/O口接受到低电平，完成相应功能。

##### 闹铃，继电器模块

单片机上电I/O口为高电平，其相应的PNP管工作在截止状态，闹铃触发后，I/O口拉低PNP管工作在放大状态，喇叭和继电器就开始工作。

### 软件设计

#### 主要数据结构

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/DataMembers-my_clock.png)

#### 函数调用关系图

其中`init`为初始化函数，`keyscan`为按键扫描函数，`play_song`为音乐播放函数，`clock_cmp`为时间对比函数，`time_adjust`为时间调整函数，`clock_display`为时钟显示函数。

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/Butterfly-main.png)

</center>

#### 主要函数的控制流程图

##### `main`函数

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-main.png)

</center>

##### `init`函数

对LCD12864，定时器0，1，喇叭以及继电器I/O口的初始化，`wela`和`dula`仅在调试中使用。

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-init.png)

</center>

##### `keyscan`函数

按顺序对三个按键进行扫描。

<center>

<img src="http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-keyscan.png" height=1500px>

</center>

##### `play_song`函数

`song[]`为歌曲存放的数组，其偶数位为闹铃频率，奇数位为对应频率的播放时间。

<center>

<img src="http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-play_song.png" height=1600px>

</center>

##### `clock_cmp`函数

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-clock_cmp.png)

</center>

##### `time_adjust`函数

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-time_adjust.png)

</center>

##### `clock_display`函数

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/QuickAlarm/ControlFlow-clock_display.png)

</center>

### 调试过程和设计效果

#### 调试过程

1. 在*protues*中完成电路原理图的绘制
2. 写好主要代码框架
3. 在*protues*完成主要功能的仿真
4. 完成单片机最小系统，按键和*lcd*接口的焊接
5. 用*led*灯测试*STC89C52*是否工作
6. 检验*lcd12864*显示无误
7. 检验3个按键控制无误
8. 焊接三极管与喇叭
9. 检验闹铃功能实现
10. 焊接三极管与继电器
11. 检验继电器控制功能的实现
12. 整体检验无误

#### 设计效果

*lcd12864*显示效果：
第一行为闹铃时间，第二行为现在时间，右下角为闹钟状态

按键1,2调整闹铃时间，按键3开启闹铃：

闹铃时间和现在时间相等且闹钟为开启状态时，继电器切换状态，绿灯亮，喇叭播放一段音乐：

再按按键3，闹钟关闭，喇叭停止播放，但继电器继续工作直到下次闹铃：

作者与作品

### 元器件表和成本核算

<table>
    <tr>
        <td>序号</td>
        <td>器件名称</td>
        <td>型号规格</td>
        <td>数量</td>
        <td>价格</td>
    </tr>
    <tr>
        <td>1</td>
        <td>STC89C52</td>
        <td>40脚直插</td>
        <td>1个</td>
        <td>3.13*1元</td>
    </tr>
    <tr>
        <td>2</td>
        <td>晶振</td>
        <td>11.0592MHz</td>
        <td>1个</td>
        <td>0.225*1元</td>
    </tr>
    <tr>
        <td>3</td>
        <td>电容</td>
        <td>33pf</td>
        <td>2个</td>
        <td>0.024*2元</td>
    </tr>
    <tr>
        <td>4</td>
        <td>电容</td>
        <td>10uf</td>
        <td>1个</td>
        <td>0.261*1元</td>
    </tr>
    <tr>
        <td>5</td>
        <td>电阻</td>
        <td>200 1K 510K 10K</td>
        <td>4个</td>
        <td>0.12*5元</td>
    </tr>
    <tr>
        <td>6</td>
        <td>S9012</td>
        <td>直插</td>
        <td>2个</td>
        <td>0.0402*2元</td>
    </tr>
    <tr>
        <td>7</td>
        <td>继电器</td>
        <td>5脚直插</td>
        <td>1个</td>
        <td>2.00*1元</td>
    </tr>
    <tr>
        <td>8</td>
        <td>喇叭</td>
        <td>8欧0.5w</td>
        <td>1个</td>
        <td>1.21*1元</td>
    </tr>
    <tr>
        <td>9</td>
        <td>轻触开关</td>
        <td>6*6*5</td>
        <td>4个</td>
        <td>0.042*4元</td>
    </tr>
    <tr>
        <td>10</td>
        <td>led</td>
        <td>5mm红，绿直插</td>
        <td>3个</td>
        <td>0.0364*3元</td>
    </tr>
    <tr>
        <td>11</td>
        <td>万用板</td>
        <td>10*10cm</td>
        <td>1个</td>
        <td>2.28*1元</td>
    </tr>
    <tr>
        <td>12</td>
        <td>LCD12864</td>
        <td>蓝屏</td>
        <td>1个</td>
        <td>25.8*1元</td>
    </tr>
    <tr>
        <td>13</td>
        <td>杜邦线</td>
        <td>10cm</td>
        <td>12根</td>
        <td>0.01*12元</td>
    </tr>
    <tr>
        <td>14</td>
        <td>排针</td>
        <td>直插</td>
        <td>2排</td>
        <td>0.20*2元</td>
    </tr>
    <tr>
        <td>15</td>
        <td>单片机测试活动底座</td>
        <td>40脚</td>
        <td>1个</td>
        <td>3.03*1元</td>
    </tr>
    <tr>
        <td>总计</td>
        <td></td>
        <td></td>
        <td></td>
        <td>39.642元</td>
    </tr>
</table>

#### 作品成本核算：

本系统的设计成本是39.642元，价格较低，其中LCD12864的成本为25.8元，占一半以上，可以使用较为便宜的LCD1608，若再追求性价比，可将LCD更换为数码管显示，再去掉一些调试用的排针，底座，杜邦线，可将成本控制再15元以下。

#### 同类型产品成本比较

相比于同类产品，比起真正商业化的成品显然没有优势（都是使用专用芯片，成本只有几元），但淘宝上51单片机的成品都在60元以上，而本系统的成本仅仅有39.522元，如去除不必要的元件，可将成本控制再15元以下，因此在价格上更加具有市场竞争力；同时，本系统具有更多的功能选择，比如继电器控制家电的作用，但在性能方面，由于定时器使用单片机内部定时器，而市场上的大多由DS12C887完成定时，所以时间准确度度不如市场上的。