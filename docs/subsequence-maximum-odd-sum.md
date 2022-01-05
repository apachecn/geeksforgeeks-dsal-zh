# 最大奇数和的子序列

> 原文:[https://www.geeksforgeeks.org/subsequence-maximum-odd-sum/](https://www.geeksforgeeks.org/subsequence-maximum-odd-sum/)

给定一组整数，检查是否有奇数和的子序列，如果有，则求最大奇数和。如果没有子序列包含奇数和，返回-1。

**示例:**

```
Input : arr[] = {2, 5, -4, 3, -1};
Output : 9
The subsequence with maximum odd 
sum is 2, 5, 3 and -1.

Input : arr[] = {4, -3, 3, -5}
Output : 7
The subsequence with maximum odd
sum is 4 and 3

Input :  arr[] = {2, 4, 6}
Output : -1
There is no subsequence with odd sum.
```

一个**简单解**生成所有子序列，求所有奇数和子序列的最大和。这个解决方案的时间复杂度将是指数级的。

一个**高效的解决方案**可以在 O(n)时间内工作。这个想法基于以下事实。
1)如果所有的数都是偶数，奇数和是不可能的。否则，我们总会找到答案。
2)如果奇数和是可能的，我们求所有正整数的和。如果和是奇数，我们返回它，因为这是最大的正和。如果和是偶数，我们从和中减去绝对值最小的奇数。如果最小的绝对奇数是负的，它就成为结果的一部分，当它是正的，它就从结果中去掉，这一事实可以证明这个步骤是正确的。

## C++

```
// C++ program to find maximum sum of odd
// subsequence if it exists.
#include<bits/stdc++.h>
using namespace std;

// Returns maximum sum odd subsequence if exists
// Else returns -1
int findMaxOddSubarraySum(int arr[], int n)
{
    // Here min_odd is the minimum odd number (in
    // absolute terms). Initializing with max value
    // of int .
    int min_odd = INT_MAX;

    // To check if there is al-least one odd number.
    bool isOdd = false;

    int sum = 0;  // To store sum of all positive elements
    for (int i=0 ; i<n ; i++)
    {
        // Adding positive number would increase
        // the sum.
        if (arr[i] > 0)
            sum = sum + arr[i];

        // To find the minimum odd number(absolute)
        // in the array.
        if (arr[i]%2 != 0)
        {
            isOdd = true;
            if (min_odd> abs(arr[i]))
                min_odd = abs(arr[i]);
        }
    }

    // If there was no odd number
    if (isOdd == false)
       return -1;

    // Now, sum will be either odd or even.
    // If even, changing it to odd. As, even - odd = odd.
    // since m is the minimum odd number(absolute).
    if (sum%2 == 0)
        sum = sum - min_odd;

    return sum;
}

// Driver code
int main()
{
    int arr[] = {2, -3, 5, -1, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMaxOddSubarraySum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum
// of odd subsequence if it exists.
import java.io.*;

class GFG {

// Returns maximum sum odd subsequence,
// if exists Else returns -1
static int findMaxOddSubarraySum(int arr[], int n)
{
    // Here min_odd is the minimum odd number
    // (in absolute terms). Initializing with
    // max value of int .
    int min_odd = Integer.MAX_VALUE;

    // To check if there is al-least
    // one odd number.
    boolean isOdd = false;

    // To store sum of all positive elements
    int sum = 0;
    for (int i = 0 ; i < n ; i++)
    {
        // Adding positive number would
        // increase the sum.
        if (arr[i] > 0)
            sum = sum + arr[i];

        // To find the minimum odd number
        // (absolute) in the array.
        if (arr[i] % 2 != 0)
        {
            isOdd = true;
            if (min_odd > Math.abs(arr[i]))
                min_odd = Math.abs(arr[i]);
        }
    }

    // If there was no odd number
    if (isOdd == false)
    return -1;

    // Now, sum will be either odd or even.
    // If even, changing it to odd.
    // As, even - odd = odd.
    // since m is the minimum odd
    // number(absolute).
    if (sum % 2 == 0)
        sum = sum - min_odd;

    return sum;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = {2, -3, 5, -1, 4};
    int n = arr.length;
    System.out.println(findMaxOddSubarraySum(arr, n));

}
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program to find
# maximum sum of odd
# subsequence if it exists.

# Returns maximum sum odd
# subsequence if exists
# Else returns -1
def findMaxOddSubarraySum(arr, n):

    # Here min_odd is the
    # minimum odd number (in
    # absolute terms).
    # Initializing with max value
    # of int .
    min_odd = +2147483647

    # To check if there is
    # at-least one odd number.
    isOdd = False

    # To store sum of
    # all positive elements
    sum = 0 
    for i in range(n):

        # Adding positive number
        # would increase
        # the sum.
        if (arr[i] > 0):
            sum = sum + arr[i]

        # To find the minimum
        # odd number(absolute)
        # in the array.
        if (arr[i]%2 != 0):

            isOdd = True
            if (min_odd > abs(arr[i])):
                min_odd = abs(arr[i])

    # If there was no odd number
    if (isOdd == False):
         return -1

    # Now, sum will be
    # either odd or even.
    # If even, changing it to
    # odd. As, even - odd = odd.
    # since m is the minimum
    # odd number(absolute).
    if (sum%2 == 0):
        sum = sum - m

    return sum

# Driver code

arr = [2, -3, 5, -1, 4]
n =len(arr)

print(findMaxOddSubarraySum(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find maximum sum
// of odd subsequence if it exists.
using System;

class GFG {

    // Returns maximum sum odd subsequence,
    // if exists Else returns -1
    static int findMaxOddSubarraySum(int []arr, int n)
    {

        // Here min_odd is the minimum odd number
        // (in absolute terms). Initializing with
        // max value of int .
        int min_odd = int.MaxValue;

        // To check if there is al-least
        // one odd number.
        bool isOdd = false;

        // To store sum of all positive elements
        int sum = 0;
        for (int i = 0 ; i < n ; i++)
        {

            // Adding positive number would
            // increase the sum.
            if (arr[i] > 0)
                sum = sum + arr[i];

            // To find the minimum odd number
            // (absolute) in the array.
            if (arr[i] % 2 != 0)
            {
                isOdd = true;
                if (min_odd > Math.Abs(arr[i]))
                    min_odd = Math.Abs(arr[i]);
            }
        }

        // If there was no odd number
        if (isOdd == false)
            return -1;

        // Now, sum will be either odd or even.
        // If even, changing it to odd.
        // As, even - odd = odd.
        // since m is the minimum odd
        // number(absolute).
        if (sum % 2 == 0)
            sum = sum - min_odd;

        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {2, -3, 5, -1, 4};
        int n = arr.Length;
        Console.Write(findMaxOddSubarraySum(arr, n));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// sum of odd subsequence if
// it exists.

// Returns maximum sum odd
// subsequence if exists Else
// returns -1
function findMaxOddSubarraySum( $arr, $n)
{
    // Here min_odd is the minimum
    // odd number (in absolute terms).
    // Initializing with max value
    // of int .
    $min_odd = PHP_INT_MAX;

    // To check if there is
    // at-least one odd number.
    $isOdd = false;

    // To store sum of all
    // positive elements
    $sum = 0;
    for ( $i = 0; $i < $n; $i++)
    {
        // Adding positive number
        // would increase the sum.
        if ($arr[$i] > 0)
            $sum = $sum + $arr[$i];

        // To find the minimum odd
        // number(absolute) in the array.
        if ($arr[$i] % 2 != 0)
        {
            $isOdd = true;
            if ($min_odd > abs($arr[$i]))
                $min_odd = abs($arr[$i]);
        }
    }

    // If there was no odd number
    if ($isOdd == false)
    return -1;

    // Now, sum will be either
    // odd or even. If even,
    // changing it to odd. As,
    // even - odd = odd. since
    // m is the minimum odd
    // number(absolute).
    if ($sum % 2 == 0)
        $sum = $sum - $min_odd;

    return $sum;
}

// Driver code
$arr = array(2, -3, 5, -1, 4);
$n = count($arr);
echo findMaxOddSubarraySum($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum sum
    // of odd subsequence if it exists.

    // Returns maximum sum odd subsequence,
    // if exists Else returns -1
    function findMaxOddSubarraySum(arr, n)
    {

        // Here min_odd is the minimum odd number
        // (in absolute terms). Initializing with
        // max value of int .
        let min_odd = Number.MAX_VALUE;

        // To check if there is al-least
        // one odd number.
        let isOdd = false;

        // To store sum of all positive elements
        let sum = 0;
        for (let i = 0 ; i < n ; i++)
        {

            // Adding positive number would
            // increase the sum.
            if (arr[i] > 0)
                sum = sum + arr[i];

            // To find the minimum odd number
            // (absolute) in the array.
            if (arr[i] % 2 != 0)
            {
                isOdd = true;
                if (min_odd > Math.abs(arr[i]))
                    min_odd = Math.abs(arr[i]);
            }
        }

        // If there was no odd number
        if (isOdd == false)
            return -1;

        // Now, sum will be either odd or even.
        // If even, changing it to odd.
        // As, even - odd = odd.
        // since m is the minimum odd
        // number(absolute).
        if (sum % 2 == 0)
            sum = sum - min_odd;

        return sum;
    }

    let arr = [2, -3, 5, -1, 4];
    let n = arr.length;
    document.write(findMaxOddSubarraySum(arr, n));

 // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
11
```

时间复杂度:O(n)
辅助空间:O(1)

本文由 **Jatin Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。