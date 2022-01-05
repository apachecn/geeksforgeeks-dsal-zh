# 斐波那契数之和

> 原文:[https://www.geeksforgeeks.org/sum-fibonacci-numbers/](https://www.geeksforgeeks.org/sum-fibonacci-numbers/)

给定一个正数 n，求 f<sub>0</sub>+f<sub>1</sub>+f<sub>2</sub>+…。+ f <sub>n</sub> 其中 f <sub>i</sub> 表示第 I 个斐波那契数。请记住，f <sub>0</sub> = 0，f <sub>1</sub> = 1，f <sub>2</sub> = 1，f <sub>3</sub> = 2，f <sub>4</sub> = 3，f <sub>5</sub> = 5，…
**示例:**

```
Input  : n = 3
Output : 4
Explanation : 0 + 1 + 1 + 2  = 4

Input  :  n = 4
Output :  7
Explanation : 0 + 1 + 1 + 2 + 3  = 7
```

**方法 1 (O(n))**
**【蛮力】**方法相当直接，找到所有的斐波那契数直到 f(n)，然后把它们加起来。

## C++

```
// C++ Program to find sum of Fibonacci numbers
#include<bits/stdc++.h>
using namespace std;

// Computes value of first fibonacci numbers
int calculateSum(int n)
{
    if (n <= 0)
       return 0;

    int fibo[n+1];
    fibo[0] = 0, fibo[1] = 1;

    // Initialize result
    int sum = fibo[0] + fibo[1];

    // Add remaining terms
    for (int i=2; i<=n; i++)
    {
        fibo[i] = fibo[i-1]+fibo[i-2];
        sum += fibo[i];
    }

    return sum;
}

// Driver program to test above function
int main()
{
    int n = 4;
    cout << "Sum of Fibonacci numbers is : "
         << calculateSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// sum of Fibonacci numbers

import java.io.*;

class GFG {

    // Computes value of first
    // fibonacci numbers
    static int calculateSum(int n)
    {
        if (n <= 0)
           return 0;

        int fibo[]=new int[n+1];
        fibo[0] = 0; fibo[1] = 1;

        // Initialize result
        int sum = fibo[0] + fibo[1];

        // Add remaining terms
        for (int i=2; i<=n; i++)
        {
            fibo[i] = fibo[i-1]+fibo[i-2];
            sum += fibo[i];
        }

        return sum;
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        int n = 4;
        System.out.println("Sum of Fibonacci" +
        " numbers is : "+ calculateSum(n));
    }
}

// This code is contributed by Nikita tiwari.
```

## 蟒蛇 3

```
# Python 3 Program to find
# sum of Fibonacci numbers

# Computes value of first
# fibonacci numbers
def calculateSum(n) :
    if (n <= 0) :
        return 0

    fibo =[0] * (n+1)
    fibo[1] = 1

    # Initialize result
    sm = fibo[0] + fibo[1]

    # Add remaining terms
    for i in range(2,n+1) :
        fibo[i] = fibo[i-1] + fibo[i-2]
        sm = sm + fibo[i]

    return sm

# Driver program to test
# above function
n = 4
print("Sum of Fibonacci numbers is : " ,
      calculateSum(n))

# This code is contributed
# by Nikita tiwari.
```

## C#

```
// C# Program to find
// sum of Fibonacci numbers
using System;

class GFG
{

    // Computes value of first
    // fibonacci numbers
    static int calculateSum(int n)
    {
        if (n <= 0)
        return 0;

        int []fibo = new int[n + 1];
        fibo[0] = 0; fibo[1] = 1;

        // Initialize result
        int sum = fibo[0] + fibo[1];

        // Add remaining terms
        for (int i = 2; i <= n; i++)
        {
            fibo[i] = fibo[i - 1] + fibo[i - 2];
            sum += fibo[i];
        }

        return sum;
    }

    // Driver Code
    static void Main()
    {
        int n = 4;
        Console.WriteLine( "Sum of Fibonacci" +
                              " numbers is : "+
                              calculateSum(n));
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum
// of Fibonacci numbers

// Computes value of first
// fibonacci numbers
function calculateSum($n)
{
    if ($n <= 0)
    return 0;

    $fibo[0] = 0;
    $fibo[1] = 1;

    // Initialize result
    $sum = $fibo[0] + $fibo[1];

    // Add remaining terms
    for($i = 2; $i <= $n; $i++)
    {
        $fibo[$i] = $fibo[$i - 1] +
                    $fibo[$i - 2];
        $sum += $fibo[$i];
    }

    return $sum;
}

    // Driver Code
    $n = 4;
    echo "Sum of Fibonacci numbers is : ",
          calculateSum($n),"\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// Javascript Program to find sum
// of Fibonacci numbers

// Computes value of first
// fibonacci numbers
function calculateSum(n)
{
    let fibo = [];
    if (n <= 0)
    return 0;

    fibo[0] = 0;
    fibo[1] = 1;

    // Initialize result
    let sum = fibo[0] + fibo[1];

    // Add remaining terms
    for(let i = 2; i <= n; i++)
    {
        fibo[i] = fibo[i - 1] +
                    fibo[i - 2];
        sum += fibo[i];
    }

    return sum;
}

    // Driver Code
    let n = 4;
    document.write(`Sum of Fibonacci numbers is :
        ${calculateSum(n)} <br>`);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
Sum of Fibonacci numbers is : 7
```

**方法 2 (O(Log n))**
思路是找出斐波那契数之和与第 n 个斐波那契数的关系。
**F(i)** 指第 I 个斐波那契数。
**S(i)** 是指斐波那契数到 F(i)的和，

```
We can rewrite the relation F(n+1) = F(n) + F(n-1) as below
F(n-1)    = F(n+1)  -  F(n)

Similarly,
F(n-2)    = F(n)    -  F(n-1)
.          .           .
.          .             .
.          .             .
F(0)      = F(2)    -  F(1)
-------------------------------
```

把所有的方程相加，在左边，我们有
F(0) + F(1) + … F(n-1)，也就是 S(n-1)。
因此，
S(n-1)= F(n+1)–F(1)
S(n-1)= F(n+1)–1
S(n)= F(n+2)–1—-(1)
为了找到 S(n)，只需计算第(n+2)个斐波那契数，然后从结果中减去 1 即可。
F(n)可在 O(log n)时间内使用本篇[中的方法 5 或方法 6 进行评估(参考方法 5 和 6)。
以下是基于本](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)
方法 6 的实施

## C++

```
// C++ Program to find sum of Fibonacci numbers in
// O(Log n) time.
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1000;

// Create an array for memoization
int f[MAX] = {0};

// Returns n'th Fibonacci number using table f[]
int fib(int n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n])
        return f[n];

    int k = (n & 1)? (n+1)/2 : n/2;

    // Applying above formula [Note value n&1 is 1
    // if n is odd, else 0].
    f[n] = (n & 1)? (fib(k)*fib(k) + fib(k-1)*fib(k-1))
           : (2*fib(k-1) + fib(k))*fib(k);

    return f[n];
}

// Computes value of first Fibonacci numbers
int calculateSum(int n)
{
    return fib(n+2) - 1;
}

// Driver program to test above function
int main()
{
    int n = 4;
    cout << "Sum of Fibonacci numbers is : "
         << calculateSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of Fibonacci numbers in
// O(Log n) time.
import java.util.*;

class GFG{
static int MAX = 1000;

// Create an array for memoization
static int []f = new int[MAX];

// Returns n'th Fibonacci number using table f[]
static int fib(int n)
{

    // Base cases
    if (n == 0)
    return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n]>0)
        return f[n];

    int k = ((n & 1)>0)? (n+1)/2 : n/2;

    // Applying above formula [Note value n&1 is 1
    // if n is odd, else 0].
    f[n] = (n & 1)>0? (fib(k)*fib(k) + fib(k-1)*fib(k-1))
           : (2*fib(k-1) + fib(k))*fib(k);

    return f[n];
}

// Computes value of first Fibonacci numbers
static int calculateSum(int n)
{
    return fib(n+2) - 1;
}

// Driver program to test above function
public static void main(String[] args)
{
    int n = 4;
    System.out.print("Sum of Fibonacci numbers is : "
         + calculateSum(n) +"\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python 3 Program to find sum of
# Fibonacci numbers in O(Log n) time.

MAX = 1000

# Create an array for memoization
f = [0] * MAX

# Returns n'th Fibonacci number
# using table f[]
def fib(n):

    n = int(n)

    # Base cases
    if (n == 0):
        return 0
    if (n == 1 or n == 2):
        return (1)

    # If fib(n) is already computed
    if (f[n] == True):
        return f[n]

    k = (n+1)/2 if (n & 1) else n/2

    # Applying above formula [Note value n&1
    # is 1 if n is odd, else 0].
    f[n] = (fib(k) * fib(k) + fib(k-1) * fib(k-1)) if (n & 1) else (2 * fib(k-1) + fib(k)) * fib(k)
    return f[n]

# Computes value of first Fibonacci numbers
def calculateSum(n):

    return fib(n+2) - 1

# Driver program to test above function
n = 4
print("Sum of Fibonacci numbers is :", calculateSum(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program to find sum
// of Fibonacci numbers in
// O(Log n) time.
using System;

class GFG {
    static int MAX = 1000;

    // Create an array for memoization
    static int []f = new int[MAX];

    // Returns n'th Fibonacci
    // number using table f[]
    static int fib(int n)
    {
        for(int i = 0;i < MAX;i++)
        f[i] = 0;

        //Arrays.fill(f, 0);
        // Base cases
        if (n == 0)
            return 0;
        if (n == 1 || n == 2)
            return (f[n] = 1);

        // If fib(n) is
        // already computed
        if (f[n] == 1)
            return f[n];
            int k;
        if((n & 1) == 1)
            k = (n + 1) / 2 ;
        else
            k = n / 2;

        // Applying above formula
        // [Note value n&1 is 1
        // if n is odd, else 0].
        if((n & 1) == 1)
            f[n] = (fib(k) * fib(k) + fib(k - 1)
                                   * fib(k - 1));
        else
            f[n] = (2 * fib(k - 1) + fib(k)) *
                                       fib(k);

        return f[n];
    }

    // Computes value of first
    // Fibonacci numbers
    static int calculateSum(int n)
    {
        return fib(n + 2) - 1;
    }

    // Driver Code
    public static void Main()
    {
        int n = 4;
        Console.Write( "Sum of Fibonacci numbers is : "
                                    + calculateSum(n));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of Fibonacci
// numbers in O(Log n) time.
$MAX = 1000;

// Create an array for memoization
$f = array_fill(0, $MAX, 0);

// Returns n'th Fibonacci number
// using table f[]
function fib($n)
{
    global $f;

    // Base cases
    if ($n == 0)
        return 0;
    if ($n == 1 || $n == 2)
        return ($f[$n] = 1);

    // If fib(n) is already computed
    if ($f[$n])
        return $f[$n];

    $k = ($n & 1) ? ($n + 1) / 2 : $n / 2;

    // Applying above formula [Note value n&1
    // is 1 if n is odd, else 0].
    $f[$n] = ($n & 1) ?
             (fib($k) * fib($k) + fib($k - 1) * fib($k - 1)) :
                  (2 * fib($k - 1) + fib($k)) * fib($k);

    return $f[$n];
}

// Computes value of first Fibonacci numbers
function calculateSum($n)
{
    return fib($n + 2) - 1;
}

// Driver Code
$n = 4;
print("Sum of Fibonacci numbers is : " .
                      calculateSum($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript Program to find sum of Fibonacci numbers in
// O(Log n) time.
    var MAX = 1000;

    // Create an array for memoization
     var f = Array(MAX).fill(0);

    // Returns n'th Fibonacci number using table f
    function fib(n) {

        // Base cases
        if (n == 0)
            return 0;
        if (n == 1 || n == 2)
            return (f[n] = 1);

        // If fib(n) is already computed
        if (f[n] > 0)
            return f[n];

        var k = ((n & 1) > 0) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = (n & 1) > 0 ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1)) : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

    // Computes value of first Fibonacci numbers
    function calculateSum(n) {
        return fib(n + 2) - 1;
    }

    // Driver program to test above function
        var n = 4;
        document.write("Sum of Fibonacci numbers is : " + calculateSum(n) + "\n");

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Sum of Fibonacci numbers is : 7
```

本文由 **Chirag Agarwal** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息