# 异或的应用

## Properties

commucative, associative, 自反性:$a\oplus b\oplus b = a$

Calculate $f(n) = 1\oplus2\oplus\cdots \oplus n$.

```bash
if n == 4*m, then f(n) = n
else if n == 4*m + 1, then f(n) = 1
else if n == 4*m + 2, then f(n) = n+1
else n = 0
```

`m` is a integer.

## Application

### Exchange Two Number without Extra Space

```c
a ^= b;
b ^= a;
a ^= b;
```

### One Question

1-1000放在含有1001个元素的数组中，只有唯一的一个元素值重复，其它均只出现一次。每个数组元素只能访问一次，设计一个算法，将它找出来；不用辅助存储空间，能否设计一个算法实现？

$$x = (\text{1001个数的异或}）\oplus(1\oplus2\oplus3\oplus\cdots\oplus1000)$$