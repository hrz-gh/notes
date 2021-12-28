# C++

## 经验

1. `&` can't use continuous.
2. In 64 bits machine pointer is `unsinged long`, if want to use pointer calculate like integer, only need forced type transport.
3. The parameters transfer of a two-dimensional array of unknown size:

```c++
void display(int *arr,const int irows,const int icols) {
    for(int i=0; i<irows; ++i) {
        for(int j=0; j<icols; ++j) {
            cout << *(arr + i * icols + j) << " ";
        }
        cout << endl;
    }
    cout << endl;
}
```



## 备忘

### Input and Output Function

`scanf` format symbol:

<center>


|   Type    | Symbol |
| :-------: | :----: |
|    int    |   %d   |
| long long |  %lld  |
|   float   |   %f   |
|  double   |  %lf   |
|   char    |   %c   |
|  string   |   %s   |

</center>

`%c`可以读入空格，除`%c`外以空白符作为结束标志

`double` of `printf` is `%f` ,but `scanf` is `%lf`

Try to use `double` ,because of accuracy

Three general format of `printf`:

1. right `m` bits add space align:`%md`
2. right `m` bits add zero align:`%0md`
3. “四舍六入五成双”规则浮点数保留`m`位小数点:`%.mf`

### `typedef`

`typedef` set alias

### Function in `<math.h>`:

```c
fabs(double x)
floor(double x), ceil(double x)
pow(double r, double p) // $r^p$
sqrt(double x)
log(double x) // e as root
sin(double x), cos(double x), tan(double x)
asin(double x), acos(double x), atan(double x) //unit is rad
round(double x)
```

### Equivalent in condition:

```c
if(n), if(n != 0)
if(!n), if(n == 0)
similarly in while(condition)
```

冒泡排序

### `memset()` and `gets()` and `getchar()`

```c 
memset(array name, value, sizeof(array name))
```

Note: `memset()` assign value as char, advice only use 0 and -1.

`gets(char array)` like `scanf("%s, array")` use `'\n` as end of input and need not add `'\0'`, except that, other method input char like `char = getchar()` can recognize `'\n'` add need add `'\0'` in string.

### Function in `<string.h>`

```c
strlen(char array) //get number of bit before first '\0'
strcmp(char array1, char array2) //if array1 < array2, retrun negtive, if array1 == array2, return 0, if array1 > array2, return postive
strcpy(char array1, char array2) //copy array2 to array1, include '\0'
strcat(char array1, char array2) //link array2 to array1
```

### `sscanf()` and `sprintf()`

```c
int n;
char str[50];
sscanf(str, "%d", &n); //str to int
sprintf(str, %d", n); //int to str
//Similarly, float, long, and so on
//sscanf also can use regular expresion
```

### Multidimensions Array

When input array dimensions more than one to a function, synthesis need the size of dimensions more one, or just use a pointer as synthesis.

Note: when one pointer will be built, and we will change it's value, we must make this pointer equal to one variables address, or just use `new`.

### Structure

Structure can't define itself, but can define it self's pointer.

Two method about structure initial function:

```c++
//First
struct StudentInfo {
    int id;
    char gender;
    StudentInfo(int _id, char _gender) : id(_id), gender(_gender) {}
};
//Second
struct StudentInfo {
    int id;
    char gender;
    StudentInfo(int _id, char _gender) {
        id = _id;
        gender = _gender;
    }
};
```

We can construct many initial function to adapt different case with different number of parameter.

### Float Point Number Compare

```c++
const double eps = 1e-8;
const double pi = acos(-1);
#define Equ(a, b) (fabs(a-b) < eps)
#define More(a, b) ((a-b) > eps) 
#define Less(a, b) ((a-b) < -eps)
#define MoreEqu(a, b) ((a-b) > -eps)
#define LessEqu(a, b) ((a-b) < eps)
```

### Input unkonwn lines

```c++
while(scanf("%s", str) != EOF) {} //string in `scanf` don't need `&`. 
while(gets(str) != NULL) {}
```

## C++ STL Induction

All need add `std::`.

### `vector`

1. As array, when number can't determine.
2. Sore uncertain number output data.
3. Represent diagram.

### `set`

1. `set` used to remove duplicate, and sort acending order.
2. If want to deal with data repetive, can use `multiset`.
3. Only need remove duplicate, can use `unordered_set`.

### `string`

### `map`

1. Map string to int.
2. Determine big number or other data structure, can as bool array.
3. Map string to string.
4. `multimap`, `unordered_map`.

### `queue`

BFS

### `priority_queue`

For `int`, `double` and `char`, default greater number have higher priority.

Set smaller is higher(For int): `priority_queue<int, vector<int>, greater<int> >`.

Set class priority:

```c++
//Only need overload `<`//Set smaller is higherstruct Fruit {    string name;    int price;    friend bool operator < (Fruit f1, Fruit f2) {        return f1.price > f2.price;    }};
```

### Some Function in `algorithm`

Firstly, need add `#include<algorithm>`.

```c++
using namespace std;// `x` and `y` can be float point numbermin(x, y);max(x, y);// `x` and `y` must be integerabs(x, y);
```

`swap(x, y)`, `x` and `y` can be structrue.

`reverse(first address, next address of last element)`.

```c++
//`next_permutation(first address, next address of last element)`, give next order of permutation.int a[3] = {1, 2 ,3};next_permutation(a, a+3);// a[3] = {1, 3, 2}
```

`fill(first address, next address of last element, value)` 

#### `sort()`

`sort(first element address, next address of last element, compare function)`, the first two parameters is must, and if the third parameter is blank, sort will use increment processing array.

Compare Function:

```c++
//Form small to large, conversely, form large to smallbool cmp(T a, T b) {    return a < b;}//Secondary orderbool cmp(node a, node b) {    if(a.x != b.x) {        return a.x < b.x;    }    else return a.y > b.y;}
```

Sort in STL: only `vector`, `string`, `deque` can use `sort()`, like `map`, `set` used Red-Black Tree can't sort.

For example:

```c++
string str[3] = {"a", "b", "c"};sort(str, str+3);vector<int> v;v.push_back(1);v.push_back(2);sort(v.begin(), v.end());
```

