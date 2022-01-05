# 所有元素都大于 K 的最小子阵列

> 原文:[https://www . geeksforgeeks . org/minist-subarray-so-all-elements-大于-k/](https://www.geeksforgeeks.org/smallest-subarray-such-that-all-elements-are-greater-than-k/)

给定一个由 N 个整数和 K 个数字组成的数组，任务是找到所有元素都大于 K 的最小子数组的长度。如果没有这样的子数组，那么打印-1。
**例:**

> **输入** : a[] = {3，4，5，6，7，2，10，11}，K = 5
> **输出** : 1
> 子阵为{10}
> **输入** : a[] = {1，2，3}，K = 13
> **输出** : -1

**方法:**任务是找到所有元素都大于 k 的最小子阵列，因为最小子阵列的大小可以是 1。因此，只需检查数组中是否有大于 k 的元素。如果有，则打印“1”，否则打印“-1”。
以下是上述办法的实施情况:

## C++

```
// C++ program to print the length of the shortest
// subarray with all elements greater than X
#include <bits/stdc++.h>
using namespace std;

// Function to return shortest array
int smallestSubarray(int a[], int n, int x)
{
    int count = 0, length = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            return 1;
        }
    }

    return -1;
}

// Driver Code
int main()
{
    int a[] = { 1, 22, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 13;

    cout << smallestSubarray(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java program to print the length of the shortest
// subarray with all elements greater than X

import java.io.*;

class GFG {

// Function to return shortest array
static int smallestSubarray(int a[], int n, int x)
{
    int count = 0, length = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            return 1;
        }
    }

    return -1;
}

// Driver Code
    public static void main (String[] args) {
    int a[] = { 1, 22, 3 };
    int n = a.length;
    int k = 13;

    System.out.println(smallestSubarray(a, n, k));
            }
}
// This code has been contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to print the
# length of the shortest subarray
# with all elements greater than X

# Function to return shortest array
def smallestSubarray(a, n, k):

    # Iterate in the array
    for i in range(n):

        # check if array element
        # greater then X or not
        if a[i] > k:
            return 1
    return -1

# Driver Code
a = [1, 22, 3]
n = len(a)
k = 13
print(smallestSubarray(a, n, k))

# This code is contributed
# by Shrikant13
```

## C#

```
using System;

class GFG
{

// Function to return shortest array
static int smallestSubarray(int []a,
                            int n, int x)
{

    // Iterate in the array
    for (int i = 0; i < n; i++)
    {

        // check if array element
        // greater then X or not
        if (a[i] > x)
        {
            return 1;
        }
    }

    return -1;
}

// Driver Code
static public void Main ()
{
    int []a = { 1, 22, 3 };
    int n = a.Length;
    int k = 13;

    Console.WriteLine(smallestSubarray(a, n, k));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the length
// of the shortest subarray with
// all elements greater than X

// Function to return shortest array
function smallestSubarray($a, $n, $x)
{
    $count = 0;
    $length = 0;

    // Iterate in the array
    for ($i = 0; $i < $n; $i++)
    {

        // check if array element
        // greater then X or not
        if ($a[$i] > $x)
        {
            return 1;
        }
    }

    return -1;
}

// Driver Code
$a = array( 1, 22, 3 );
$n = sizeof($a);
$k = 13;

echo smallestSubarray($a, $n, $k);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// JavaScriptto print the length of the shortest
// subarray with all elements greater than X

// Function to return shortest array
function smallestSubarray(a, n, x)
{
    let count = 0, length = 0;

    // Iterate in the array
    for (let i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            return 1;
        }
    }

    return -1;
}

// Driver Code

    let a = [1, 22, 3 ]
    let n = a.length
    let k = 13;

    document.write(smallestSubarray(a, n, k));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
1
```

**时间复杂度**:O(N)
T3】辅助空间: O(1)