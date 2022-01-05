# 打印 n 个 0 和 m 个 1，使得没有两个 0 和三个 1 在一起

> 原文:[https://www . geesforgeks . org/print-n-0s-和-m-1s-这样-不-二-0s-和-不-三-1s-在一起/](https://www.geeksforgeeks.org/print-n-0s-and-m-1s-such-that-no-two-0s-and-no-three-1s-are-together/)

给定两个整数 **n** 和 **m** ，其中 **n** 是 **0s** 的个数 **m** 是 **1s** 的个数。任务是将所有 **0s** 和 **1s** 打印在一行中，使得没有两个 **0s** 在一起，也没有三个 **1s** 在一起。如果无法根据情况排列 **0s** 和 **1s** ，则打印 **-1** 。
**举例:**

> **输入:** n = 1，m = 2
> **输出:** 011
> **输入:** n = 4，m = 8
> **输出:** 110110110101

**方法:**我们只有在**((n–1)≤m**和 **m ≤ 2 * (n + 1)** 时才有答案。

*   如果**(m = = n–1)**则打印图案**010101……**从 **0** 开始，直到所有 **0s** 和 **1s** 都已使用。
*   如果 **(m > n)** 和 **m ≤ 2 * (n + 1)** 则打印图案**110110110……**直到有多余的 **1s** 并在 **m** 变为等于**n–1**时变为图案**0101010……**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required pattern
void printPattern(int n, int m)
{

    // When condition fails
    if (m > 2 * (n + 1) || m < n - 1) {
        cout << "-1";
    }

    // When m = n - 1
    else if (abs(n - m) <= 1) {
        while (n > 0 && m > 0) {
            cout << "01";
            n--;
            m--;
        }
        if (n != 0) {
            cout << "0";
        }
        if (m != 0) {
            cout << "1";
        }
    }
    else {
        while (m - n > 1 && n > 0) {
            cout << "110";
            m = m - 2;
            n = n - 1;
        }
        while (n > 0) {
            cout << "10";
            n--;
            m--;
        }
        while (m > 0) {
            cout << "1";
            m--;
        }
    }
}

// Driver program
int main()
{
    int n = 4, m = 8;
    printPattern(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    // Function to print the required pattern
    static void printPattern(int n, int m)
    {
        // When condition fails
        if (m > 2 * (n + 1) || m < n - 1)
        {
            System.out.print("-1");
        }

        // When m = n - 1
        else if (Math.abs(n - m) <= 1)
        {
            while (n > 0 && m > 0)
            {
                System.out.print("01");
                n--;
                m--;

            }
            if (n != 0)
            {
                System.out.print("0");
            }
            if (m != 0)
            {
                System.out.print("1");
            }
        }
        else
        {
            while (m - n > 1 && n > 0)
            {
                System.out.print("110");
                m = m - 2;
                n = n - 1;
            }
            while (n > 0)
            {
                System.out.print("10");
                n--;
                m--;
            }
            while (m > 0)
            {
                System.out.print("1");
                m--;
            }
        }
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 4, m = 8;
        printPattern(n, m);
    }
}

// This code is contributed by Ita_c.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print the required pattern
def printPattern(n, m):

    # When condition fails
    if (m > 2 * (n + 1) or m < n - 1):
        print("-1", end = "")

    # When m = n - 1
    elif (abs(n - m) <= 1):
        while (n > 0 and m > 0):
            print("01", end = "");
            n -= 1
            m -= 1

        if (n != 0):
            print("0", end = "")
        if (m != 0):
            print("1", end = "")
    else:
        while (m - n > 1 and n > 0):
            print("110", end = "")
            m = m - 2
            n = n - 1

        while (n > 0):
            print("10", end = "")
            n -= 1
            m -= 1

        while (m > 0):
            print("1", end = "")
            m -= 1

# Driver Code
if __name__ == '__main__':
    n = 4
    m = 8
    printPattern(n, m)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to print the required pattern
    static void printPattern(int n, int m)
    {
        // When condition fails
        if (m > 2 * (n + 1) || m < n - 1)
        {
            Console.Write("-1");
        }
        // When m = n - 1
        else if (Math.Abs(n - m) <= 1)
        {
            while (n > 0 && m > 0)
            {
                Console.Write("01");
                n--;
                m--;

            }
            if (n != 0)
            {
                Console.Write("0");
            }
            if (m != 0)
            {
                Console.Write("1");
            }
        }
        else
        {
            while (m - n > 1 && n > 0) 
            {
                Console.Write("110");
                m = m - 2;
                n = n - 1;
            }
            while (n > 0)
            {
                Console.Write("10");
                n--;
                m--;
            }
            while (m > 0)
            {
                Console.Write("1");
                m--;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 4, m = 8;
        printPattern(n, m);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print the required pattern
function printPattern($n, $m)
{
    // When condition fails
    if ($m > 2 * ($n + 1) || $m < $n - 1)
    {
        echo("-1");
    }

    // When m = n - 1
    else if (abs($n - $m) <= 1)
    {
        while ($n > 0 && $m > 0)
        {
            System.out.print("01");
            $n--;
            $m--;

        }
        if ($n != 0)
        {
            echo("0");
        }
        if ($m != 0)
        {
            echo("1");
        }
    }
    else
    {
        while ($m - $n > 1 && $n > 0)
        {
            echo("110");
            $m = $m - 2;
            $n = $n - 1;
        }
        while ($n > 0)
        {
            echo("10");
            $n--;
            $m--;
        }
        while ($m > 0)
        {
            echo("1");
            $m--;
        }
    }
}

// Driver code
$n = 4; $m = 8;    
printPattern($n, $m);

// This code is contributed by
// Mukul Singh.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to print the required pattern
function printPattern( n,  m)
{

    // When condition fails
    if (m > 2 * (n + 1) || m < n - 1) {
        document.write("-1");
    }

    // When m = n - 1
    else if (Math.abs(n - m) <= 1) {
        while (n > 0 && m > 0) {
            document.write("01");
            n--;
            m--;
        }
        if (n != 0) {
            document.write("0");
        }
        if (m != 0) {
            document.write("1");
        }
    }
    else {
        while (m - n > 1 && n > 0) {
            document.write("110");
            m = m - 2;
            n = n - 1;
        }
        while (n > 0) {
            document.write("10");
            n--;
            m--;
        }
        while (m > 0) {
            document.write("1");
            m--;
        }
    }
}

var n = 4, m = 8;
    printPattern(n, m);

</script>
```

**Output**

```
110110110101
```