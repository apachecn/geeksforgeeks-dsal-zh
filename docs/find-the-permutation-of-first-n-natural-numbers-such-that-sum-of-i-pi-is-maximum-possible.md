# 求前 N 个自然数的排列，使得 i % Pi 的和最大可能

> 原文:[https://www . geesforgeks . org/find-第一个 n 个自然数的排列-这样 I-pi-的和就是最大可能/](https://www.geeksforgeeks.org/find-the-permutation-of-first-n-natural-numbers-such-that-sum-of-i-pi-is-maximum-possible/)

给定一个数字 **N** 。任务是找到第一个 **N** 自然数的排列 **P** ，使得**I % P<sub>I</sub>T9】的和最大可能。任务是找到最大可能的和，而不是它的排列。**

**示例:**

> **输入:** N = 5
> **输出:** 10
> 可能的排列是 2 3 4 5 1。
> 模数值将为{1，2，3，4，0}。
> 1 + 2 + 3 + 4 + 0 = 10
> 
> **输入:**N = 8
> T3】输出: 28

**逼近:**最大可能和为**(N *(N–1))/2**，由排列 **2，3，4，5，…..n，1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the permutation of
// the first N natural numbers such that
// the sum of (i % Pi) is maximum possible
// and return the maximum sum
int Max_Sum(int n)
{
    return (n * (n - 1)) / 2;
}

// Driver code
int main()
{
    int n = 8;

    // Function call
    cout << Max_Sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the permutation of
// the first N natural numbers such that
// the sum of (i % Pi) is maximum possible
// and return the maximum sum
static int Max_Sum(int n)
{
    return (n * (n - 1)) / 2;
}

// Driver code
public static void main (String[] args)
{
    int n = 8;

    // Function call
    System.out.println(Max_Sum(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the permutation of
# the first N natural numbers such that
# the sum of (i % Pi) is maximum possible
# and return the maximum sum
def Max_Sum(n) :

    return (n * (n - 1)) // 2;

# Driver code
if __name__ == "__main__" :

    n = 8;

    # Function call
    print(Max_Sum(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the permutation of
// the first N natural numbers such that
// the sum of (i % Pi) is maximum possible
// and return the maximum sum
static int Max_Sum(int n)
{
    return (n * (n - 1)) / 2;
}

// Driver code
public static void Main (String[] args)
{
    int n = 8;

    // Function call
    Console.WriteLine(Max_Sum(n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the permutation of
// the first N natural numbers such that
// the sum of (i % Pi) is maximum possible
// and return the maximum sum
function Max_Sum(n)
{
    return parseInt((n * (n - 1)) / 2);
}

// Driver code
let n = 8;

// Function call
document.write(Max_Sum(n));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
28
```