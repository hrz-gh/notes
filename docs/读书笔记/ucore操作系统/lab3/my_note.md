#### 笔记

**check_pgfault()**

在`check_pgfault()`可以看到产生页异常时，是对全局指针`check_mm_struct`进行检查，但是产生页异常对应的页目录在CR3中，所以要保持`check_mm_struct->pgdir`和CR3中的页目录地址相等。

**do_pgfault()**

- 中断号

```c
#define T_PGFLT                 14  // page fault
```

错误码的低三位的意义如下。lab3中只检测了最低2位，只有 (W/R=0, P=1)时直接处理失败，其余情况均要检测`vma->flags`是否允许读或写操作。

- The P flag   (bit 0) indicates whether the exception was due to a not-present page (0) or to either an access rights violation or the use of a reserved bit (1).
- The W/R flag (bit 1) indicates whether the memory access that caused the exception was a read (0) or write (1).
- The U/S flag (bit 2) indicates whether the processor was executing at user mode (1) or supervisor mode (0) at the time of the exception.

当前物理页和虚拟页产生关联共采用了两种方法，都是先通过`ptep = get_pte(pgdir, la, 1)`：

- 在`boot_map_segment()`中由于已知pa与va的映射关系，使用`*ptep = pa | PTE_P | perm`
- 在`page_insert()`则需要传入一个空闲pa的地址，最后也是`*ptep = page2pa(page) | PTE_P | perm`

**swap_in()**

当pte表示硬盘上的信息时，结构如下。为区分与无效pte的区别，swap的第一个页不使用，即当pte_p为0且offset不为0时，pte表示页到硬盘扇区的一个映射。offset表示硬盘上的第offset页。

```
swap_entry_t
-------------------------
| offset | reserved | 0 |
-------------------------
24 bits    7 bits   1 bit
```

**swap_out()**

使用的是消极的换出策略，在`alloc_pages()`中有空闲块不够时，换出已有块，如果一直不够，将一直循环。

虚拟地址和对应的硬盘扇区有一一对应关系，后续显然不能这样做，因为存在多个进程时，若另一个进程的虚拟地址和当前的相同且存在于硬盘中，就无法换出。

**swap_check()**

1. 调用mm\_create建立mm变量，并调用vma\_create创建vma变量，设置合法的访问范围为4KB\~24KB；
2. 调用free\_page等操作，模拟形成一个只有4个空闲 physical page；并设置了从4KB\~24KB的连续5个虚拟页的访问操作；
3. 设置记录缺页次数的变量pgfault\_num=0，执行check\_content\_set函数，使得起始地址分别对起始地址为0x1000, 0x2000, 0x3000, 0x4000的虚拟页按时间顺序先后写操作访问，由于之前没有建立页表，所以会产生page fault异常，如果完成练习1，则这些从4KB\~20KB的4虚拟页会与ucore保存的4个物理页帧建立映射关系；
4. 然后对虚页对应的新产生的页表项进行合法性检查；
5. 然后进入测试页替换算法的主体，执行函数check\_content\_access，并进一步调用到\_fifo\_check\_swap函数，如果通过了所有的assert。这进一步表示FIFO页替换算法基本正确实现；
6. 最后恢复ucore环境。
