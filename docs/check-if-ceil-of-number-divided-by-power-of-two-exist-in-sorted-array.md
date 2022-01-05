# 检查排序后的数组中是否存在除以二次方的数字上限

> 原文:[https://www . geesforgeks . org/check-if-ceil-of-number-除以二的幂-exist-in-sorted-array/](https://www.geeksforgeeks.org/check-if-ceil-of-number-divided-by-power-of-two-exist-in-sorted-array/)

给定一个排序的数组 **arr[]** 和一个整数 **K** ，任务是检查数组中是否存在数字 **K** 除以 2 的某个幂的上限。
**注意:**如果没有这样的元素 print -1。
**示例:**

> **输入:** arr[] = {3，5，7，8，10}，K = 4
> **输出:** -1
> **说明:**
> 没有这样的元素。
> **输入:** arr[] = {1，2，3，5，7，8}，K = 4
> **输出:** 2
> **说明:**
> 当 4 除以 2 的幂 1 时，数组中存在一个元素。

**方法:**想法是尝试 2 的每一次幂，并检查是否存在从幂 0 开始的该数的上限。使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以检查数组中是否存在元素。
以下是上述办法的实施情况:

## C++14

```
// C++14 implementation to check
// if a number divided by power
// of two exist in the sorted array
#include <bits/stdc++.h>
using namespace std;

// Function to find there exist a
// number or not in the array
int findNumberDivByPowerofTwo(int ar[],
                              int k, int n)
{
    int found = -1, m = k;

    // Loop to check if there exist
    // a number by divided by power of 2
    while (m > 0)
    {
        int l = 0;
        int r = n - 1;

        // Binary Search
        while (l <= r)
        {
            int mid = (l + r) / 2;

            if (ar[mid] == m)
            {
                found = m;
                break;
            }
            else if (ar[mid] > m)
            {
                r = mid - 1;
            }
            else if (ar[mid] < m)
            {
                l = mid + 1;
            }
        }

        // Condition to check the number
        // is found in the array or not
        if (found != -1)
        {
            break;
        }

        // Otherwise divide the number
        // by increasing the one more
        // power of 2
        m = m / 2;
    }
    return found;
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 7, 8, 10 };
    int k = 4, n = 5;

    cout << findNumberDivByPowerofTwo(arr, k, n);
}

// This code is contributed by code_hunt
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if a number divided by power
// of two exist in the sorted array

import java.util.Scanner;

public class GreeksForGreeksQuestions {

    // Function to find there exist a
    // number or not in the array
    static int findNumberDivByPowerofTwo(
        int[] ar, int k, int n)
    {
        int found = -1, m = k;

        // Loop to check if there exist
        // a number by divided by power of 2
        while (m > 0) {
            int l = 0;
            int r = n - 1;

            // Binary Search
            while (l <= r) {
                int mid = (l + r) / 2;

                if (ar[mid] == m) {
                    found = m;
                    break;
                }
                else if (ar[mid] > m) {
                    r = mid - 1;
                }
                else if (ar[mid] < m) {
                    l = mid + 1;
                }
            }

            // Condition to check the number
            // is found in the array or not
            if (found != -1) {
                break;
            }

            // Otherwise divide the number
            // by increasing the one more
            // power of 2
            m = m / 2;
        }

        return found;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 5, 7, 8, 10 };
        int k = 4, n = 5;

        System.out.println(
            findNumberDivByPowerofTwo(
                arr, k, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a number divided by power
# of two exist in the sorted array

# Function to find there exist a
# number or not in the array
def findNumberDivByPowerofTwo(ar, k, n):

    found = -1
    m = k

    # Loop to check if there exist
    # a number by divided by power of 2
    while (m > 0):
        l = 0
        r = n - 1

        # Binary Search
        while (l <= r):
            mid = (l + r) // 2

            if (ar[mid] == m):
                found = m
                break

            elif (ar[mid] > m):
                r = mid - 1

            elif (ar[mid] < m):
                l = mid + 1

        # Condition to check the number
        # is found in the array or not
        if (found != -1):
            break

        # Otherwise divide the number
        # by increasing the one more
        # power of 2
        m = m // 2

    return found

# Driver Code
arr = [ 3, 5, 7, 8, 10 ]
k = 4
n = 5

print(findNumberDivByPowerofTwo(arr, k, n))

# This code is contributed by code_hunt
```

## C#

```
// C# implementation to check
// if a number divided by power
// of two exist in the sorted array
using System;

class GFG{

// Function to find there exist a
// number or not in the array
static int findNumberDivByPowerofTwo(int[] ar, int k,
                                     int n)
{
    int found = -1, m = k;

    // Loop to check if there exist
    // a number by divided by power of 2
    while (m > 0)
    {
        int l = 0;
        int r = n - 1;

        // Binary Search
        while (l <= r)
        {
            int mid = (l + r) / 2;

            if (ar[mid] == m)
            {
                found = m;
                break;
            }
            else if (ar[mid] > m)
            {
                r = mid - 1;
            }
            else if (ar[mid] < m)
            {
                l = mid + 1;
            }
        }

        // Condition to check the number
        // is found in the array or not
        if (found != -1)
        {
            break;
        }

        // Otherwise divide the number
        // by increasing the one more
        // power of 2
        m = m / 2;
    }
    return found;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 5, 7, 8, 10 };
    int k = 4, n = 5;

    Console.WriteLine(findNumberDivByPowerofTwo(
                      arr, k, n));
}
}

// This code is contributed by princi singh
```

## java 描述语言

```
<script>
// javascript implementation to check
// if a number divided by power
// of two exist in the sorted array

    // Function to find there exist a
    // number or not in the array
    function findNumberDivByPowerofTwo(ar , k , n) {
        var found = -1, m = k;

        // Loop to check if there exist
        // a number by divided by power of 2
        while (m > 0) {
            var l = 0;
            var r = n - 1;

            // Binary Search
            while (l <= r) {
                var mid = parseInt((l + r) / 2);

                if (ar[mid] == m) {
                    found = m;
                    break;
                } else if (ar[mid] > m) {
                    r = mid - 1;
                } else if (ar[mid] < m) {
                    l = mid + 1;
                }
            }

            // Condition to check the number
            // is found in the array or not
            if (found != -1) {
                break;
            }

            // Otherwise divide the number
            // by increasing the one more
            // power of 2
            m = parseInt(m / 2);
        }

        return found;
    }

    // Driver Code

        var arr = [ 3, 5, 7, 8, 10 ];
        var k = 4, n = 5;

        document.write(findNumberDivByPowerofTwo(arr, k, n));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
-1
```