# 佩兰号码程序

> 原文:[https://www.geeksforgeeks.org/program-perrin-numbers/](https://www.geeksforgeeks.org/program-perrin-numbers/)

佩兰数是以下整数序列中的数字。
3，0，2，3，2，5，5，7，10，12，17，22，29，39……
在数学术语中，佩兰数的序列 p(n)由递推关系
定义

```
 P(n) = P(n-2) + P(n-3) for n > 2, 

with initial values
    P(0) = 3, P(1) = 0, P(2) = 2\. 
```

写一个返回 p(n)的函数 int per(int n)。例如，如果 n = 0，那么 per()应该返回 3。如果 n = 1，那么它应该返回 0。如果 n = 2，那么它应该返回 2。对于 n > 2，应该返回 p(n-2) + p(n-3)

**方法 1(使用递归:指数)**
下面是上面公式的简单递归实现。

## C++

```
// n'th perrin number using Recursion'
#include <bits/stdc++.h>
using namespace std;

int per(int n)
{
    if (n == 0)
        return 3;
    if (n == 1)
        return 0;
    if (n == 2)
        return 2;
    return per(n - 2) + per(n - 3);
}

// Driver code
int main()
{
    int n = 9;
    cout << per(n);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// n'th perrin number using Recursion'
#include <stdio.h>
int per(int n)
{
    if (n == 0)
        return 3;
    if (n == 1)
        return 0;
    if (n == 2)
        return 2;
    return per(n - 2) + per(n - 3);
}

// Driver code
int main()
{
    int n = 9;
    printf("%d", per(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for n'th perrin number
// using Recursion'
import java.io.*;

class GFG {

    static int per(int n)
    {
        if (n == 0)
            return 3;
        if (n == 1)
            return 0;
        if (n == 2)
            return 2;
        return per(n - 2) + per(n - 3);
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 9;

        System.out.println(per(n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code for n'th perrin
# number using Recursion'

# function return n'th
# perrin number
def per(n):

    if (n == 0):
        return 3;
    if (n == 1):
        return 0;
    if (n == 2):
        return 2;
    return per(n - 2) + per(n - 3);

# Driver Code
n = 9;
print(per(n));

# This code is contributed mits
```

## C#

```
// C# code for n'th perrin number
// using Recursion'
using System;

class GFG {

    static int per(int n)
    {
        if (n == 0)
            return 3;
        if (n == 1)
            return 0;
        if (n == 2)
            return 2;
        return per(n - 2) + per(n - 3);
    }

    // Driver code
    public static void Main()
    {

        int n = 9;

        Console.Write(per(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for n'th perrin
// number using Recursion'

// function return n'th
// perrin number
function per($n)
{
    if ($n == 0)
        return 3;
    if ($n == 1)
        return 0;
    if ($n == 2)
        return 2;
    return per($n - 2) +
           per($n - 3);
}

    // Driver Code
    $n = 9;
    echo per($n);

#This code is contributed ajit.
?>
```

## java 描述语言

```
<script>

// Javascript code for n'th perrin number
// using Recursion'

    function per(n)
    {
        if (n == 0)
            return 3;
        if (n == 1)
            return 0;
        if (n == 2)
            return 2;
        return per(n - 2) + per(n - 3);
    }

// Driver code   

           let n = 9;

        document.write(per(n));

</script>
```

**输出:**

```
12
```

我们看到在这个实现中，在下面的递归树中有很多重复的工作。

```
                           per(8)   
                       /           \     
               per(6)             per(5)   
              /      \             /     \
        per(4)      per(3)        per(3)    per(2)
       /     \        /    \        /  \  
   per(2)   per(1)  per(1) per(0) per(1) per(0)
```

**方法二: (优化:线性)**

## C++

```
// Optimized C++ program for n'th perrin number
#include <bits/stdc++.h>
using namespace std;
int per(int n)
{
    int a = 3, b = 0, c = 2, i;
    int m;
    if (n == 0)
        return a;
    if (n == 1)
        return b;
    if (n == 2)
        return c;
    while (n > 2) {
        m = a + b;
        a = b;
        b = c;
        c = m;
        n--;
    }
    return m;
}

// Driver code
int main()
{
    int n = 9;
    cout << per(n);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// Optimized C program for n'th perrin number
#include <stdio.h>
int per(int n)
{
    int a = 3, b = 0, c = 2, i;
    int m;
    if (n == 0)
        return a;
    if (n == 1)
        return b;
    if (n == 2)
        return c;
    while (n > 2) {
        m = a + b;
        a = b;
        b = c;
        c = m;
        n--;
    }
    return m;
}

// Driver code
int main()
{
    int n = 9;
    printf("%d", per(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Optimized Java program for n'th perrin number
import java.io.*;

class GFG {

    static int per(int n)
    {
        int a = 3, b = 0, c = 2, i;
        int m = 0;
        if (n == 0)
            return a;
        if (n == 1)
            return b;
        if (n == 2)
            return c;
        while (n > 2) {
            m = a + b;
            a = b;
            b = c;
            c = m;
            n--;
        }
        return m;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 9;

        System.out.println(per(n));
    }
}

// This code is contributed by vt_m.
```

## C#

```
// Optimized C# program for n'th perrin number
using System;

class GFG {

    static int per(int n)
    {
        int a = 3, b = 0, c = 2;

        // int i;
        int m = 0;
        if (n == 0)
            return a;
        if (n == 1)
            return b;
        if (n == 2)
            return c;

        while (n > 2) {
            m = a + b;
            a = b;
            b = c;
            c = m;
            n--;
        }

        return m;
    }

    // Driver code
    public static void Main()
    {

        int n = 9;

        Console.WriteLine(per(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Optimized PHP program for
// n'th perrin number

// function return the
// n'th perrin number
function per($n)
{
    $a = 3; $b = 0;
    $c = 2; $i;
    $m;
    if ($n == 0)
        return $a;
    if ($n == 1)
        return $b;
    if ($n == 2)
        return $c;
    while ($n > 2)
    {
        $m = $a + $b;
        $a = $b;
        $b = $c;
        $c = $m;
        $n--;
    }
    return $m;
}

    // Driver code
    $n = 9;
    echo per($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Optimized Javascript program for
// n'th perrin number

// function return the
// n'th perrin number
function per(n)
{
    let a = 3;
    let b = 0;
    let c = 2;
    let i;
    let m;

    if (n == 0)
        return a;
    if (n == 1)
        return b;
    if (n == 2)
        return c;
    while (n > 2)
    {
        m = a + b;
        a = b;
        b = c;
        c = m;
        n--;
    }
    return m;
}

    // Driver code
    n = 9;
    document.write(per(n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
12
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
**方法三:(进一步优化:对数)**
我们可以利用[矩阵求幂](https://www.geeksforgeeks.org/matrix-exponentiation/)进一步优化。第 n 个佩兰数的矩阵幂公式为
![{\Huge \begin{pmatrix} 0& 1 & 0\\ 0& 0&1 \\ 1 &1 & 0 \\ \end{pmatrix}^n \begin{pmatrix} 3\\ 0\\ 2 \end{pmatrix} = \begin{pmatrix} P(n)\\ P(n+1)\\ P(n+2) \end{pmatrix}}    ](img/e3bb9fc07b84fcbcc5419b8ad1ab5cd6.png "Rendered by QuickLaTeX.com")
我们可以类似于斐波那契数的[方法 5 的实现来实现这个方法。由于我们可以在 O(Log n)中计算一个常数矩阵的 n 次幂，所以该方法的时间复杂度为 O(Log n)
**应用:**
n 顶点循环图中不同的](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)[极大独立集](https://en.wikipedia.org/wiki/Maximal_independent_set)的个数按 n 的第 n 个 Perrin 数计数> 1
**相关文章:**
[Perrin 数之和](https://www.geeksforgeeks.org/sum-perrin-numbers/)
**参考:**
如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。