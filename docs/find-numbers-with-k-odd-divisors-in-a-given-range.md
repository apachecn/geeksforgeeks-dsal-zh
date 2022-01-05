# 求给定范围内有 K 个奇数除数的数

> 原文:[https://www . geesforgeks . org/find-numbers-with-k-奇数除数-在给定范围内/](https://www.geeksforgeeks.org/find-numbers-with-k-odd-divisors-in-a-given-range/)

给定两个数字 a 和 b，以及一个奇数 k。任务是找出 a 和 b(包括 a 和 b)之间所有正好有 k 个除数的数。
示例:

```
Input : a = 2, b = 49, k = 3
Output: 4
// Between 2 and 49 there are four numbers
// with three divisors
// 4 (Divisors 1, 2, 4), 9 (Divisors 1, 3, 9),
// 25 (Divisors 1, 5, 25} and 49 (1, 7 and 49)

Input : a = 1, b = 100, k = 9
Output: 2
// between 1 and 100 there are 36 (1, 2, 3, 4, 6, 9, 12, 18, 36)
// and 100 (1, 2, 4, 5, 10, 20, 25, 50, 100) having exactly 9 
// divisors
```

这个问题有**简单解**，这里我们给出 **k** 是奇数，我们知道只有完美平方数才有奇数除数，所以我们只需要**检查 a 和 b 之间的所有完美平方数**，[只计算那些完美平方数的除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)。

## C++

```
// C++ program to count numbers with k odd
// divisors in a range.
#include<bits/stdc++.h>
using namespace std;

// Utility function to check if number is
// perfect square or not
bool isPerfect(int n)
{
    int s = sqrt(n);

    return (s*s == n);
}

// Utility Function to return count of divisors
// of a number
int divisorsCount(int n)
{
    // Note that this loop runs till square root
    int count=0;
    for (int i=1; i<=sqrt(n)+1; i++)
    {
        if (n%i==0)
        {
            // If divisors are equal, count it
            // only once
            if (n/i == i)
                count += 1;

            // Otherwise print both
            else
                count += 2;
        }
    }
    return count;
}

// Function to calculate all divisors having
// exactly k divisors  between a and b
int kDivisors(int a,int b,int k)
{
    int count = 0; // Initialize result

    // calculate only for perfect square numbers
    for (int i=a; i<=b; i++)
    {
        // check if number is perfect square or not
        if (isPerfect(i))

            // total divisors of number equals to
            // k or not
            if (divisors(i) == k)
                count++;

    }
    return count;
}

// Driver program to run the case
int main()
{
    int a = 2, b = 49, k = 3;
    cout << kDivisors(a, b, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers
// with k odd divisors in a range.
import java.io.*;
import java.math.*;

class GFG {

    // Utility function to check if
    // number is perfect square or not
    static boolean isPerfect(int n)
    {
        int s = (int)(Math.sqrt(n));

        return (s*s == n);
    }

    // Utility Function to return
    // count of divisors of a number
    static int divisorsCount(int n)
    {
        // Note that this loop
        // runs till square root
        int count=0;

      for (int i = 1; i <= Math.sqrt(n) + 1; i++)
      {
        if (n % i == 0)
        {

            // If divisors are equal,
            // count it only once
            if (n / i == i)
                count += 1;

            // Otherwise print both
            else
                count += 2;
        }
      }
        return count;
    }

    // Function to calculate all
    // divisors having exactly k
    // divisors between a and b
    static int kDivisors(int a,int b,int k)
    {
        // Initialize result
        int count = 0;

        // calculate only for
        // perfect square numbers
        for (int i = a; i <= b; i++)
        {
            // check if number is
            // perfect square or not
            if (isPerfect(i))

                // total divisors of number
                // equals to k or not
                if (divisorsCount(i) == k)
                    count++;

        }
        return count;
    }

    // Driver program to run the case
    public static void main(String args[])
    {
        int a = 21, b = 149, k = 333;
        System.out.println(kDivisors(a, b, k));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to count numbers
# with k odd divisors in a range.
import math

# Utility function to check if number
# is perfect square or not
def isPerfect(n) :
    s = math.sqrt(n)

    return (s * s == n)

# Utility Function to return
# count of divisors of a number
def divisorsCount(n) :

    # Note that this loop runs till
    # square root
    count = 0
    for i in range(1, (int)(math.sqrt(n) + 2)) :

        if (n % i == 0) :
            # If divisors are equal,
            # counbt it only once
            if (n // i == i) :
                count = count + 1

            # Otherwise print both
            else :
                count = count + 2

    return count

# Function to calculate all divisors having
# exactly k divisors between a and b
def kDivisors(a, b, k) :
    count = 0 # Initialize result

    # calculate only for perfect square numbers
    for i in range(a, b + 1) :

        # check if number is perfect square or not
        if (isPerfect(i)) :
            # total divisors of number equals to
            # k or not
            if (divisorsCount(i) == k) :
                count = count + 1

    return count

# Driver program to run the case
a = 2
b = 49
k = 3
print(kDivisors(a, b, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to count numbers with
// k odd divisors in a range.
using System;

class GFG {

    // Utility function to check if number
    // is perfect square or not
    static bool isPerfect(int n)
    {
        int s = (int)(Math.Sqrt(n));

        return (s * s == n);
    }

    // Utility Function to return
    // count of divisors of a number
    static int divisorsCount(int n)
    {
        // Note that this loop
        // runs till square root
        int count=0;

    for (int i = 1; i <= Math.Sqrt(n) + 1; i++)
    {
        if (n % i == 0)
        {

            // If divisors are equal,
            // count it only once
            if (n / i == i)
                count += 1;

            // Otherwise print both
            else
                count += 2;
        }
    }
        return count;
    }

    // Function to calculate all
    // divisors having exactly k
    // divisors between a and b
    static int kDivisors(int a, int b,
                         int k)
    {
        // Initialize result
        int count = 0;

        // calculate only for
        // perfect square numbers
        for (int i = a; i <= b; i++)
        {
            // check if number is
            // perfect square or not
            if (isPerfect(i))

                // total divisors of number
                // equals to k or not
                if (divisorsCount(i) == k)
                    count++;

        }
        return count;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int a = 21, b = 149, k = 333;
        Console.Write(kDivisors(a, b, k));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers
// with k odd divisors in a range.

// function to check if number is
// perfect square or not
function isPerfect($n)
{
    $s = sqrt($n);
    return ($s * $s == $n);
}

// Function to return count
// of divisors of a number
function divisorsCount($n)
{

    // Note that this loop
    // runs till square root
    $count = 0;
    for ($i = 1; $i <= sqrt($n) + 1; $i++)
    {
        if ($n % $i == 0)
        {

            // If divisors are equal,
            // count it only once
            if ($n / $i == $i)
                $count += 1;

            // Otherwise print both
            else
                $count += 2;
        }
    }
    return $count;
}

// Function to calculate
// all divisors having
// exactly k divisors
// between a and b
function kDivisors($a, $b, $k)
{  

    // Initialize result
    $count = 0;

    // calculate only for
    // perfect square numbers
    for ($i = $a; $i <= $b; $i++)
    {

        // check if number is
        // perfect square or not
        if (isPerfect($i))

            // total divisors of
            // number equals to
            // k or not
            if (divisorsCount($i) == $k)
                $count++;

    }
    return $count;
}

    // Driver Code
    $a = 2;
    $b = 49;
    $k = 3;
    echo kDivisors($a, $b, $k);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count numbers with
// k odd divisors in a range.

// Utility function to check if number
// is perfect square or not
function isPerfect(n)
{
    var s = parseInt((Math.sqrt(n)));

    return (s * s == n);
}

// Utility Function to return
// count of divisors of a number
function divisorsCount(n)
{
    // Note that this loop
    // runs till square root
    var count=0;

for (var i = 1; i <= parseInt(Math.sqrt(n)) + 1; i++)
{

    if (n % i == 0)
    {

        // If divisors are equal,
        // count it only once
        if (parseInt(n / i) == i)
            count += 1;
        // Otherwise print both
        else
            count += 2;
    }
}

    return count;
}

// Function to calculate all
// divisors having exactly k
// divisors between a and b
function kDivisors(a, b, k)
{
    // Initialize result
    var count = 0;

    // calculate only for
    // perfect square numbers
    for(var i = a; i <= b; i++)
    {
        // check if number is
        // perfect square or not
        if (isPerfect(i))
        {
            // total divisors of number
            // equals to k or not
            if (divisorsCount(i)==k)
            {
                count++;
            }
        }

    }
    return count;
}

// Driver Code
var a = 2, b = 49, k = 3;
document.write(kDivisors(a, b, k));

</script>
```

**输出:**

```
4
```

**这个问题可以更高效地解决。请参考下面帖子的方法 2，了解有效的解决方案。**
[**两个给定数字之间的完美平方数**](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers/)
本文由 [**Shashank Mishra(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。