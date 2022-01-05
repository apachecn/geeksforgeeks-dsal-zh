# 以霍夫施塔特雌性和雄性序列为例的相互递归

> 原文:[https://www . geeksforgeeks . org/相互-递归-示例-Hofstadter-女性-男性-序列/](https://www.geeksforgeeks.org/mutual-recursion-example-hofstadter-female-male-sequences/)

相互递归是一种变异[递归](https://www.geeksforgeeks.org/recursion/)。如果第一个函数递归调用第二个函数，而第二个函数又调用第一个函数，则两个函数被称为相互递归。
在软件开发中，这个概念用在循环依赖中，循环依赖是两个或多个模块之间的关系，它们直接或间接地相互依赖以正常运行。这种模块也被称为相互递归。
相互递归的一个很好的例子是实现霍夫施塔特序列。

**霍夫施塔德序列**

在数学中，霍夫施塔特序列是由**非线性**递归关系定义的相关整数序列族的成员。在这个例子中，我们将关注**霍夫施塔特女性和男性序列:**

## C++

```
// C++ program to implement Hofstader Sequence
// using mutual recursion
#include <bits/stdc++.h>
using namespace std;

int hofstaderFemale(int);
int hofstaderMale(int);

// Female function
int hofstaderFemale(int n)
{
    if (n < 0)
        return 0;
    else
        if (n == 0)
            return 1;
        else
            return (n - hofstaderFemale(n - 1));
}

// Male function
int hofstaderMale(int n)
{
    if (n < 0)
        return 0;
    else
        if (n == 0)
            return 0;
        else
            return (n - hofstaderMale(n - 1));
}

// Driver Code
int main()
{
    int i;
    cout << "F: ";
    for (i = 0; i < 20; i++)
        cout << hofstaderFemale(i) << " ";

    cout << "\n";

    cout << "M: ";
    for (i = 0; i < 20; i++)
        cout << hofstaderMale(i)<< " ";

    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to implement Hofstader Sequence
// using mutual recursion
#include <stdio.h>

int hofstaderFemale(int);
int hofstaderMale(int);

// Female function
int hofstaderFemale(int n)
{
    if (n < 0)
        return;
    else
        return (n == 0) ? 1 : n - hofstaderFemale(n - 1);
}

// Male function
int hofstaderMale(int n)
{
    if (n < 0)
        return;
    else
        return (n == 0) ? 0 : n - hofstaderMale(n - 1);
}

// hard coded driver function to run the program
int main()
{
    int i;
    printf("F: ");
    for (i = 0; i < 20; i++)
        printf("%d ", hofstaderFemale(i));

    printf("\n");

    printf("M: ");
    for (i = 0; i < 20; i++)
        printf("%d ", hofstaderMale(i));   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Hofstader
// Sequence using mutual recursion
import java .io.*;

class GFG {

    // Female function
    static int hofstaderFemale(int n)
    {
        if (n < 0)
            return 0;
        else
            return (n == 0) ? 1 : n -
            hofstaderFemale(n - 1);
    }

    // Male function
    static int hofstaderMale(int n)
    {
        if (n < 0)
            return 0;
        else
            return (n == 0) ? 0 : n -
                hofstaderMale(n - 1);
    }

    // Driver Code
    static public void main (String[] args)
    {
        int i;
        System.out.print("F: ");
        for (i = 0; i < 20; i++)
            System.out.print(hofstaderFemale(i)
                                        + " ");

        System.out.println();

        System.out.print("M: ");
        for (i = 0; i < 20; i++)
            System.out.print(hofstaderMale(i)
                                      + " ");
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to implement
# Hofstader Sequence using
# mutual recursion

# Female function
def hofstaderFemale(n):
    if n < 0:
        return;
    else:
        val = 1 if n == 0 else (
                   n - hofstaderFemale(n - 1))
        return val

# Male function
def hofstaderMale(n):
    if n < 0:
        return;
    else:
        val = 0 if n == 0 else (
                   n - hofstaderMale(n - 1))
        return val

# Driver code
print("F:", end = " ")
for i in range(0, 20):
    print(hofstaderFemale(i), end = " ")

print("\n")
print("M:", end = " ")
for i in range(0, 20):
    print(hofstaderMale(i), end = " ")

# This code is contributed
# by Shantanu Sharma
```

## C#

```
// C# program to implement Hofstader
// Sequence using mutual recursion
using System;

class GFG {

    // Female function
    static int hofstaderFemale(int n)
    {
        if (n < 0)
            return 0;
        else
            return (n == 0) ? 1 : n -
               hofstaderFemale(n - 1);
    }

    // Male function
    static int hofstaderMale(int n)
    {
        if (n < 0)
            return 0;
        else
            return (n == 0) ? 0 : n -
                 hofstaderMale(n - 1);
    }

    // Driver Code
    static public void Main ()
    {
        int i;
        Console.WriteLine("F: ");
        for (i = 0; i < 20; i++)
            Console.Write(hofstaderFemale(i) + " ");

        Console.WriteLine();

        Console.WriteLine("M: ");
        for (i = 0; i < 20; i++)
            Console.Write(hofstaderMale(i) + " ");
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// Hofstader Sequence
// using mutual recursion

//function hofstaderFemale(int);
//int hofstaderMale(int);

// Female function
function hofstaderFemale($n)
{
    if ($n < 0)
        return;
    else
        return ($n == 0) ? 1 : $n - hofstaderFemale($n - 1);
}

// Male function
function hofstaderMale($n)
{
    if ($n < 0)
        return;
    else
        return ($n == 0) ? 0 : $n - hofstaderMale($n - 1);
}

    // Driver Code
    $i;
    echo "F: ";
    for ($i = 0; $i < 20; $i++)
        echo hofstaderFemale($i), " ";

    echo "\n";

    echo "M: ";
    for ($i = 0; $i < 20; $i++)
        echo hofstaderMale($i), " ";

// This code contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to implement Hofstader
// Sequence using mutual recursion

// Female function
function hofstaderFemale(n)
{
    if (n < 0)
        return 0;
    else
        return (n == 0) ? 1 :
                n - hofstaderFemale(n - 1);
}

// Male function
function hofstaderMale(n)
{
    if (n < 0)
        return 0;
    else
        return (n == 0) ? 0 :
                n - hofstaderMale(n - 1);
}

// Driver code
let i;
document.write("F: ");
for(i = 0; i < 20; i++)
    document.write(hofstaderFemale(i) + " ");

document.write("</br>");

document.write("M: ");
for(i = 0; i < 20; i++)
    document.write(hofstaderMale(i) + " ");

// This code is contributed by rameshtravel07
</script>
```

**输出:**

```
F: 1 0 2 1 3 2 4 3 5 4 6 5 7 6 8 7 9 8 10 9 
M: 0 1 1 2 2 3 3 4 4 5 5 6 6 7 7 8 8 9 9 10 
```

**循环依赖/相互递归的缺点:**

1.  当一个模块中的一个小的局部变化扩散到其他模块并产生不必要的全局效应时，循环依赖会导致多米诺骨牌效应
2.  循环依赖还会导致无限递归或其他意外失败。
3.  循环依赖还可能导致内存泄漏，因为它会阻止某些非常原始的自动垃圾收集器(那些使用引用计数的收集器)释放未使用的对象。

**参考文献:** [维基百科](https://en.wikipedia.org/wiki/Hofstadter_sequence)

本文由 [Palash Nigam](https://www.linkedin.com/in/palash25) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。