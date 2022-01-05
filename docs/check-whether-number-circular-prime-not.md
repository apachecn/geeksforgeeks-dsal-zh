# 检查一个数是否是循环素数

> 原文:[https://www . geesforgeks . org/check-when-number-circular-prime-not/](https://www.geeksforgeeks.org/check-whether-number-circular-prime-not/)

给我们一个数 n，我们的任务是检查这个数是否是循环素数。
**【循环素数】**:一个素数如果在数字的任何循环排列之后，它仍然是素数，那么它就被称为循环素数。
**示例:**

```
Input :  n = 113 
Output : Yes
All cyclic permutations of 113 (311
and 131) are prime. 

Input : 1193
Output : Yes
```

想法很简单，我们生成给定数字的所有排列，并检查每个排列的素数。为了产生排列，我们一个接一个地把最后一个数字移到第一个位置。

## C++

```
// Program to check if a number is circular
// prime or not.
#include <iostream>
#include <cmath>
using namespace std;

// Function to check if a number is prime or not.
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if the number is circular
// prime or not.
bool checkCircular(int N)
{
    // Count digits.
    int count = 0, temp = N;
    while (temp) {
        count++;
        temp /= 10;
    }

    int num = N;
    while (isPrime(num)) {

        // Following three lines generate the next
        // circular permutation of a number. We move
        // last digit to first position.
        int rem = num % 10;
        int div = num / 10;
        num = (pow(10, count - 1)) * rem + div;

        // If all the permutations are checked and
        // we obtain original number exit from loop.
        if (num == N)
            return true;
    }

    return false;
}

// Driver Program
int main()
{
    int N = 1193;
    if (checkCircular(N))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a number
// is circular prime or not.
import java.lang.*;

class GFG
{
    // Function to check if a number is prime or not.
    static boolean isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to check if the number is circular
    // prime or not.
    static boolean checkCircular(int N)
    {
        // Count digits.
        int count = 0, temp = N;
        while (temp>0) {
            count++;
            temp /= 10;
        }

        int num = N;
        while (isPrime(num)) {

        // Following three lines generate the next
        // circular permutation of a number. We
        // move last digit to first position.
        int rem = num % 10;
        int div = num / 10;
        num = (int)((Math.pow(10, count - 1)) * rem)
                                             + div;

        // If all the permutations are checked and
        // we obtain original number exit from loop.
        if (num == N)
            return true;
        }

        return false;
    }

    // Driver Program
    public static void main (String[] args)
    {
        int N = 1193;
        if (checkCircular(N))
        System.out.println("Yes");
        else
        System.out.println("No");
    }
}
/* This code is contributed by Kriti Shukla */
```

## 计算机编程语言

```
# Python Program to check if a number
# is circular prime or not.

import math

# Function to check if a number is prime
# or not.
def isPrime(n) :

    # Corner cases
    if (n <= 1) :
        return False
    if (n <= 3) :
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0) :
        return False

    i = 5
    while i * i <= n :
        if (n % i == 0 or n % (i + 2) == 0) :
            return False
        i = i + 6

    return True

# Function to check if the number is
# circular prime or not.
def checkCircular(N) :

    #Count digits.
    count = 0
    temp = N
    while (temp > 0) :
        count = count + 1
        temp = temp / 10

    num = N;
    while (isPrime(num)) :

        # Following three lines generate the
        # next circular permutation of a
        # number. We move last digit to
        # first position.
        rem = num % 10
        div = num / 10
        num = (int)((math.pow(10, count - 1))
                                * rem)+ div

        # If all the permutations are checked
        # and we obtain original number exit
        # from loop.
        if (num == N) :
            return True

    return False

# Driver Program
N = 1193;
if (checkCircular(N)) :
    print "Yes"
else :
    print "No"

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# Program to check if a number
// is circular prime or not.
using System;

class GFG {

    // Function to check if a
    // number is prime or not.
    static bool isPrime(int n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we
        // can skip middle five numbers
        // in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to check if the number
    // is circular prime or not.
    static bool checkCircular(int N)
    {

        // Count digits.
        int count = 0, temp = N;
        while (temp > 0)
        {
            count++;
            temp /= 10;
        }

        int num = N;
        while (isPrime(num))
        {

            // Following three lines generate
            // the next circular permutation
            // of a number. We move last digit
            // to first position.
            int rem = num % 10;
            int div = num / 10;
            num = (int)((Math.Pow(10, count -
                         1)) * rem) + div;

            // If all the permutations are
            // checked and we obtain original
            // number exit from loop.
            if (num == N)
                return true;
        }

        return false;
    }

    // Driver code
    public static void Main ()
    {
        int N = 1193;
        if (checkCircular(N))
        Console.Write("Yes");
        else
        Console.Write("No");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to check if
// a number is circular
// prime or not.

// Function to check if a
// number is prime or not.
function isPrime($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if ($n % 2 == 0 ||
        $n % 3 == 0)
        return false;

    for ($i = 5;
         $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
            return -1;

    return true;
}

// Function to check if
// the number is circular
// prime or not.
function checkCircular($N)
{
    // Count digits.
    $count = 0;
    $temp = $N;
    while ($temp)
    {
        $count++;
        $temp =(int)$temp / 10;
    }

    $num = $N;
    while (isPrime($num))
    {

        // Following three lines generate
        // the next circular permutation
        // of a number. We move last digit
        // to first position.
        $rem = $num % 10;
        $div = (int)$num / 10;
        $num = (pow(10, $count - 1)) *
                        $rem + $div;

        // If all the permutations are
        // checked and we obtain original
        // number exit from loop.
        if ($num == $N)
            return true;
    }

    return -1;
}

// Driver Code
$N = 1193;
if (checkCircular($N))
    echo "Yes" ,"\n";
else
    echo "No" ,"\n";

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

    // Javascript Program to check if a number
    // is circular prime or not.

    // Function to check if a
    // number is prime or not.
    function isPrime(n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we
        // can skip middle five numbers
        // in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to check if the number
    // is circular prime or not.
    function checkCircular(N)
    {

        // Count digits.
        let count = 0, temp = N;
        while (temp > 0)
        {
            count++;
            temp = parseInt(temp / 10, 10);
        }

        let num = N;
        while (isPrime(num))
        {

            // Following three lines generate
            // the next circular permutation
            // of a number. We move last digit
            // to first position.
            let rem = num % 10;
            let div = parseInt(num / 10, 10);
            num = ((Math.pow(10, count - 1)) * rem) + div;

            // If all the permutations are
            // checked and we obtain original
            // number exit from loop.
            if (num == N)
                return true;
        }

        return false;
    }

    let N = 1193;
    if (checkCircular(N))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**输出:**

```
Yes
```

***时间复杂度:** O(N*N <sup>1/2</sup> )*

***辅助空间:** O(1)*
**优化:**
显然包含 0、2、4、5、6 或 8 的数字永远不可能是循环素数，因为以这些数字结尾的数字总是可以被 2 或 5 整除。因此它们的排列中有一个不是质数。在第一步计数数字的同时，我们还可以检查当前数字是否是其中之一。
本文由**vinet Joshi**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。