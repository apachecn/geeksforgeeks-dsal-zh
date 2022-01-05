# 前 N 个非负整数的连续位差之和

> 原文:[https://www . geesforgeks . org/第一 n 个非负整数的连续位差之和/](https://www.geeksforgeeks.org/sum-of-consecutive-bit-differences-of-first-n-non-negative-integers/)

给定一个正整数 **N** ，任务是找出从 0 到 N 的所有连续位差的和。
**注:**如果像(3，4)这样的两个数字的位长不同，则在开头追加 0(011，100)。
**示例:**

> **输入:** N = 3
> **输出:** 4
> **解释:**
> 位差为(0，1) + (1，2) + (2，3) = 1 + 2 + 1 = 4。
> **输入:** N = 7
> **输出:** 11

**天真方法:**
最简单的方法是按位比较范围内的两个连续值，找出这两个数字相差多少位。把这个位差加到和上。这样得到的最终和就是所需的解。
***时间复杂度:** O(N)*
**方法:**
将进行以下观察以优化上述解决方案:

*   数字的连续位差遵循一种模式，即每个等于(2 <sup>i</sup> )的值 X 与其前一个数字的位差为(i + 1)，X 以上的(2<sup>I</sup>–1)个数字和 X 以下的(2<sup>I</sup>–1)个数字遵循相同的模式。
*   对于 X = 4 (2 <sup>2</sup> ，i = 2 有一个位差是(2 + 1)，数字(1，2，3)和(5，6，7)遵循相同的位差模式。

```
For X = 4, the pattern is as follows:
NUM   BIT Diff
1     1(0, 1)
2     2(1, 2)
3     1(2, 3)
4     3(3, 4)
5     1(4, 5)
6     2(5, 6)
7     1(6, 7)
```

按照以下步骤解决问题:

*   对于每 **N** ，求最近的小于等于 N 的数，是 2 的幂。说那个号码是 **M** 。
*   对于所有小于 M 的数字，下面的递归方法可以用来找出连续位差的和。

> Count(I)=(I+1)+2 * Count(I–1)
> 其中 I 是 2 的最近幂的指数。

*   初始化一个大小为 65(基于 0 的索引)的数组，以存储使用递归函数 Count()时获得的值，以便将来如果需要 Count()的相同值，可以直接获得这些值，而无需递归调用 Count()函数来节省时间。
*   使用下面的公式对大于 M 的其余数字重复相同的过程。

> 总和=总和+ (i+1) +计数(i-1)

**例如:**
对于 N = 10，使用**计数(3)** 计算最接近的 2 的幂即 M = 8 的和，然后对大于 8 的剩余数重复该过程。
以下是上述方法的实施:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

long long a[65] = { 0 };

// Recursive function to count
// the sum of bit differences
// of numbers from 1 to
// pow(2, (i+1)) - 1
long long Count(int i)
{
    // base cases
    if (i == 0)
        return 1;

    else if (i < 0)
        return 0;

    // Recursion call if the sum
    // of bit difference of numbers
    // around i are not calculated
    if (a[i] == 0) {
        a[i] = (i + 1) + 2 * Count(i - 1);
        return a[i];
    }

    // return the sum of bit
    // differences if already
    // calculated
    else
        return a[i];
}

// Function to calculate the
// sum of bit differences up to N
long long solve(long long n)
{
    long long i, sum = 0;

    while (n > 0) {

        // nearest smaller power
        // of 2
        i = log2(n);

        // remaining numbers
        n = n - pow(2, i);

        // calculate the count
        // of bit diff
        sum = sum + (i + 1) + Count(i - 1);
    }
    return sum;
}

// Driver code
int main()
{
    long long n = 7;
    cout << solve(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;
class GFG{

static int a[] = new int[65];

// Recursive function to count
// the sum of bit differences
// of numbers from 1 to
// pow(2, (i+1)) - 1
static int Count(int i)
{

    // base cases
    if (i == 0)
        return 1;

    else if (i < 0)
        return 0;

    // Recursion call if the sum
    // of bit difference of numbers
    // around i are not calculated
    if (a[i] == 0)
    {
        a[i] = (i + 1) + 2 * Count(i - 1);
        return a[i];
    }

    // return the sum of bit
    // differences if already
    // calculated
    else
        return a[i];
}

// Function to calculate the
// sum of bit differences up to N
static int solve(int n)
{
    int i, sum = 0;

    while (n > 0)
    {

        // nearest smaller power
        // of 2
        i = (int)(Math.log(n) / Math.log(2));

        // remaining numbers
        n = n - (int)Math.pow(2, i);

        // calculate the count
        // of bit diff
        sum = sum + (i + 1) + Count(i - 1);
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int  n = 7;
    System.out.println(solve(n));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above problem
import math

a = [0] * 65

# Recursive function to count
# the sum of bit differences
# of numbers from 1 to
# pow(2, (i+1)) - 1
def Count(i):

    # Base cases
    if (i == 0):
        return 1

    elif (i < 0):
        return 0

    # Recursion call if the sum
    # of bit difference of numbers
    # around i are not calculated
    if (a[i] == 0):
        a[i] = (i + 1) + 2 * Count(i - 1)
        return a[i]

    # Return the sum of bit
    # differences if already
    # calculated
    else:
        return a[i]

# Function to calculate the
# sum of bit differences up to N
def solve(n):

    sum = 0

    while (n > 0):

        # Nearest smaller power
        # of 2
        i = int(math.log2(n))

        # Remaining numbers
        n = n - pow(2, i)

        # Calculate the count
        # of bit diff
        sum = sum + (i + 1) + Count(i - 1)

    return sum

# Driver code
n = 7

print(solve(n))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above problem
using System;
class GFG{

static int []a = new int[65];

// Recursive function to count
// the sum of bit differences
// of numbers from 1 to
// pow(2, (i+1)) - 1
static int Count(int i)
{

    // base cases
    if (i == 0)
        return 1;

    else if (i < 0)
        return 0;

    // Recursion call if the sum
    // of bit difference of numbers
    // around i are not calculated
    if (a[i] == 0)
    {
        a[i] = (i + 1) + 2 * Count(i - 1);
        return a[i];
    }

    // return the sum of bit
    // differences if already
    // calculated
    else
        return a[i];
}

// Function to calculate the
// sum of bit differences up to N
static int solve(int n)
{
    int i, sum = 0;

    while (n > 0)
    {

        // nearest smaller power
        // of 2
        i = (int)(Math.Log(n) / Math.Log(2));

        // remaining numbers
        n = n - (int)Math.Pow(2, i);

        // calculate the count
        // of bit diff
        sum = sum + (i + 1) + Count(i - 1);
    }
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int n = 7;
    Console.Write(solve(n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program for the above problem

    let a = new Array(65);
    a.fill(0);

    // Recursive function to count
    // the sum of bit differences
    // of numbers from 1 to
    // pow(2, (i+1)) - 1
    function Count(i)
    {
        // base cases
        if (i == 0)
            return 1;

        else if (i < 0)
            return 0;

        // Recursion call if the sum
        // of bit difference of numbers
        // around i are not calculated
        if (a[i] == 0) {
            a[i] = (i + 1) + 2 * Count(i - 1);
            return a[i];
        }

        // return the sum of bit
        // differences if already
        // calculated
        else
            return a[i];
    }

    // Function to calculate the
    // sum of bit differences up to N
    function solve(n)
    {
        let i, sum = 0;

        while (n > 0) {

            // nearest smaller power
            // of 2
            i = parseInt(Math.log(n) / Math.log(2), 10);

            // remaining numbers
            n = n - parseInt(Math.pow(2, i), 10);

            // calculate the count
            // of bit diff
            sum = sum + (i + 1) + Count(i - 1);
        }
        return sum;
    }

    let n = 7;
    document.write(solve(n));

</script>
```

**Output:** 

```
11
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*