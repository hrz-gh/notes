# 音频频谱分析仪设计与实现

## 1. 实验项目名称

音频频谱分析仪设计与实现。

## 2. 实验目的

构建交互界面，具有播放声音文件，显示波形与频谱，并可测量声音时域参数。

## 3. 实验内容与步骤

实验内容：

MATLAB是一个数据分析和处理功能十分强大的工程实用软件，其数据采集工具箱为实现数据的输入和输出提供了十分方便的函数和命令。本实验要求基于声卡与MATLAB实现音频信号频谱分析仪的设计原理与实现，功能包括：

(1) 音频信号输入，从声卡输入、从WAV文件输入、从标准信号发生器输入。

(2) 信号波形分析，包括幅值、频率、周期、相位的估计，以及统计量峰值、均值、均方值和方差的计算。

(3) 信号频谱分析，频率、周期的估计，图形显示幅值谱、相位谱、实频谱、虚频谱和功率谱的曲线。

**频率（周期）检测**
对周期信号来说，可以用时域波形分析来确定信号的周期，也就是计算相
邻的两个信号波峰的时间差，或过零点的时间差。这里采用过零点($t_s$)的时间差$T$(周期)。频率即为$f = 1/T$，由于能够求得多个$T$值($t_i$有多个)，故采用它们的平均值作为周期的估计值。

**幅值检测**
在一个周期内，求出信号最大值$y_{max}$与最小值$y_{min}$的差的一半，即$A = (y_{max}-y_{min})/2$,同样，也会求出多个$A$值，但第一个$A$值对应的$y_{max}$和$y_{min}$不是在一个周期内搜索得到的，故以除第一个以外的$A$值的平均值作为幅值的估计值。

**相位检测**
采用过零法，即通过判断与同频率零相位信号过零点时刻，计算其时间差，然后换成相应的相位差。$\phi = 2\pi(1-t_i/T)$，同样，以$\phi$的平均值作为相位的估计值。

**数字信号统计量估计**

1. 峰值P的估计：在样本数据x中找出最大值与最小值，其差值为双峰值，双峰值的一半即为峰值。

$$
P = 0.5[max(y_i)-min(y_i)]
$$

   2. 均值估计：

$$
E(y) = \frac{1}{N}\sum_{i=0}^N y_i
$$
   式中，N为样本容量，下同。

   3. 均方值估计

$$
E(y^2) = \frac{1}{N}\sum_{i=0}^N y_i^2
$$

   4. 方差估计

$$
D(y) = \frac{1}{N}\sum_{i=0}^N [y_i-E(y)]^2
$$

**频谱分析原理**
时域分析只能反映信号的幅值随时间的变化情况，除单频率分量的简单波
形外，很难明确提示信号的频率组成和各频率分量大小，而频谱分析能很好的解决此问题。

1. DFT与FFT
 对于给定的时域信号$y$，可以通过*Fourier*变换得到频域信息$Y$。
    采样信号的频谱是一个连续的频谱，不可能计算出所有的点的值，故采用离散*Fourier*变换(DFT)。但计算效率很低，因为有大量的指数(等价于三角函数)运算，故实际中多采用快速*Fourier*变换(FFT)。其原理即是将重复的三角函数算计的中间结果保存起来，以减少重复三角函数计算带来的时间浪费。由于三角函数计算的重复量相当大，故FFT能极大地提高运算效率。

2. 频率、周期的估计
 对于$Y(k\triangle f)$，如果当$\triangle f = \tilde{f}$时，$Y(k\triangle f)$取最大值，则$\tilde{f}$为频率的估计值，由于采样间隔的误差，$\tilde{f}$也存在误差，其误差最大为$\triangle f/2$。
    周期$T=1/f$。
    从原理上可以看出，如果在标准信号中混有噪声，用上述方法仍能够精确地估计出原标准信号的频率和周期。

3. 频谱图
 为了直观地表示信号的频率特性，工程上常常将Fourier变换的结果用图形的方式表示，即频谱图。
    以频率$f$为横坐标，$|Y(f)|$为纵坐标，可以得到幅值谱；
    以频率$f$为横坐标，$arg Y(f)$为纵坐标，可以得到相位谱；
    以频率$f$为横坐标，$Re Y(f)$为纵坐标，可以得到实频谱；
    以频率$f$为横坐标，$Im Y(f)$为纵坐标，可以得到虚频谱。
    根据采样定理，只有频率不超过$F_s/2$的信号才能被正确采集，即*Fourier*变换的结果中频率大于$F_s/2$的部分是不正确的部分，故不在频谱图中显示。即横坐标$f \in [0 ,F_s/2]$。 

4. 模块划分
 模块化就是把程序划分成独立命名且可独立访问的模块，每个模块完成一个子功能，把这些模块集成起来构成一个整体，可以完成指定的功能满足用户需求。根据人类解决一般问题的经验，如果一个问题由两个问题组合而成，那么它的复杂程度大于分别考虑每个问题时的复杂程度之和，也就是说把复杂的问题分解成许多容易解决的小问题，原来的问题也就容易解决了。这就是模块化的根据。
    在模块划分时应遵循如下规则：改进软件结构提高模块独立性；模块规模应该适中；深度、宽度、扇出和扇入都应适当；模块的作用域应该在控制域之内；力争降低模块接口的复杂程度；设计单入口单出口的模块；模块功能应该可以预测。

## 4. 实验环境

MATLAB R2019b

## 5. 实验过程与分析程序文本

### 音频信号输入

#### 声卡输入

```matlab
function button_recording_Callback(hObject, eventdata, handles)%开始录音按钮
    if (get(handles.radio_audio,'Value')==1)%当选择声卡时，才能进行相应操作，否则提示错误信息
        if(isempty(get(handles.input_fs_fre,'String'))==0)%判断设定的采样频率是否为空
            recordtime=str2double(get(handles.recording_time,'String'));%读取录音时间数据
            if(recordtime>0)
                handles.fs=str2double(get(handles.input_fs_fre,'String'));%获取设定的采样频率，转为数字格式
                sound_length=round(recordtime*handles.fs);%录音点数
                record=audiorecorder(handles.fs,24,1);%依据采样频率创建录音序列，位数为24，单声道
                recordblocking(record,recordtime);%输入录音序列，长度信息=时间
                msgbox('Recording complete','Tip');
                handles.sound=getaudiodata(record);%创建获取录音数据的数组
                n=0:1:sound_length-1;
                time=n/handles.fs;%创建显示用的时间序列
                plot(handles.axes_analysis,time,handles.sound);%在分析对象区域打印出采集到的信号结果
                title('Waveform of the Acquisition Signal');
                set(handles.input_fs_num,'String',num2str(sound_length));%在采样点数量的框内显示当前采样频率下对样本信号的采样点数
                handles.complete=1;%表明为声卡采集完成
                guidata(handles.button_recording,handles);%储存handles结构体，储存sound信号,fs数值
            else
                errordlg('No recording time set','Enter error');%提示未设定录音时间
            end
        else
            errordlg('Sample frequency not set','Enter error');%提示未设定采样频率
        end  
    else
        errordlg('Sound card button not enabled','Choose error');%提示未选择声卡 
    end
end
```

结果如图1.1

#### WAV文件输入

```matlab
function choice_files_Callback(hObject, eventdata, handles)%手动选择文件按钮
    [filename, pathname] = uigetfile('*', '读取音频文件')
    if([pathname,filename]~=0)
        set(handles.filename,'String',[pathname,filename]);
    end
end
function button_open_file_Callback(hObject, eventdata, handles)%打开文件按钮
    if (get(handles.radio_wav,'Value')==1)%当选择文件读取时，才能进行相应操作，否则提示错误信息
            if((isempty(get(handles.filename,'String'))==0))%判断文件名输入是否为空
                [y,Fs] =audioread(get(handles.filename,'String'));%获取所选文件的声音信号，得到信号矩阵和信号频率
                [leng,channel]=size(y);%对y进行列数判断，求得声道数目,以及所得到的数据点的数目
                set(handles.input_fs_fre,'String',num2str(Fs));
                set(handles.input_fs_num,'String',num2str(leng));%设置采样频率和点数
                switch (channel)
                    case 1%单声道
                        set(handles.sound_channel,'Value',1);
                        set(handles.sound_channel,'Enable','off');
                        msgbox('输入的是单声道文件','Tip');
                        handles.fs=Fs;
                        handles.sound=y(:,channel);%矩阵维度一致，均为多行单列
                        guidata(handles.button_open_file,handles);%储存sound信息
                        time=0:1/handles.fs:(leng-1)/handles.fs;
                        plot(handles.axes_analysis,time,handles.sound);%在分析对象区域打印出采集到的信号结果
                        title('音频信号的波形');
                    otherwise
                        set(handles.sound_channel,'Value',2);
                        msgbox('声道数目超过一个，请选择所选取的声道，默认选取左声道','Tip');
                        handles.fs=Fs;
                        handles.sound=y(:,:);
                        guidata(handles.button_open_file,handles);
                        set(handles.filename,'Enable','off');
                        set(handles.choice_files,'Enable','off');
                        set(handles.button_open_file,'Enable','off');
                end
            else
                errordlg('未设置文件目录','Enter error');%提示未设置文件目录
            end  
    else
        errordlg('未启用文件读取按钮','Choose error');%提示未选择文件读取
    end        
end
function sound_channel_Callback(hObject, eventdata, handles)
    choice_channel=get(handles.sound_channel,'Value');
    if(choice_channel>1)
        choice_channel=choice_channel-1;
    end
    handles.sound=handles.sound(:,choice_channel);
    leng=length(handles.sound);
    guidata(handles.button_open_file,handles);%储存sound信息
    time=0:1/handles.fs:(leng-1)/handles.fs;
    plot(handles.axes_analysis,time,handles.sound);%在分析对象区域打印出采集到的信号结果
    title('音频信号的波形');
    set(handles.filename,'Enable','on');
    set(handles.choice_files,'Enable','on');
    set(handles.button_open_file,'Enable','on');
end
function sound_channel_CreateFcn(hObject, eventdata, handles)
    if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
        set(hObject,'BackgroundColor','white');
    end
end
```
结果如图1.2

#### 信号发生器输入

```matlab
function button_signal_Callback(hObject, eventdata, handles) %生成波形按钮
    if ((get(handles.radio_signal,'Value')+get(handles.check_mixing,'Value'))==1)
        if(isempty(get(handles.input_fs_fre,'String'))==0)%判断设定的采样频率是否为空
            if((isempty(get(handles.input_am,'String'))==0)&&(isempty(get(handles.input_vlotage,'String'))==0)&&(isempty(get(handles.input_phase,'String'))==0))
                handles.fs=str2double(get(handles.input_fs_fre,'String'));%获取设定的采样频率，转为数字格式 
                signal_soundtype=get(handles.signal_choice,'Value');%获取信号发生器区域的数据
                signal_fre=str2double(get(handles.input_am,'String'));%获取信号发生器的三个浮点数数据，用于产生信号使用
                signal_vlotage=str2double(get(handles.input_vlotage,'String'));
                signal_phase=str2double(get(handles.input_phase,'String'))/180*pi;%转换为pi
                if (get(handles.radio_signal,'Value')==1)%如果不选择混叠，按照频率进行采样操作
                    signal_time=str2double(get(handles.signal_nmix_time,'String'));%获取非混叠情况下生成信号的时间
                    if(signal_time==0)
                        errordlg('非混叠情况下需设置发生器时间','error');
                        return;
                    end
                    number=round(handles.fs*signal_time);
                    t=(0:1.0/handles.fs:(number-1)/handles.fs);%采样时间序列
                else%如果产生混叠，则读取已经有的数据的采样点数
                    number=str2double(get(handles.input_fs_num,'String'));%获取采样点数
                    t=(0:1.0/handles.fs:(number-1)/handles.fs);%采样时间序列
                end%创建时间序列
                switch signal_soundtype%不需要加入break
                    case 1%标准正弦波
                        y=signal_vlotage*sin(2*pi*t*signal_fre+signal_phase);
                    case 2%方波
                        y=signal_vlotage*sign(sin(2*pi*t*signal_fre+signal_phase));
                    case 3%三角波
                        y=signal_vlotage*sawtooth(2*pi*t*signal_fre+signal_phase,0.5);
                    case 4%锯齿波
                        y=signal_vlotage*sawtooth(2*pi*t*signal_fre+signal_phase);
                    case 5%白噪声
                        y=signal_vlotage*sin(2*rand(size(t))-1);
                    otherwise%不满足则报错
                        errordlg('波形类型选择出错','Choose error');
                end
                if (get(handles.radio_signal,'Value')==1)%如果没有选择混叠按钮，则不与另外两个信号相叠加
                    handles.sound=y';
                else%sound与y长度相同，但矩阵维度不同
                    size(y');
                    handles.sound=handles.sound+y';
                    size(handles.sound);
                end
                n=0:1:number-1;
                time=n/handles.fs;%创建显示用的时间序列
                plot(handles.axes_analysis,time,handles.sound);%在分析对象区域打印出采集到的信号结果
                title('采集信号的波形');
                set(handles.input_fs_num,'String',num2str(number));%在采样点数量的框内显示当前采样频率下对样本信号的采样点数
                guidata(handles.button_signal,handles);%储存数据
            else
                errordlg('未设定发生器配置','Enter error');%提示未设定发生器配置信息
            end
        else
            errordlg('未设定采样频率','Enter error');%提示未设定采样频率
        end  
    else
        errordlg('必须选择信号发生器和混叠按钮之中的一个','Choose error');
    end
end
```

结果如图1.3.1-1.3.4，其中如1.3.4为幅值为1，频率分别为1Hz和2Hz正弦的混叠

### 时域分析

```matlab
function button_time_Callback(hObject, eventdata, handles)%时域分析按钮
    n=1;
    ymax=0;ymin=0;
    i=3;%初始化相应变量
    N=length(handles.sound);%获取声音信号的长度
    ti=0;
    while(1)
        if((handles.sound(i-1)<0)&&(handles.sound(i-2)<0)&&(handles.sound(i)>=0)&&(handles.sound(i+1)>0))
            if(handles.sound(i)>0)
                ti(n)=i/handles.fs;
            else
                ti(n)=(i-handles.sound(i)/(handles.sound(i)-handles.sound(i-1)))/handles.fs;
            end
            A(n)=(ymax-ymin)/2;
            ymax=0;ymin=0;
            n=n+1;
        else
            if(ymax<handles.sound(i))
                ymax=handles.sound(i);
            end
            if(ymin>handles.sound(i))
                ymin=handles.sound(i);
            end
        end
        i=i+1;
        if(i>N-1)
            break;
        end
    end
    len_ti=length(ti);
    if(len_ti<2)
        errordlg('过零点个数不足，无法进行分析','error');%提示未选择声卡
        return;
    end
    for temp=2:1:len_ti
        T(temp-1)=(ti(temp)-ti(temp-1));
    end
    freq=1/mean(T)%计算频率
    set(handles.analysis_cycle,'String',num2str(1/freq));
    set(handles.analysis_fre,'String',num2str(freq));%输出频率估计值
    set(handles.analysis_vlotage,'String',num2str(mean(A(2:n-1))));
    if (get(handles.check_point,'Value')==1)
        from=1;
        to=str2double(get(handles.input_fs_num,'String'));
    else
        from=str2num(get(handles.first_point,'String'));
        to=str2num(get(handles.last_point,'String'));
    end
    phase=2*180*(1-(ti(2:n-1)-1)./T+floor((ti(2:n-1)-1)./T));
    set(handles.analysis_phase,'String',num2str(mean(phase)));%相位
    set(handles.analysis_high,'String',(max(handles.sound(from:to))-min(handles.sound(from:to)))/2);%最大值与最小值的一半即为峰值
    set(handles.analysis_mean,'String',mean(handles.sound(from:to)));%均值
    set(handles.analysis_square,'String',mean(handles.sound(from:to).^2));%均方值
    set(handles.analysis_variance,'String',std(handles.sound(from:to))^2);%输出方差
end
```

结果如图2

### 频域分析

```matlab
function button_fre_Callback(hObject, eventdata, handles)%频域分析按钮
    if (get(handles.check_point,'Value')==1)
        from=1;
        to=str2double(get(handles.input_fs_num,'String'));
    else
        from=str2num(get(handles.first_point,'String'));
        to=str2num(get(handles.last_point,'String'));
    end
    sample=handles.sound(from:to);%取出sound信号的数据，存放到临时空间中
    f=linspace(0,handles.fs/2,(to-from+1)/2);%生成离散化的频率点，以采样频率作为离散化时间间隔
    Y=fft(sample,to-from+1);%对离散信号进行傅里叶变换
    [C,I]=max(abs(Y));%求的幅值最大的点及其下标
    set(handles.fre_cycle,'String',1/f(I));%计算并输出周期
    set(handles.fre_fre,'String',f(I));%输出频率
    Y=Y(1:(to-from+1)/2);
    plot(handles.axes_fre,f,2*sqrt(Y.*conj(Y)));
    plot(handles.axes_time,f,angle(Y));
    plot(handles.axes_real,f,real(Y));
    plot(handles.axes_img,f,imag(Y));
    plot(handles.axes_power,f,abs(Y));
end
```

结果如图3

## 6. 实验结果总结

<center>

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_1_1.png)

图1.1

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_1_2.png)

图1.2

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_1_3_1.png)

图1.3.1

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_1_3_2.png)

图1.3.2

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_1_3_3.png)

图1.3.3

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_1_3_6.png)

图1.3.4

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_2.png)

图2

![](http://gitee.com/mostiray/Images_bed/raw/master/blog/Digital_Signal_Processing_Experiment/lab7/7_3.png)

图3

</center>

## 7. 结果分析

### 音频信号输入

实现录音，文件，以及直接生成正弦波、方波、三角波、锯齿波、白噪声的方式输入。

### 时域分析

结果大致准确，但存在些许误差。这是由于过零检测无法包括所有点。

### 频域分析

结果大致正确，窗函数的选取误差导致有频谱泄露的现象发生。

## 8.心得体会

1. 学会了guide工具箱的使用，学会了编写简单交互式界面。
2. 学会了模块化设计。
3. 由matlab面向过程编程转变为面向对象编程。
