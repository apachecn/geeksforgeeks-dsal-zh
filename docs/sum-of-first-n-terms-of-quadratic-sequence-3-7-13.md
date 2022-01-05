# 二次序列 3 + 7 + 13 +的前 N 项之和……

> 原文:[https://www . geesforgeks . org/一次 n 项二次序列之和-3-7-13/](https://www.geeksforgeeks.org/sum-of-first-n-terms-of-quadratic-sequence-3-7-13/)

给定一个如下所示的二次级数，任务是求这个级数的前 n 项之和。

> Sn = 3 + 7 + 13 + 21 + 31 + …..+最新条款

**示例:**

```
Input: N = 3
Output: 23

Input: N = 4
Output: 44
```

**进场:**
让系列表现为

```
Sn = 3 + 7 + 13 + ... + tn
```

在哪里

*   **S <sub>n</sub>** 代表级数直到 n 项的和。
*   **t <sub>n</sub>** 代表级数的第 n 项。

现在，为了公式化该系列，需要通过取该系列的连续元素的差来形成元素。

> 方程式 1: Sn = 3 + 7 + 13 + 21 + 31 +…..+ tn-1 + tn
> 方程式 2:Sn = 0+3+7+13+21+31+……+TN-1+TN
> (通过将所有元素向右移动 1 个位置来编写上述系列)

现在，从等式 1 中减去等式 2，即**(等式 1–等式 2)**

> Sn–Sn =(3–0)+(7–3)+(13–7)+(31–21)+……+(TN-TN-1)–TN
> =>0 = 3+4+6+8+10+……+(TN–TN-1)–TN

在上面的系列中，除了 3，从 4 到(TN–TN-1)的项将形成 A.P.
，因为 A.P 的 n 个项之和的公式为:

> sn = n *(2 * a+(n–1)* d)/2

这意味着，

> 串联:4+6+8+……+(TN–TN-1)
> AP 由(n-1)项组成。

因此，

> **本系列之和:(n-1)*(2 * 4+(n-2)* 2)/2**T2】

因此，原级数:
0 = 3+(n-1)*(2 * 4+(n-2)* 2)/2–TN
其中 **tn = n^2 + n + 1** 这是第 n 项。
因此，

> 系列的前 n 项之和将为:
> TN = n^2+n+1
> sn =![\sum   ](img/80dcc82c5be724a933f51395b0f59185.png "Rendered by QuickLaTeX.com")(n^2)+![\sum   ](img/80dcc82c5be724a933f51395b0f59185.png "Rendered by QuickLaTeX.com")n+![\sum   ](img/80dcc82c5be724a933f51395b0f59185.png "Rendered by QuickLaTeX.com")(1)
> sn = n *(n+1)*(n+2)/6+n *(n+1)/2+n
> sn = n*(n^2+3 * n+5)/3

**以下是上述方法的实施:**

## C++

```
// C++ program to find sum of first n terms

#include <bits/stdc++.h>
using namespace std;

int calculateSum(int n)
{
    // Sum = n*(n^2 + 3*n + 5)/3
    return n * (pow(n, 2) + 3 * n + 5) / 3;
}

int main()
{
    // number of terms to be included in the sum
    int n = 3;

    // find the Sum
    cout << "Sum = " << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of first n terms
import java.util.*;

class solution
{
//function to calculate sum of n terms of the series
static int calculateSum(int n)
{
    // Sum = n*(n^2 + 3*n + 5)/3
    return n * (int)  (Math.pow(n, 2) + 3 * n + 5 )/ 3;
}

public static void main(String arr[])
{
    // number of terms to be included in the sum
    int n = 3;

    // find the Sum
    System.out.println("Sum = " +calculateSum(n));

}
}
```

## 蟒蛇 3

```
# Python 3 program to find sum
# of first n terms
from math import pow

def calculateSum(n):

    # Sum = n*(n^2 + 3*n + 5)/3
    return n * (pow(n, 2) + 3 * n + 5) / 3

if __name__ == '__main__':

    # number of terms to be included
    # in the sum
    n = 3

    # find the Sum
    print("Sum =", int(calculateSum(n)))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find sum of first n terms
using System;
class gfg
{
 public double calculateSum(int n)
 {
    // Sum = n*(n^2 + 3*n + 5)/3
    return (n * (Math.Pow(n, 2) + 3 * n + 5) / 3);
  }
}

//driver code
class geek
{
 public static int Main()
 {
     gfg g = new gfg();
    // number of terms to be included in the sum
    int n = 3;
    //find the Sum
    Console.WriteLine( "Sum = {0}", g.calculateSum(n));
    return 0;
 }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of first n terms

function calculateSum($n)
{
    // Sum = n*(n^2 + 3*n + 5)/3
    return $n * (pow($n, 2) + 3 *
                     $n + 5) / 3;
}

// Driver Code

// number of terms to be
// included in the sum
$n = 3;

// find the Sum
echo "Sum = " . calculateSum($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of first n terms

// Function to find the quadratic
// equation whose roots are a and b
function calculateSum(n)
{

    // Sum = n*(n^2 + 3*n + 5)/3
    return n * (Math.pow(n, 2) + 3 * n + 5 ) / 3;
}

// Driver Code

// Number of terms to be
// included in the sum
var n = 3;

// Find the Sum

document.write("Sum = " + calculateSum(n));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
Sum = 23
```