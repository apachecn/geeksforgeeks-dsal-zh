# 计算具有连续数字的子集(或子序列)的最小数量

> 原文:[https://www . geeksforgeeks . org/count-最小数-子集-子序列-连续数/](https://www.geeksforgeeks.org/count-minimum-number-subsets-subsequences-consecutive-numbers/)

给定一个不同正数的数组，任务是从数组中计算子集(或子序列)的数量，使得每个子集包含连续的数字。

**示例:**

```
Input :  arr[] = {100, 56, 5, 6, 102, 58, 
                            101, 57, 7, 103, 59}
Output : 3
{5, 6, 7}, { 56, 57, 58, 59}, {100, 101, 102, 103}
are 3 subset in which numbers are consecutive.

Input :  arr[] = {10, 100, 105}
Output : 3
{10}, {100} and {105} are 3 subset in which 
numbers are consecutive. 
```

其思想是对数组进行排序，并遍历排序后的数组来计算此类子集的数量。为了计算这种子集的数量，我们需要计算连续的数字，使得它们之间的差值不等于 1。
以下是寻找包含连续数的子集数的算法:

```
1\. Sort the array arr[ ] and count = 1.
2\. Traverse the sorted array and for each element arr[i].
   If arr[i] + 1 != arr[i+1], 
       then increment the count by one.
3\. Return the count. 
```

下面是该方法的实现:

## C++

```
// C++ program to find number of subset containing
// consecutive numbers
#include <bits/stdc++.h>
using namespace std;

// Returns count of subsets with consecutive numbers
int numofsubset(int arr[], int n)
{
    // Sort the array so that elements which are
    // consecutive in nature became consecutive
    // in the array.
    sort(arr, arr + n);

    int count = 1; // Initialize result
    for (int i = 0; i < n - 1; i++) {
        // Check if there is beginning of another
        // subset of consecutive number
        if (arr[i] + 1 != arr[i + 1])
            count++;
    }

    return count;
}

// Driven Program
int main()
{
    int arr[] = { 100, 56, 5, 6, 102, 58, 101,
                  57, 7, 103, 59 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << numofsubset(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of subset
// containing consecutive numbers
import java.util.*;
class GFG {

    // Returns count of subsets with consecutive numbers
    static int numofsubset(int arr[], int n)
    {
        // Sort the array so that elements
        // which are consecutive in nature
        // became consecutive in the array.
        Arrays.sort(arr);

        // Initialize result
        int count = 1;
        for (int i = 0; i < n - 1; i++) {
            // Check if there is beginning
            // of another subset of
            // consecutive number
            if (arr[i] + 1 != arr[i + 1])
                count++;
        }

        return count;
    }

    // Driven Program
    public static void main(String[] args)
    {
        int arr[] = { 100, 56, 5, 6, 102, 58, 101,
                      57, 7, 103, 59 };
        int n = arr.length;
        System.out.println(numofsubset(arr, n));
    }
}

// This code is contributed by prerna saini.
```

## 计算机编程语言

```
# Python program to find number of subset containing
# consecutive numbers
def numofsubset(arr, n):

  # Sort the array so that elements which are consecutive
  # in nature became consecutive in the array.
  x = sorted(arr)

  count = 1

  for i in range(0, n-1):

    # Check if there is beginning of another subset of
    # consecutive number
    if (x[i] + 1 != x[i + 1]):
      count = count + 1

  return count

# Driven Program
arr = [ 100, 56, 5, 6, 102, 58, 101, 57, 7, 103, 59 ]
n = len(arr)
print numofsubset(arr, n)

# This code is contributed by Afzal Ansari.
```

## C#

```
// C# program to find number of subset
// containing consecutive numbers
using System;

class GFG {

    // Returns count of subsets with
    // consecutive numbers
    static int numofsubset(int[] arr, int n)
    {
        // Sort the array so that elements
        // which are consecutive in nature
        // became consecutive in the array.
        Array.Sort(arr);

        // Initialize result
        int count = 1;
        for (int i = 0; i < n - 1; i++) {

            // Check if there is beginning
            // of another subset of
            // consecutive number
            if (arr[i] + 1 != arr[i + 1])
                count++;
        }

        return count;
    }

    // Driven Program
    public static void Main()
    {
        int[] arr = { 100, 56, 5, 6, 102, 58, 101,
                                 57, 7, 103, 59 };
        int n = arr.Length;
        Console.WriteLine(numofsubset(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of subset containing
// consecutive numbers

// Returns count of subsets
// with consecutive numbers
function numofsubset( $arr, $n)
{

    // Sort the array so that
    // elements which are
    // consecutive in nature
    // became consecutive
    // in the array.
    sort($arr);

    // Initialize result
    $count = 1;
    for ($i = 0; $i < $n - 1; $i++)
    {

        // Check if there is
        // beginning of another
        // subset of consecutive
        // number
        if ($arr[$i] + 1 != $arr[$i + 1])
            $count++;
    }

    return $count;
}

    // Driver Code
    $arr = array(100, 56, 5, 6, 102, 58, 101,
                 57, 7, 103, 59 );
    $n = sizeof($arr);
    echo numofsubset($arr, $n);

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>
// javascript program to find number of subset
// containing consecutive numbers

    // Returns count of subsets with consecutive numbers
    function numofsubset(arr , n) {
        // Sort the array so that elements
        // which are consecutive in nature
        // became consecutive in the array.
        arr.sort((a,b)=>a-b);

        // Initialize result
        var count = 1;
        for (i = 0; i < n - 1; i++) {
            // Check if there is beginning
            // of another subset of
            // consecutive number
            if (arr[i] + 1 != arr[i + 1])
                count++;
        }

        return count;
    }

    // Driven Program

        var arr = [ 100, 56, 5, 6, 102, 58, 101, 57, 7, 103, 59 ];
        var n = arr.length;
        document.write(numofsubset(arr, n));

// This code contributed by Rajput-Ji
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(nlogn)

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。