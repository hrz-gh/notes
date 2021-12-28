##### GCC扩展内联汇编

GCC扩展内联汇编的基本格式是：          

```c
asm [volatile] ( Assembler Template
   : Output Operands
   [ : Input Operands
   [ : Clobbers ] ])
```

如果不希望汇编语句被 gcc 优化而改变位置，就需要在 asm 符号后添加 volatile 关键词：asm volatile(...)；

` Assembler Template` 为汇编指令部分，例如，"movl %%cr0,%0\n\t"。数字前加前缀 “％“，如％1，％2等表示使用寄存器的样板操作数，这类寄存器的值和这之后的约束关联，如%0（The first constraint following）。在用到具体的寄存器时就在前面加**两个“％”**，如**%%cr0**。

输出部分（output operand list），用以规定对输出变量（目标操作数）如何与寄存器结合的约束（constraint）,输出部分可以有多个约束，互相以逗号分开。每个约束以“＝”开头，接着用一个字母来表示操作数的类型，然后是关于变量结合的约束。例如，上例中：

	:"=r" (__dummy)

“＝r”表示相应的目标操作数（指令部分的%0）可以使用任何一个通用寄存器，并且变量__dummy 存放在这个寄存器中，但如果是：               

	:“＝m”(__dummy)

“＝m”就表示相应的目标操作数是存放在内存单元__dummy中。表示约束条件的字母很多，下表给出几个主要的约束字母及其含义：

<table>
	<tr><td>字母</td><td>含义</td></tr>
	<tr><td>m, v, o</td><td>内存单元</td></tr>
	<tr><td>R</td><td>任何通用寄存器</td>	</tr>
	<tr><td>Q</td><td>寄存器eax, ebx, ecx,edx之一</td></tr>
	<tr><td>I, h</td><td>直接操作数</td></tr>
	<tr><td>E, F</td><td>浮点数</td></tr>
	<tr><td>G</td><td>任意</td></tr>
	<tr><td>a, b, c, d</td><td>寄存器eax/ax/al, ebx/bx/bl, ecx/cx/cl或edx/dx/dl</td></tr>
	<tr><td>S, D</td><td>寄存器esi或edi</td></tr>
	<tr><td>I</td><td>常数（0～31）</td></tr>
</table>


输入部分（input  operand list）：输入部分与输出部分相似，但没有“＝”。如果输入部分一个操作数所要求使用的寄存器，与前面输出部分某个约束所要求的是同一个寄存器，那就把对应操作数的编号（如“1”，“2”等）放在约束条件中。在后面的例子中，可看到这种情况。

修改部分（clobber list,也称 乱码列表）:这部分常常以“memory”为约束条件，以表示操作完成后内存中的内容已有改变，如果原来某个寄存器的内容来自内存，那么现在内存中这个单元的内容已经改变。乱码列表通知编译器，有些寄存器或内存因内联汇编块造成乱码，可隐式地破坏了条件寄存器的某些位（字段）。 注意，指令部分为必选项，而输入部分、输出部分及修改部分为可选项，当输入部分存在，而输出部分不存在时，冒号“：”要保留，当“memory”存在时，三个冒号都要保留，例如

```c
#define __cli() __asm__ __volatile__("cli": : :"memory")
```

下面是一个例子：

```c
int count=1;
int value=1;
int buf[10];
void main()
{
    asm(
        "cld \n\t"
        "rep \n\t"
        "stosl"
    :
    : "c" (count), "a" (value) , "D" (buf)
    );
}
```

得到的主要汇编代码为：

```asm
movl count,%ecx
movl value,%eax
movl buf,%edi
#APP
cld
rep
stosl
#NO_APP
```

cld,rep,stos这几条语句的功能是向buf中写上count个value值。冒号后的语句指明输入，输出和被改变的寄存器。通过冒号以后的语句，编译器就知道你的指令需要和改变哪些寄存器，从而可以优化寄存器的分配。其中符号"c"(count)指示要把count的值放入ecx寄存器。类似的还有：

	0 same as the first
	a eax
	b ebx
	c ecx
	d edx
	S esi
	D edi
	I 常数值，(0 - 31)
	q,r 动态分配的寄存器
	g eax,ebx,ecx,edx或内存变量
	A 把eax和edx合成一个64位的寄存器(use long longs)

也可以让gcc自己选择合适的寄存器。如下面的例子：

```c
asm("leal (%1,%1,4),%0"    : "=r" (x)    : "0" (x));
```

这段代码到的主要汇编代码为：

```asm
movl x,%eax
#APP
leal (%eax,%eax,4),%eax
#NO_APP
movl %eax,x
```

几点说明：

* [1] 使用q指示编译器从eax, ebx, ecx, edx分配寄存器。
  使用r指示编译器从eax, ebx, ecx, edx, esi, edi分配寄存器。
* [2] 不必把编译器分配的寄存器放入改变的寄存器列表，因为寄存器已经记住了它们。
* [3] "="是标示输出寄存器，必须这样用。
* [4] 数字%n的用法：数字表示的寄存器是按照出现和从左到右的顺序映射到用"r"或"q"请求的寄存器．如果要重用"r"或"q"请求的寄存器的话，就可以使用它们。
* [5] 如果强制使用固定的寄存器的话，如不用%1，而用ebx，则：

```c
asm("leal (%%ebx,%%ebx,4),%0"    : "=r" (x)    : "0" (x) );
```

> 注意要使用两个%,因为一个%的语法已经被%n用掉了。

参考：

- [GCC Manual， 版本为5.0.0 pre-release,6.43节（How to Use Inline Assembly Language in C Code）](https://gcc.gnu.org/onlinedocs/gcc.pdf)
- [GCC-Inline-Assembly-HOWTO](http://www.ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html)