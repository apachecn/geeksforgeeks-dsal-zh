# 在 2n+1 个整数元素的数组中寻找单个

> 原文:[https://www . geesforgeks . org/find-single-array-2 n1-integer-elements/](https://www.geeksforgeeks.org/find-single-array-2n1-integer-elements/)

给定一个有 2n+1 个整数的数组，n 个元素在数组的任意位置出现两次，一个整数在数组内部的某个地方只出现一次。用 O(n)次运算和 O(1)次额外内存求孤独整数。
**例:**

```
Input : { 1, 1, 2, 2, 3, 3, 4, 4, 5}
Output : 5

Input : { 7, 9, 6, 8, 3, 7, 8, 6, 9}
Output : 3
```

想法是对所有元素进行异或运算。所有元素的异或运算给了我们结果。这个想法是基于下面的异或属性。

1.  一个数与自身的异或是 0。
2.  数与 0 的异或就是数。

## C++

```
// CPP program to find only
// element in an array where
// every element appears twice.
#include <bits/stdc++.h>
using namespace std;

// Find non repeating
// number in an array
int findNonRepeating(int arr[],
                     int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 3, 8, 3, 2, 2, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findNonRepeating(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find only element
// in an array where every element
// appears twice.
import java.io.*;

class GFG
{

// Find non repeating
// number in an array
static int findNonRepeating(int []arr,
                            int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];
    return res;
}

// Driver Code
static public void main (String[] args)
{
int []arr = {3, 8, 3, 2, 2, 1, 1};
int n = arr.length;
System.out.println(findNonRepeating(arr, n));
}
}

// This code is contributed by vt_m.
```

## 计算机编程语言

```
# Find non repeating
# number in an array

def findNonRepeating(a, n):
    res = 0

    # XOR of all numbers
    for i in range(n):
        res ^= a[i]
    return res

# Driver code
a = [ 3, 8, 3, 2, 2, 1, 1 ]
n = len(a)

print findNonRepeating(a, n)

# This code is contributed
# by 'Striver'.
```

## C#

```
// C# program to find only element
// in an array where every element
// appears twice.
using System;

class GFG
{

// Find non repeating number in an array
static int findNonRepeating(int []arr,
                            int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];
    return res;
}

// Driver Code
static public void Main (String []args)
{
int []arr = {3, 8, 3, 2, 2, 1, 1};
int n = arr.Length;
Console.WriteLine(findNonRepeating(arr,
                                   n));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find only
// element in an array where
// every element appears twice.

// Find non repeating number
// in an array
function findNonRepeating($arr, $n)
{
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res = $res ^ $arr[$i];
    return $res;
}

// Driver Code
$arr = array( 3, 8, 3, 2, 2, 1, 1 );
$n = sizeof($arr);
echo(findNonRepeating($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find only
// element in an array where
// every element appears twice.

// Find non repeating
// number in an array
function findNonRepeating(arr, n)
{
    let res = 0;
    for (let i = 0; i < n; i++)
        res = res ^ arr[i];
    return res;
}

// Driver Code
    let arr = [ 3, 8, 3, 2, 2, 1, 1 ];
    let n = arr.length;
    document.write(findNonRepeating(arr, n));

</script>
```

**输出:**

```
8
```

时间复杂度:O(n)。
空间复杂度:O(1)。
本文由 [**阿西普·帕万·库马尔**](https://auth.geeksforgeeks.org/profile.php?user=Pawan Asipu) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。