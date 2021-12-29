#### 笔记

**kmalloc()**

由原先的按4KB的倍数分配，改为使用slub算法分配更小粒度的内存块。

![](https://gitee.com/mostiray/Images_bed/raw/master/notes/svg1.svg)

**copy_thread()**

内核线程的`tf->tf_esp`为0，由此cpu在`iret`时不会切换特权级，仍运行在内核态。

**forkrets**

`forkrets`是在`forkret()`中进行调用的，所以有`movl 4(%esp), %esp`

**遗留问题**

- `forkrets`经`forkret()`调用有什么意义。
