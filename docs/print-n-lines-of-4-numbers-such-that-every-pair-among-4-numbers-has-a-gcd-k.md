# 打印 N 行 4 个数字，使 4 个数字中的每一对都有一个 GCD K

> 原文:[https://www . geeksforgeeks . org/print-n-line-of-4-numbers-so-4-numbers 中的每对都有-a-gcd-k/](https://www.geeksforgeeks.org/print-n-lines-of-4-numbers-such-that-every-pair-among-4-numbers-has-a-gcd-k/)

给定 N 和 K，任务是打印 N 行，其中每行包含 4 个数字，使得这 4 个数字中的每一个都有一个 [GCD](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) K，并且 N*4 中使用的最大数字应该最小化。
**注:**如有多输出，打印任意一个。
**示例:**

> **输入:** N = 1，K = 1
> **输出**:1 2 3 5
> 1、2、3 和 5 中的每一对给出一个 GCD K，其中最大的数字是 5，这是最小的可能。
> 
> **输入** : 2 2
> **输出** :
> 2 4 6 2 2
> 14 18 10 16
> 在上面的输入中，最大的数字是 22，这是制作 2 行 4 个数字的最小可能。

**方法:**第一个观察是，如果我们能解出 K=1 的给定问题，那么我们可以通过简单地将答案与 K 相乘来解决带有 GCD K 的问题，我们知道任何三个连续的奇数在配对时总是有一个 GCD 1，所以每一行的三个数字都可以很容易地得到。因此，这些行看起来像:

```
1 3 5 _ 
7 9 11 _ 
13 15 17 _  
.
.
.
```

偶数不能总是插入，因为在第三行插入 6 会使 GCD(6，9)为 3。因此，可以插入的最佳数字是每行前两个 off 数字之间的数字。因此，模式如下所示:

```
1 2 3 5  
7 8 9 11  
13 14 15 17  
.
.
.
```

为了获得给定的 GCD K，人们可以很容易地将 K 乘以所获得的数字。因此对于第一行:

1.  第一个数字将是 k * (6*i+1)
2.  第二个数字将是 k * (6*i+1)
3.  第三个数字将是 k * (6*i+3)
4.  第四个数字将是 k * (6*i+5)

N*4 个数字中最大的数字将是***k *(6 * I–1)***
以下是上述方法的实现。

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print N lines
void printLines(int n, int k)
{
    // Iterate N times to print N lines
    for (int i = 0; i < n; i++) {
        cout << k * (6 * i + 1) << " "
             << k * (6 * i + 2) << " "
             << k * (6 * i + 3) << " "
             << k * (6 * i + 5) << endl;
    }
}
// Driver Code
int main()
{
    int n = 2, k = 2;
    printLines(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// Function to print N lines
static void printLines(int n, int k)
{
    // Iterate N times to print N lines
    for (int i = 0; i < n; i++) {
        System.out.println ( k * (6 * i + 1) + " "
            + k * (6 * i + 2) + " "
            + k * (6 * i + 3) + " "
            + k * (6 * i + 5) );
    }
}
// Driver Code
public static void main(String args[])
{
    int n = 2, k = 2;
    printLines(n, k);
}
}
```

## 蟒蛇 3

```
# Python implementation of the
# above approach.

# Function to print N lines
def printLines(n, k) :

    # Iterate N times to print N lines
    for i in range(n) :
        print( k * (6 * i + 1),
                k * (6 * i + 2),
               k * (6 * i + 3),
               k * (6 * i + 5))

# Driver code    
if __name__ == "__main__" :

    n, k = 2, 2
    printLines(n, k)

# This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to print N lines
function printLines($n, $k)
{
    // Iterate N times to print N lines
    for ($i = 0; $i < $n; $i++)
    {
        echo ($k * (6 * $i + 1));
        echo (" ");
        echo ($k * (6 * $i + 2));
        echo (" ");
        echo ($k * (6 * $i + 3));
        echo (" ");
        echo ($k * (6 * $i + 5));
        echo ("\n");
    }
}

// Driver Code
$n = 2;
$k = 2;
printLines($n, $k);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{
// Function to print N lines
static void printLines(int n, int k)
{
    // Iterate N times to print N lines
    for (int i = 0; i < n; i++)
    {
        Console.WriteLine ( k * (6 * i + 1) + " " +
                            k * (6 * i + 2) + " " +
                            k * (6 * i + 3) + " " +
                            k * (6 * i + 5) );
    }
}

// Driver Code
public static void Main()
{
    int n = 2, k = 2;
    printLines(n, k);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
// javascript implementation of the
// above approach

    // Function to print N lines
    function printLines(n , k)
    {

        // Iterate N times to print N lines
        for (i = 0; i < n; i++)
        {
            document.write(k * (6 * i + 1)
            + " " + k * (6 * i + 2) + " "
            + k * (6 * i + 3) + " "
            + k * (6 * i + 5)+"<br/>");
        }
    }

    // Driver Code
        var n = 2, k = 2;
        printLines(n, k);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
2 4 6 10
14 16 18 22
```

**时间复杂度:**O(4 * N)
T3】辅助空间: O(1)