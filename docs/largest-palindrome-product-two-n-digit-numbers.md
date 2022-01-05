# 两个 n 位数乘积的最大回文

> 原文:[https://www . geesforgeks . org/maximum-回文-product-两位数-数字/](https://www.geeksforgeeks.org/largest-palindrome-product-two-n-digit-numbers/)

给定值 n，找出最大的回文数，它是两个 n 位数的乘积。

**示例:**

```
Input  : n = 2
Output : 9009 
9009 is the largest number which is product of two 
2-digit numbers. 9009 = 91*99.

Input : n = 3
Output : 906609
```

以下是找到所需号码的步骤。

1.  找到 n 位数的下限。例如，对于 n = 2，lower_limit 为 10。
2.  找出 n 位数的上限。例如，对于 n = 2，upper_limit 为 99。
3.  考虑所有的数对，其中任何一个数都在范围内[下限，上限]

下面是以上步骤的实现。

## C++

```
// C++ problem to find out the
// largest palindrome number which
// is product of two n digit numbers
#include <bits/stdc++.h>
using namespace std;

// Function to calculate largest
// palindrome which is product of
// two n-digits numbers
int larrgestPalindrome(int n)
{
    int upper_limit = pow(10,n) - 1;

    // largest number of n-1 digit.
    // One plus this number is lower
    // limit which is product of two numbers.
    int lower_limit = 1 + upper_limit / 10;

    // Initialize result
    int max_product = 0;
    for (int i = upper_limit;
             i >= lower_limit;
             i--)
    {
        for (int j = i; j >= lower_limit; j--)
        {
            // calculating product of
            // two n-digit numbers
            int product = i * j;
            if (product < max_product)
                break;
            int number = product;
            int reverse = 0;

            // calculating reverse of
            // product to check whether
            // it is palindrome or not
            while (number != 0)
            {
                reverse = reverse * 10 +
                          number % 10;
                number /= 10;
            }

            // update new product if exist
            // and if greater than previous one
            if (product == reverse &&
                product > max_product)

                max_product = product;
        }
    }
    return max_product;
}

// Driver code
int main()
{
    int n = 2;
    cout << larrgestPalindrome(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java problem to find out the
// largest palindrome number
// which is product of two
// n digit numbers.
import java.lang.Math;

class GFG
{
    // Function to calculate largest
    // palindrome which isproduct of
    // two n-digits numbers
    static int larrgestPalindrome(int n)
    {
        int upper_limit = (int)Math.pow(10, n) - 1;

        // largest number of n-1 digit.
        // One plus this number
        // is lower limit which is
        // product of two numbers.
        int lower_limit = 1 + upper_limit / 10;

        // Initialize result
        int max_product = 0;

        for (int i = upper_limit; i >= lower_limit; i--)
        {
            for (int j = i; j >= lower_limit; j--)
            {
                // calculating product of two
                // n-digit numbers
                int product = i * j;
                if (product < max_product)
                    break;
                int number = product;
                int reverse = 0;

                // calculating reverse of product
                // to check whether it is
                // palindrome or not
                while (number != 0)
                {
                    reverse = reverse * 10 + number % 10;
                    number /= 10;
                }

                // update new product if exist and if
                // greater than previous one
                if (product == reverse && product > max_product)
                    max_product = product;
            }
        }
        return max_product;
    }

    // Driver code
    public static void main (String[] args)
    {

        int n = 2;
        System.out.print(larrgestPalindrome(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python problem to find
# out the largest palindrome
# number which is product of
# two n digit numbers.

# Function to calculate largest
# palindrome which is
#  product of two n-digits numbers

def larrgestPalindrome(n):

    upper_limit = (10**(n))-1

    # largest number of n-1 digit.
    # One plus this number
    # is lower limit which is
    # product of two numbers.
    lower_limit = 1 + upper_limit//10

    max_product = 0 # Initialize result
    for i in range(upper_limit,lower_limit-1, -1):

        for j in range(i,lower_limit-1,-1):

            # calculating product of
            # two n-digit numbers
            product = i * j
            if (product < max_product):
                break
            number = product
            reverse = 0

            # calculating reverse of
            # product to check
            # whether it is palindrome or not
            while (number != 0):

                reverse = reverse * 10 + number % 10
                number =number // 10

             # update new product if exist and if
             # greater than previous one
            if (product == reverse and product > max_product):
                max_product = product

    return max_product

# Driver code

n = 2
print(larrgestPalindrome(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# problem to find out the
// largest palindrome number
// which is product of two
// n digit numbers.
using System;

class GFG
{
    // Function to calculate largest
    // palindrome which isproduct of
    // two n-digits numbers
    static int larrgestPalindrome(int n)
    {
        int upper_limit = (int)Math.Pow(10, n) - 1;

        // largest number of n-1 digit.
        // One plus this number
        // is lower limit which is
        // product of two numbers.
        int lower_limit = 1 + upper_limit / 10;

        // Initialize result
        int max_product = 0;

        for (int i = upper_limit; i >= lower_limit; i--)
        {
            for (int j = i; j >= lower_limit; j--)
            {
                // calculating product of two
                // n-digit numbers
                int product = i * j;
                if (product < max_product)
                    break;
                int number = product;
                int reverse = 0;

                // calculating reverse of product
                // to check whether it is
                // palindrome or not
                while (number != 0)
                {
                    reverse = reverse * 10 + number % 10;
                    number /= 10;
                }

                // update new product if exist and if
                // greater than previous one
                if (product == reverse && product > max_product)
                    max_product = product;
            }
        }
        return max_product;
    }

    // Driver code
    public static void Main ()
    {

        int n = 2;
        Console.Write(larrgestPalindrome(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP problem to find out
// the largest palindrome
// number which is product
// of two n digit numbers

// Function to calculate
// largest palindrome which
// is product of two n-digit numbers
function larrgestPalindrome($n)
{
    $upper_limit = 0;

    // Loop to calculate upper bound
    // (largest number of n-digit)
    for ($i = 1; $i <= $n; $i++)
    {
        $upper_limit *= 10;
        $upper_limit += 9;
    }

    // largest number of n-1 digit
    // One plus this number
    // is lower limit which is
    // product of two numbers.
    $lower_limit = 1 + (int)($upper_limit / 10);

    // Initialize result
    $max_product = 0;
    for ($i = $upper_limit;
         $i >= $lower_limit;
         $i--)
    {
        for ($j = $i;
             $j >= $lower_limit;
             $j--)
        {
            // calculating product of
            // two n-digit numbers
            $product = $i * $j;
            if ($product < $max_product)
                break;
            $number = $product;
            $reverse = 0;

            // calculating reverse of
            // product to check whether
            // it is palindrome or not
            while ($number != 0)
            {
                $reverse = $reverse * 10 +
                           $number % 10;
                $number = (int)($number / 10);
            }

            // update new product if exist
            // and if greater than previous one
            if ($product == $reverse &&
                $product > $max_product)

                $max_product = $product;
        }
    }
    return $max_product;
}

// Driver code
$n = 2;
echo(larrgestPalindrome($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript problem to find out the
    // largest palindrome number
    // which is product of two
    // n digit numbers.

    // Function to calculate largest
    // palindrome which isproduct of
    // two n-digits numbers
    function larrgestPalindrome(n)
    {
        let upper_limit = Math.pow(10, n) - 1;

        // largest number of n-1 digit.
        // One plus this number
        // is lower limit which is
        // product of two numbers.
        let lower_limit = 1 +
        parseInt(upper_limit / 10, 10);

        // Initialize result
        let max_product = 0;

        for (let i = upper_limit; i >= lower_limit; i--)
        {
            for (let j = i; j >= lower_limit; j--)
            {
                // calculating product of two
                // n-digit numbers
                let product = i * j;
                if (product < max_product)
                    break;
                let number = product;
                let reverse = 0;

                // calculating reverse of product
                // to check whether it is
                // palindrome or not
                while (number != 0)
                {
                    reverse = reverse * 10 + number % 10;
                    number = parseInt(number / 10, 10);
                }

                // update new product if exist and if
                // greater than previous one
                if (product == reverse &&
                product > max_product)
                    max_product = product;
            }
        }
        return max_product;
    }

    let n = 2;
      document.write(larrgestPalindrome(n));

</script>
```

**输出:**

```
9009
```

这篇文章中使用的方法简单明了。如果你找到更好的方法，请评论。
本文由**希瓦姆·普拉丹(anuj_charm)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息