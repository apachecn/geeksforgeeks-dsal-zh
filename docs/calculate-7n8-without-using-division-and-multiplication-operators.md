# 不使用除法和乘法运算符计算 7n/8

> 原文:[https://www . geeksforgeeks . org/calculate-7n 8-不使用除法和乘法运算符/](https://www.geeksforgeeks.org/calculate-7n8-without-using-division-and-multiplication-operators/)

给定一个整数，编写一个函数来计算⌈7n/8⌉ ( [上限](http://en.wikipedia.org/wiki/Floor_and_ceiling_functions)为 7n/8)，而不使用除法和乘法运算符。
**强烈建议尽量减少浏览器，先自己试试这个。**

**方法 1:**
思路是先计算 n/8 的楼层，即⌊n/8⌋使用右移[按位运算符](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)。表达式 n > > 3 产生同样的结果。如果我们从 n 中减去⌊n/8⌋，就得到⌈7n/8⌉

以下是上述想法的实现:

## C++

```
// C++ program to evaluate ceil(7n/8)
// without using * and /
#include <iostream>
using namespace std;

int multiplyBySevenByEight(int n)
{

    // Note the inner bracket here. This is needed
    // because precedence of '-' operator is higher
    // than '<<'
    return (n - (n >> 3));
}

// Driver code
int main()
{
    int n = 9;
    cout << multiplyBySevenByEight(n);
    return 0;
}

// This code is contributed by khushboogoyal499
```

## C

```
// C program to evaluate ceil(7n/8) without using * and /
#include <stdio.h>

int multiplyBySevenByEight(unsigned int n)
{
    /* Note the inner bracket here. This is needed
       because precedence of '-' operator is higher
       than '<<' */
    return (n - (n >> 3));
}

/* Driver program to test above function */
int main()
{
    unsigned int n = 9;
    printf("%d", multiplyBySevenByEight(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate ceil(7n/8)
// without using * and
import java.io.*;

class GFG {
    static int multiplyBySevenByEight(int n)
    {
        /* Note the inner bracket here. This is needed
        because precedence of '-' operator is higher
        than '<<' */
        return (n - (n >> 3));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 9;
        System.out.println(multiplyBySevenByEight(n));
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python program to evaluate ceil(7n/8) without using * and /

def multiplyBySevenByEight(n):

    # Note the inner bracket here. This is needed
    # because precedence of '-' operator is higher
    # than '<<'
    return (n - (n >> 3))

# Driver program to test above function */
n = 9
print(multiplyBySevenByEight(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to evaluate ceil(7n/8)
// without using * and
using System;

public class GFG {

    static int multiplyBySevenByEight(int n)
    {
        /* Note the inner bracket here.
        This is needed because precedence
        of '-' operator is higher than
        '<<' */
        return (n - (n >> 3));
    }

    // Driver code
    public static void Main()
    {
        int n = 9;

        Console.WriteLine(multiplyBySevenByEight(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to evaluate ceil
// (7n/8) without using * and

function multiplyBySevenByEight( $n)
{
    // Note the inner bracket here.
    // This is needed because
    // precedence of '-' operator
    // is higher than '<<'

    return ($n - ($n >> 3));
}

// Driver Code
$n = 9;
echo multiplyBySevenByEight($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to evaluate ceil(7n/8) without using * and /

function multiplyBySevenByEight(n)
{
    /* Note the inner bracket here. This is needed
    because precedence of '-' operator is higher
    than '<<' */
    return (n - (n>>3));
}

/* Driver program to test above function */

    let n = 9;
    document.write(multiplyBySevenByEight(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
8
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**方法 2(总是与 7*n/8 匹配):**
上述方法并不总是产生与“printf(% u，7*n/8)”相同的结果。例如，对于 n = 15，表达式 7*n/8 的值是 13，但是上面的程序产生 14。下面是始终匹配 7*n/8 的修改版本。这个想法是首先将数字乘以 7，然后除以 8，就像表达式 7*n/8 中发生的那样。

## C++

```
// C++ program to evaluate 7n/8 without using * and /
#include<iostream>
using namespace std;

int multiplyBySevenByEight(unsigned int n)
{   
    /* Step 1) First multiply number by 7 i.e. 7n = (n << 3) -n
     * Step 2) Divide result by 8 */
   return ((n << 3) -n) >> 3;
}

/* Driver program to test above function */
int main()
{
    unsigned int n = 15;
    cout<<" "<< multiplyBySevenByEight(n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to evaluate 7n/8 without using * and /
#include<stdio.h>

int multiplyBySevenByEight(unsigned int n)
{   
    /* Step 1) First multiply number by 7 i.e. 7n = (n << 3) -n
     * Step 2) Divide result by 8 */
   return ((n << 3) -n) >> 3;
}

/* Driver program to test above function */
int main()
{
    unsigned int n = 15;
    printf("%u", multiplyBySevenByEight(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate 7n/8
// without using * and /
import java.io.*;

class GFG
{

    static int multiplyBySevenByEight(int n)
    {
        // Step 1) First multiply number
        // by 7 i.e. 7n = (n << 3) -n
        // * Step 2) Divide result by 8
        return ((n << 3) -n) >> 3;
    }

    // Driver program
    public static void main(String args[])
    {

        int n = 15;
        System.out.println(multiplyBySevenByEight(n));
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python3 program to evaluate 7n/8
# without using * and /

def multiplyBySevenByEight(n):

    #Step 1) First multiply number
    # by 7 i.e. 7n = (n << 3) -n
    # Step 2) Divide result by 8
    return ((n << 3) -n) >> 3;

# Driver code
n = 15;
print(multiplyBySevenByEight(n));

#this code is contributed by sam007.
```

## C#

```
// C# program to evaluate 7n/8
// without using * and /
using System;

public class GFG {

    static int multiplyBySevenByEight(int n)
    {

        // Step 1) First multiply number
        // by 7 i.e. 7n = (n << 3) -n
        // * Step 2) Divide result by 8
        return ((n << 3) -n) >> 3;
    }

    // Driver program
    public static void Main()
    {
        int n = 15;

        Console.WriteLine(
            multiplyBySevenByEight(n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to evaluate 7n/8
// without using * and /

function multiplyBySevenByEight( $n)
{

     /* Step 1) First multiply number by
                7 i.e. 7n = (n << 3) - n
         Step 2) Divide result by 8 */
    return (($n << 3) -$n) >> 3;
}

    // Driver Code
    $n = 15;
    echo multiplyBySevenByEight($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to evaluate 7n/8
// without using * and /
function multiplyBySevenByEight(n)
{

    // Step 1) First multiply number
    // by 7 i.e. 7n = (n << 3) -n
    // * Step 2) Divide result by 8
    return ((n << 3) -n) >> 3;
}

// Driver code
var n = 15;

document.write(multiplyBySevenByEight(n));

// This code is contributed by shikhasingrajput

</script>
```

**输出:**

```
13
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**注:**两种方法的结果存在差异。方法 1 产生上限(7n/8)，但方法 2 产生整数值 7n/8。例如，对于 n = 15，第一种方法的结果是 14，但是对于第二种方法是 13。

感谢纳伦德拉·康拉尔卡 r 提出这个方法。
本文由**拉杰夫**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论