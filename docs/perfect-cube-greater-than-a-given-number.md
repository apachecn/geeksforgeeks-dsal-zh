# 大于给定数的完美立方体

> 原文:[https://www . geesforgeks . org/perfect-cube-大于给定数字/](https://www.geeksforgeeks.org/perfect-cube-greater-than-a-given-number/)

给定一个数字 N，任务是找到下一个大于 N 的完美立方体
**例:**

```
Input: N = 6
Output: 8
8 is a greater number than 6 and
is also a perfect cube

Input: N = 9
Output: 27
```

**进场:**

1.  求给定 n 的立方根。
2.  使用 C++中的[楼层函数](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)计算其楼层值。
3.  然后再加 1。
4.  打印该数字的立方体。

## C++

```
// C++ implementation of above approach
#include <cmath>
#include <iostream>
using namespace std;

// Function to find the next perfect cube
int nextPerfectCube(int N)
{
    int nextN = floor(cbrt(N)) + 1;

    return nextN * nextN * nextN;
}

// Driver Code
int main()
{
    int n = 35;

    cout << nextPerfectCube(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{
// Function to find the next perfect cube
static int nextPerfectCube(int N)
{
    int nextN = (int)Math.floor(Math.cbrt(N)) + 1;

    return nextN * nextN * nextN;
}

// Driver Code
public static void main(String args[])
{
    int n = 35;

    System.out.print(nextPerfectCube(n));
}
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# from math import everything
from math import *

# Function to find the next perfect cube
def nextPerfectCube(N) :

    nextN = floor(N ** (1/3)) + 1

    return nextN ** 3

# Driver code    
if __name__ == "__main__" :

    n = 35
    print(nextPerfectCube(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{
// Function to find the next perfect cube
static int nextPerfectCube(int N)
{
    int nextN = (int)Math.Floor(Math.Pow(N,
                         (double)1/3)) + 1;

    return nextN * nextN * nextN;
}

// Driver Code
public static void Main()
{
    int n = 35;

    Console.Write(nextPerfectCube(n));
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// from math import everything

// Function to find the next perfect cube
function nextPerfectCube($N)
{
    $nextN = (int)(floor(pow($N,(1/3))) + 1);

    return $nextN * $nextN * $nextN ;
}

// Driver code    

    $n = 35;
    print(nextPerfectCube($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find the next perfect cube
function nextPerfectCube(N)
{
    let nextN = Math.floor(Math.cbrt(N)) + 1;

    return nextN * nextN * nextN;
}

// Driver Code
let n = 35;

document.write(nextPerfectCube(n));

</script>
```

**Output:** 

```
64
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*