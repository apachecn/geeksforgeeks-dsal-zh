# 计算没有前导零的 N 0 和 M 1 的数字

> 原文:[https://www . geesforgeks . org/count-numbers-having-n-0s-and-m-1s-不带前导零/](https://www.geeksforgeeks.org/count-numbers-having-n-0s-and-and-m-1s-with-no-leading-zeros/)

给定两个整数 **N** 和 **M** ，任务是找出不含前导零的 **N** 0 和 **M** 1 以及 **N + M** 总位数的不同数字。

**示例:**

> **输入:** N = 2，M = 2
> **输出:** 3
> 数字为 1001、1010、1100。
> 
> **输入:** N = 2，M = 3
> **输出:** 6
> 数字为 10011、10101、10110、11001、11010、11100。

**方法:**通过求 **N** 相似项和**M–1**相似项的全排列，可以很容易地解决问题。由于不允许前导零，1**1**始终固定在数字的开头。剩余的**M–1**1 和 **N** 0 以不同的排列方式排列。现在 **(A + B)** 对象的排列数，其中 **A** 同类型对象和 **B** 其他类型对象由 **(A + B)给出！/(一！* B！)**。因此，相异数的个数由 **(N + M -1)给出！/ (N！*(M–1)！)**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the factorial of a number
ll factorial(int f)
{
    ll fact = 1;

    for (int i = 2; i <= f; i++)
        fact *= (ll)i;

    return fact;
}

// Function to return the count of distinct
// (N + M) digit numbers having N 0's
// and and M 1's with no leading zeros
ll findPermutation(int N, int M)
{
    ll permutation = factorial(N + M - 1)
                     / (factorial(N) * factorial(M - 1));
    return permutation;
}

// Driver code
int main()
{
    int N = 3, M = 3;
    cout << findPermutation(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{
// Function to return the factorial of a number
static int factorial(int f)
{
    int fact = 1;

    for (int i = 2; i <= f; i++)
        fact *= (int)i;

    return fact;
}

// Function to return the count of distinct
// (N + M) digit numbers having N 0's
// and and M 1's with no leading zeros
static int findPermutation(int N, int M)
{
    int permutation = factorial(N + M - 1)
                    / (factorial(N) * factorial(M - 1));
    return permutation;
}

// Driver code
public static void main (String[] args)
{

    int N = 3, M = 3;
    System.out.println(findPermutation(N, M));
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the factorial
# of a number
def factorial(f):
    fact = 1
    for i in range(2, f + 1):
        fact *= i
    return fact

# Function to return the count of distinct
# (N + M) digit numbers having N 0's
# and and M 1's with no leading zeros
def findPermuatation(N, M):
    permutation = (factorial(N + M - 1) //
                  (factorial(N) * factorial(M - 1)))
    return permutation

# Driver code
N = 3; M = 3
print(findPermuatation(N, M))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function to return the factorial of a number
static int factorial(int f)
{
    int fact = 1;

    for (int i = 2; i <= f; i++)
        fact *= (int)i;

    return fact;
}

// Function to return the count of distinct
// (N + M) digit numbers having N 0's
// and and M 1's with no leading zeros
static int findPermutation(int N, int M)
{
    int permutation = factorial(N + M - 1)
                    / (factorial(N) * factorial(M - 1));
    return permutation;
}

// Driver code
public static void Main()
{
    int N = 3, M = 3;
    Console.Write(findPermutation(N, M));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach
// Function to return the factorial of a number
function factorial($f)
{
    $fact = 1;

    for ($i = 2; $i <= $f; $i++)
        $fact *= $i;

    return $fact;
}

// Function to return the count of distinct
// (N + M) digit numbers having N 0's
// and and M 1's with no leading zeros
function findPermutation($N,$M)
{
    $permutation = factorial($N + $M - 1)
                    / (factorial($N) * factorial($M - 1));
    return $permutation;
}

    // Driver code
    $N = 3;
    $M = 3;
    echo findPermutation($N, $M);

// This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the factorial of a number
function factorial(f)
{
    var fact = 1;

    for(var i = 2; i <= f; i++)
        fact *= i;

    return fact;
}

// Function to return the count of distinct
// (N + M) digit numbers having N 0's
// and and M 1's with no leading zeros
function findPermutation(N, M)
{
    var permutation = factorial(N + M - 1) /
                    (factorial(N) * factorial(M - 1));
    return permutation;
}

// Driver code
var N = 3, M = 3;

document.write(findPermutation(N, M));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
10
```