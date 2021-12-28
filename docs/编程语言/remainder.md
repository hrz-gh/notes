# 余数的值

Mathematically ,the remainder is for arbitrary dividend and positive divisor ,but the results are different in different programming languages ,such as python and c++.

For example:

| Dividend & Divisor | Math   | Python | C++  |
| ------------------ | ------ | ------ | ---- |
| $7\div 3$          | 1      | 1      | 1    |
| $7\div (-3)$       | \ or 1 | -2     | 1    |
| $(-7)\div 3$       | 2      | 2      | -1   |
| $(-7)\div (-3)$    | \ or 2 | -1     | -1   |

If divisor could be negative ,results in Math could be 1 or 2.
Generalizing ,sign of remainder of Python is same as divisor ,and that of C++ is same as dividend. 