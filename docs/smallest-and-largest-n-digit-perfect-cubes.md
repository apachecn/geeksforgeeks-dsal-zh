# 最小和最大的 N 位完美立方体

> 原文:[https://www . geesforgeks . org/最小和最大 n 位数完美立方体/](https://www.geeksforgeeks.org/smallest-and-largest-n-digit-perfect-cubes/)

给定一个整数 **N** ，任务是找到最小和最大的 **N** 位数，它们也是完美的立方体。
**例:**

> **输入:** N = 2
> **输出:** 27 64
> 27 和 64 是最小和最大的两位数，也是完美立方体。
> **输入:** N = 3
> **输出:** 125 729

**方式:**从 **N = 1** 开始增加 **N** 的数值，系列将像 **8、64、729、9261、…..**为**最大的 N 位完美立方体**，其 **N <sup>第</sup>** 项将为**幂(ceil(cbrt(pow(10，(N)))))-1，3)** 。
和 **1，27，125，1000，…..**表示最小的 N 位完美立方体，其 **N <sup>第</sup>** 项为**幂(ceil(cbrt(pow(10，(N–1)))))、3)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the largest and
// the smallest n-digit perfect cube
void nDigitPerfectCubes(int n)
{

    // Smallest n-digit perfect cube
    cout << pow(ceil(cbrt(pow(10, (n - 1)))), 3) << " ";

    // Largest n-digit perfect cube
    cout << (int)pow(ceil(cbrt(pow(10, (n)))) - 1, 3);
}

// Driver code
int main()
{
    int n = 3;
    nDigitPerfectCubes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the largest and
    // the smallest n-digit perfect cube
    static void nDigitPerfectCubes(int n)
    {

        // Smallest n-digit perfect cube
        int smallest = (int)Math.pow(Math.ceil(Math.cbrt(Math.pow(10, (n - 1)))), 3);
        System.out.print(smallest + " ");

        int largest = (int)Math.pow(Math.ceil(Math.cbrt(Math.pow(10, (n)))) - 1, 3);
        System.out.print(largest);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 3;
        nDigitPerfectCubes(n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil

# Function to print the largest and
# the smallest n-digit perfect cube
def nDigitPerfectCubes(n):

    # Smallest n-digit perfect cube
    print(pow(ceil((pow(10, (n - 1))) **
                       (1 / 3)), 3), end = " ")

    # Largest n-digit perfect cube
    print(pow(ceil((pow(10, (n))) **
                       (1 / 3)) - 1, 3))

# Driver code
if __name__ == "__main__":

    n = 3
    nDigitPerfectCubes(n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the largest and
    // the smallest n-digit perfect cube
    static void nDigitPerfectCubes(int n)
    {

        // Smallest n-digit perfect cube
        int smallest = (int)Math.Pow(Math.Ceiling(MathF.Cbrt((float)Math.Pow(10, (n - 1)))), 3);
        Console.Write(smallest + " ");

        int largest = (int)Math.Pow(Math.Ceiling(MathF.Cbrt((float)Math.Pow(10, (n)))) - 1, 3);
        Console.Write(largest);
    }

    // Driver code
    static void Main()
    {
        int n = 3;
        nDigitPerfectCubes(n);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the largest and
// the smallest n-digit perfect cube
function nDigitPerfectCubes($n)
{

    // Smallest n-digit perfect cube
    print(pow(ceil(pow(pow(10, ($n - 1)),1/3)), 3)." ");

    // Largest n-digit perfect cube
    print((int)pow(ceil(pow(pow(10, ($n)),1/3)) - 1, 3));
}

// Driver code
$n = 3;
nDigitPerfectCubes($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to print the largest and
// the smallest n-digit perfect cube
function nDigitPerfectCubes( n)
{

    // Smallest n-digit perfect cube
     document.write( Math.pow(Math.ceil(Math.cbrt(Math.pow(10, (n - 1)))), 3) + " ");

    // Largest n-digit perfect cube
     document.write( Math.pow(Math.ceil(Math.cbrt(Math.pow(10, (n)))) - 1, 3));
}

// Driver code

    let n = 3;
    nDigitPerfectCubes(n);

    // This code contributed by aashish1995

</script>
```

**Output:** 

```
125 729
```