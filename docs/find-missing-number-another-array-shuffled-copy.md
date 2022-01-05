# 在另一个被混洗的数组中找到缺失的数字

> 原文:[https://www . geesforgeks . org/find-missing-number-other-array-shuffled-copy/](https://www.geeksforgeeks.org/find-missing-number-another-array-shuffled-copy/)

给定 n 个正整数的数组“arr1”。arr1[]的内容被复制到另一个数组“arr2”中，但数字被打乱，一个元素被删除。找到丢失的元素(不使用任何额外的空间，时间复杂度为 0(n))。
**例:**

```
Input : arr1[] = {4, 8, 1, 3, 7}, 
        arr2[] = {7, 4, 3, 1}
Output : 8

Input : arr1[] = {12, 10, 15, 23, 11, 30}, 
        arr2[] = {15, 12, 23, 11, 30}
Output : 10
```

一个**简单的解决方法**就是逐个考虑第一个数组的每个元素，在第二个数组中搜索。一旦我们找到一个丢失的元素，我们就返回。这个解的时间复杂度为 O(n <sup>2</sup> )
一个**高效解**基于异或。每个元素组合出现两次，一次在“arr1”中，另一次在“arr2”中，只有一个元素在“arr1”中出现一次。我们知道(a Xor a) = 0。所以，简单地对两个数组的元素进行异或运算。结果将是缺少的数字。

## C++

```
// C++ implementation to find the
// missing number in shuffled array
// C++ implementation to find the
// missing number in shuffled array
#include <bits/stdc++.h>
using namespace std;

// Returns the missing number
// Size of arr2[] is n-1
int missingNumber(int arr1[], int arr2[],
                                   int n)
{
    // Missing number 'mnum'
    int mnum = 0;

    // 1st array is of size 'n'
    for (int i = 0; i < n; i++)
        mnum = mnum ^ arr1[i];

    // 2nd array is of size 'n - 1'
    for (int i = 0; i < n - 1; i++)
        mnum = mnum ^ arr2[i];

    // Required missing number
    return mnum;
}

// Driver Code
int main()
{
    int arr1[] = {4, 8, 1, 3, 7};
    int arr2[] = {7, 4, 3, 1};
    int n = sizeof(arr1) / sizeof(arr1[0]);
    cout << "Missing number = "
        << missingNumber(arr1, arr2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// missing number in shuffled array

class GFG
{
    // Returns the missing number
    // Size of arr2[] is n-1
    static int missingNumber(int arr1[],
                             int arr2[],
                                  int n)
    {
        // Missing number 'mnum'
        int mnum = 0;

        // 1st array is of size 'n'
        for (int i = 0; i < n; i++)
            mnum = mnum ^ arr1[i];

        // 2nd array is of size 'n - 1'
        for (int i = 0; i < n - 1; i++)
            mnum = mnum ^ arr2[i];

        // Required missing number
        return mnum;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr1[] = {4, 8, 1, 3, 7};
        int arr2[] = {7, 4, 3, 1};
        int n = arr1.length;

        System.out.println("Missing number = "
            + missingNumber(arr1, arr2, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the
# missing number in shuffled array

# Returns the missing number
# Size of arr2[] is n - 1
def missingNumber(arr1, arr2, n):

    # missing number 'mnum'
    mnum = 0

    # 1st array is of size 'n'
    for i in range(n):
        mnum = mnum ^ arr1[i]

    # 2nd array is of size 'n - 1'
    for i in range(n - 1):
        mnum = mnum ^ arr2[i]

    # Required missing number
    return mnum

# Driver Code
arr1 = [4, 8, 1, 3, 7]
arr2= [7, 4, 3, 1]
n = len(arr1)
print("Missing number = ",
    missingNumber(arr1, arr2, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to find the
// missing number in shuffled array
using System;

class GFG
{
    // Returns the missing number
    // Size of arr2[] is n-1
    static int missingNumber(int []arr1,
                             int []arr2,
                                  int n)
    {
        // Missing number 'mnum'
        int mnum = 0;

        // 1st array is of size 'n'
        for (int i = 0; i < n; i++)
            mnum = mnum ^ arr1[i];

        // 2nd array is of size 'n - 1'
        for (int i = 0; i < n - 1; i++)
            mnum = mnum ^ arr2[i];

        // Required missing number
        return mnum;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr1 = {4, 8, 1, 3, 7};
        int []arr2 = {7, 4, 3, 1};
        int n = arr1.Length;

    Console.Write("Missing number = "
            + missingNumber(arr1, arr2, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the
// missing number in shuffled array
// PHP implementation to find the
// missing number in shuffled array

// Returns the missing number
// Size of arr2[] is n-1
function missingNumber($arr1, $arr2,
                                $n)
{

    // Missing number 'mnum'
    $mnum = 0;

    // 1st array is of size 'n'
    for ($i = 0; $i < $n; $i++)
        $mnum = $mnum ^ $arr1[$i];

    // 2nd array is of size 'n - 1'
    for ($i = 0; $i < $n - 1; $i++)
        $mnum = $mnum ^ $arr2[$i];

    // Required missing number
    return $mnum;
}

    // Driver Code
    $arr1 = array(4, 8, 1, 3, 7);
    $arr2 = array(7, 4, 3, 1);
    $n = count($arr1);
    echo "Missing number = "
        , missingNumber($arr1, $arr2, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// missing number in shuffled array
// Javascript implementation to find the
// missing number in shuffled array

// Returns the missing number
// Size of arr2[] is n-1
function missingNumber(arr1, arr2, n)
{
    // Missing number 'mnum'
    let mnum = 0;

    // 1st array is of size 'n'
    for (let i = 0; i < n; i++)
        mnum = mnum ^ arr1[i];

    // 2nd array is of size 'n - 1'
    for (let i = 0; i < n - 1; i++)
        mnum = mnum ^ arr2[i];

    // Required missing number
    return mnum;
}

// Driver Code
    let arr1 = [4, 8, 1, 3, 7];
    let arr2 = [7, 4, 3, 1];
    let n = arr1.length;
    document.write("Missing number = "
        + missingNumber(arr1, arr2, n));

</script>
```

**输出:**

```
Missing number = 8
```

复杂度:O(n)时间复杂度和 O(1)额外空间。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。