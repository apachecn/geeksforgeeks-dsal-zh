# 求最小的数 K，使得 K % p = 0，q % K = 0

> 原文:[https://www . geesforgeks . org/find-minist-number-k-so-k-p-0-and-q-k-0/](https://www.geeksforgeeks.org/find-smallest-number-k-such-that-k-p-0-and-q-k-0/)

给定两个整数 **p** 和 **q** ，任务是找到最小的数 **K** ，使得 **K % p = 0** 和 **q % K = 0** 。如果没有这样的 **K** 是可能的，那么打印 **-1** 。
**举例:**

> **输入:** p = 2，q = 8
> **输出:** 2
> 2 % 2 = 0 和 8 % 2 = 0
> **输入:** p = 5，q = 14
> **输出:** -1

**方法:**为了使 **K** 成为可能， **q** 必须能被 **p** 整除。

*   如果 **q % p = 0** 则打印 **p**
*   否则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// value K such that K % p = 0
// and q % k = 0
int getMinVal(int p, int q)
{

    // If K is possible
    if (q % p == 0)
        return p;

    // No such K is possible
    return -1;
}

// Driver code
int main()
{
    int p = 24, q = 48;
    cout << getMinVal(p, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the minimum
// value K such that K % p = 0
// and q % k = 0
static int getMinVal(int p, int q)
{

    // If K is possible
    if (q % p == 0)
        return p;

    // No such K is possible
    return -1;
}

// Driver code
public static void main (String[] args)
{
    int p = 24, q = 48;
    System.out.println(getMinVal(p, q));
}
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# value K such that K % p = 0
# and q % k = 0
def getMinVal(p, q):

    # If K is possible
    if q % p == 0:
        return p

    # No such K is possible
    return -1

# Driver code
p = 24; q = 48
print(getMinVal(p, q))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// value K such that K % p = 0
// and q % k = 0
static int getMinVal(int p, int q)
{

    // If K is possible
    if (q % p == 0)
        return p;

    // No such K is possible
    return -1;
}

// Driver code
public static void Main ()
{
    int p = 24, q = 48;
    Console.WriteLine(getMinVal(p, q));
}
}

// This code is contributed
// by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// value K such that K % p = 0
// and q % k = 0
function getMinVal($p, $q)
{

    // If K is possible
    if ($q % $p == 0)
        return $p;

    // No such K is possible
    return -1;
}

// Driver code
$p = 24;
$q = 48;
echo getMinVal($p, $q);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the minimum
// value K such that K % p = 0
// and q % k = 0
function getMinVal(p, q)
{

    // If K is possible
    if (q % p == 0)
        return p;

    // No such K is possible
    return -1;
}

// driver program

    let p = 24, q = 48;
    document.write(getMinVal(p, q));

</script>
```

**Output:** 

```
24
```