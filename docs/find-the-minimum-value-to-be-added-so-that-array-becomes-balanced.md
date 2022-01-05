# 找到要相加的最小值，使数组达到平衡

> 原文:[https://www . geeksforgeeks . org/find-要添加的最小值-使阵列变得平衡/](https://www.geeksforgeeks.org/find-the-minimum-value-to-be-added-so-that-array-becomes-balanced/)

给定一个均匀大小的数组，任务是找到可以添加到元素中的最小值，使数组变得平衡。如果数组元素左半部分的总和等于右半部分的总和，则数组是平衡的。假设我们有一个数组 1 3 1 2 4 3。前三个元素的和是 1 + 3 + 1 = 5，后三个元素的和是 2 + 4 + 3 = 9
所以这是不平衡的，为了使其平衡，我们可以在前半部分给任何元素加的最小数是 4。
**例:**

```
Input : 1 2 1 2 1 3
Output : 2
Sum of first 3 elements is 1 + 2 + 1 = 4, 
sum of last three elements is 2 + 1 + 3 = 6
To make the array balanced you can add 2.

Input : 20 10
Output : 10
```

想法很简单，我们计算第一半和第二半的和。一旦计算出这些和，我们就返回这两个值的绝对差。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Returns minimum value that need to be added
// to make array balanced.
int minValueToBalance(int a[], int n)
{
    // Calculating sum of first half elements
    // of an array
    int sum1 = 0;
    for (int i = 0; i < n/2; i++)
        sum1 += a[i];

    // Calculating sum of other half elements
    // of an array
    int sum2 = 0;
    for (int i = n/2; i < n; i++)
        sum2 += a[i];

    // calculating difference
    return abs(sum1 - sum2);
}

// Driver code
int main()
{
    int arr[] = {1, 7, 1, 1, 3, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << minValueToBalance(arr, n)<<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find the minimum value
// to be added so that array becomes balanced

class Minimum
{
    // Returns minimum value that need to
    // be added to make array balanced.
    public static int minValueToBalance(int a[],
                                        int n)
    {
        // Calculating sum of first half
        // elements of an array
        int sum1 = 0;
        for (int i = 0; i < n / 2; i++)
            sum1 += a[i];

        // Calculating sum of other half
        // elements of an array
        int sum2 = 0;
        for (int i = n/2; i < n; i++)
            sum2 += a[i];

        // calculating difference
        return Math.abs(sum1 - sum2);
    }

    // driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 7, 1, 1, 3, 1};
        int n = 6;
        System.out.print(minValueToBalance(arr, n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program to Find the
# minimum value to be added so that
# array becomes balanced

# Returns minimum value that need to
# be added to make array balanced.
def minValueToBalance(a, n):

    # Calculating sum of first
    # half elements of an array
    sum1 = 0
    for i in range( int(n / 2)):
        sum1 += a[i]

    # Calculating sum of other
    # half elements of an array
    sum2 = 0;
    i = int(n / 2)
    while i < n:
        sum2 += a[i]
        i = i + 1

    # calculating difference
    return abs(sum1 - sum2)

# Driver code
arr = [1, 7, 1, 1, 3, 1]
n = len(arr)
print(minValueToBalance(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to Find the minimum value
// to be added so that array becomes balanced
using System;

class Minimum {

    // Returns minimum value that need to
    // be added to make array balanced.
    public static int minValueToBalance(int []a,
                                        int n)
    {

        // Calculating sum of first half
        // elements of an array
        int sum1 = 0;
        for (int i = 0; i < n / 2; i++)
            sum1 += a[i];

        // Calculating sum of other half
        // elements of an array
        int sum2 = 0;
        for (int i = n / 2; i < n; i++)
            sum2 += a[i];

        // calculating difference
        return Math.Abs(sum1 - sum2);
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 7, 1, 1, 3, 1};
        int n = 6;
        Console.Write(minValueToBalance(arr, n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Returns minimum value
// that need to be added
// to make array balanced.
function minValueToBalance($a, $n)
{
    // Calculating sum of first
    // half elements of an array
    $sum1 = 0;
    for ($i = 0; $i < $n / 2; $i++)
        $sum1 += $a[$i];

    // Calculating sum of other
    // half elements of an array
    $sum2 = 0;
    for ( $i = $n / 2; $i < $n; $i++)
        $sum2 += $a[$i];

    // calculating difference
    return abs($sum1 - $sum2);
}

// Driver code
$arr = array(1, 7, 1, 1, 3, 1);
$n = sizeof($arr) / sizeof($arr[0]);
echo minValueToBalance($arr, $n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Returns minimum value that need to be added
// to make array balanced.
function minValueToBalance(a, n)
{
    // Calculating sum of first half elements
    // of an array
    let sum1 = 0;
    for (let i = 0; i < Math.floor(n/2); i++)
        sum1 += a[i];

    // Calculating sum of other half elements
    // of an array
    let sum2 = 0;
    for (let i = Math.floor(n/2); i < n; i++)
        sum2 += a[i];

    // calculating difference
    return Math.abs(sum1 - sum2);
}

// Driver code
    let arr = [1, 7, 1, 1, 3, 1];
    let n = arr.length;
    document.write(minValueToBalance(arr, n) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
4
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。