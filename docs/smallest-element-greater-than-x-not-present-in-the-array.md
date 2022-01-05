# 数组中不存在大于 X 的最小元素

> 原文:[https://www . geesforgeks . org/最小元素大于 x 不在数组中/](https://www.geeksforgeeks.org/smallest-element-greater-than-x-not-present-in-the-array/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **X** 。任务是找到数组中不存在的大于 **X** 的最小元素。
**举例:**

> **输入:** arr[] = {1，5，10，4，7}，X = 4
> **输出:** 6
> 6 是数组中不存在的大于 4
> 的最小数。
> **输入:** arr[] = {1，5，10，6，11}，X = 10
> **输出:** 12

**方法:**高效的解决方案基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。首先对数组进行排序。将**低电平**设为**零点**，高电平为**N–1**。并搜索元素 **X + 1。**如果**中间**的元素(即**(低+高)/** 2)小于或等于搜索元素，则使**低**为**中间+ 1** 。否则，将**高**设为**中-1**。如果中间的元素等于搜索元素，那么将搜索元素增加 1，使**变高**为**N–1**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest element greater
// than x which is not present in a[]
int Next_greater(int a[], int n, int x)
{

    // Sort the array
    sort(a, a + n);

    int low = 0, high = n - 1, ans = x + 1;

    // Continue until low is less
    // than or equals to high
    while (low <= high) {

        // Find mid
        int mid = (low + high) / 2;

        // If element at mid is less than
        // or equals to searching element
        if (a[mid] <= ans) {

            // If mid is equals
            // to searching element
            if (a[mid] == ans) {

                // Increment searching element
                ans++;

                // Make high as N - 1
                high = n - 1;
            }

            // Make low as mid + 1
            low = mid + 1;
        }

        // Make high as mid - 1
        else
            high = mid - 1;
    }

    // Return the next greater element
    return ans;
}

// Driver code
int main()
{
    int a[] = { 1, 5, 10, 4, 7 }, x = 4;
    int n = sizeof(a) / sizeof(a[0]);

    cout << Next_greater(a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the smallest element greater
// than x which is not present in a[]
static int Next_greater(int a[], int n, int x)
{

    // Sort the array
    Arrays.sort(a);

    int low = 0, high = n - 1, ans = x + 1;

    // Continue until low is less
    // than or equals to high
    while (low <= high)
    {

        // Find mid
        int mid = (low + high) / 2;

        // If element at mid is less than
        // or equals to searching element
        if (a[mid] <= ans)
        {

            // If mid is equals
            // to searching element
            if (a[mid] == ans)
            {

                // Increment searching element
                ans++;

                // Make high as N - 1
                high = n - 1;
            }

            // Make low as mid + 1
            low = mid + 1;
        }

        // Make high as mid - 1
        else
            high = mid - 1;
    }

    // Return the next greater element
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 5, 10, 4, 7 }, x = 4;
    int n = a.length;

    System.out.println(Next_greater(a, n, x));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the smallest element
# greater than x which is not present in a[]
def Next_greater(a, n, x):

    # Sort the array
    a = sorted(a)

    low, high, ans = 0, n - 1, x + 1

    # Continue until low is less
    # than or equals to high
    while (low <= high):

        # Find mid
        mid = (low + high) // 2

        # If element at mid is less than
        # or equals to searching element
        if (a[mid] <= ans):

            # If mid is equals
            # to searching element
            if (a[mid] == ans):

                # Increment searching element
                ans += 1

                # Make high as N - 1
                high = n - 1

            # Make low as mid + 1
            low = mid + 1

        # Make high as mid - 1
        else:
            high = mid - 1

    # Return the next greater element
    return ans

# Driver code
a = [1, 5, 10, 4, 7]
x = 4
n = len(a)

print(Next_greater(a, n, x))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the smallest element greater
// than x which is not present in a[]
static int Next_greater(int []a, int n, int x)
{

    // Sort the array
    Array.Sort(a);

    int low = 0, high = n - 1, ans = x + 1;

    // Continue until low is less
    // than or equals to high
    while (low <= high)
    {

        // Find mid
        int mid = (low + high) / 2;

        // If element at mid is less than
        // or equals to searching element
        if (a[mid] <= ans)
        {

            // If mid is equals
            // to searching element
            if (a[mid] == ans)
            {

                // Increment searching element
                ans++;

                // Make high as N - 1
                high = n - 1;
            }

            // Make low as mid + 1
            low = mid + 1;
        }

        // Make high as mid - 1
        else
            high = mid - 1;
    }

    // Return the next greater element
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 5, 10, 4, 7 };
    int x = 4;
    int n = a.Length;

    Console.WriteLine(Next_greater(a, n, x));
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the smallest element greater
// than x which is not present in a[]
function Next_greater($a, $n, $x)
{

    // Sort the array
    sort($a);

    $low = 0;
    $high = $n - 1;
    $ans = $x + 1;

    // Continue until low is less
    // than or equals to high
    while ($low <= $high)
    {

        // Find mid
        $mid = ($low + $high) / 2;

        // If element at mid is less than
        // or equals to searching element
        if ($a[$mid] <= $ans)
        {

            // If mid is equals
            // to searching element
            if ($a[$mid] == $ans)
            {

                // Increment searching element
                $ans++;

                // Make high as N - 1
                $high = $n - 1;
            }

            // Make low as mid + 1
            $low = $mid + 1;
        }

        // Make high as mid - 1
        else
            $high = $mid - 1;
    }

    // Return the next greater element
    return $ans;
}

// Driver code
$a = array( 1, 5, 10, 4, 7 );
$x = 4;
$n = count($a);

echo Next_greater($a, $n, $x);

// This code is contributed by Naman_garg.
?>
```

## java 描述语言

```
<script>

// Js implementation of the approach

// Function to return the smallest element greater
// than x which is not present in a[]
function Next_greater( a, n, x){
    // Sort the array
    a.sort(function(aa, bb){return aa - bb});

    let low = 0, high = n - 1, ans = x + 1;

    // Continue until low is less
    // than or equals to high
    while (low <= high) {

        // Find mid
        let mid = Math.floor((low + high) / 2);

        // If element at mid is less than
        // or equals to searching element
        if (a[mid] <= ans) {

            // If mid is equals
            // to searching element
            if (a[mid] == ans) {

                // Increment searching element
                ans++;

                // Make high as N - 1
                high = n - 1;
            }

            // Make low as mid + 1
            low = mid + 1;
        }

        // Make high as mid - 1
        else
            high = mid - 1;
    }

    // Return the next greater element
    return ans;
}

// Driver code
let a = [ 1, 5, 10, 4, 7 ]
let x = 4;
let n = a.length;

document.write( Next_greater(a, n, x));
</script>
```

**Output:** 

```
6
```