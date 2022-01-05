# 使用间接递归打印数字 1 到 n

> 原文:[https://www . geesforgeks . org/print-numbers-1-n-using-间接-递归/](https://www.geeksforgeeks.org/print-numbers-1-n-using-indirect-recursion/)

给定一个数字 N，我们需要打印从 1 到 N 的数字，不需要直接递归、循环和标签。基本上我们需要插入上面的代码片段，这样它就可以打印从 1 到 N 的数字？

## C

```
#include <stdio.h>
#define N 20;
int main()
{
   // Your code goes Here.
}
```

**示例:**

```
Input  : 10
Output : 1 2 3 4 5 6 7 8 9 10

Input  : 5
Output : 1 2 3 4 5
```

我们已经在下面的帖子中讨论了解决方案:
[用 C++打印 1 到 100，没有循环和递归](https://www.geeksforgeeks.org/output-of-c-program-set-18-3/)
[不使用循环你怎么打印 1 到 100 的数字？](https://www.geeksforgeeks.org/how-will-you-print-numbers-from-1-to-200-without-using-loop/)

下面的代码可以打印从 1 到 100 的数字，不需要直接递归、循环和标签。代码使用[间接递归](https://www.geeksforgeeks.org/recursion/)。

## C++

```
// C++ program to print from 1 to N using
// indirect recursion/
#include<bits/stdc++.h>
using namespace std;

// We can avoid use of these using references
int N = 20;
int n = 1;

void fun1();
void fun2();

// Prints n, increments n and calls fun1()
void fun1()
{
    if (n <= N)
    {
        cout << n << " ";
        n++;
        fun2();
    }
    else
        return;
}

// Prints n, increments n and calls fun2()
void fun2()
{
    if (n <= N)
    {
        cout << n << " ";
        n++;
        fun1();
    }
    else
        return;
}

// Driver Program
int main()
{
    fun1();
    return 0;
}

// This code is contributed by pankajsharmagfg.
```

## C

```
// C program to print from 1 to N using
// indirect recursion/
#include<stdio.h>

// We can avoid use of these using references
#define N 20;
int n = 1;

// Prints n, increments n and calls fun1()
void fun1()
{
    if (n <= N)
    {
        printf("%d", n);
        n++;
        fun2();
    }
    else
        return;
}

// Prints n, increments n and calls fun2()
void fun2()
{
    if (n <= N)
    {
        printf("%d", n);
        n++;
        fun1();
    }
    else
        return;
}

// Driver Program
int main(void)
{
    fun1();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print from 1 to N using
// indirect recursion
class GFG
{
    // We can avoid use of these using references
    static final int N = 20;
    static int n = 1;

    // Prints n, increments n and calls fun1()
    static void fun1()
    {
        if (n <= N)
        {
            System.out.printf("%d ", n);
            n++;
            fun2();
        }
        else
        {
            return;
        }
    }

    // Prints n, increments n and calls fun2()
    static void fun2()
    {
        if (n <= N)
        {
            System.out.printf("%d ", n);
            n++;
            fun1();
        }
        else
        {
            return;
        }
    }

    // Driver Program
    public static void main(String[] args)
    {
        fun1();
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to prfrom 1 to N using
# indirect recursion

# We can avoid use of these using references
N = 20;
n = 1;

# Prints n, increments n and calls fun1()
def fun1():
    global N, n;
    if (n <= N):
        print(n, end = " ");
        n += 1;
        fun2();
    else:
        return;

# Prints n, increments n and calls fun2()
def fun2():
    global N, n;
    if (n <= N):
        print(n, end = " ");
        n += 1;
        fun1();
    else:
        return;

# Driver Program
if __name__ == '__main__':

    fun1();

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to print from 1 to N using
// indirect recursion
using System;

class GFG
{
    // We can avoid use of these using references
    static readonly int N = 20;
    static int n = 1;

    // Prints n, increments n and calls fun1()
    static void fun1()
    {
        if (n <= N)
        {
            Console.Write("{0} ", n);
            n++;
            fun2();
        }
        else
        {
            return;
        }
    }

    // Prints n, increments n and calls fun2()
    static void fun2()
    {
        if (n <= N)
        {
            Console.Write("{0} ", n);
            n++;
            fun1();
        }
        else
        {
            return;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        fun1();
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// from 1 to N using
// indirect recursion

// We can avoid use of
// these using references
$N = 20;
$n = 1;

// Prints n, increments
// n and calls fun1()
function fun1()
{
    global $N;
    global $n;

    if ($n <= $N)
    {
        echo $n, " ";
        $n++;
        fun2();
    }
    else
        return;
}

// Prints n, increments
// n and calls fun2()
function fun2()
{
    global $N;
    global $n;
    if ($n <= $N)
    {
        echo $n, " ";
        $n++;
        fun1();
    }
    else
        return;
}

// Driver Code
fun1();

// This code is contributed
// by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to print from 1 to N using
// indirect recursion

// We can avoid use of these using references
let N = 20;
let n = 1

// Prints n, increments n and calls fun1()
function fun1()
{
    if (n <= N)
    {
        document.write( n+" ");
        n++;
        fun2();
    }
    else
    {
        return;
    }
}

// Prints n, increments n and calls fun2()
function fun2()
{
    if (n <= N)
    {
        document.write(n+" ");
        n++;
        fun1();
    }
    else
    {
        return;
    }
}

// Driver code
fun1();

// This code is contributed by rag2127

</script>
```

**输出:**

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 
```

**这是如何工作的？:**
在上面的程序中，我们只使用了两个函数。一个叫别人，另一个叫前一个，所以间接递归。

**练习:**
修改上面的程序，使用 N 作为参数，而不是使其全局化。

本文由海得拉巴 **Jntuh 工程学院**的[**Umamaheswararao Tumma**](https://www.linkedin.com/in/umamaheswararao-tumma-3a0050130/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。