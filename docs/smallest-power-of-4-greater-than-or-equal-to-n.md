# 大于或等于 N 的 4 的最小幂

> 原文:[https://www . geesforgeks . org/4 的最小幂大于或等于 n/](https://www.geeksforgeeks.org/smallest-power-of-4-greater-than-or-equal-to-n/)

给定一个整数 **N** ，任务是找到大于或等于 **N** 的 4 的最小幂。

**示例:**

> **输入:** N = 12
> **输出:** 16
> 2 <sup>4</sup> = 16 这是 12 之后下一个需要的
> 更大的数。
> 
> **输入:**N = 81
> T3】输出: 81

**进场:**

1.  求给定 n 的第四个根。
2.  使用 [floor()](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 函数计算其楼层值。
3.  如果 n 本身是四的幂，那么返回 n。
4.  否则在底价上加 1。
5.  返回该数的四次幂。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest power
// of 4 greater than or equal to n
int nextPowerOfFour(int n)
{
    int x = floor(sqrt(sqrt(n)));

    // If n is itself is a power of 4
    // then return n
    if (pow(x, 4) == n)
        return n;
    else {
        x = x + 1;
        return pow(x, 4);
    }
}

// Driver code
int main()
{
    int n = 122;
    cout << nextPowerOfFour(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.Math;
import java.io.*;

class GFG
{

// Function to return the smallest power
// of 4 greater than or equal to n
static int nextPowerOfFour(int n)
{
    int x = (int)Math.floor(Math.sqrt(Math.sqrt(n)));

    // If n is itself is a power of 4
    // then return n
    if (Math.pow(x, 4) == n)
        return n;
    else {
        x = x + 1;
        return (int)Math.pow(x, 4);
    }
}

// Driver code
public static void main (String[] args)
              throws java.lang.Exception
{
    int n = 122;
    System.out.println(nextPowerOfFour(n));
}
}

// This code is contributed by nidhiva
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import math

# Function to return the smallest power
# of 4 greater than or equal to n
def nextPowerOfFour(n):
    x = math.floor((n**(1/2))**(1/2));

    # If n is itself is a power of 4
    # then return n
    if ((x**4) == n):
        return n;
    else:
        x = x + 1;
        return (x**4);

# Driver code

n = 122;
print(nextPowerOfFour(n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{

// Function to return the smallest power
// of 4 greater than or equal to n
static int nextPowerOfFour(int n)
{
    int x = (int)Math.Floor(Math.Sqrt(Math.Sqrt(n)));

    // If n is itself is a power of 4
    // then return n
    if (Math.Pow(x, 4) == n)
        return n;
    else
    {
        x = x + 1;
        return (int)Math.Pow(x, 4);
    }
}

// Driver code
public static void Main ()
{
    int n = 122;
    Console.WriteLine(nextPowerOfFour(n));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to return the smallest power
// of 4 greater than or equal to n
function nextPowerOfFour(n)
{
    let x = Math.floor(Math.sqrt(
            Math.sqrt(n)));

    // If n is itself is a power of 4
    // then return n
    if (Math.pow(x, 4) == n)
        return n;
    else
    {
        x = x + 1;
        return Math.pow(x, 4);
    }
}

// Driver code
let n = 122;
document.write(nextPowerOfFour(n));

// This code is contributed by mohit kumar 29

</script>
```

**Output:** 

```
256
```