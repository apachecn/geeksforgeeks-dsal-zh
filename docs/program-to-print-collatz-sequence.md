# 打印排序顺序的程序

> 原文:[https://www . geesforgeks . org/program-to-print-collaz-sequence/](https://www.geeksforgeeks.org/program-to-print-collatz-sequence/)

从任意正整数 N 开始，对应 N 定义[排序序列](https://en.wikipedia.org/wiki/Collatz_conjecture)为以下运算形成的数:

1.  如果 n 是偶数，那么 n = n / 2。
2.  如果 n 是奇数，那么 n = 3*n + 1。
3.  重复以上步骤，直到变成 1。

**例:**

```
Input : 3
Output : 3, 10, 5, 16, 8, 4, 2, 1       

Input : 6
Output : 6, 3, 10, 5, 16, 8, 4, 2, 1
```

下面是实现:

## C++

```
// CPP program to print Collatz sequence
#include <bits/stdc++.h>
using namespace std;

void printCollatz(int n)
{
    // We simply follow steps
    // while we do not reach 1
    while (n != 1)
    {
        cout << n << " ";

        // If n is odd
        if (n & 1)
            n = 3*n + 1;

        // If even
        else
            n = n/2;
    }

    // Print 1 at the end
    cout << n;
}

// Driver code
int main()
{
    printCollatz(6);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// Collatz sequence
import java.io.*;

class GFG
{
    static void printCollatz(int n)
    {
        // We simply follow steps
        // while we do not reach 1
        while (n != 1)
        {
            System.out.print(n + " ");

            // If n is odd
            if ((n & 1) == 1)
                n = 3 * n + 1;

            // If even
            else
                n = n / 2;
        }

        // Print 1 at the end
        System.out.print(n);
    }

    // Driver code
    public static void main (String[] args)
    {
        printCollatz(6);
    }
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python 3 program to print
# Collatz sequence

def printCollatz(n):

    # We simply follow steps
    # while we do not reach 1
    while n != 1:
        print(n, end = ' ')

        # If n is odd
        if n & 1:
            n = 3 * n + 1

        # If even
        else:
            n = n // 2

    # Print 1 at the end
    print(n)

# Driver code
printCollatz(6)

# This code is contributed
# by vaibhav29498
```

## C#

```
// C# program to print Collatz sequence
using System;

class GFG {

    static void printCollatz(int n)
    {
        // We simply follow steps
        // while we do not reach 1
        while (n != 1)
        {
            Console.Write (n + " ");

            // If n is odd
            if ((n & 1) == 1)
                n = 3 * n + 1;

            // If even
            else
                n = n / 2;
        }

        // Print 1 at the end
        Console.Write (n);
    }

    // Driver code
    static void Main()
    {
        printCollatz(6);
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print Collatz sequence

function printCollatz($n)
{
    // We simply follow steps
    // while we do not reach 1
    while ($n != 1)
    {
        echo $n . " ";

        // If $n is odd
        if ($n & 1)
            $n = 3 * $n + 1;

        // If even
        else
            $n = $n / 2;
    }

    // Print 1 at the end
    echo $n;
}

// Driver code
printCollatz(6);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

    // Javascript program to print Collatz sequence

    function printCollatz(n)
    {
        // We simply follow steps
        // while we do not reach 1
        while (n != 1)
        {
            document.write(n + " ");

            // If n is odd
            if ((n & 1) != 0)
                n = 3*n + 1;

            // If even
            else
                n = parseInt(n/2, 10);
        }

        // Print 1 at the end
        document.write(n);
    }

    printCollatz(6);

</script>
```

**输出**T2】

```
6 3 10 5 16 8 4 2 1
```