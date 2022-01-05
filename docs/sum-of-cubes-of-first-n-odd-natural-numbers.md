# 前 n 个奇数自然数的立方之和

> 原文:[https://www . geeksforgeeks . org/第一个 n 个奇数自然数的立方之和/](https://www.geeksforgeeks.org/sum-of-cubes-of-first-n-odd-natural-numbers/)

给定一个数 n，求前 n 个奇数自然数的和。

```
Input  : 2
Output : 28
1^3 + 3^3 = 28

Input  : 4
Output : 496
1^3 + 3^3 + 5^3 + 7^3 = 496
```

一个**简单的解法**就是遍历 n 个奇数，求立方体的和。

## C++

```
// Simple C++ method to find sum of cubes of
// first n odd numbers.
#include <iostream>
using namespace std;

int cubeSum(int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += (2*i + 1)*(2*i + 1)*(2*i + 1);
    return sum;
}

int main()
{
    cout << cubeSum(2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform sum of
// cubes of first n odd natural numbers

public class GFG
{

    public static int cubesum(int n)
    {
        int sum = 0;
        for(int i = 0; i < n; i++)
            sum += (2 * i + 1) * (2 * i +1)
                   * (2 * i + 1);

        return sum;
    }

    // Driver function
    public static void main(String args[])
    {
        int a = 5;
        System.out.println(cubesum(a));

    }
}

// This article is published Akansh Gupta
```

## 蟒蛇 3

```
# Python3 program to find sum of
# cubes of first n odd numbers.

def cubeSum(n):
    sum = 0

    for i in range(0, n) :
        sum += (2 * i + 1) * (2 * i + 1) * (2 * i + 1)
    return sum

# Driven code
print(cubeSum(2))

# This code is contributed by Shariq Raza
```

## C#

```
// C# program to perform sum of
// cubes of first n odd natural numbers
using System;

public class GFG
{

    public static int cubesum(int n)
    {
        int sum = 0;
        for(int i = 0; i < n; i++)
            sum += (2 * i + 1) * (2 * i +1)
                   * (2 * i + 1);

        return sum;
    }

    // Driver function
    public static void Main()
    {
        int a = 5;
        Console.WriteLine(cubesum(a));

    }
}

// This code is published vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP method to find sum of
// cubes of first n odd numbers.

function cubeSum($n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += (2 * $i + 1) *
                (2 * $i + 1) *
                (2 * $i + 1);
    return $sum;
}

// Driver Code
echo cubeSum(2);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// Simple javascript method to find sum of cubes of
// first n odd numbers.
function cubeSum( n)
{
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += (2*i + 1)*(2*i + 1)*(2*i + 1);
    return sum;
}

    document.write(cubeSum(2));

// This code is contributed by Rajput-Ji

</script>
```

输出:

```
28
```

一个**有效的解决方案**是应用下面的公式。

```
***sum = n<sup>2(2n2 - 1)</sup>*** 

How does it work? 

We know that sum of cubes of first 
n natural numbers is = n2(n+1)2 / 4

Sum of first n even numbers is 2 *  n<sup>2(n+1)2</sup> 

Sum of cubes of first n odd natural numbers = 
            Sum of cubes of first 2n natural numbers - 
            Sum of cubes of first n even natural numbers 

         =  (2n)2(2n+1)2 / 4 - 2 *  n2(n+1)2 
         =  n2(2n+1)2 - 2 *  n2(n+1)2 
         =  n2[(2n+1)2 - 2*(n+1)2]
         =  n2(2n2 - 1)
```

## C++

```
// Efficient C++ method to find sum of cubes of
// first n odd numbers.
#include <iostream>
using namespace std;

int cubeSum(int n)
{
    return n * n * (2 * n * n - 1);
}

int main()
{
    cout << cubeSum(4);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform sum of
// cubes of first n odd natural numbers

public class GFG
{
    public static int cubesum(int n)
    {

        return (n) * (n) * (2 * n * n - 1);
    }

    // Driver function
    public static void main(String args[])
    {
        int a = 4;
        System.out.println(cubesum(a));

    }
}

// This code is contributed by Akansh Gupta.
```

## 蟒蛇 3

```
# Python3 program to find sum of
# cubes of first n odd numbers.

# Function to find sum of cubes
# of first n odd number
def cubeSum(n):
    return (n * n * (2 * n * n - 1))

# Driven code
print(cubeSum(4))

# This code is contributed by Shariq Raza
```

## C#

```
// C# program to perform sum of
// cubes of first n odd natural numbers
using System;

public class GFG
{
    public static int cubesum(int n)
    {

        return (n) * (n) * (2 * n * n - 1);
    }

    // Driver function
    public static void Main()
    {
        int a = 4;
        Console.WriteLine(cubesum(a));

    }
}

// This code is published vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP method to
// find sum of cubes of
// first n odd numbers.

function cubeSum($n)
{
    return $n * $n * (2 * $n * $n - 1);
}

// Driver Code
echo cubeSum(4);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript program to perform sum of
// cubes of first n odd natural numbers

function cubesum(n)
{

    return (n) * (n) * (2 * n * n - 1);
}

// Driver function
var a = 4;
document.write(cubesum(a));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
496
```

本文由**达曼德拉·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。