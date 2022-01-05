# 在范围[L，R]

内的所有完全数的和

> 原文:[https://www . geesforgeks . org/所有完全数之和-范围内-l-r/](https://www.geeksforgeeks.org/sum-of-all-perfect-numbers-lying-in-the-range-l-r/)

给定两个数字 **L** 、 **R** ，表示范围**【L，R】**，任务是找出范围【L，R】内所有[完全数](https://www.geeksforgeeks.org/perfect-number/)的和。
**举例:**

> **输入:** L = 6，R = 10
> **输出:** 6
> **说明:**
> 从 6 到 10，唯一的完全数是 6。
> **输入:** L = 6，R = 28
> **输出:** 34
> **说明:**
> 范围内有两个完全数【6，28】。它们是，{6，28}
> 6 + 28 = 34。

**天真方法:**这个问题的天真方法是[通过迭代范围[L，R]中的每个数字来检查一个数字是否是完全数](https://www.geeksforgeeks.org/perfect-number/)。如果范围内有 N 个数字，这种方法的时间复杂度是 **O(N * sqrt(K))** ，其中 K 是范围[L，R]内的最大数字(R)。
**高效方法:**思路是利用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念进行预计算，将所有数字的和存储在一个数组中。

*   将数组初始化到最大大小，使数组的每个索引“I”代表从**【0，I】**开始的所有完全数的总和。
*   迭代数组，对于每个索引，检查它是否是一个完美的数字。
*   如果它是一个完全数，那么将存储在前一个索引(I–1)和当前索引“I”的总和相加。
*   如果它不是一个完美的数字，那么将存储在前一个索引(I–1)的总和和值 0 相加。
*   最后，对于每个查询[L，R]，返回值:

```
sum = arr[R] - arr[L - 1]
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// sum of all perfect numbers
// lying in the range [L, R]

#include <bits/stdc++.h>
#define ll int
using namespace std;

// Array to store the sum
long long pref[100010];

// Function to check if a number is
// a perfect number or not
int isPerfect(int n)
{
    int sum = 1;

    // Iterating till the square root
    // of the number and checking if
    // the sum of divisors is equal
    // to the number or not
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }

    // If it is a perfect number, then
    // return the number
    if (sum == n && n != 1)
        return n;

    // Else, return 0
    return 0;
}

// Function to precompute the sum
// of perfect squares and store
// then in an array
void precomputation()
{
    for (int i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1] + isPerfect(i);
    }
}

int main()
{

    int L = 6, R = 28;

    precomputation();

    cout << pref[R] - pref[L - 1];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// sum of all perfect numbers
// lying in the range [L, R]
class GFG {

    // Array to store the sum
    static int pref [] = new int[10000];

    // Function to check if a number is
    // a perfect number or not
    static int isPerfect(int n)
    {
        int sum = 1;

        // Iterating till the square root
        // of the number and checking if
        // the sum of divisors is equal
        // to the number or not
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                if (i * i != n)
                    sum = sum + i + n / i;
                else
                    sum = sum + i;
            }
        }

        // If it is a perfect number, then
        // return the number
        if (sum == n && n != 1)
            return n;

        // Else, return 0
        return 0;
    }

    // Function to precompute the sum
    // of perfect squares and store
    // then in an array
    static void precomputation()
    {
        for (int i = 1; i < 10000; ++i) {
            pref[i] = pref[i - 1] + isPerfect(i);
        }
    }

    public static void main (String[] args)
    {

        int L = 6, R = 28;

        precomputation();

        System.out.println(pref[R] - pref[L - 1]);

    }

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find the
# sum of all perfect numbers
# lying in the range [L, R]

from math import sqrt

# Array to store the sum
pref = [0]*10000;

# Function to check if a number is
# a perfect number or not
def isPerfect(n)  :

    sum = 1;

    # Iterating till the square root
    # of the number and checking if
    # the sum of divisors is equal
    # to the number or not
    for i in range(2, int(sqrt(n)) + 1) :
        if (n % i == 0) :
            if (i * i != n) :
                sum = sum + i + n // i;
            else :
                sum = sum + i;

    # If it is a perfect number, then
    # return the number
    if (sum == n and n != 1) :
        return n;

    # Else, return 0
    return 0;

# Function to precompute the sum
# of perfect squares and store
# then in an array
def precomputation() :

    for i in range(1, 10000) :
        pref[i] = pref[i - 1] + isPerfect(i);

if __name__ == "__main__" :

    L = 6; R = 28;

    precomputation();

    print(pref[R] - pref[L - 1]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// sum of all perfect numbers
// lying in the range [L, R]
using System;

public class GFG {

    // Array to store the sum
    static int []pref = new int[10000];

    // Function to check if a number is
    // a perfect number or not
    static int isPerfect(int n)
    {
        int sum = 1;

        // Iterating till the square root
        // of the number and checking if
        // the sum of divisors is equal
        // to the number or not
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                if (i * i != n)
                    sum = sum + i + n / i;
                else
                    sum = sum + i;
            }
        }

        // If it is a perfect number, then
        // return the number
        if (sum == n && n != 1)
            return n;

        // Else, return 0
        return 0;
    }

    // Function to precompute the sum
    // of perfect squares and store
    // then in an array
    static void precomputation()
    {
        for (int i = 1; i < 10000; ++i) {
            pref[i] = pref[i - 1] + isPerfect(i);
        }
    }

    public static void Main(String[] args)
    {

        int L = 6, R = 28;

        precomputation();

        Console.WriteLine(pref[R] - pref[L - 1]);

    }

}
// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// sum of all perfect numbers
// lying in the range [L, R]

// Array to store the sum
var pref = Array(100010).fill(0);

// Function to check if a number is
// a perfect number or not
function isPerfect(n)
{
    var sum = 1;

    // Iterating till the square root
    // of the number and checking if
    // the sum of divisors is equal
    // to the number or not
    for (var i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }

    // If it is a perfect number, then
    // return the number
    if (sum == n && n != 1)
        return n;

    // Else, return 0
    return 0;
}

// Function to precompute the sum
// of perfect squares and store
// then in an array
function precomputation()
{
    for (var i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1] + isPerfect(i);
    }
}

var L = 6, R = 28;
precomputation();
document.write( pref[R] - pref[L - 1]);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
34
```

**时间复杂度:**

*   预计算所花费的时间是 **O(K * sqrt(K))** ，其中 K 是我们正在执行预计算的数字
*   预计算后，在 **O(1)** 中回答每个查询。

**辅助空间:** O(10 <sup>5</sup>