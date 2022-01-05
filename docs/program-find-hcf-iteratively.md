# 程序迭代寻找 HCF

> 原文:[https://www.geeksforgeeks.org/program-find-hcf-iteratively/](https://www.geeksforgeeks.org/program-find-hcf-iteratively/)

两个数的 HCF(最高公因数)或 GCD(最大公约数)是两个数相除的最大数。

![GCD](img/82f964bae761265c34df89322d538024.png)

比如 20 和 28 的 GCD 是 4，98 和 56 的 GCD 是 14。

我们已经在下面的帖子中讨论了递归解决方案。[求两个数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)
GCD 或 HCF 的递归程序下面是[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)T5 的迭代实现

## C++

```
// C++ program to find HCF of two
// numbers iteratively.
#include <bits/stdc++.h>
using namespace std;

int hcf(int a, int b)
{
    if (a == 0)
        return b;
    else if (b == 0)
        return a;
    while (a != b) {
        if (a > b)
            a = a - b;
        else
            b = b - a;
    }
    return a;
}

// Driver code
int main()
{
    int a = 60, b = 96;
    cout << hcf(a, b) << endl;
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to find HCF of two
// numbers iteratively.
#include <stdio.h>

int hcf(int a, int b)
{
    if (a == 0)
        return b;
    else if (b == 0)
        return a;
    while (a != b) {
        if (a > b)
            a = a - b;
        else
            b = b - a;
    }
    return a;
}
int main()
{
    int a = 60, b = 96;
    printf("%d\n", hcf(a, b));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Program to find
// HCF iteratively
import java.util.*;

class GFG {

    static int hcf(int a, int b)
    {
        if (a == 0)
            return b;
        else if (b == 0)
            return a;
        while (a != b) {
            if (a > b)
                a = a - b;
            else
                b = b - a;
        }
        return a;
    }

    /* Driver program */
    public static void main(String[] args)
    {
        int a = 60, b = 96;
        System.out.println(hcf(a, b));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
// Python program to find HCF of two
// numbers iteratively.

def hcf(a, b):
    if(a == 0):
      return b
    else if(b == 0):
      return a
    while (a != b):
        if (a > b):
            a = a - b
        else:
            b = b - a
    return a

a = 60
b = 96
print(hcf(a, b))
```

## C#

```
// C# Code for Program to find
// HCF iteratively
using System;

class GFG {

    static int hcf(int a, int b)
    {
        if (a == 0)
            return b;
        else if (b == 0)
            return a;
        while (a != b) {
            if (a > b)
                a = a - b;
            else
                b = b - a;
        }
        return a;
    }

    // Driver program
    public static void Main()
    {
        int a = 60, b = 96;
        Console.WriteLine(hcf(a, b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find HCF of two
// numbers iteratively.

function hcf($a, $b)
{   if($a==0)
      return $b;
   else if($b==0)
      return $a;
    while ($a != $b) {
        if ($a > $b)    
            $a = $a - $b;    
        else
            $b = $b - $a;    
    }

    return $a;
}

// Driver code
$a = 60; $b = 96;
echo hcf($a, $b), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

//Javascript program to find HCF of two
// numbers iteratively.

function hcf(a, b)
{   if (a == 0)
        return b;
    else if (b == 0)
        return a;
    while (a != b)
    {
        if (a > b)    
            a = a - b;    
        else   
            b = b - a;    
    }
    return a;
}

// Driver code
    let a = 60, b = 96;
    document.write(hcf(a, b) + "<br>");    

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
12
```

**时间复杂度:** O(最大值(a，b))

**辅助空间:** O(1)