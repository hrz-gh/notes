# 时间函数

## Compare

| Function | Type | Accuracy | Time |
| :---: | :---: | :---: | :---: |
| time | C system call | low | < 1s |
| clock | C system call | low | < 10 ms |
| timeGetTime | Windows API | middle | < 1 ms |
| GetTickCount | Windows API | middle | < 1 ms |
| QueryPerformanceCounter | Windows API | high | < 0.1ms |
| gettimeofday | C system call in linux | high | < 0.1ms |
| RDTSC | induction | high | < 0.1ms |

## Example

### `time()`

**Prototype:** `time_t time(time_t * timer)` in `<time.h>`, and `typedef long time_t;`

**Function:** 获取当前的系统时间，返回的结果是一个time_t类型，其值表示从CUT（Coordinated Universal Time）时间1970年1月1日00:00:00（称为UNIX系统的Epoch时间）到当前时刻的秒数。

#### Usage

**As timer:**

```c++
time_t start,stop;
start = time(NULL);
foo();//Dosomething
stop = time(NULL);
printf("Use Time:%ld\n",(stop-start));
```

**As random seed:**

```c++
srand((unsigned) time(NULL));
printf("Ten random numbers from 0 to 99\n");
for(int i=0;i<10;i++) {
    printf("%d\n",rand()%100);
}
```

**Combine with other function:**

Example: `localtime, gmtime, asctime, ctime`

```c++
time_t timer;
time(&timer);
printf("Local time is: %s\n",asctime(localtime(&timer)));
printf("Local time is: %s\n",ctime(&timer));
```

### clock()

**Prototype:** `clock_t clock(void)` in `<time.h>`, and  `typedef long clock_t;`

**Function:** 返回从“开启这个程序进程”到“程序中调用clock()函数”时之间的CPU时钟计时单元（clock tick）数，在MSDN中称之为挂钟时间（wal-clock）。

In `<time.h>`, there is a const `CLOCKS_PER_SEC`，indicating how many clock units in a second, so we can use `clock()/CLOCKS_PER_SEC` to calculate.

#### Usage

```c++
clock_t start, stop;
start = clock();
foo();//Dosomething
stop = clock();
printf("%f", (double)(stop-start)/CLOCKS_PER_SEC);
```

### `gettimeofday`

**Prototype:** `int gettimeofday(struct timeval* tv, struct timezone* tz)` in `<sys/time.h>`, `struct timeval` and `struct timezone` are defined as follows:

```c++
struct timeval{
long tv_sec; /*秒*/
long tv_usec; /*微秒*/
};
struct timezone{
int tz_minuteswest; /*和Greenwich 时间差了多少分钟*/
int tz_dsttime; /*日光节约时间的状态*/
};
```

**Function:** `gettimeofday()`是linux环境下的计时函数，把当地时区的信息放到tz所指的结构中。

#### Usage

```c++
struct timeval t1,t2;
double timeuse;
gettimeofday(&t1,NULL);
foo();
gettimeofday(&t2,NULL);
timeuse = t2.tv_sec-t1.tv_sec+(t2.tv_usec-t1.tv_usec)/1e6;
printf("Use Time:%f\n",timeuse);
```