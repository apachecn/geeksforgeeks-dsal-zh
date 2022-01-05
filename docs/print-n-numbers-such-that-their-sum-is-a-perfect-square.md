# 打印 n 个数字，使其和为一个完美的正方形

> 原文:[https://www . geeksforgeeks . org/print-n-numbers-so-sum-is-a-perfect-square/](https://www.geeksforgeeks.org/print-n-numbers-such-that-their-sum-is-a-perfect-square/)

给定一个整数 **n** ，任务是打印 **n** 个数字，这样它们的和就是一个完美的正方形。
**例:**

> **输入:** n = 3
> **输出:** 1 3 5
> 1 + 3 + 5 = 9 = 3 <sup>2</sup>
> 
> **输入:** n = 4
> **输出:**1 3 5 7
> 1+3+5+7 = 16 = 4<sup>2</sup>

**逼近:**第一个 **n 个**奇数的和总是一个完美的平方。因此，我们将打印第一个 **n** 奇数作为输出。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print n numbers such that
// their sum is a perfect square
void findNumbers(int n)
{
    int i = 1;
    while (i <= n) {

        // Print ith odd number
        cout << ((2 * i) - 1) << " ";
        i++;
    }
}

// Driver code
int main()
{
    int n = 3;
    findNumbers(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print n numbers such that
    // their sum is a perfect square
    static void findNumbers(int n)
    {
        int i = 1;
        while (i <= n) {

            // Print ith odd number
            System.out.print(((2 * i) - 1) + " ");
            i++;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 3;
        findNumbers(n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print n numbers such that
# their sum is a perfect square
def findNumber(n):
    i = 1
    while i <= n:

        # Print ith odd number
        print((2 * i) - 1, end = " ")
        i += 1

# Driver code    
n = 3
findNumber(n)

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to print n numbers such that
    // their sum is a perfect square
    public static void findNumbers(int n)
    {
        int i = 1;
        while (i <= n) {

            // Print ith odd number
            Console.Write(((2 * i) - 1) + " ");
            i++;
        }
    }

    // Driver code
    public static void Main(string[] args)
    {
        int n = 3;
        findNumbers(n);
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to prn numbers such that
// their sum is a perfect square
function findNumbers($n)
{
    $i = 1;
    while ($i <= $n)
    {

        // Print ith odd number
        echo ((2 * $i) - 1) . " ";
        $i++;
    }
}

// Driver code
$n = 3;
findNumbers($n);

// This code contributed by PrinciRaj1992
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to print n numbers such that
// their sum is a perfect square
function findNumbers(n)
{
    var i = 1;
    while (i <= n) {

        // Print ith odd number
        document.write(((2 * i) - 1)+" ") ;
        i++;
    }
}

var n = 3;
    findNumbers(n);

</script>
```

**Output**

```
1 3 5 
```

**时间复杂度:** O(N)

**辅助空间:** O(1)