# 根据给定条件

将数组拆分成等份

> 原文:[https://www . geeksforgeeks . org/根据给定条件将数组拆分成等份/](https://www.geeksforgeeks.org/split-the-array-into-equal-sum-parts-according-to-given-conditions/)

给定一个整数数组 **arr[]** ，任务是检查输入数组是否可以分成两个子数组，例如:

*   两个子阵列的总和相等。
*   所有能被 5 整除的元素都应该在同一个组中。
*   所有能被 3 整除(但不能被 5 整除)的元素都应该在另一组。
*   既不能被 5 整除也不能被 3 整除的元素可以归入任何一组。

如果可能，那么打印**是**否则打印**否**。
**例:**

> **输入:** arr[] = {1，2}
> **输出:**否
> 元素不能分组，这样总和就相等了。
> **输入:** arr[] = {1，4，3}
> **输出:**是
> {1，3}和{4}是满足给定条件的组。

**方法:**我们可以使用递归方法，通过保持左和和右和来维持两个不同的组。**左和**为**5 的倍数**、**右和**为**3 的倍数**(不是 5 的倍数)并且**既不能被 5 整除也不能被 3 整除的元素**可以位于满足等和法则的任意组中(将它们一一包含在左和右和中)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function that returns true if the array
// can be divided into two sub-arrays
// satisfying the given condition
bool helper(int* arr, int n, int start, int lsum, int rsum)
{

    // If reached the end
    if (start == n)
        return lsum == rsum;

    // If divisible by 5 then add to the left sum
    if (arr[start] % 5 == 0)
        lsum += arr[start];

    // If divisible by 3 but not by 5
    // then add to the right sum
    else if (arr[start] % 3 == 0)
        rsum += arr[start];

    // Else it can be added to any of the sub-arrays
    else

        // Try adding in both the sub-arrays (one by one)
        // and check whether the condition satisfies
        return helper(arr, n, start + 1, lsum + arr[start], rsum)
           || helper(arr, n, start + 1, lsum, rsum + arr[start]);

    // For cases when element is multiple of 3 or 5.
    return helper(arr, n, start + 1, lsum, rsum);
}

// Function to start the recursive calls
bool splitArray(int* arr, int n)
{
    // Initially start, lsum and rsum will all be 0
    return helper(arr, n, 0, 0, 0);
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (splitArray(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Solution
{

// Recursive function that returns true if the array
// can be divided into two sub-arrays
// satisfying the given condition
static boolean helper(int arr[], int n,
                    int start, int lsum, int rsum)
{

    // If reached the end
    if (start == n)
        return lsum == rsum;

    // If divisible by 5 then add to the left sum
    if (arr[start] % 5 == 0)
        lsum += arr[start];

    // If divisible by 3 but not by 5
    // then add to the right sum
    else if (arr[start] % 3 == 0)
        rsum += arr[start];

    // Else it can be added to any of the sub-arrays
    else

        // Try adding in both the sub-arrays (one by one)
        // and check whether the condition satisfies
        return helper(arr, n, start + 1, lsum + arr[start], rsum)
        || helper(arr, n, start + 1, lsum, rsum + arr[start]);

    // For cases when element is multiple of 3 or 5.
    return helper(arr, n, start + 1, lsum, rsum);
}

// Function to start the recursive calls
static boolean splitArray(int arr[], int n)
{
    // Initially start, lsum and rsum will all be 0
    return helper(arr, n, 0, 0, 0);
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 4, 3 };
    int n = arr.length;

    if (splitArray(arr, n))
        System.out.println( "Yes");
    else
        System.out.println( "No");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Recursive function that returns true if
# the array can be divided into two sub-arrays
# satisfying the given condition
def helper(arr, n, start, lsum, rsum):

    # If reached the end
    if (start == n):
        return lsum == rsum

    # If divisible by 5 then add
    # to the left sum
    if (arr[start] % 5 == 0):
        lsum += arr[start]

    # If divisible by 3 but not by 5
    # then add to the right sum
    elif (arr[start] % 3 == 0):
        rsum += arr[start]

    # Else it can be added to any of
    # the sub-arrays
    else:

        # Try adding in both the sub-arrays
        # (one by one) and check whether
        # the condition satisfies
        return (helper(arr, n, start + 1,
                lsum + arr[start], rsum) or
                helper(arr, n, start + 1,
                lsum, rsum + arr[start]));

    # For cases when element is multiple of 3 or 5.
    return helper(arr, n, start + 1, lsum, rsum)

# Function to start the recursive calls
def splitArray(arr, n):

    # Initially start, lsum and rsum
    # will all be 0
    return helper(arr, n, 0, 0, 0)

# Driver code
if __name__ == "__main__":

    arr = [ 1, 4, 3 ]
    n = len(arr)

    if (splitArray(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function that returns true if the array
    // can be divided into two sub-arrays
    // satisfying the given condition
    static bool helper(int []arr, int n,
                        int start, int lsum, int rsum)
    {

        // If reached the end
        if (start == n)
            return lsum == rsum;

        // If divisible by 5 then add to the left sum
        if (arr[start] % 5 == 0)
            lsum += arr[start];

        // If divisible by 3 but not by 5
        // then add to the right sum
        else if (arr[start] % 3 == 0)
            rsum += arr[start];

        // Else it can be added to any of the sub-arrays
        else

            // Try adding in both the sub-arrays (one by one)
            // and check whether the condition satisfies
            return helper(arr, n, start + 1, lsum + arr[start], rsum)
            || helper(arr, n, start + 1, lsum, rsum + arr[start]);

        // For cases when element is multiple of 3 or 5.
        return helper(arr, n, start + 1, lsum, rsum);
    }

    // Function to start the recursive calls
    static bool splitArray(int []arr, int n)
    {
        // Initially start, lsum and rsum will all be 0
        return helper(arr, n, 0, 0, 0);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 4, 3 };
        int n = arr.Length;

        if (splitArray(arr, n))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine( "No");
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Recursive function that returns true
// if the array can be divided into two
// sub-arrays satisfying the given condition
function helper(&$arr, $n, $start,
                    $lsum, $rsum)
{

    // If reached the end
    if ($start == $n)
        return $lsum == $rsum;

    // If divisible by 5 then
    // add to the left sum
    if ($arr[$start] % 5 == 0)
        $lsum += $arr[$start];

    // If divisible by 3 but not by 5
    // then add to the right sum
    else if ($arr[$start] % 3 == 0)
        $rsum += $arr[$start];

    // Else it can be added to any
    // of the sub-arrays
    else

        // Try adding in both the sub-arrays (one by one)
        // and check whether the condition satisfies
        return helper($arr, $n, $start + 1,
                      $lsum + $arr[$start], $rsum) ||
               helper($arr, $n, $start + 1,
                      $lsum, $rsum + $arr[$start]);

    // For cases when element is
    // multiple of 3 or 5.
    return helper($arr, $n, $start + 1,
                        $lsum, $rsum);
}

// Function to start the recursive calls
function splitArray($arr, $n)
{
    // Initially start, lsum and r
    // sum will all be 0
    return helper($arr, $n, 0, 0, 0);
}

// Driver code
$arr = array( 1, 4, 3 );
$n = count($arr);

if (splitArray($arr, $n))
    print("Yes");
else
    print("No");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

//js implementation of the approach

// Recursive function that returns true if the array
// can be divided into two sub-arrays
// satisfying the given condition
function helper( arr, n, start, lsum, rsum)
{
    // If reached the end
    if (start == n)
        return lsum == rsum;

    // If divisible by 5 then add to the left sum
    if (arr[start] % 5 == 0)
        lsum += arr[start];

    // If divisible by 3 but not by 5
    // then add to the right sum
    else if (arr[start] % 3 == 0)
        rsum += arr[start];

    // Else it can be added to any of the sub-arrays
    else

        // Try adding in both the sub-arrays (one by one)
        // and check whether the condition satisfies
        return helper(arr, n, start + 1, lsum + arr[start], rsum)
           || helper(arr, n, start + 1, lsum, rsum + arr[start]);

    // For cases when element is multiple of 3 or 5.
    return helper(arr, n, start + 1, lsum, rsum);
}

// Function to start the recursive calls
function splitArray(arr, n)
{
    // Initially start, lsum and rsum will all be 0
    return helper(arr, n, 0, 0, 0);
}

// Driver code
let arr = [1, 4, 3 ];
let n =arr.length;
if (splitArray(arr, n))
    document.write( "Yes");
else
     document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**o(2 ^ n)
T3】辅助空间: O(N)