# 公约数与公倍数

## 最大公约数

```c++
//欧几里得算法
int gcd(int a, int b) { return b ? gcd(b, a % b) : a; }
```

## 最小公倍数

```c++
int lcm = a / gcd(a, b) * b;
```

# 分数的四则运算

```c++
struct Fraction {
	int up, down;
}
// 核心部分是分数的化简，其最简形式满足以下三点
// 1. down为非负数
// 2. 值为0时，up = 0, down = 1
// 3. gcd(up, down) = 1
void reduction(Fraction &ans) {
    if (ans.down < 0) {
        ans.up = -ans.up;
        ans.down = -ans.down;
    }
    if (ans.up == 0) {
        ans.up = 0;
        ans.down = 1;
    } else {
        int g = gcd(ans.up, ans.down);
        ans.up /= g;
        ans.down /= g;
    }
}
// 运算部分很容易写出来
```
# 素数

## 数筛法判断素数

表的大小参考素数定理：$\pi(n)$为值不超过$n$素数的个数

$$
\lim_{n\rightarrow \infty} \frac{ln(n)\pi(n)}{n} = 1
$$

```c++
// pi(n) > 1e5时，取MAX = 100 * n比较合适
bool notPrime[MAX];
vector<int> prime(n);
// 查找n个素数
void findPrime(int n) {
    int cnt = 0;
    for (int i = 2; i < MAX; ++i) {
        if (!notPrime[i]) {
	        prime[cnt++] = i;
            if (cnt == n) break;
            for (int j = 2 * i; j < MAX; j += i) {
                notPrime[j] = true;
            }
        }
    }
}
```

## 质因子分解

```c++
// x为质因子的值，cnt为个数
struct factor {
    int x, cnt;
    factor(int _x, int _cnt) : x(_x), cnt(_cnt) {}
};
vector<factor> factors;
// 数n的质因子最多有一个大于sqrt(n)的值
void getFactors(int n) {
    int m = sqrt(n);
    for (int i = 0; i < prime.size() && prime[i] <= m; ++i) {
        if (n % prime[i] == 0) {
            factors.emplace_back(prime[i], 0);
            while (n % prime[i] == 0) {
                ++factors.back().cnt;
                n /= prime[i];
            }
        }
    }
    if (n != 1) {
        factors.emplace_back(n, 1);
    }
}
```

# 快速幂

求$a^b$ mod $p$

```c++
using ll = long long;
ll binaryPow(ll a, ll b, ll p) {
    ll ans = 1;
    while (b > 0) {
        if (b & 1) {
            ans = ans * a % p;
        }
        a = a * a % p;
        b >>= 1;
    }
    return ans;
}
```

# 组合数

## 求n!的质因子p的个数

$n!$中有$(\frac{n}{p} + \frac{n}{p^2} +  \frac{n}{p^3} + \cdots)$个$p$。

```c++
int cal(int n, int p) {
    int ans = 0;
    while (n) {
        ans += (n /= p);
    }
    return ans;
}
```

## 计算 $C_n^m$

1. 由$C_n^m = C_{n - 1}^{m} + C_{n - 1}^{m - 1}$，递推
2. 定义式变形计算

```c++
ll calC(ll m, ll n) {
    int ans = 0;
    for (int i = 1; i <= m; ++i) {
        ans += ans * (n - i + 1) / i;  //要先乘再除，否则无法整除
    }
    return ans;
}
```

## 计算 $C_n^m$ mod p

1. 当$m \le n \le 1000$时，用递推
2. 当$m \le n \le 10^6$时，使用定义算

```c++
ll C(ll m, ll n, ll p) {
    ll ans = 1;
    for (int i = 0; prime[i] <= n; ++i) {
        int b = cal(n, p) - cal(m, p) - cal(n - m, p);
        ans = ans * binaryPow(prime[i], b, p) % p;
    }
    return ans;
}
```
