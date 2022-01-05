# 给定基中最大的可左截断素数

> 原文:[https://www . geesforgeks . org/最大-左-可截断-给定基数中的质数/](https://www.geeksforgeeks.org/largest-left-truncatable-prime-in-a-given-base/)

给定一个代表一个数的基数的整数 **N** ，任务是在给定的基数 **N** 中找到最大的[左截断素数](https://www.geeksforgeeks.org/left-truncatable-prime/)。

**示例:**

> **输入:** N = 3
> **输出:** 23
> **说明:**
> 基数 N =(3)中的左可截断素数如下:
> (12)<sub>3</sub>=(5)<sub>10</sub>
> (212)<sub>3</sub>=(23)<sub>10</sub>
> 因此，最大的左可截断素数
> 
> **输入:**N = 5
> T3】输出: 7817

**方法:**想法是在给定基数 **N** 中生成所有可左截断的素数，并根据以下观察结果打印最大的可左截断素数:

> 如果一个包含 **(i)** 数字的数是一个可左截断的素数，那么从最后一个**(I–1)**数字形成的数必须是一个可左截断的素数。
> 
> 因此，要做一个数字的左可截质数 **i** ，首先要找到所有的**(I–1)**数字的左可截质数。

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如**候选[]** ，将所有可能的左可截断素数存储在给定的基数 **N** 中。
*   使用变量 **i** 迭代范围**【0，无穷大】**，并插入所有可截断的左素数位数 **i** 。如果没有找到由 **i** 位组成的左侧可截断数字，则从循环中返回。
*   最后，打印数组中出现的[最大元素**候选[]** 。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to implement
# the above approach
import random

# Function to check if a is
# a composite number or not
# using Miller-Rabin primality test
def try_composite(a, d, n, s):

    # ((a) ^ d) % n equal to 1
    if pow(a, d, n) == 1:
        return False

    for i in range(s):
        if pow(a, 2**i * d, n) == n-1:
            return False
    return True

# Function to check if a number
# is prime or not using
# Miller-Rabin primality test
def is_probable_prime(n, k):

    # Base Case
    if n == 0 or n == 1:
        return False

    if n == 2:
        return True

    if n % 2 == 0:
        return False

    s = 0
    d = n-1

    while True:
        quotient, remainder = divmod(d, 2)
        if remainder == 1:
            break
        s += 1
        d = quotient

    # Iterate given number of k times 
    for i in range(k):
        a = random.randrange(2, n)

        # If a is a composite number
        if try_composite(a, d, n, s):
            return False

    # No base tested showed
    # n as composite
    return True

# Function to find the largest
# left-truncatable prime number
def largest_left_truncatable_prime(base):

    # Stores count of digits
    # in a number
    radix = 0

    # Stores left-truncatable prime
    candidates = [0]

    # Iterate over the range [0, infinity]
    while True:

        # Store left-truncatable prime
        # containing i digits
        new_candidates = []

        # Stores base ^ radix
        multiplier = base ** radix

        # Iterate over all possible 
        # value of the given base
        for i in range(1, base):

            # Append the i in radix-th digit
            # in all (i - 1)-th digit 
            # left-truncatable prime
            for x in candidates:

                # If a number with i digits
                # is prime
                if is_probable_prime(
                    x + i * multiplier, 30):
                    new_candidates.append(
                         x + i * multiplier)

        # If no left-truncatable prime found
        # whose digit is radix                 
        if len(new_candidates) == 0:
            return max(candidates)

        # Update candidates[] to all 
        # left-truncatable prime
        # whose digit is radix 
        candidates = new_candidates

        # Update radix
        radix += 1

# Driver Code
if __name__ == "__main__": 
    N = 3
    ans = largest_left_truncatable_prime(N)
    print(ans)
```

**Output:**

```
23

```

***时间复杂度:** O(k * log <sup>3</sup> N，其中 k 是在[米勒-拉宾素性检验](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/)*
***中进行的回合数辅助空间:** O(X)* ，其中 **X** 是以 N 为基数的可左截断素数的总数