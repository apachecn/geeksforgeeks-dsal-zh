# 将 N 分成 M 个部分，使得最大和最小部分之间的差值最小

> 原文:[https://www . geeksforgeeks . org/partition-n-in-m-parts-这样-max-and-min-part-之间的差异最小/](https://www.geeksforgeeks.org/partition-n-into-m-parts-such-that-difference-between-max-and-min-part-is-smallest/)

给定两个整数 **N** 和 **M** ，将 N 分割成 M 个整数，使得分割得到的最大和最小整数之间的差值尽可能小。

打印 M 号 **A1、A2……。Am** ，如:

*   总和(A) = N
*   最大(α)-最小(α)被最小化。

**示例**:

```
Input : N = 11, M = 3
Output : A[] = {4, 4, 3}

Input : N = 8, M = 4
Output : A[] = {2, 2, 2, 2}
```

为了尽量缩小条款之间的差异，我们应该让所有条款尽可能地相互接近。假设，我们可以打印任何浮点值而不是整数，在这种情况下，答案是 0(打印 N/M ^ M 次)。但是因为我们需要打印整数，所以我们可以把它分成两部分，地板(N/M)和地板(N/M)+1，这样我们得到的答案最多是 1。
我们需要打印每种类型的多少个术语？
假设我们打印**楼层(N/M)** M 次，总和等于**N –( N % M)**。所以我们需要选择 **N%M** 项，增加 1。

下面是上述方法的实现:

## C++

```
// C++ program to partition N into M parts
// such that difference Max and Min
// part is smallest

#include <bits/stdc++.h>
using namespace std;

// Function to partition N into M parts such
// that difference Max and Min part
// is smallest
void printPartition(int n, int m)
{
    int k = n / m; // Minimum value

    int ct = n % m; // Number of (K+1) terms

    int i;

    for (i = 1; i <= ct; i++)
        cout << k + 1 << " ";

    for (; i <= m; i++)
        cout << k << " ";
}

// Driver Code
int main()
{
    int n = 5, m = 2;

    printPartition(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to partition N into M parts
// such that difference Max and Min
// part is smallest

import java.io.*;

class GFG {

// Function to partition N into M parts such
// that difference Max and Min part
// is smallest
static void printPartition(int n, int m)
{
    int k = n / m; // Minimum value

    int ct = n % m; // Number of (K+1) terms

    int i;

    for (i = 1; i <= ct; i++)
        System.out.print( k + 1 + " ");

    for (; i <= m; i++)
        System.out.print( k + " ");
}

// Driver Code

    public static void main (String[] args) {
    int n = 5, m = 2;

    printPartition(n, m);
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to partition N into M parts
# such that difference Max and Min
# part is the smallest

# Function to partition N into M parts such
# that difference Max and Min part
# is smallest
def printPartition(n, m):
    k = int(n / m)
    # Minimum value

    ct = n % m
    # Number of (K+1) terms

    for i in range(1,ct+1,1):
        print(k + 1,end= " ")
    count = i
    for i in range(count,m,1):
        print(k,end=" ")

# Driver Code
if __name__ == '__main__':
    n = 5
    m = 2
    printPartition(n, m)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to partition N into M parts
// such that difference Max and Min
// part is smallest
using System;

class GFG
{
static void printPartition(int n, int m)
{
    int k = n / m; // Minimum value

    int ct = n % m; // Number of (K+1) terms

    int i;

    for (i = 1; i <= ct; i++)
        Console.Write( k + 1 + " ");

    for (; i <= m; i++)
        Console.Write( k + " ");
}

// Driver Code
static public void Main ()
{
    int n = 5, m = 2;

    printPartition(n, m);
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to partition N into
// M parts such that difference
// Max and Min part is smallest

// Function to partition N into M
// parts such that difference Max
// and Min part is smallest
function printPartition($n, $m)
{
    $k = (int)($n / $m); // Minimum value

    $ct = $n % $m; // Number of (K+1) terms

    for ($i = 1; $i <= $ct; $i++)
        echo $k + 1 . " ";

    for (; $i <= $m; $i++)
        echo $k . " ";
}

// Driver Code
$n = 5; $m = 2;

printPartition($n, $m);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to partition N into M parts
// such that difference Max and Min
// part is smallest

// Function to partition N into M parts such
// that difference Max and Min part
// is smallest
function prletPartition(n, m)
{
    let k = Math.floor(n / m); // Minimum value

    let ct = n % m; // Number of (K+1) terms

    let i;

    for (i = 1; i <= ct; i++)
        document.write( k + 1 + " ");

    for (; i <= m; i++)
        document.write( k + " ");
}

// driver program

    let n = 5, m = 2;

    prletPartition(n, m);

</script>
```

**Output:** 

```
3 2
```

**时间复杂度:** O(M)