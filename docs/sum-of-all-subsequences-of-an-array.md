# 一个数组所有子序列的和

> 原文:[https://www . geesforgeks . org/数组所有子序列之和/](https://www.geeksforgeeks.org/sum-of-all-subsequences-of-an-array/)

给定 n 个整数的数组。求数组中所有可能子序列的和。

**示例:**

```
Input : arr[] = { 1, 2 }
Output : 6
All possible subsequences are {}, {1}, {2} 
and { 1, 2 }

Input : arr[] = { 1, 2, 3 }
Output : 24
```

我们已经在下面的帖子中讨论了两种不同的解决方案。
[所有子阵列之和|集合 1](https://www.geeksforgeeks.org/sum-of-all-subarrays/)

这篇文章讨论了一个不同的解决方案。让我们仔细看看这个问题，并尝试找到一个模式

```
Let a[] = { 1, 2, 3 }

All subsequences are {}, {1}, {2}, {3}, {1, 2}, 
                     {1, 3}, {2, 3}, {1, 2, 3}

So sum of subsequences are 0 + 1 + 2 + 3 + 3 + 
                             4 + 5 + 8 = 24

Here we can observe that in sum every elements 
occurs 4 times. Or in general every element 
will occur 2^(n-1) times. And we can also 
observe that sum of array elements is 6\. So
final result will be 6*4.
```

一般来说，我们可以通过将数组的所有元素乘以 2 <sup>(n-1)</sup> 得到所有子序列的和，其中 n 是数组中的元素数。

## C++

```
// CPP program to find sum of
// all subarrays of array
#include <bits/stdc++.h>
using namespace std;

// To find sum of all subsequences
int findSum(int arr[], int n)
{
    // Sum all array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Result is sum * 2^(n-1)
    return sum * (1 << (n - 1));
}

// Driver program to test findSum()
int main()
{
    int arr[] = { 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// all subarrays of array

public class Main {
    // To find sum of all subsequences
    static int findSum(int arr[], int n)
    {
        // Sum all array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Result is sum * 2^(n-1)
        return sum * (1 << (n - 1));
    }

    // Driver program to test findSum()
    public static void main(String[] args)
    {
        int arr[] = { 1, 2 };
        int n = arr.length;
        System.out.print(findSum(arr, n));
    }
}
```

## 计算机编程语言

```
# Python program to find sum of
# all subarrays of array

# To find sum of all subsequences
def findSum(arr, n):

    # Sum all array elements
    sum = 0
    for i in range(n):
        sum += arr[i]

    # Result is sum * 2^(n-1)
    return sum * (1 << (n - 1))

# Driver program to test findSum()
arr = [1, 2]
n = len(arr)
print findSum(arr, n)

# This code is submitted by Sachin Bisht
```

## C#

```
// C# program to find sum of
// all subarrays of array
using System;

class GFG
{

// To find sum of all subsequences
static int findSum(int []arr, int n)
{
    // Sum all array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Result is sum * 2^(n-1)
    return sum * (1 << (n - 1));
}

// Driver Code
static public void Main ()
{
    int []arr = { 1, 2 };
    int n = arr.Length;
    Console.WriteLine(findSum(arr, n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// all subarrays of array

// To find sum of all subsequences

function findSum($arr, $n)
{
    // Sum all array elements
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // Result is sum * 2^(n-1)
    return $sum * (1 << ($n - 1));
}

// Driver Code
$arr = array( 1, 2 );
$n = sizeof($arr);

echo findSum($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of
// all subarrays of array

// To find sum of all subsequences
function findSum(arr, n)
{

    // Sum all array elements
    let sum = 0;
    for(let i = 0; i < n; i++)
        sum += arr[i];

    // Result is sum * 2^(n-1)
    return sum * (1 << (n - 1));
}

// Driver code
let arr = [ 1, 2 ];
let n = arr.length;

document.write(findSum(arr, n));

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
6
```

本文由 [**核素**](https://www.facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。