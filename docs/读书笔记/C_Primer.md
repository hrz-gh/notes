# C++ Primer

## 1. Start

读一行：

```c++
// 1
string s;
getline(cin, s); // Defined in <string>
// 2
char str[100];
cin.getline(str, 100);
// 3
gets(str);
```

`scanf()`中的`"%c"`和`char c = getchar()`一样会吸收空格。

`scanf()`返回读入成功的个数，失败时返回-1，且`EOF`为-1。

`<<`, `>>`都是返回其左侧的运算对象。

多点测试时，输入：

```c++
while (scanf() != EOF) {
    // Statement
}
while (scanf() != EOF, /*Condition*/) {
    // Statement
}
int value;
while (cin >> value) { // 读到`EOF`或非整数时，返回无效的`istream`
    // Statement
}
```

## 2. Variables and Foundation Type

C++11：空指针`nullptr`

Separation Compilation：
1. 只声明不定义：`extern int i;`
2. 可以声明多次，但定义只能有一次

用术语“引用”是指“左值引用”

`const`修饰：在编译或运行时初始化
`constexpr`：在编译时初始化，必须使用字面值类型初始化，引用和指针时，但只能用于固定地址的对象

`const`修饰的变量默认只在文件内生效，若要共享，无论是声明还是定义都需要加`extern`

```c++
//file.h
extern const i = fcn(); // Defination
//file.c
extern const i; // Declaration
```

`::`为作用域操作符

```c++
// 显示使用全局作用域
int i = 1;
int main() {
    int i = 2;
    std::cout << ::i << std::endl;
    return 0;
}
```

C++11中无论是对象还是内置类型都可以使用列表初始化，特点是存在数据丢失风险时会报错：

```c++
int i{0};
int i = {0};
// 报错
int i = {1.2};
```

在函数体内部的内置类型不会被默认初始化

Reference ot const: 都不能改，可以绑定非常量，字面值，表达式，其实质是再定义了个变量

```c++
int i = 0;
// Const pointer
int *const p = &i;
// Pointer to const
const int *p = &i;
```

普通类型只有top-level const，引用只有low-level const，指针都可以，top-level const 时拷贝不影响，而low-level const 拷贝时不能是常量转非常量

`constexpr`只修饰顶层对象

Alias declaration in C++11: `using LL = long long` 

别名不能简单的理解为直接替换：

```c++
using pstring = char *;
const pstring p; // `char`类型的常量指针
const char *p; // 指向`char`常量的指针
```

`auto`会忽略`const`，若要推断为`const`类型，要手动加上

当表达式返回左值时，`decltype(\*expersion*\)`返回该类型的引用

## 3. String, Vector and Array

下标类型`string<T>::size_type`，`vector<T>::size_type`是无符号整数
`iterator`运算返回`difference_type`为带符号整数

向迭代器所属容器添加元素，会使迭代器失效

理解数组修饰符时，从内到外，从左到右，如`int *(&a)[10] = p;`，是一个含10`int`指针的数组的引用

数组大小类型为`size_t`，下标运算可以处理负值为`ptrdiff_t`类型
有`begin`和`end`函数

`auto`推断数组会自动转化为该数组的头指针，而`decltype`会把大小一起表示出来

```c++
int a[] = {1, 2};
auto a1{a}; // a1为指针
delctype(a) a2 = {1, 2}; //a2为 int[2]
```

对多维数组使用范围`for`时，除最内层以外`auto`都要加上`&`，防止自动转化为指针

## 4. Expersion

一个对象被当作左值时用的使其身份（内存中的位置），当作右值是用的是值（内容）
（除一种特殊情况），左值可以当作右值，但右值不能当作左值
