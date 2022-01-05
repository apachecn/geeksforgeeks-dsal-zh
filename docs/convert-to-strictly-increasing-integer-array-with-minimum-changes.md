# 转换为变化最小的严格递增整数数组

> 原文:[https://www . geesforgeks . org/convert-to-严格递增整数数组-最小变化/](https://www.geeksforgeeks.org/convert-to-strictly-increasing-integer-array-with-minimum-changes/)

给定 n 个整数的数组。写一个程序，找出数组中最小的变化数，使数组严格增加整数。在严格递增数组 A[i] < A[i+1] for 0 <= i < n
**中举例:**

```
Input : arr[] = { 1, 2, 6, 5, 4}
Output : 2
We can change a[2] to any value 
between 2 and 5.
and a[4] to any value greater then 5\. 

Input : arr[] = { 1, 2, 3, 5, 7, 11 }
Output : 0
Array is already strictly increasing.
```

问题是[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)的变异。已经是 LIS 一部分的数字不需要改变。因此，需要改变的最小元素是 LIS 中数组大小和元素数量的差异。请注意，我们还需要确保数字是整数。因此，在制作 LIS 时，我们不认为那些元素是 LIS 的一部分，不能通过在中间插入元素来形成严格的递增。
例{1，2，5，3，4}，我们认为 LIS 的长度为三{1，2，5}，而不是{ 1，2，3，4 }，因为我们不能用这个 LIS 构成一个严格递增的整数数组。

## C++

```
// CPP program to find min elements to
// change so array is strictly increasing
#include <bits/stdc++.h>
using namespace std;

// To find min elements to remove from array
// to make it strictly increasing
int minRemove(int arr[], int n)
{
    int LIS[n], len = 0;

    // Mark all elements of LIS as 1
    for (int i = 0; i < n; i++)
        LIS[i] = 1;

    // Find LIS of array
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (arr[i] > arr[j] && (i-j)<=(arr[i]-arr[j])){
                LIS[i] = max(LIS[i], LIS[j] + 1);
            }
        }
        len = max(len, LIS[i]);
    }

    // Return min changes for array
    // to strictly increasing
    return n - len;
}

// Driver program to test minRemove()
int main()
{
    int arr[] = { 1, 2, 6, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minRemove(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find min elements to
// change so array is strictly increasing
public class Main {

    // To find min elements to remove from array
    // to make it strictly increasing
    static int minRemove(int arr[], int n)
    {
        int LIS[] = new int[n];
        int len = 0;

        // Mark all elements of LIS as 1
        for (int i = 0; i < n; i++)
            LIS[i] = 1;

        // Find LIS of array
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (arr[i] > arr[j] && (i-j)<=(arr[i]-arr[j]))
                    LIS[i] = Math.max(LIS[i],
                                 LIS[j] + 1);
            }
            len = Math.max(len, LIS[i]);
        }

        // Return min changes for array
        // to strictly increasing
        return n - len;
    }

    // Driver program to test minRemove()
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 6, 5, 4 };
        int n = arr.length;

        System.out.println(minRemove(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find min elements to
# change so array is strictly increasing

# Find min elements to remove from array
# to make it strictly increasing
def minRemove(arr, n):
    LIS = [0 for i in range(n)]
    len = 0

    # Mark all elements of LIS as 1
    for i in range(n):
        LIS[i] = 1

    # Find LIS of array
    for i in range(1, n):

        for j in range(i):
            if (arr[i] > arr[j] and (i-j)<=(arr[i]-arr[j]) ):
                LIS[i] = max(LIS[i], LIS[j] + 1)

        len = max(len, LIS[i])

    # Return min changes for array
    # to strictly increasing
    return (n - len)

# Driver Code
arr = [ 1, 2, 6, 5, 4 ]
n = len(arr)
print(minRemove(arr, n))

# This code is contributed by Azkia Anam.
```

## C#

```
// C# program to find min elements to change so
// array is strictly increasing
using System;

class GFG
{

    // To find min elements to remove from array to
    // make it strictly increasing
    static int minRemove(int []arr,
                        int n)
    {
        int []LIS = new int[n];
        int len = 0;

        // Mark all elements
        // of LIS as 1
        for (int i = 0; i < n; i++)
            LIS[i] = 1;

        // Find LIS of array
        for (int i = 1; i < n; i++)
        {
            for (int j = 0; j < i; j++)
            {
                if (arr[i] > arr[j] && (i-j)<=(arr[i]-arr[j]))
                    LIS[i] = Math.Max(LIS[i],
                                LIS[j] + 1);
            }
            len = Math.Max(len, LIS[i]);
        }

        // Return min changes for array 
        // to strictly increasing
        return n - len;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 6, 5, 4};
        int n = arr.Length;

        Console.WriteLine(minRemove(arr, n));
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find min elements to change so
// array is strictly increasing

// To find min elements to remove from array 
// to make it strictly increasing
function minRemove($arr, $n)
{
    $LIS = array();
    $len = 0;

    // Mark all elements
    // of LIS as 1
    for ($i = 0; $i < $n; $i++)
        $LIS[$i] = 1;

    // Find LIS of array
    for ($i = 1; $i < $n; $i++)
    {
        for ($j = 0; $j < $i; $j++)
        {
            if ($arr[$i] > $arr[$j])
                $LIS[$i] = max($LIS[$i],
                            $LIS[$j] + 1);
        }
        $len = max($len, $LIS[$i]);
    }

    // Return min changes for array to strictly
    // increasing
    return $n - $len;
}

// Driver Code
$arr = array(1, 2, 6, 5, 4);
$n = count($arr);

echo minRemove($arr, $n);

// This code is contributed
// by anuj_6
?>
```

## java 描述语言

```
<script>

// Javascript program to find min elements to
// change so array is strictly increasing

    // To find min elements to remove from array
    // to make it strictly increasing
    function minRemove(arr, n)
    {
        let LIS = new Array(n).fill(0);
        let len = 0;

        // Mark all elements of LIS as 1
        for (let i = 0; i < n; i++)
            LIS[i] = 1;

        // Find LIS of array
        for (let i = 1; i < n; i++) {
            for (let j = 0; j < i; j++) {
                if (arr[i] > arr[j] && (i-j)<=(arr[i]-arr[j]))
                    LIS[i] = Math.max(LIS[i],
                                 LIS[j] + 1);
            }
            len = Math.max(len, LIS[i]);
        }

        // Return min changes for array
        // to strictly increasing
        return n - len;
    }

// driver program

        let arr = [ 1, 2, 6, 5, 4 ];
        let n = arr.length;

        document.write(minRemove(arr, n));

// This code is contributed by Code_hunt.
</script>
```

**输出:**

```
2
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。