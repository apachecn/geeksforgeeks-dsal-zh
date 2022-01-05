# 可重构编号

> 原文:[https://www.geeksforgeeks.org/refactorable-number/](https://www.geeksforgeeks.org/refactorable-number/)

给定一个整数 **n** 。检查号码是否可重构。一个可重构的数是一个整数 n，它可以被它的除数整除。
**例:**

```
Input:  n = 8
Output: yes

Explanation:
8 has 4 divisors: 1, 2, 4, 8
Since 8 is divisible by 4 therefore 8 is 
refactorable number.

Input : n = 4 
Output: no
```

这个解决方案非常简单。其思想是从 1 迭代到 sqrt(n)，并计算一个数的所有除数。之后我们只需要检查数字 **n** 是否能被它的总计数整除。

## C++

```
// C++ program to check whether number is
// refactorable or not
#include <bits/stdc++.h>

// Function to count all divisors
bool isRefactorableNumber(int n)
{
    // Initialize result
    int divCount = 0;

    for (int i = 1; i <= sqrt(n); ++i)
    {
        if (n % i==0)
        {
            // If divisors are equal, count
            // only one.
            if (n / i == i)
                ++divCount;

            // Otherwise count both
            else
                divCount += 2;
        }
    }

    return n % divCount == 0;
}

//Driver Code
int main()
{
    int n = 8;
    if (isRefactorableNumber(n))
        puts("yes");
    else
        puts("no");

    n = 14;
    if (isRefactorableNumber(n))
        puts("yes");
    else
        puts("no");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether number is
// refactorable or not

class GFG
{
    // Function to count all divisors
    static boolean isRefactorableNumber(int n)
    {
        // Initialize result
        int divCount = 0;

        for (int i = 1; i <= Math.sqrt(n); ++i)
        {
            if (n % i==0)
            {
                // If divisors are equal, count
                // only one.
                if (n / i == i)
                    ++divCount;

                // Otherwise count both
                else
                    divCount += 2;
            }
        }
        return n % divCount == 0;
    }

    public static void main (String[] args)
    {
        int n = 8;
        if (isRefactorableNumber(n))
            System.out.println("yes");
        else
            System.out.println("no");

        n = 14;
        if (isRefactorableNumber(n))
            System.out.println("yes");
        else
            System.out.println("no");
    }
}

// This code is contributed by Saket Kumar
```

## 计算机编程语言

```
# Python program to check whether number is
# refactorable or not
import math

def isRefactorableNumber(n):

    # Initialize result
    divCount = 0

    for i in range(1,int(math.sqrt(n))+1):

        if n % i == 0:

            # If divisors are equal, count only one
            if n/i == i:
                divCount += 1

            else:  # Otherwise count both
                divCount += 2

    return n % divCount == 0

# Driver Code
n = 8
if isRefactorableNumber(n):
    print "yes"
else:
    print "no"

n = 14
if (isRefactorableNumber(n)):
    print "yes"
else:
    print "no"
```

## C#

```
// C# program to check whether number is
// refactorable or not
using System;

class GFG
{
    // Function to count all divisors
    static bool isRefactorableNumber(int n)
    {

        // Initialize result
        int divCount = 0;

        for (int i = 1; i <= Math.Sqrt(n); ++i)
        {
            if (n % i==0)
            {
                // If divisors are equal, count
                // only one.
                if (n / i == i)
                    ++divCount;

                // Otherwise count both
                else
                    divCount += 2;
            }
        }
        return n % divCount == 0;
    }

    // Driver code
    public static void Main ()
    {
        int n = 8;
        if (isRefactorableNumber(n))
            Console.WriteLine("yes");
        else
            Console.Write("no");

        n = 14;
        if (isRefactorableNumber(n))
            Console.Write("yes");
        else
            Console.Write("no");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// whether number is
// refactorable or not

// Function to count all divisors
function isRefactorableNumber($n)
{

    // Initialize result
    $divCount = 0;

    for ($i = 1; $i <= sqrt($n); ++$i)
    {
        if ($n % $i==0)
        {

            // If divisors are equal,
            // count only one.
            if ($n / $i == $i)
                ++$divCount;

            // Otherwise count both
            else
                $divCount += 2;
        }
    }

    return $n % $divCount == 0;
}

    // Driver Code
    $n = 8;
    if (isRefactorableNumber($n))
        echo "yes";
    else
        echo "no";
        echo"\n";
    $n = 14;
    if (isRefactorableNumber($n))
        echo "yes";
    else
        echo "no";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to count all divisors
    function isRefactorableNumber(n)
    {
        // Initialize result
        let divCount = 0; 

        for (let i = 1; i <= Math.sqrt(n); ++i)
        {
            if (n % i==0)
            {
                // If divisors are equal, count 
                // only one.
                if (n / i == i)
                    ++divCount;

                // Otherwise count both
                else
                    divCount += 2;
            }
        }
        return n % divCount == 0;
    }

// Driver Code
    let n = 8;
    if (isRefactorableNumber(n))
        document.write("yes" + "<br />");
    else
        document.write("no" + "<br />");

    n = 14;
    if (isRefactorableNumber(n))
        document.write("yes");
    else
        document.write("no");

        // This code is contributed by splevel62.
</script>
```

```
Output:
yes
no
```

**时间复杂度:** O(sqrt(n))
**辅助空间:** O(1)
**关于可重构数的事实**

1.  没有可重构的数字是[完美的](https://www.geeksforgeeks.org/perfect-number/)。

2.  没有三个连续的整数可以全部重构。

3.  可重构数的自然密度为零。

**参考:**[【https://en.wikipedia.org/wiki/Refactorable_number】](https://en.wikipedia.org/wiki/Refactorable_number)
本文由[舒巴姆·班萨尔](https://www.facebook.com/banalshubham)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。