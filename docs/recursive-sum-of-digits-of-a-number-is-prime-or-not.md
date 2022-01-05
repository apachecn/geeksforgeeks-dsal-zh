# 一个数的位数递归和是不是素数

> 原文:[https://www . geesforgeks . org/递归数字总和是质数还是非质数/](https://www.geeksforgeeks.org/recursive-sum-of-digits-of-a-number-is-prime-or-not/)

给定一个数字 n，我们需要找到这个数字的每个数字的和，直到这个数字变成一个数字。如果总和是质数，我们需要打印“是”，如果不是质数，我们需要打印“否”。

**示例:**

```
Input : 5602
Output: No
Explanation:
Step 1- 5+6+0+2 = 13
Step 2- 1+3 = 4 
4 is not prime

Input : 56
Output : Yes
Explanation:
Step 1- 5+6 = 11
Step 2- 1+1 = 2 hence 2 is prime 
```

思路很简单，我们可以[快速找到数字的递归和](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)。

```
int recDigSum(int n)
{
    if (n == 0) 
       return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}
```

一旦计算出递归和，只需检查它是 2、3、5 还是 7(这些只是个位数的素数)就可以检查它是不是素数。

## C++

```
// CPP code to check if
// recursive sum of
// digits is prime or not.
#include<iostream>
using namespace std;

// Function for recursive
// digit sum
int recDigSum(int n)
{
    if (n == 0)
        return 0;
    else
    {
        if (n % 9 == 0)
            return 9;
        else
            return n % 9;
    }
}

// function to check if prime
// or not the single digit
void check(int n)
{
    // calls function which
    // returns sum till
    // single digit
    n = recDigSum(n);

    // checking prime
    if (n == 2 or n == 3 or n == 5 or n == 7)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
   int n = 5602;
    check(n);
}

// This code is contributed by Shreyanshi.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java code to check if
// recursive sum of
// digits is prime or not.
import java.io.*;

class GFG
{

    // Function for recursive
    // digit sum
    static int recDigSum(int n)
    {
        if (n == 0)
            return 0;
        else
        {
            if (n % 9 == 0)
                return 9;
            else
                return n % 9;
        }
    }

    // function to check if prime
    // or not the single digit
    static void check(int n)
    {
        // calls function which
        // returns sum till
        // single digit
        n = recDigSum(n);

        // checking prime
        if (n == 2 || n == 3 || n == 5 || n == 7)
            System.out.println ( "Yes");
        else
            System.out.println("No");
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5602;
        check(n);

    }
}

// This code is contributed by vt_m
```

## 计算机编程语言

```
# Python code to check if recursive sum
# of digits is prime or not.
def recDigSum(n):

    if n == 0:
        return 0
    else:
        if n % 9 == 0:
            return 9
        else:
            return n % 9

# function to check if prime or not
# the single digit
def check(n):

    # calls function which returns sum
    # till single digit
    n = recDigSum(n)

    # checking prime
    if n == 2 or n == 3 or n == 5 or n == 7:
        print "Yes"
    else:
        print "No"

# driver code
n = 5602
check(n)
```

## C#

```
// C# code to check if
// recursive sum of
// digits is prime or not.
using System;

class GFG
{

    // Function for recursive
    // digit sum
    static int recDigSum(int n)
    {
        if (n == 0)
            return 0;
        else
        {
            if (n % 9 == 0)
                return 9;
            else
                return n % 9;
        }
    }

    // function to check if prime
    // or not the single digit
    static void check(int n)
    {
        // calls function which
        // returns sum till
        // single digit
        n = recDigSum(n);

        // checking prime
        if (n == 2 || n == 3
            || n == 5 || n == 7)
            Console.WriteLine ( "Yes");
        else
            Console.WriteLine("No");
    }

    // Driver code
    public static void Main ()
    {
        int n = 5602;
        check(n);

    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if
// recursive sum of
// digits is prime or not.

// Function for recursive
// digit sum
function recDigSum($n)
{
    if ($n == 0)
        return 0;
    else
    {
        if ($n % 9 == 0)
            return 9;
        else
            return $n % 9;
    }
}

// function to check if prime
// or not the single digit
function check( $n)
{
    // calls function which
    // returns sum till
    // single digit
    $n = recDigSum($n);

    // checking prime
    if ($n == 2 or $n == 3 or
        $n == 5 or $n == 7)
        echo "Yes";
    else
        echo "No";
}

// Driver code
$n = 5602;
check($n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript code to check if
// recursive sum of digits is
// prime or not.

// Function for recursive
// digit sum
function recDigSum(n)
{
    if (n == 0)
        return 0;
    else
    {
        if (n % 9 == 0)
            return 9;
        else
            return n % 9;
    }
}

// Function to check if prime
// or not the single digit
function check(n)
{

    // Calls function which
    // returns sum till
    // single digit
    n = recDigSum(n);

    // Checking prime
    if (n == 2 || n == 3 ||
        n == 5 || n == 7)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
let n = 5602;

check(n);

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
No
```

本文由 [**钿巴贾杰**](https://auth.geeksforgeeks.org/profile.php?user=Twinkle Bajaj) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。