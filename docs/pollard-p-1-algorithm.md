# 波拉德 p-1 算法

> 原文:[https://www.geeksforgeeks.org/pollard-p-1-algorithm/](https://www.geeksforgeeks.org/pollard-p-1-algorithm/)

将一个大的奇整数 **n** 分解成其对应的素因子可能是一项困难的任务。蛮力方法可以测试所有小于 n 的整数，直到找到除数。这被证明是非常耗时的，因为除数本身可能是一个非常大的素数。

**波拉德 p-1 算法**是求任意整数素因子的较好方法。利用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)和 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 的组合帮助，它能够在短时间内计算所有不同的素因子。

#### 算法

*   给定一个数 n.
    初始化 a = 2，i = 2
*   直到返回一个因子为止，如果 1 < d < n，则
    返回 d
    否则
    I<-I+1
    T7】
*   其他因素，d'
*   如果 d '不是质因数
    n < - d'
    转到 1
    否则
    d 和 d '是两个质因数。

在上面的算法中,“a”的幂不断增加，直到得到 n 的因子“d”。一旦得到 d，另一个因子“d”就是 n/d。如果 d’不是素数，那么对 d’重复同样的任务

**示例:**

```
Input : 1403
Output : Prime factors of 1403 are 61 23.
Explanation : n = 1403, a = 2, i = 2

1st Iteration:
    a = (2^2) mod 1403 = 4
    d = GCD(3, 1403) = 1
    i = 2 + 1 = 3

2nd Iteration:
    a = (4^3) mod 1403 = 64
    d = GCD(63, 1403) = 1
    i = 3 + 1 = 4

3rd Iteration:
    a = (64^4) mod 1403 = 142
    d = GCD(141, 1403) = 1
    i = 4 + 1 = 5

4th Iteration:
    a = (142^5) mod 1403 = 794
    d = GCD(793, 1403) = 61

Since 1 < d < n, one factor is 61.
d' = 1403 / 61 = 23.

Input : 2993
Output : Prime factors of 2993 are 41 73.

```

下面是实现。

```
# Python code for Pollard p-1 
# factorization Method

# importing "math" for 
# calculating GCD
import math

# importing "sympy" for 
# checking prime
import sympy

# function to generate 
# prime factors
def pollard(n):

    # defining base
    a = 2

    # defining exponent
    i = 2

    # iterate till a prime factor is obtained
    while(True):

        # recomputing a as required
        a = (a**i) % n

        # finding gcd of a-1 and n
        # using math function
        d = math.gcd((a-1), n)

        # check if factor obtained
        if (d > 1):

            #return the factor
            return d

            break

        # else increase exponent by one 
        # for next round
        i += 1

# Driver code
n = 1403

# temporarily storing n
num = n

# list for storing prime factors
ans = []

# iterated till all prime factors
# are obtained
while(True):

    # function call
    d = pollard(num)

    # add obtained factor to list
    ans.append(d)

    # reduce n
    r = int(num/d)

    # check for prime using sympy
    if(sympy.isprime(r)):

        # both prime factors obtained
        ans.append(r)

        break

    # reduced n is not prime, so repeat
    else:

        num = r

# print the result
print("Prime factors of", n, "are", *ans)
```

**输出:**

```
Prime factors of 1403 are 61 23
```