# n 个男孩和女孩围绕圆桌交替的座位安排

> 原文:[https://www . geeksforgeeks . org/座位安排-n 个男孩和女孩-交替围绕圆桌会议/](https://www.geeksforgeeks.org/seating-arrangement-of-n-boys-and-girls-alternatively-around-a-round-table/)

有 n 个男孩和 n 个女孩围着一张圆桌坐成一圈。任务是找出 n 个男孩和 n 个女孩轮流坐在圆桌旁的方法。给出 n<10
T1】个例子:T3】

```
Input: n = 5 
Output: 2880

Input: n = 1
Output: 1
```

**进场:**

1.  首先找出男生可以被安排在圆桌上的方式总数。
    安排男生上桌的方式数= **(n-1)！**
2.  给男生安排后，现在给女生安排。和坐男孩一样，他们之间有 n 个空位。所以有 n 个位置和 n 个女生。所以女生坐男生中间的排列总数是 **n！**。

3.  因此总方式数=(男生排列数)*(男生中女生坐的方式数)= **(n-1)！* (n！)**

以下是上述方法的实现:

## C++

```
// C++ program to find number of ways in which
// n boys and n girls can sit alternatively
// sound a round table.
#include <bits/stdc++.h>
using namespace std;

#define ll long int

int main()
{

    // Get n
    ll n = 5;

    // find fac1 = (n-1)!
    ll fac1 = 1;
    for (int i = 2; i <= n - 1; i++)
        fac1 = fac1 * i;

    // Find fac2 = n!
    ll fac2 = fac1 * n;

    // Find total number of ways
    ll totalWays = fac1 * fac2;

    // Print the total number of ways
    cout << totalWays << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways
// in which n boys and n girls can sit
// alternatively sound a round table.
import java .io.*;

class GFG
{
public static void main(String[] args)
{

    // Get n
    long n = 5;

    // find fac1 = (n-1)!
    long fac1 = 1;
    for (int i = 2; i <= n - 1; i++)
        fac1 = fac1 * i;

    // Find fac2 = n!
    long fac2 = fac1 * n;

    // Find total number of ways
    long totalWays = fac1 * fac2;

    // Print the total number of ways
    System.out.println(totalWays);
}
}

// This code is contributed
// by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find number
# of ways in which n boys and n
# girls can sit alternatively
# sound a round table.

# Get n
n = 5

# find fac1 = (n-1)!
fac1 = 1
for i in range(2, n):
    fac1 = fac1 * i

# Find fac2 = n!
fac2 = fac1 * n

# Find total number of ways
totalWays = fac1 * fac2

# Print the total number of ways
print(totalWays)

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find number of ways
// in which n boys and n girls can sit
// alternatively sound a round table.
using System;

class GFG
{
public static void Main()
{

    // Get n
    long n = 5;

    // find fac1 = (n-1)!
    long fac1 = 1;
    for (int i = 2; i <= n - 1; i++)
        fac1 = fac1 * i;

    // Find fac2 = n!
    long fac2 = fac1 * n;

    // Find total number of ways
    long totalWays = fac1 * fac2;

    // Print the total number of ways
    Console.WriteLine(totalWays);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// ways in which n boys and n
// girls can sit alternatively
// sound a round table.

// Driver Code

// Get n
$n = 5;

// find fac1 = (n-1)!
$fac1 = 1;
for ($i = 2; $i <= $n - 1; $i++)
    $fac1 = $fac1 * $i;

// Find fac2 = n!
$fac2 = $fac1 * $n;

// Find total number of ways
$totalWays = $fac1 * $fac2;

// Print the total number of ways
echo $totalWays . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// Javascript program to find number of
// ways in which n boys and n
// girls can sit alternatively
// sound a round table.

// Driver Code

// Get n
let n = 5;

// find fac1 = (n-1)!
let fac1 = 1;
for (let i = 2; i <= n - 1; i++)
    fac1 = fac1 * i;

// Find fac2 = n!
fac2 = fac1 * n;

// Find total number of ways
totalWays = fac1 * fac2;

// Print the total number of ways
document.write(totalWays + "<br>");

// This code is contributed
// by gfgking

</script>
```

**Output:** 

```
2880
```