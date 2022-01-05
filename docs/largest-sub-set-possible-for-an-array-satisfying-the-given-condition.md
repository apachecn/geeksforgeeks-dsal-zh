# 满足给定条件的阵列的最大可能子集

> 原文:[https://www . geesforgeks . org/最大子集-可能满足给定条件的数组/](https://www.geeksforgeeks.org/largest-sub-set-possible-for-an-array-satisfying-the-given-condition/)

给定一个数组 **arr[]** 和一个整数 **K** 。任务是找到最大子集的大小，使得子集 **(X，Y)** 中的每一对都是 **Y 的形式！= (X * K)** 其中 **X < Y** 。

**示例:**

> **输入:** arr[] = {2，3，6，5，4，10}，K = 2
> **输出:** 3
> {2，3，5}为所需子集
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10}，K = 2
> **输出:** 6

**进场:**

*   [排序](https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/)所有数组元素。
*   创建一个空的整数集 **S** ，它将保存子集的元素。
*   遍历排序后的数组，对于数组中的每个整数 **x** :
    *   如果 **x % k = 0** 或 **x / k** 尚未出现在 **S** 中，则将 **x** 插入 **S** 中。
    *   否则丢弃 **x** 并检查下一个元素。
*   最后打印套装 **S** 的尺寸。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the size of the required sub-set
int sizeSubSet(int a[], int k, int n)
{
    // Sort the array
    sort(a, a + n);

    // Set to store the contents of the required sub-set
    unordered_set<int> s;

    // Insert the elements satisfying the conditions
    for (int i = 0; i < n; i++) {
        if (a[i] % k != 0 || s.count(a[i] / k) == 0)
            s.insert(a[i]);
    }

    // Return the size of the set
    return s.size();
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 2;

    cout << sizeSubSet(a, k, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the size of the required sub-set
static int sizeSubSet(int a[], int k, int n)
{
    // Sort the array
    Arrays.sort(a);

    // HashMap to store the contents
    // of the required sub-set
    HashMap< Integer, Integer> s = new HashMap< Integer, Integer>();

    // Insert the elements satisfying the conditions
    for (int i = 0; i < n; i++)
    {
        if (a[i] % k != 0 || s.get(a[i] / k) == null)
            s.put(a[i], s.get(a[i]) == null ? 1 : s.get(a[i]) + 1);
    }

    // Return the size of the set
    return s.size();
}

// Driver code
public static void main(String args[])
{
    int a[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int n = a.length;
    int k = 2;
    System.out.println( sizeSubSet(a, k, n));
}
}
// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import math as mt
# Function to return the size of the required sub-set
def sizeSubSet(a, k, n):

    # Sort the array
    a.sort()

    # Set to store the contents of the required sub-set
    s=set()

    # Insert the elements satisfying the conditions
    for i in range(n):
        if (a[i] % k != 0 or a[i] // k not in s):
            s.add(a[i])

    # Return the size of the set
    return len(s)

# Driver code
a=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
n = len(a)
k = 2

print(sizeSubSet(a, k, n))

# This is contributed by Mohit kumar 29
```

## C#

```
// C# mplementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the size of
// the required sub-set
static int sizeSubSet(int []a, int k, int n)
{
    // Sort the array
    Array.Sort(a);

    // HashMap to store the contents
    // of the required sub-set
    Dictionary<int,
               int> s = new Dictionary<int,
                                       int>();

    // Insert the elements satisfying the conditions
    for (int i = 0; i < n; i++)
    {
        if (a[i] % k != 0 || !s.ContainsKey(a[i] / k))
        {
            if(s.ContainsKey(a[i]))
            {
                var val = s[a[i]];
                s.Remove(a[i]);
                s.Add(a[i], val + 1);
            }
            else
            {
                s.Add(a[i], 1);
            }
        }
    }

    // Return the size of the set
    return s.Count;
}

// Driver code
public static void Main(String []args)
{
    int []a = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int n = a.Length;
    int k = 2;
    Console.WriteLine(sizeSubSet(a, k, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to return the size of
// the required sub-set
function sizeSubSet($a, $k, $n)
{

    // Sort the array
    sort($a) ;

    // Set to store the contents of
    // the required sub-set
    $s = array();

    // Insert the elements satisfying
    // the conditions
    for ($i = 0 ; $i < $n ; $i++)
    {
        if ($a[$i] % $k != 0 or
            !in_array(floor($a[$i] / $k), $s))
            array_push($s, $a[$i]);
    }

    // Return the size of the set
    return sizeof($s);

}

// Driver code
$a = array(1, 2, 3, 4, 5, 6, 7, 8, 9, 10 );
$n = sizeof($a);
$k = 2;

echo sizeSubSet($a, $k, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the size of the
// required sub-set
function sizeSubSet(a, k, n)
{

    // Sort the array
    a.sort(function(a, b){return a - b;});

    // HashMap to store the contents
    // of the required sub-set
    let s = new Map();

    // Insert the elements satisfying the conditions
    for(let i = 0; i < n; i++)
    {
        if (a[i] % k != 0 ||
            s.get(a[i] / k) == null)
            s.set(a[i], s.get(a[i]) == null ?
                    1 : s.get(a[i]) + 1);
    }

    // Return the size of the set
    return s.size;
}

// Driver code
let a = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
let n = a.length;
let k = 2;

document.write(sizeSubSet(a, k, n));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
6
```