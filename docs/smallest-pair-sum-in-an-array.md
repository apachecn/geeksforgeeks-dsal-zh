# 数组中的最小对和

> 原文:[https://www . geesforgeks . org/最小对数组求和/](https://www.geeksforgeeks.org/smallest-pair-sum-in-an-array/)

给定一组不同的整数 **arr[]** ，任务是找到一对具有最小和的整数并打印和。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 3
> 该对(1，2)将具有最小和对，即 1 + 2 = 3
> **输入:** arr[] = {3，5，6，2}
> **输出:** 5

**进场:**

*   从数组中找到最小元素并存储在 **min** 中。
*   从数组中找到第二个最小元素，并将其存储在**秒分钟**中。
*   打印**分钟+秒分钟**。

以下是上述方法的实现:

## C++

```
// C++ program to print the sum of the minimum pair
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of
// the minimum pair from the array
int smallest_pair(int a[], int n)
{
    int min = INT_MAX, secondMin = INT_MAX;
    for (int j = 0; j < n; j++) {

        // If found new minimum
        if (a[j] < min) {

            // Minimum now becomes second minimum
            secondMin = min;

            // Update minimum
            min = a[j];
        }

        // If current element is > min and < secondMin
        else if ((a[j] < secondMin) && a[j] != min)

            // Update secondMin
            secondMin = a[j];
    }

    // Return the sum of the minimum pair
    return (secondMin + min);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << smallest_pair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the sum
// of the minimum pair
import java .io.*;

class GFG
{
// Function to return the sum of
// the minimum pair from the array
static int smallest_pair(int[] a, int n)
{
    int min =  Integer.MAX_VALUE, secondMin =  Integer.MAX_VALUE;
    for (int j = 0; j < n; j++)
    {

        // If found new minimum
        if (a[j] < min)
        {

            // Minimum now becomes second minimum
            secondMin = min;

            // Update minimum
            min = a[j];
        }

        // If current element is > min and < secondMin
        else if ((a[j] < secondMin) && a[j] != min)

            // Update secondMin
            secondMin = a[j];
    }

    // Return the sum of the minimum pair
    return (secondMin + min);
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3 };
    int n = arr.length;

    System.out.println(smallest_pair(arr, n));
}
}

// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python3 program to print the
# sum of the minimum pair
import sys

# Function to return the sum of
# the minimum pair from the array
def smallest_pair(a, n) :

    min = sys.maxsize
    secondMin = sys.maxsize

    for j in range(n) :

        # If found new minimum
        if (a[j] < min) :

            # Minimum now becomes
            # second minimum
            secondMin = min

            # Update minimum
            min = a[j]

        # If current element is > min
        # and < secondMin
        elif ((a[j] < secondMin) and
               a[j] != min) :

            # Update secondMin
            secondMin = a[j]

    # Return the sum of the minimum pair
    return (secondMin + min)

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3 ]
    n = len(arr)

    print(smallest_pair(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to print the sum
// of the minimum pair
using System;

class GFG
{
// Function to return the sum of
// the minimum pair from the array
static int smallest_pair(int[] a, int n)
{
    int min = int.MaxValue, secondMin = int.MaxValue;
    for (int j = 0; j < n; j++)
    {

        // If found new minimum
        if (a[j] < min)
        {

            // Minimum now becomes second minimum
            secondMin = min;

            // Update minimum
            min = a[j];
        }

        // If current element is > min and < secondMin
        else if ((a[j] < secondMin) && a[j] != min)

            // Update secondMin
            secondMin = a[j];
    }

    // Return the sum of the minimum pair
    return (secondMin + min);
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 3 };
    int n = arr.Length;

    Console.Write(smallest_pair(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the sum
// of the minimum pair

// Function to return the sum of
// the minimum pair from the array
function smallest_pair($a, $n)
{
    $min = PHP_INT_MAX;
    $secondMin = PHP_INT_MAX;
    for ($j = 0; $j < $n; $j++)
    {

        // If found new minimum
        if ($a[$j] < $min)
        {

            // Minimum now becomes
            // second minimum
            $secondMin = $min;

            // Update minimum
            $min = $a[$j];
        }

        // If current element is > min
        // and < secondMin
        else if (($a[$j] < $secondMin) &&
                  $a[$j] != $min)

            // Update secondMin
            $secondMin = $a[$j];
    }

    // Return the sum of the minimum pair
    return ($secondMin + $min);
}

// Driver code
$arr = array( 1, 2, 3 );
$n = sizeof($arr);
echo smallest_pair($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to print the sum
    // of the minimum pair

    // Function to return the sum of
    // the minimum pair from the array
    function smallest_pair(a, n)
    {
        let min = Number.MAX_VALUE,
        secondMin = Number.MAX_VALUE;
        for (let j = 0; j < n; j++)
        {

            // If found new minimum
            if (a[j] < min)
            {

                // Minimum now becomes second minimum
                secondMin = min;

                // Update minimum
                min = a[j];
            }

            // If current element is > min
            // and < secondMin
            else if ((a[j] < secondMin) &&
                      a[j] != min)

                // Update secondMin
                secondMin = a[j];
        }

        // Return the sum of the minimum pair
        return (secondMin + min);
    }

    let arr = [ 1, 2, 3 ];
    let n = arr.length;

    document.write(smallest_pair(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** ON)
**辅助空间:** O(1)