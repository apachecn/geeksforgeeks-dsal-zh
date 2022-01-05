# 最大的子阵列，带有一个 GCD

> 原文:[https://www.geeksforgeeks.org/largest-subarray-gcd-one/](https://www.geeksforgeeks.org/largest-subarray-gcd-one/)

有一个包含 n 个元素的数组。求 GCD 等于 1 的最大子阵的长度。如果没有带 GCD 1 的子阵列，则打印-1。

**示例:**

```
Input  : 1 3 5 
Output : 3

Input : 2 4 6
Output :-1 
```

一个**简单的解决方案**就是考虑每个子阵，找到它的 GCD，用 GCD 一个跟踪最大的子阵。最后用 GCD 1 返回最大子阵的长度。

一个**有效的解决方案**是基于这样一个事实:如果任何两个元素的 GCD 等于 1，那么整个数组的 GCD 就是 1。所以输出不是-1 就是数组长度。

## C++

```
// C++ program, to find length of the largest
// subarray with GCD equals to 1.
#include<bits/stdc++.h>
using namespace std;

int findLargest(int arr[], int n)
{
    /*If gcd of any subarray is 1 then gcd of
     any number with the sub array will be 1.
     so if we are getting any subarray with
     gcd 1, then maximum number of element of
      the subarray will be equal to the number
      of elements of the array. Else it will be -1.*/
    int gcd = arr[0];
    for (int i=1; i<n; i++)
        gcd = __gcd(gcd, arr[i]);

    return (gcd == 1)? n : -1;
}

// Driver code
int main()
{
    int arr[] = {1, 3, 5, 7};
    int n = sizeof(arr)/sizeof(int);
    cout << "Length of the largest subarray = "
         << findLargest(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program, to find length of the
// largest subarray with GCD equals to 1.
class GFG {

    static int ___gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return ___gcd(a - b, b);

        return ___gcd(a, b - a);
    }

    static int findLargest(int arr[],
                                int n)
    {

        /*If gcd of any subarray is 1
        then gcd of any number with the
        sub array will be 1\. so if we
        are getting any subarray with
        gcd 1, then maximum number of
        element of the subarray will
        be equal to the number of 
        elements of the array. Else
        it will be -1.*/
        int gcd = arr[0];

        for (int i = 1; i < n; i++)
            gcd = ___gcd(gcd, arr[i]);

        return (gcd == 1)? n : -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {1, 3, 5, 7};
        int n = arr.length;

        System.out.print("Length of the "
                   + "largest subarray = "
                   + findLargest(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program, to find
# length of the largest
# subarray with GCD equals to 1.

def ___gcd(a,b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return ___gcd(a-b, b)
    return ___gcd(a, b-a)

def findLargest(arr, n):

    '''If gcd of any subarray is 1 then gcd of
     any number with the sub array will be 1.
     so if we are getting any subarray with
     gcd 1, then maximum number of element of
      the subarray will be equal to the number
      of elements of the array. Else it will be -1.'''
    gcd = arr[0]
    for i in range(1,n):
        gcd = ___gcd(gcd, arr[i])

    return n if (gcd == 1) else -1

# Driver code
arr=[1, 3, 5, 7]
n=len(arr)

print("Length of the largest subarray = ",
         findLargest(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program, to find length of the
// largest subarray with GCD equals to 1.
using System;

class GFG {

    static int ___gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return ___gcd(a - b, b);

        return ___gcd(a, b - a);
    }

    static int findLargest(int []arr,
                           int n)
    {

        // If gcd of any subarray is 1
        // then gcd of any number with the
        // sub array will be 1\. so if we
        // are getting any subarray with
        // gcd 1, then maximum number of
        // element of the subarray will
        // be equal to the number of
        // elements of the array. Else
        // it will be -1.
        int gcd = arr[0];

        for (int i = 1; i < n; i++)
            gcd = ___gcd(gcd, arr[i]);

        return (gcd == 1)? n : -1;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {1, 3, 5, 7};
        int n = arr.Length;

        Console.Write("Length of the "
                       + "largest subarray = "
                       + findLargest(arr, n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program, to find length
// of the largest subarray with
// GCD equals to 1.
function ___gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0 || $b == 0)
        return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return ___gcd($a - $b, $b);

    return ___gcd($a, $b - $a);
}

function findLargest($arr, $n)
{

    /*If gcd of any subarray is 1
    then gcd of any number with the
    sub array will be 1\. so if we
    are getting any subarray with
    gcd 1, then maximum number of
    element of the subarray will
    be equal to the number of
    elements of the array. Else
    it will be -1.*/
    $gcd = $arr[0];

    for ($i = 1; $i < $n; $i++)
        $gcd = ___gcd($gcd, $arr[$i]);

    return ($gcd == 1)? $n : -1;
}

// Driver code
$arr = array(1, 3, 5, 7);
$n = count($arr);

echo "Length of the " .
     "largest subarray = " .
      findLargest($arr, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program, to find length of the
// largest subarray with GCD equals to 1.

    function ___gcd(a, b)
    {

        // Everything divides 0 
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return ___gcd(a - b, b);

        return ___gcd(a, b - a);
    } 

    function findLargest(arr, n)
    {

        /*If gcd of any subarray is 1 
        then gcd of any number with the 
        sub array will be 1\. so if we 
        are getting any subarray with
        gcd 1, then maximum number of
        element of the subarray will 
        be equal to the number of  
        elements of the array. Else 
        it will be -1.*/
        let gcd = arr[0];

        for (let i = 1; i < n; i++)
            gcd = ___gcd(gcd, arr[i]);

        return (gcd == 1)? n : -1;
    }

// Driver Code

        let arr = [1, 3, 5, 7];
        let n = arr.length;

        document.write("Length of the "
                   + "largest subarray = "
                   + findLargest(arr, n));

</script>
```

**输出:**

```
Length of the largest subarray = 4
```

本文由 **Smarak Chopdar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。