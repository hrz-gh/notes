#### 管理PCB

为了管理系统中所有的进程控制块，uCore维护了如下全局变量（位于*kern/process/proc.c*）：

- static int nr_process：进程总数。

- static struct proc \*current：当前占用CPU且处于“运行”状态进程控制块指针。

- static struct proc \*initproc：lab4中，指向一个内核线程。lab4以后，此指针将指向第一个用户态进程。

- static list\_entry\_t hash\_list[HASH\_LIST\_SIZE]：所有进程控制块的哈希表，proc\_struct中的成员变量hash\_link将基于pid链接入这个哈希表中。

- list\_entry\_t proc\_list：所有进程控制块的双向线性列表，proc\_struct中的成员变量list\_link将链接入这个链表中。