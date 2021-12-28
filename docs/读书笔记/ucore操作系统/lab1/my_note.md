#### 笔记

**CPU上电**

为保证了向下兼容与物理地址空间的连续性，Intel让4GB地址空间的最高一个64KB的内容等同于1MB地址空间的最高一个64K的内容，从而使得执行了长跳转指令后，其实是回到了早期的8086 CPU初始化控制流。

```
寻址方式为：CS.Base+EIP
CS=0xf000，CS.Base=0xffff0000，EIP=0xfff0
第一条指令：0xfffffff0 JMP F000:E05B
CS.Base->0x000f0000
第二条指令：0x000fe05b BIOS 指令
```

**BIOS**

- 硬件自检和初始化
- 选择一个启动设备（例如软盘、硬盘、光盘等）
- 读取该设备的第一扇区\(即主引导扇区或启动扇区\)到0x7c00处
- 跳转至0x7c00处，执行bootloader

**bootloader**

- 切换到保护模式，启用分段机制
    - 通过键盘控制器8042，使能A20控制线
        - A20控制线（0时）是为了在实模式下模仿早期8086寻址的回绕特征，为访问全部内存需使其为1。
    - 加载全局描述符表，将CR0第0位置1，更新CS
        - 更新CS使用长跳转指令
- 读磁盘中ELF执行文件格式的kernel到内存指定的内存起始地址去（ELFHDR=0x10000），kernel的起始地址是在硬盘第1扇区。
- 把控制权交给ucore操作系统

主引导扇区的大小为512B，启动代码部分不超过446B，`obj/bootblock.out`是移除所有多余信息的启动代码为442B。

全局描述符表起始地址保存在全局描述符表寄存器GDTR中。GDTR长48位，其中高32位为基地址，低16位为段界限。全局描述符表中第一个段描述符设定为空段描述符。GDTR中的段界限以字节为单位。对于含有N个描述符的描述符表的段界限通常可设为8*N-1，即最多只有pow(2, 16)/8=8192个段，段选择子的索引位数为log2(8192)=13位。

访问一个段特权级检测：max(CPL, RPL)<=DPL，但堆栈寄存器要求CPL=RPL=DPL。


**操作系统初始化**
- 初始化终端；
- 显示字符串；
- 显示堆栈中的多层函数调用关系；
- 更新gdt；
- 初始化中断控制器，设置中断描述符表，初始化时钟中断，使能整个系统的中断机制；
- 执行while（1）死循环。

`gdt_init()`中重新划分了栈空间，kern的ess和esp定义在TTS中，大小为1KB。

共256个中断向量，[32, 255]可由操作系统定义。其地址保存在`__vectors`中，需要将其加载到IDT中去，IDT包含3种类型的Descriptor：

- Task-gate descriptor （这里没有使用）
- Interrupt-gate descriptor （中断方式用到，Interrupt会被CPU自动禁止）
- Trap-gate descriptor（系统调用用到，CPU不改变中断）

访问一个门特权级检测：CPL<=DPL（门）且CPL>=DPL（段），CPL>DPL（段）满足了用户态到系统态的跳转。所有IDT项中只有`idt[T_SWITCH_TOK=121]`（对应系统调用）中的DPL为`DPL_USER=3`，其他的为`DPL_KERNEL=0`。而门中选择子位数为16位，实际只用了高13位，低3位为0。

中断处理时：
- 由硬件保存完对应的值后，多数中断均压入0代表error_code，以及相应的中断号，某些中断的error_code由硬件压入，如`vector8`到`vector14`。
- 服务例程参数保存在`trapframe`中，其中`pushal`压栈的顺序为：eax，ecx，edx，ebx，oesp，ebp，ebp，esi，edi

**遗留问题**

```c
// boot/bootmain.c
// 为什么读8个扇区
88: readseg((uintptr_t)ELFHDR, SECTSIZE * 8, 0); 

// kern/debug/kdebug.c
// 为什么要先读ebp，否则print_debugifo会出错
305: uint32_t ebp = read_ebp(), eip = read_eip(); 
```