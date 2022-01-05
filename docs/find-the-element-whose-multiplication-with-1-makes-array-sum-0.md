# 找到与-1 相乘使数组和为 0 的元素

> 原文:[https://www . geeksforgeeks . org/find-the-element-what-乘-1-make-array-sum-0/](https://www.geeksforgeeks.org/find-the-element-whose-multiplication-with-1-makes-array-sum-0/)

给定一个 N 个整数的数组。任务是找到元素的最小索引，这样当乘以-1 时，整个数组的和变成 0。如果没有这样的索引返回-1。
**例:**

```
Input : arr[] = {1, 3, -5, 3, 4}
Output : 2

Input : arr[] = {5, 3, 6, -7, -4}
Output : -1
```

**天真方法:**
简单的解决方法是取每个元素，乘以-1，检查新的和是否为 0。该算法在 **O(N <sup>2</sup> )** 中工作。
**有效方法:**
如果我们将 S 作为数组的初始和，并将当前元素 A <sub>i</sub> 乘以-1，那么新的和将变成 S–2 * A<sub>I</sub>，这应该等于 0。因此，当第一次 **S = 2*A <sub>i</sub>** 时，当前索引是我们必需的，如果没有元素满足条件，那么我们的答案将是-1。该算法的时间复杂度为 **O(N)** 。
以下是上述想法的实现:

## C++

```
// C++ program to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1
int minIndex(int arr[], int n)
{
    // Find array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Find element with value equal to sum/2
    for (int i = 0; i < n; i++) {

        // when sum is equal to 2*element
        // then this is our required element
        if (2 * arr[i] == sum)
            return (i + 1);
    }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, -5, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minIndex(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1

import java.io.*;

class GFG {

// Function to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1
 static int minIndex(int arr[], int n)
{
    // Find array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Find element with value equal to sum/2
    for (int i = 0; i < n; i++) {

        // when sum is equal to 2*element
        // then this is our required element
        if (2 * arr[i] == sum)
            return (i + 1);
    }

    return -1;
}

// Driver code

    public static void main (String[] args) {
            int []arr = { 1, 3, -5, 3, 4 };
    int n =arr.length;
    System.out.print( minIndex(arr, n));
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find minimum index
# such that sum becomes 0 when the
# element is multiplied by -1

# Function to find minimum index
# such that sum becomes 0 when the
# element is multiplied by -1
def minIndex(arr, n):

    # Find array sum
    sum = 0
    for i in range (0, n):
        sum += arr[i]

    # Find element with value
    # equal to sum/2
    for i in range(0, n):

        # when sum is equal to 2*element
        # then this is our required element
        if (2 * arr[i] == sum):
            return (i + 1)

    return -1

# Driver code
arr = [ 1, 3, -5, 3, 4 ];
n = len(arr);
print(minIndex(arr, n))

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1

using System;

class GFG {

// Function to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1
 static int minIndex(int[] arr, int n)
{
    // Find array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Find element with value equal to sum/2
    for (int i = 0; i < n; i++) {

        // when sum is equal to 2*element
        // then this is our required element
        if (2 * arr[i] == sum)
            return (i + 1);
    }

    return -1;
}

// Driver code

    public static void Main () {
            int[] arr = { 1, 3, -5, 3, 4 };
    int n =arr.Length;
    Console.Write( minIndex(arr, n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1

// Function to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1
function minIndex(&$arr, $n)
{
    // Find array sum
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // Find element with value equal to sum/2
    for ($i = 0; $i < $n; $i++)
    {

        // when sum is equal to 2*element
        // then this is our required element
        if (2 * $arr[$i] == $sum)
            return ($i + 1);
    }
    return -1;
}

// Driver code
$arr = array(1, 3, -5, 3, 4 );
$n = sizeof($arr);
echo (minIndex($arr, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1   

// Function to find minimum index
// such that sum becomes 0 when the
// element is multiplied by -1
    function minIndex(arr , n)
    {
        // Find array sum
        var sum = 0;
        for (i = 0; i < n; i++)
            sum += arr[i];

        // Find element with value equal to sum/2
        for (i = 0; i < n; i++) {

            // when sum is equal to 2*element
            // then this is our required element
            if (2 * arr[i] == sum)
                return (i + 1);
        }

        return -1;
    }

    // Driver code

        var arr = [ 1, 3, -5, 3, 4 ];
        var n = arr.length;
        document.write(minIndex(arr, n));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```