# 大于 n 的最小整数，由数字 m 正好 k 倍组成

> 原文:[https://www . geesforgeks . org/最小-整数-大于-n-这样-它-它-由-数字-m-精确-k-倍组成/](https://www.geeksforgeeks.org/smallest-integer-greater-than-n-such-that-it-consists-of-digit-m-exactly-k-times/)

给定三个整数 **n** 、 **m** 和 **k** ，任务是找到最小的整数 **> n** ，使得**数字 m** 在其中恰好出现 **k** 次。
**示例:**

> **输入:** n = 111，m = 2，k = 2
> **输出:** 122
> **输入:** n = 111，m = 2，k = 3
> **输出:** 222

**方法:**从 **n + 1** 开始迭代，对于每个整数 **i** 检查它是否由数字 **m** 精确地构成 **k** 次。这样就可以找到最小整数 **> n** 与**数字 m** 正好出现 **k** 次。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n contains
// digit m exactly k times
bool digitWell(int n, int m, int k)
{
    int cnt = 0;
    while (n > 0) {
        if (n % 10 == m)
            ++cnt;
        n /= 10;
    }
    return cnt == k;
}

// Function to return the smallest integer > n
// with digit m occurring exactly k times
int findInt(int n, int m, int k)
{

    int i = n + 1;

    while (true) {
        if (digitWell(i, m, k))
            return i;
        i++;
    }
}

// Driver code
int main()
{
    int n = 111, m = 2, k = 2;
    cout << findInt(n, m, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if n contains
// digit m exactly k times
static boolean digitWell(int n, int m, int k)
{
    int cnt = 0;
    while (n > 0)
    {
        if (n % 10 == m)
            ++cnt;
        n /= 10;
    }
    return cnt == k;
}

// Function to return the smallest integer > n
// with digit m occurring exactly k times
static int findInt(int n, int m, int k)
{

    int i = n + 1;

    while (true)
    {
        if (digitWell(i, m, k))
            return i;
        i++;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 111, m = 2, k = 2;
    System.out.println(findInt(n, m, k));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if n
# contains digit m exactly k times
def digitWell(n, m, k):

    cnt = 0
    while (n > 0):

        if (n % 10 == m):
            cnt = cnt + 1;
        n = (int)(n / 10);

    return cnt == k;

# Function to return the smallest integer > n
# with digit m occurring exactly k times
def findInt(n, m, k):

    i = n + 1;

    while (True):
        if (digitWell(i, m, k)):
            return i;
        i = i + 1;

# Driver code
n = 111; m = 2; k = 2;
print(findInt(n, m, k));

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function that returns true if n contains
// digit m exactly k times
static bool digitWell(int n, int m, int k)
{
    int cnt = 0;
    while (n > 0)
    {
        if (n % 10 == m)
            ++cnt;
        n /= 10;
    }
    return cnt == k;
}

// Function to return the smallest integer > n
// with digit m occurring exactly k times
static int findInt(int n, int m, int k)
{

    int i = n + 1;

    while (true)
    {
        if (digitWell(i, m, k))
            return i;
        i++;
    }
}

// Driver code
public static void Main()
{
    int n = 111, m = 2, k = 2;
    Console.WriteLine(findInt(n, m, k));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if n
// contains digit m exactly k times
function digitWell($n, $m, $k)
{
    $cnt = 0;
    while ($n > 0)
    {
        if ($n % 10 == $m)
            ++$cnt;
        $n = floor($n / 10);
    }
    return $cnt == $k;
}

// Function to return the smallest integer > n
// with digit m occurring exactly k times
function findInt($n, $m, $k)
{
    $i = $n + 1;

    while (true)
    {
        if (digitWell($i, $m, $k))
            return $i;
        $i++;
    }
}

// Driver code
$n = 111;
$m = 2;
$k = 2;

echo findInt($n, $m, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if n contains
// digit m exactly k times
function digitWell(n, m, k)
{
    var cnt = 0;
    while (n > 0) {
        if (n % 10 == m)
            ++cnt;
        n = Math.floor(n/10);
    }
    if(cnt == k)
      return true;
    else
        return false;
}

// Function to return the smallest integer > n
// with digit m occurring exactly k times
function findInt(n, m, k)
{

    var i = n + 1;

    while (true) {
        if (digitWell(i, m, k))
            return i;
        i++;
    }
}

// Driver code
    var n = 111, m = 2, k = 2;
    document.write(findInt(n, m, k));

</script>
```

**Output:** 

```
122
```

**时间复杂度:** O(n * log <sub>10</sub> n)

**辅助空间:** O(1)