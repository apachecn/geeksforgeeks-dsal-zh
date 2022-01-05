# 检查一个数组中大小为 k 的每个段中是否有一个键

> 原文:[https://www . geesforgeks . org/check-if-a-key-present-in-每段大小-k-in-a-array/](https://www.geeksforgeeks.org/check-if-a-key-is-present-in-every-segment-of-size-k-in-an-array/)

给定一个数组 arr[]，数组的大小是 n，另一个是键 x，给你一个段大小 k。任务是在 arr[]，找到大小为 k 的每个段中存在的键 x。
**例:**

> **输入:**
> arr[] = { 3，5，2，4，9，3，1，7，3，11，12，3}
> x = 3
> k = 3
> **输出:**是
> 数组中有 4 个大小为 k 的非重叠段，{ 3，5，2}，{4，9，3}，{1，7，3}和{11，12，3}。3 代表所有细分市场。
> **输入:**
> arr[] = { 21，23，56，65，34，54，76，32，23，45，21，23，25}
> x = 23
> k = 5
> **输出:**是
> 有三段，最后一段未满{ 21，23，56，65，34}，{54，76
> 23 是呈现所有窗口。
> **输入:** arr[] = { 5，8，7，12，14，3，9}
> x = 8
> k = 2
> **输出:**否

想法很简单，我们考虑大小为 k 的每个片段，并检查窗口中是否存在 x。我们需要仔细处理最后一段。
下面是上述方法的实现:

## C++

```
// C++ code to find the  every segment size of
// array have a search key x
#include <bits/stdc++.h>
using namespace std;

bool findxinkindowSize(int arr[], int x, int k, int n)
{
    int i;
    for (i = 0; i < n; i = i + k) {

        // Search x in segment starting
        // from index i.
        int j;
        for (j = 0; j < k; j++)
            if (arr[i + j] == x)
                break;

        // If loop didn't break
        if (j == k)
           return false;
    }

    // If n is a multiple of k
    if (i == n)
       return true;

    // Check in last segment if n
    // is not multiple of k.
    int j;
    for (j=i-k; j<n; j++)
      if (arr[j] == x)
          break;
    if (j == n)
       return false; 

    return true;
}

// main driver
int main()
{
    int arr[] = { 3, 5, 2, 4, 9, 3, 1, 7, 3, 11, 12, 3 };
    int x = 3, k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    if (findxinkindowSize(arr, x, k, n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the every
// segment size of array have
// a search key x
import java.util.*;
class GFG {
    static boolean findxinkindowSize(int N, int[] arr,
                                     int x, int k)
    {
        int i;
        boolean b = false;

        // Iterate from 0 to N - 1
        for (i = 0; i < N; i = i + k) {

            // Iterate from 0 to k - 1
            for (int j = 0; j < k; j++) {
                if (i + j < N && arr[i + j] == x)
                    break;

                if (j == k)
                    return false;
                if (i + j >= N)
                    return false;
            }
        }
        if (i >= N)
            return true;
        else
            return b;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = new int[] { 3, 5, 2, 4,  9,  3,
                                1, 7, 3, 11, 12, 3 };
        int x = 3, k = 3;
        int n = arr.length;
        if (findxinkindowSize(n, arr, x, k))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Vivek258709
```

## 蟒蛇 3

```
# Python 3 program to find
# the every segment size of
# array have a search key x

def findxinkindowSize(arr, x, k, n) :

    i = 0
    while i < n :

        j = 0

        # Search x in segment
        # starting from index i
        while j < k :

            if arr[i + j] == x :
                break

            j += 1

        # If loop didn't break
        if j == k :
            return False

        i += k

    # If n is a multiple of k    
    if i == n :
        return True

    j = i - k

    # Check in last segment if n
    # is not multiple of k.
    while j < n :
        if arr[j] == x :
            break

        j += 1

    if j == n :
        return False

    return True

# Driver Code
if __name__ == "__main__" :

    arr = [ 3, 5, 2, 4, 9, 3,
            1, 7, 3, 11, 12, 3 ]
    x, k = 3, 3
    n = len(arr)

    if (findxinkindowSize(arr, x, k, n)) :
        print("Yes")
    else :
        print("No")

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# code to find the every
// segment size of array have
// a search key x
using System;

class GFG
{
static bool findxinkindowSize(int[] arr, int x,
                              int k, int n)
{
    int i;
    for (i = 0; i < n; i = i + k)
    {

        // Search x in segment
        // starting from index i.
        int j;
        for (j = 0; j < k; j++)
            if (arr[i + j] == x)
                break;

        // If loop didn't break
        if (j == k)
        return false;
    }

    // If n is a multiple of k
    if (i == n)
    return true;

    // Check in last segment if
    // n is not multiple of k.
    int l;
    for (l = i - k; l < n; l++)
    if (arr[l] == x)
        break;
    if (l == n)
    return false;

    return true;
}

// Driver Code
public static void Main()
{
    int[] arr = new int[] {3, 5, 2, 4, 9, 3,
                         1, 7, 3, 11, 12, 3};
    int x = 3, k = 3;
    int n = arr.Length;
    if (findxinkindowSize(arr, x, k, n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the every
// segment size of array have
// a search key x

function findxinkindowSize(&$arr, $x,
                            $k, $n)
{
    for ($i = 0;
         $i < $n; $i = $i + $k)
    {

        // Search x in segment
        // starting from index i.
        for ($j = 0; $j < $k; $j++)
            if ($arr[$i + $j] == $x)
                break;

        // If loop didn't break
        if ($j == $k)
        return false;
    }

    // If n is a multiple of k
    if ($i == $n)
    return true;

    // Check in last segment if n
    // is not multiple of k.
    for ($j = $i - $k; $j < $n; $j++)
    if ($arr[$j] == $x)
        break;
    if ($j == $n)
    return false;

    return true;
}

// Driver Code
$arr = array(3, 5, 2, 4, 9, 3, 1,
             7, 3, 11, 12, 3);
$x = 3;
$k = 3;
$n = sizeof($arr);
if (findxinkindowSize($arr, $x, $k, $n))
    echo "Yes" ;
else
    echo "No" ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript code to find the  every segment size of
// array have a search key x

function findxinkindowSize( arr,  x,  k,  n)
{
    let i;
    for (i = 0; i < n; i = i + k) {

        // Search x in segment starting
        // from index i.
        let j;
        for (j = 0; j < k; j++)
            if (arr[i + j] == x)
                break;

        // If loop didn't break
        if (j == k)
           return false;
    }

    // If n is a multiple of k
    if (i == n)
       return true;

    // Check in last segment if n
    // is not multiple of k.
    let j;
    for (j=i-k; j<n; j++)
      if (arr[j] == x)
          break;
    if (j == n)
       return false; 

    return true;
}

// main driver
  let arr = [ 3, 5, 2, 4, 9, 3, 1, 7, 3, 11, 12, 3 ];
    let x = 3, k = 3;
    let n = arr.length;
    if (findxinkindowSize(arr, x, k, n))
        document.write("Yes");
    else
        document.write("No");

// This code contributed by aashish1995

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:O(n)**