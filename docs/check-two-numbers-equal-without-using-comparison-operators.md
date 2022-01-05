# 不使用比较运算符

检查两个数是否相等

> 原文:[https://www . geesforgeks . org/check-两个数字-相等-不使用比较运算符/](https://www.geeksforgeeks.org/check-two-numbers-equal-without-using-comparison-operators/)

以下不允许使用
1)比较运算符
2)字符串函数
示例:

```
Input : num1 = 1233, num2 - 1233
Output : Same

Input : num1 = 223, num2 = 233
Output : Not Same
```

**方法一:**思路是用异或运算符。如果两个数相同，则两个数的异或为 0，否则为非零。

## C++

```
#include <iostream>
using namespace std;

// Finds if a and b are same.
void areSame(int a, int b)
{
   if (a^b)
       cout << "Not Same";
   else
       cout << "Same";
}

int main()
{ 
   areSame(10, 20);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
    // Finds if a and b are same
    static void areSame(int a,int b)
    {
        if( (a ^ b) != 0 )
            System.out.println("Not Same");
        else
            System.out.println("Same");
    }

    public static void main(String args[])
    {
        areSame(10,20);
    }

}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Finds if a and b are same.
def areSame(a, b):
   if (a ^ b):
       print "Not Same"
   else:
       print "Same"

# Driver code
areSame(10, 20)

# This code is submitted by Sachin Bisht
```

## C#

```
// C# program to check if 2
// numbers are same
using System;

class GFG
{
    // Finds if a and b are same
    static void areSame(int a, int b)
    {
        if( (a ^ b) != 0 )
          Console.Write("Not Same");
        else
          Console.Write("Same");
    }

    // Driver code
    public static void Main()
    {

        // Calling Function
        areSame(10, 20);
    }

}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Finds if a and b are same.
function areSame($a, $b)
{
    if ($a ^ $b)
        echo "Not Same";
    else
        echo "Same";
}

// Driver Code
areSame(10, 20);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Finds if a and b are same.

function areSame(a, b)
{
if (a^b)
    document.write("Not Same");
else
    document.write("Same");
}

// Driver code
areSame(10, 20);

// This code is contributed by Surbhi Tyagi.

</script>
```

输出:

```
Not Same
```

**方法二:**我们可以减去数字。相同的数字得出 0。如果答案不是 0，数字就不一样。

## C++

```
// CPP code to check if 2 numbers are same
#include <bits/stdc++.h>
using namespace std;

// Finds if a and b are same
void areSame(int a, int b)
{
    if (!(a - b))
        cout << "Same";
    else
        cout << "Not Same";
}

// Driver code
int main()
{   
     areSame(10, 20);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if 2 numbers are same
class GFG{

    // Finds if a and b are same
    static void areSame(int a, int b)
    {
        if ((a - b) == 0)
            System.out.println("Same");
        else
            System.out.println("Not Same");
    }

    // Driver code
    public static void main(String args[])
    {   
        areSame(10, 20);   

    }
}
//This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python code to check if 2 numbers are same

# Finds if a and b are same
def areSame(a, b):
    if (not(a - b)):
        print "Same"
    else:
        print "Not Same"
# Driver code
areSame(10, 20)

# This code is submitted by Sachin Bisht
```

## C#

```
// C# code to check if 2
// numbers are same
using System;

class GFG
{

    // Finds if a and b are same
    static void areSame(int a, int b)
    {
        if ((a - b) == 0)
            Console.Write("Same");
        else
            Console.Write("Not Same");
    }

    // Driver code
    public static void Main()
    {

        // Calling Function
        areSame(10, 20);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if 2
// numbers are same

// Finds if a and b are same
function areSame($a, $b)
{
    if (!($a - $b))
        echo "Same";
    else
        echo "Not Same";
}

// Driver code
areSame(10, 20);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// javascript code to check if 2 numbers are same

// Finds if a and b are same
function areSame(a , b)
{
    if ((a - b) == 0)
        document.write("Same");
    else
        document.write("Not Same");
    }

    // Driver code
areSame(10, 20);

// This code contributed by Princi Singh
</script>
```

输出:

```
Not Same
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。