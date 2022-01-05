# 不使用任何循环打印图案

> 原文:[https://www . geesforgeks . org/print-a-pattern-不使用任何循环/](https://www.geeksforgeeks.org/print-a-pattern-without-using-any-loop/)

给定一个数字 n，按照一个模式打印，不使用任何循环。

**示例:**

```
Input: n = 16
Output: 16, 11, 6, 1, -4, 1, 6, 11, 16

Input: n = 10
Output: 10, 5, 0, 5, 10
```

我们基本上首先一个接一个地减少 5，直到达到负值或 0。达到 0 或负数后，再加一个 5，直到达到 n.
来源:[微软面试问题。](https://www.geeksforgeeks.org/microsoft-interview-experience-set-70-on-campus-for-idc-and-it/)

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/print-pattern3549/1)

想法是使用递归。这是一个自己尝试的有趣问题。
下面是代码。代码使用一个标志变量来指示我们是向 0 前进还是向 n 后退。

## C++

```
// C++ program to print pattern that first reduces 5 one
// by one, then adds 5\. Without any loop
#include <iostream>
using namespace std;

// Recursive function to print the pattern.
// n indicates input value
// m indicates current value to be printed
// flag indicates whether we need to add 5 or
// subtract 5\. Initially flag is true.
void printPattern(int n, int m, bool flag)
{
    // Print m.
    cout << m << " ";

    // If we are moving back toward the n and
    // we have reached there, then we are done
    if (flag == false && n ==m)
        return;

    // If we are moving toward 0 or negative.
    if (flag)
    {
    // If m is greater, then 5, recur with true flag
    if (m-5 > 0)
        printPattern(n, m-5, true);
    else // recur with false flag
        printPattern(n, m-5, false);
    }
    else // If flag is false.
        printPattern(n, m+5, false);
}

// Recursive function to print the pattern
// variance where m is the input int32 value
void PrintPattern(int m)
{
    if (m > 0)
    {
        cout << m << '\n';
        PrintPattern(m - 5);
    }

    cout << m << '\n';
}

// Driver Program
int main()
{
    int n = 16;
    //printPattern(n, n, true);
    PrintPattern(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print pattern that first reduces 5 one
// by one, then adds 5\. Without any loop
import java.io.*;

class GFG {

    // Recursive function to print the pattern.
    // n indicates input value
    // m indicates current value to be printed
    // flag indicates whether we need to add 5 or
    // subtract 5\. Initially flag is true.
    static void printPattern(int n, int m, boolean flag)
    {

        // Print m.
        System.out.print(m + " ");

        // If we are moving back toward the n and
        // we have reached there, then we are done
        if (flag == false && n == m)
            return;

        // If we are moving toward 0 or negative.
        if (flag) {

            // If m is greater, then 5, recur with
            // true flag
            if (m - 5 > 0)
                printPattern(n, m - 5, true);

            else // recur with false flag
                printPattern(n, m - 5, false);
        }

        else // If flag is false.
            printPattern(n, m + 5, false);
    }

    // Driver Program
    public static void main(String[] args)
    {
        int n = 16;
        printPattern(n, n, true);
    }
}
// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program to print pattern
# that first reduces 5 one by one,
# then adds 5\. Without any loop.

# Recursive function to print
# the pattern.n indicates
# input value m indicates
# current value to be printed
# flag indicates whether we
# need to add 5 or subtract 5.
# Initially flag is True.
def printPattern(n, m, flag):

    # Print m.
    print(m)

    # If we are moving back
    # toward the n and we
    # have reached there,
    # then we are done
    if flag == False and n == m:
        return
    # If we are moving
    # toward 0 or negative.
    if flag:
    # If m is greater, then 5,
    # recur with true flag
        if m - 5 > 0:
            printPattern(n, m - 5, True)
        else: # recur with false flag
            printPattern(n, m - 5, False)
    else: # If flag is false.
        printPattern(n, m + 5, False)

# Driver Code
n = 16
printPattern(n, n, True)

# This code is contributed
# by HrushikeshChoudhary
```

## C#

```
// C# program to print pattern that first reduces 5 one
// by one, then adds 5\. Without any loop
using System;

class GFG {

    // Recursive function to print the pattern.
    // n indicates input value
    // m indicates current value to be printed
    // flag indicates whether we need to add 5 or
    // subtract 5\. Initially flag is true.
    static void printPattern(int n, int m, bool flag)
    {

        // Print m.
        Console.Write(m + " ");

        // If we are moving back toward the n and
        // we have reached there, then we are done
        if (flag == false && n == m)
            return;

        // If we are moving toward 0 or negative.
        if (flag) {

            // If m is greater, then 5, recur with
            // true flag
            if (m - 5 > 0)
                printPattern(n, m - 5, true);

            else // recur with false flag
                printPattern(n, m - 5, false);
        }

        else // If flag is false.
            printPattern(n, m + 5, false);
    }

    // Driver Program
    public static void Main()
    {
        int n = 16;
        printPattern(n, n, true);
    }
}
// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print pattern
// that first reduces 5 one by one,
// then adds 5\. Without any loop

// Recursive function to print
// the pattern. n indicates input
// value m indicates current value
// to be printed flag indicates whether
// we need to add 5 or subtract 5.
// Initially flag is true.
function printPattern($n, $m, $flag)
{
    // Print m.
    echo $m ," ";

    // If we are moving back
    // toward the n and we
    // have reached there,
    // then we are done
    if ($flag == false && $n == $m)
        return;

    // If we are moving
    // toward 0 or negative.
    if ($flag)
    {
    // If m is greater, then 5,
    // recur with true flag
    if ($m - 5 > 0)
        printPattern($n, $m - 5, true);

    // recur with false flag
    else
        printPattern($n, $m - 5, false);
    }

    // If flag is false.
    else
        printPattern($n, $m + 5, false);
}

// Driver Code
$n = 16;
printPattern($n, $n, true);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to print pattern that
// first reduces 5 one by one, then adds 5.
// Without any loop

// Recursive function to print the pattern.
// n indicates input value m indicates current
// value to be printed flag indicates whether
// we need to add 5 or subtract 5\. Initially
// flag is true.
function printPattern(n, m, flag)
{

    // Print m.
    document.write(m + " ");

    // If we are moving back toward the n and
    // we have reached there, then we are done
    if (flag == false && n == m)
        return;

    // If we are moving toward 0 or negative.
    if (flag)
    {

        // If m is greater, then 5, recur with
        // true flag
        if (m - 5 > 0)
            printPattern(n, m - 5, true);

        // Recur with false flag
        else
            printPattern(n, m - 5, false);
    }

    // If flag is false.
    else
        printPattern(n, m + 5, false);
}

// Driver code
let n = 16;
printPattern(n, n, true);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
16, 11, 6, 1, -4, 1, 6, 11, 16
```

**如何在没有任何额外变量和循环的情况下打印上述图案？**
上述程序运行良好，打印出所需的输出，但使用了额外的变量。我们可以使用两个打印语句。打印所有递减序列的递归调用之前的第一个。递归调用打印递增序列后的第二个。

下面是这个想法的实现。

## C++

```
// C++ program to print pattern that first reduces 5 one
// by one, then adds 5\. Without any loop an extra variable.
#include <iostream>
using namespace std;

// Recursive function to print the pattern without any extra
// variable
void printPattern(int n)
{
    // Base case (When n becomes 0 or negative)
    if (n ==0 || n<0)
    {
        cout << n << " ";
        return;
    }

    // First print decreasing order
    cout << n << " ";
    printPattern(n-5);

    // Then print increasing order
    cout << n << " ";
}

// Driver Program
int main()
{
    int n = 16;
    printPattern(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print pattern that first
// reduces 5 one by one, then adds 5.
// Without any loop an extra variable.

import java.io.*;

class GFG {

    // Recursive function to print the
    // pattern without any extra variable
    static void printPattern(int n)
    {

        // Base case (When n becomes 0 or
        // negative)
        if (n == 0 || n < 0) {

            System.out.print(n + " ");

            return;
        }

        // First print decreasing order
        System.out.print(n + " ");

        printPattern(n - 5);

        // Then print increasing order
        System.out.print(n + " ");
    }

    // Driver Program
    public static void main(String[] args)
    {

        int n = 16;

        printPattern(n);
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to print pattern that
# first reduces 5 one by one, then adds 5.
# Without any loop an extra variable.

# Recursive function to print the pattern
# without any extra variable
def printPattern(n):

    # Base case (When n becomes 0 or negative)
    if (n == 0 or n < 0):
        print(n, end = ", ")
        return

    # First print decreasing order
    print(n, end = ", ")
    printPattern(n - 5)

    # Then print increasing order
    print(n, end = ", ")

# Driver Code
n = 16
printPattern(n)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to print pattern that first
// reduces 5 one by one, then adds 5.
// Without any loop an extra variable.

using System;

class GFG {

    // Recursive function to print the
    // pattern without any extra variable
    static void printPattern(int n)
    {

        // Base case (When n becomes 0 or
        // negative)
        if (n == 0 || n < 0) {

            Console.Write(n + " ");

            return;
        }

        // First print decreasing order
        Console.Write(n + " ");

        printPattern(n - 5);

        // Then print increasing order
        Console.Write(n + " ");
    }

    // Driver Program
    public static void Main()
    {

        int n = 16;

        printPattern(n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print pattern
// that first reduces 5 one
// by one, then adds 5\. Without
// any loop an extra variable.

// Recursive function to print the
// pattern without any extra variable
function printPattern( $n)
{

    // Base case (When n becomes
    // 0 or negative)
    if ($n == 0 or $n < 0)
    {
        echo $n , " ";
        return;
    }

    // First print decreasing order
    echo $n , " ";
    printPattern($n-5);

    // Then print increasing order
    echo $n , " ";
}

    // Driver Code
    $n = 16;
    printPattern($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to print pattern that first reduces 5 one
    // by one, then adds 5\. Without any loop an extra variable.

    // Recursive function to print the pattern without any extra
    // variable
    function printPattern(n)
    {

        // Base case (When n becomes 0 or negative)
        if (n == 0 || n < 0)
        {
            document.write(n + ", ");
            return;
        }

        // First print decreasing order
        document.write(n + ", ");
        printPattern(n - 5);

        // Then print increasing order
        document.write(n + ", ");
    }

    let n = 16;
    printPattern(n);

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
16, 11, 6, 1, -4, 1, 6, 11, 16
```

感谢 AKSHAY RATHORE 提出上述解决方案。
本文由**高森**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息