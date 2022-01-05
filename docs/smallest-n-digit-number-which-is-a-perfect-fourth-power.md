# 最小的 N 位数，是完美的四次方

> 原文:[https://www . geeksforgeeks . org/最小 n 位数-哪是完美的四次方/](https://www.geeksforgeeks.org/smallest-n-digit-number-which-is-a-perfect-fourth-power/)

给定一个整数 **N** ，任务是找到最小的 **N 位**数，这是一个完美的四次方。
**例:**

> **输入:** N = 2
> **输出:** 16
> 唯一有效的数字是 2 <sup>4</sup> = 16
> 和 3 <sup>4</sup> = 81 但 16 是最小值。
> **输入:** N = 3
> **输出:**256
> 4<sup>4</sup>= 256

**方法:**可以观察到，对于 **N = 1，2，3，…** 的值，该系列将像 **1，16，256，1296，10000，104976，1048576，…** 一样继续，其 **N <sup>第</sup>T9】项将是**幂(ceil( (pow(pow(10，(N-1))，1 / 4))))
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>

using namespace std;

// Function to return the smallest n-digit
// number which is a perfect fourth power
int cal(int n)
{
    double res = pow(ceil((pow(pow(10,
                          (n - 1)), 1 / 4) )), 4);
    return (int)res;
}

// Driver code
int main()
{
    int n = 1;
    cout << (cal(n));
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the smallest n-digit
// number which is a perfect fourth power
static int cal(int n)
{
    double res = Math.pow(Math.ceil((
                 Math.pow(Math.pow(10,
                (n - 1)), 1 / 4) )), 4);
    return (int)res;
}

// Driver code
public static void main(String[] args)
{
    int n = 1;
    System.out.println(cal(n));
}
}

// This code is contributed by CodeMech
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import *

# Function to return the smallest n-digit
# number which is a perfect fourth power
def cal(n):
    res = pow(ceil( (pow(pow(10, (n - 1)), 1 / 4) ) ), 4)
    return int(res)

# Driver code
n = 1
print(cal(n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the smallest n-digit
// number which is a perfect fourth power
static int cal(int n)
{
    double res = Math.Pow(Math.Ceiling((
                 Math.Pow(Math.Pow(10,
                 (n - 1)), 1 / 4) )), 4);
    return (int)res;
}

// Driver code
public static void Main()
{
    int n = 1;
    Console.Write(cal(n));
}
}

// This code is contributed
// by Akanksha_Rai
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest n-digit
// number which is a perfect fourth power
function cal(n)
{
    var res = Math.pow(Math.ceil((Math.pow(Math.pow(10,
                          (n - 1)), 1 / 4) )), 4);
    return parseInt(res);
}

// Driver code
var n = 1;
document.write(cal(n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
1
```