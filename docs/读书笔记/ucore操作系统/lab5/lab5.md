# Lab5 Report

## 练习1：加载应用程序并执行

在kern/process/proc.c中补充load\_icode()函数。代码为：

```c
    tf->tf_cs = USER_CS;
    tf->tf_ds = tf->tf_es = tf->tf_ss = USER_DS;
    tf->tf_esp = USTACKTOP;
    tf->tf_eip = elf->e_entry;
    tf->tf_eflags = FL_IF;
```

完成对trapframe中代码段、数据段的初始化。

### 问题1.1：描述当创建一个用户态进程并加载了应用程序后，CPU是如何让这个应用程序最终在用户态执行起来的。即这个用户态进程被ucore选择占用CPU执行（RUNNING态）到具体执行应用程序第一条指令的整个经过。

1. 通过schedule找到需要执行的进程或线程
2. 调用proc_run，切换栈和页表，调用switch\_to函数切换上下文
3. switch\_to函数返回至forkret，进而执行forkrets函数
4. 设置栈指针，弹出段寄存器，执行tf->tf\_eip的指令
5. 由于tf->tf\_eip被设置为了elf->e\_entry，从而开始执行用户程序

## 练习2：父进程复制自己的内存空间给子进程

在kern/mm/pmm.c中完成copy\_range()函数，增加以下代码：

```c
	void *src_kvaddr = page2kva(page);
	void *dst_kvaddr = page2kva(npage);
	memcpy(dst_kvaddr, src_kvaddr, PGSIZE);
	ret = page_insert(to, npage, start, perm);
```

代码执行步骤为：

1. 获得源页、目标页地址
2. 用memcpy进行拷贝
3. 设置与物理页的映射关系

### 问题2.1：请在实验报告中简要说明如何设计实现”Copy on Write 机制“，给出概要设计，鼓励给出详细设计。

在copy\_range函数中，不直接拷贝，而是用一个标记为表示此页被多个使用者访问。当进行读操作时，可以共享资源。当进行写操作时，通过判断此页是否共享，再进行拷贝的操作。

## 练习3：阅读分析源代码，理解进程执行 fork/exec/wait/exit 的实现，以及系统调用的实现

> fork: 通过do\_fork函数实现，分配进程的TCB和pid，在链表中加入此进程，最后通过wakeup\_proc唤醒进程

> exec: 通过do\_execve函数实现，首先为加载新的执行码做好用户态内存空间清空准备。如果mm不为NULL，则设置页表为内核空间页表，且进一步判断mm的引用计数减1后是否为0，如果为0，则表明没有进程再需要此进程所占用的内存空间，为此将根据mm中的记录，释放进程所占用户空间内存和进程页表本身所占空间。最后把当前进程的mm内存管理指针为空。接下来的一步是加载应用程序执行码到当前进程的新创建的用户态虚拟空间中。这里涉及到读ELF格式的文件，申请内存空间，建立用户态虚存空间，加载应用程序执行码等。load\_icode函数完成了整个复杂的工作。

> wait: 通过do\_wait函数实现。如果pid!=0，表示只找一个进程id号为pid的退出状态的子进程，否则找任意一个处于退出状态的子进程；如果此子进程的执行状态不为PROC\_ZOMBIE，表明此子进程还没有退出，则当前进程只好设置自己的执行状态为PROC\_SLEEPING，睡眠原因为WT\_CHILD（即等待子进程退出），调用schedule()函数选择新的进程执行，自己睡眠等待，如果被唤醒，则重复跳回步骤1处执行；如果此子进程的执行状态为PROC\_ZOMBIE，表明此子进程处于退出状态，需要当前进程（即子进程的父进程）完成对子进程的最终回收工作，即首先把子进程控制块从两个进程队列proc\_list和hash\_list中删除，并释放子进程的内核堆栈和进程控制块。自此，子进程才彻底地结束了它的执行过程，消除了它所占用的所有资源。

> exit: 通过do\_exit函数实现。1. 如果current->mm != NULL，表示是用户进程，则开始回收此用户进程所占用的用户态虚拟内存空间，包括切换页表和回收资源。2. 这时，设置当前进程的执行状态current->state=PROC\_ZOMBIE，当前进程的退出码current->exit\_code=error\_code。此时当前进程已经不能被调度了，需要此进程的父进程来做最后的回收工作（即回收描述此进程的内核栈和进程控制块；3. 如果当前进程的父进程current->parent处于等待子进程状态:current->parent->wait\_state==WT\_CHILD，则唤醒父进程（即执行“wakup\_proc(current->parent)”），让父进程帮助自己完成最后的资源回收。4. 如果当前进程还有子进程，则需要把这些子进程的父进程指针设置为内核线程initproc，且各个子进程指针需要插入到initproc的子进程链表中。如果某个子进程的执行状态是PROC\_ZOMBIE，则需要唤醒initproc来完成对此子进程的最后回收工作。5. 执行schedule()函数，选择新的进程执行.

> 系统调用：首先初始化系统调用的中断描述符，设置特权级为DPL\_USER；然后建立系统调用的用户库准备；在用户进行系统调用时，根据系统调用编号，跳转到相应的入口进行处理。


### 问题3.1：请分析fork/exec/wait/exit在实现中是如何影响进程的执行状态的？

- fork: runnable
- exec: runnable
- wait: sleeping
- exit: zombie

### 问题3.2：请给出ucore中一个用户态进程的执行状态生命周期图（包执行状态，执行状态之间的变换关系，以及产生变换的事件或函数调用）。

```
process state changing:
                                            
  alloc_proc                                 RUNNING
      +                                   +--<----<--+
      +                                   + proc_run +
      V                                   +-->---->--+ 
PROC_UNINIT -- proc_init/wakeup_proc --> PROC_RUNNABLE -- try_free_pages/do_wait/do_sleep --> PROC_SLEEPING --
                                           A      +                                                           +
                                           |      +--- do_exit --> PROC_ZOMBIE                                +
                                           +                                                                  + 
                                           -----------------------wakeup_proc----------------------------------
-----------------------------
```

## 列出你认为本实验中重要的知识点，以及与对应的OS原理中的知识点，并简要说明你对二者的含义，关系，差异等方面的理解（也可能出现实验中的知识点没有对应的原理知识点）

1. 用户进程的加载与执行
2. 进程控制的各个状态及其转换




    


