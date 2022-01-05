# 找到大于给定数的下一个完美正方形

> 原文:[https://www . geesforgeks . org/find-下一个完美平方-大于给定数/](https://www.geeksforgeeks.org/find-the-next-perfect-square-greater-than-a-given-number/)

给定一个数字 N，任务是找到下一个大于 N 的完美正方形
**例**:

```
Input: N = 6
Output: 9
9 is a greater number than 6 and
is also a perfect square

Input: N = 9
Output: 16
```

**进场:**

1.  求给定 n 的平方根。
2.  使用 C++中的[楼层函数](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)计算其楼层值。
3.  然后再加 1。
4.  打印该数字的平方。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <iostream>
#include<cmath>
using namespace std;

// Function to find the next perfect square
int nextPerfectSquare(int N)
{
    int nextN = floor(sqrt(N)) + 1;

    return nextN * nextN;
}

// Driver Code
int main()
{
    int n = 35;

    cout << nextPerfectSquare(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to find the
// next perfect square
static int nextPerfectSquare(int N)
{
    int nextN = (int)Math.floor(Math.sqrt(N)) + 1;

    return nextN * nextN;
}

// Driver Code
public static void main(String args[])
{
    int n = 35;

    System.out.println (nextPerfectSquare(n));
}
}

// This code is contributed by Subhadeep
```

## 蟒蛇 3

```
# Python3 implementation of above approach

import math
#Function to find the next perfect square

def nextPerfectSquare(N):

    nextN = math.floor(math.sqrt(N)) + 1

    return nextN * nextN

if __name__=='__main__':
    N = 35
    print(nextPerfectSquare(N))

# this code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the
// next perfect square
static int nextPerfectSquare(int N)
{
    int nextN = (int)Math.Floor(Math.Sqrt(N)) + 1;

    return nextN * nextN;
}

// Driver Code
public static void Main()
{
    int n = 35;

    Console.WriteLine(nextPerfectSquare(n));
}
}

// This code is contributed
// by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation
// of above approach

// Function to find the
// next perfect square
function nextPerfectSquare($N)
{
    $nextN = floor(sqrt($N)) + 1;

    return $nextN * $nextN;
}

// Driver Code
$n = 35;

echo nextPerfectSquare($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find the next perfect square
function nextPerfectSquare(N)
{
    let nextN = Math.floor(Math.sqrt(N)) + 1;

    return nextN * nextN;
}

// Driver Code
let n = 35;

document.write(nextPerfectSquare(n));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
36
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*