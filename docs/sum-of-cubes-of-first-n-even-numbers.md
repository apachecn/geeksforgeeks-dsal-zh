# 前 n 个偶数的立方之和

> 原文:[https://www . geesforgeks . org/第一个 n 个偶数的立方之和/](https://www.geeksforgeeks.org/sum-of-cubes-of-first-n-even-numbers/)

给定一个数 n，求前 n 个偶数自然数的和。
示例:

```
Input : 2
Output : 72
2^3 + 4^3 = 72

Input : 8
Output :10368
2^3 + 4^3 + 6^3 + 8^3 + 10^3 + 12^3 + 14^3 + 16^3 = 10368
```

一个**简单的解法**就是遍历 n 个偶数，求立方体的和。

## C++

```
// Simple C++ method to find sum of cubes of
// first n even numbers.
#include <iostream>
using namespace std;

int cubeSum(int n)
{
    int sum = 0;
    for (int i = 1; i <=  n; i++)
        sum += (2*i) * (2*i) * (2*i);
    return sum;
}

int main()
{
    cout << cubeSum(8);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform
// sum of cubes of first
// n even natural numbers

public class GFG
{
    public static int cubesum(int n)
    {
        int sum = 0;
        for(int i = 1; i <= n; i++)
            sum += (2 * i) * (2 * i)
                   * (2 * i);

        return sum;
    }

    // Driver function
    public static void main(String args[])
    {
        int a = 8;
        System.out.println(cubesum(a));

    }
}

// This code is contributed by Akansh Gupta
```

## 蟒蛇 3

```
# Python3 program to find sum of
# cubes of first n even numbers

# Function to find sum of cubes
# of first n even numbers
def cubeSum(n):

    sum = 0
    for i in range(1, n + 1):
        sum += (2 * i) * (2 * i) * (2 * i)
    return sum

# Driven code
print(cubeSum(8))

# This code is contributed by Shariq Raza
```

## C#

```
// C# program to perform
// sum of cubes of first
// n even natural numbers
using System;

public class GFG
{
    public static int cubesum(int n)
    {
        int sum = 0;
        for(int i = 1; i <= n; i++)
            sum += (2 * i) * (2 * i)
                * (2 * i);

        return sum;
    }

    // Driver function
    public static void Main()
    {
        int a = 8;
        Console.WriteLine(cubesum(a));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP method to
// find sum of cubes of
// first n even numbers.

function cubeSum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += (2 * $i) *
                (2 * $i) *
                (2 * $i);
    return $sum;
}

// Driver Code
echo cubeSum(8);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find sum of cubes of
// first n even numbers.

    function cubeSum(n)
    {
        let sum = 0;
        for (let i = 1; i <=  n; i++)
        sum += (2*i) * (2*i) * (2*i);
        return sum;
    }

    document.write(cubeSum(8)); 

// This code is contributed by Surbhi Tyagi

</script>
```

输出:

```
10368
```

一个**有效的解决方案**是应用下面的公式。

```
***sum = 2 *  n<sup>2(n+1)2</sup>*** 

How does it work? 

We know that sum of cubes of first 
n natural numbers is = n2(n+1)2 / 4

Sum of cubes of first n natural numbers = 
                2^3 + 4^3 + .... + (2n)^3
              = 8 * (1^3 + 2^3 + .... + n^3)
              = 8 *  n2(n+1)2 / 4
              = 2 *  n2(n+1)2 
```

## C++

```
// Efficient C++ method to find sum of cubes of
// first n even numbers.
#include <iostream>
using namespace std;

int cubeSum(int n)
{
    return 2 * n * n * (n + 1) * (n + 1);
}

int main()
{
    cout << cubeSum(8);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform
// sum of cubes of first
// n even natural numbers

public class GFG
{
    public static int cubesum(int n)
    {

        return 2 * n * n * (n + 1) * (n + 1);
    }

    // Driver function
    public static void main(String args[])
    {
        int a = 8;
        System.out.println(cubesum(a));

    }
}

// This code is contributed by Akansh Gupta
```

## 蟒蛇 3

```
# Python3 program to find sum of
# cubes of first n even numbers

# Function to find sum of cubes
# of first n even numbers
def cubeSum(n):

    return 2 * n * n * (n + 1) * (n + 1)

# Driven code
print(cubeSum(8))

# This code is contributed by Shariq Raza
```

## C#

```
// C# program to perform
// sum of cubes of first
// n even natural numbers
using System;

class GFG
{
    public static int cubesum(int n)
    {
        return 2 * n * n *
               (n + 1) * (n + 1);
    }

    // Driver code
    public static void Main()
    {
        int a = 8;
        Console.WriteLine(cubesum(a));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP code to
// find sum of cubes of
// first n even numbers.

function cubeSum($n)
{
    return 2 * $n * $n *
           ($n + 1) * ($n + 1);
}

// Driver code
echo cubeSum(8);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript program to perform
// sum of cubes of first
// n even natural numbers
function cubesum(n)
{    
    return 2 * n * n * (n + 1) * (n + 1);
}

// Driver function
var a = 8;
document.write(cubesum(a));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
10368
```

[前 n 个奇数自然数的立方之和](https://www.geeksforgeeks.org/sum-of-cube-of-first-n-odd-natural-numbers/)
本文由**达曼德拉·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。