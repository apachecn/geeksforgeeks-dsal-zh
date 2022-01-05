# 从自然数中去掉给定整数后的第 K 个最小元素|集合 2

> 原文:[https://www . geesforgeks . org/k-th-最小-元素-移除-给定-整数-自然数-集合-2/](https://www.geeksforgeeks.org/k-th-smallest-element-removing-given-integers-natural-numbers-set-2/)

给定一个大小为“n”的数组 arr[]和一个正整数 k。考虑一系列自然数，并从中删除 arr[0]、arr[1]、arr[2]、…、arr[n-1]。现在的任务是在剩下的自然数集中找到第 k 个最小的数。
**例:**

```
Input : arr[] = { 1 } and k = 1.
Output: 2
Natural numbers are {1, 2, 3, 4, .... }
After removing {1}, we get {2, 3, 4, ...}.
Now, K-th smallest element = 2.

Input : arr[] = {1, 3}, k = 4.
Output : 6
First 5 Natural number {1, 2, 3, 4, 5, 6,  .. }
After removing {1, 3}, we get {2, 4, 5, 6, ... }.
```

2 种方法在本[篇](https://www.geeksforgeeks.org/k-th-smallest-element-removing-integers-natural-numbers/)中讨论。
这篇文章讨论了另一种方法。
**算法:**

1.  开始遍历数组，I 范围从 0 到 N-1

2.  如果 arr[i] ![<=  ](img/b2e4fdc35137d55002277126876860da.png "Rendered by QuickLaTeX.com") k，则增加 k。否则中断遍历数组的其余部分

3.  得到的 k 就是最终答案

## C++

```
// C++ program to find the K-th smallest element
// after removing some integers from natural number.
#include <bits/stdc++.h>
using namespace std;

// Return the K-th smallest element.
int ksmallest(int arr[], int n, int k)
{
    for (int i = 0; i < n; i++) {
        if (arr[i] <= k)
            k++;
        else
            break;
    }
    return k;
}

// Driven Program
int main()
{
    int k = 1;
    int arr[] = { 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << ksmallest(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// K-th smallest element
// after removing some
// integers from natural number.
class GFG
{

// Return the K-th
// smallest element.
static int ksmallest(int arr[],
                     int n, int k)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] <= k)
            k++;
        else
            break;
    }
    return k;
}

// Driver Code
public static void main(String args[])
{
    int k = 1;
    int arr[] = { 1 };
    int n = arr.length;
    System.out.println(ksmallest(arr, n, k));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find
# the K-th smallest element
# after removing some integers
# from natural number.

# Return the K-th
# smallest element.
def ksmallest(arr, n, k):
    for i in range(n):
        if (arr[i] <= k):
            k = k + 1;
        else:
            break;
    return k;

# Driver Code
k = 1;
arr = [1];
n = len(arr);
print(ksmallest(arr, n, k));

# This code is contributed by mits
```

## C#

```
// C# program to find the
// K-th smallest element
// after removing some
// integers from natural number.
using System;

class GFG
{
// Return the K-th
// smallest element.

static int ksmallest(int []arr,
                     int n, int k)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] <= k)
            k++;
        else
            break;
    }
    return k;
}

// Driver Code
static public void Main ()
{
    int k = 1;
    int []arr = { 1 };
    int n = arr.Length;
    Console.WriteLine(ksmallest(arr,
                                n, k));
}
}

// This code is contributed @ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the K-th
// smallest element after removing
// some integers from natural number.

// Return the K-th smallest element.
function ksmallest($arr, $n, $k)
{
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] <= $k)
            $k++;
        else
            break;
    }
    return $k;
}

    // Driver Code
    $k = 1;
    $arr = array(1);
    $n = sizeof($arr);
    echo ksmallest($arr, $n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // K-th smallest element
    // after removing some
    // integers from natural number.

    // Return the K-th
    // smallest element.

    function ksmallest(arr, n, k)
    {
        for (let i = 0; i < n; i++)
        {
            if (arr[i] <= k)
                k++;
            else
                break;
        }
        return k;
    }

    let k = 1;
    let arr = [ 1 ];
    let n = arr.length;
    document.write(ksmallest(arr, n, k));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
```