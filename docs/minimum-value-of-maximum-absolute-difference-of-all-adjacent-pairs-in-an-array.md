# 一个数组中所有相邻对的最大绝对差的最小值

> 原文:[https://www . geesforgeks . org/数组中所有相邻对的最大绝对差值最小值/](https://www.geeksforgeeks.org/minimum-value-of-maximum-absolute-difference-of-all-adjacent-pairs-in-an-array/)

给定一个数组 **arr** ，包含非负整数和大小为 **N** 的(-1)s，任务是用一个公共的非负整数替换那些 **(-1)s** ，使得所有相邻对的最大绝对差最小。打印最大绝对差值的最小可能值。

**示例:**

> **输入:** arr = {-1，-1，11，-1，3，-1}
> 输出: 4
> 用 7 替换每-1 个元素。现在所有相邻对的最大绝对差最小，等于 4
> 
> **输入:** arr = {4，-1 }
> T3】输出: 0

**进场:**

1.  只考虑那些与至少一个缺失元素相邻的非缺失元素。
2.  找出其中的最大元素和最小元素。
3.  我们需要找到一个值，使公共值和这些值之间的最大绝对差最小化。
4.  最佳值等于

```
(minimum element + maximum element) / 2
```

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum value
// of maximum absolute difference of
// all adjacent pairs in an Array
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum possible
// value of the maximum absolute difference.
int maximumAbsolute(int arr[], int n)
{
    // To store minimum and maximum elements
    int mn = INT_MAX;
    int mx = INT_MIN;

    for (int i = 0; i < n; i++) {
        // If right side element is equals -1
        // and left side is not equals -1
        if (i > 0
            && arr[i] == -1
            && arr[i - 1] != -1) {
            mn = min(mn, arr[i - 1]);
            mx = max(mx, arr[i - 1]);
        }

        // If left side element is equals -1
        // and right side is not equals -1
        if (i < n - 1
            && arr[i] == -1
            && arr[i + 1] != -1) {
            mn = min(mn, arr[i + 1]);
            mx = max(mx, arr[i + 1]);
        }
    }

    // Calculating the common integer
    // which needs to be replaced with
    int common_integer = (mn + mx) / 2;

    // Replace all -1 elements
    // with the common integer
    for (int i = 0; i < n; i++) {
        if (arr[i] == -1)
            arr[i] = common_integer;
    }

    int max_diff = 0;

    // Calculating the maximum
    // absolute difference
    for (int i = 0; i < n - 1; i++) {
        int diff = abs(arr[i] - arr[i + 1]);

        if (diff > max_diff)
            max_diff = diff;
    }

    // Return the maximum absolute difference
    return max_diff;
}

// Driver Code
int main()
{
    int arr[] = { -1, -1, 11, -1, 3, -1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << maximumAbsolute(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum value
// of maximum absolute difference of
// all adjacent pairs in an Array
import java.util.*;

class GFG{

// Function to find the minimum possible
// value of the maximum absolute difference.
static int maximumAbsolute(int arr[], int n)
{
    // To store minimum and maximum elements
    int mn = Integer.MAX_VALUE;
    int mx = Integer.MIN_VALUE;

    for (int i = 0; i < n; i++) {

        // If right side element is equals -1
        // and left side is not equals -1
        if (i > 0
            && arr[i] == -1
            && arr[i - 1] != -1) {
            mn = Math.min(mn, arr[i - 1]);
            mx = Math.max(mx, arr[i - 1]);
        }

        // If left side element is equals -1
        // and right side is not equals -1
        if (i < n - 1
            && arr[i] == -1
            && arr[i + 1] != -1) {
            mn = Math.min(mn, arr[i + 1]);
            mx = Math.max(mx, arr[i + 1]);
        }
    }

    // Calculating the common integer
    // which needs to be replaced with
    int common_integer = (mn + mx) / 2;

    // Replace all -1 elements
    // with the common integer
    for (int i = 0; i < n; i++) {
        if (arr[i] == -1)
            arr[i] = common_integer;
    }

    int max_diff = 0;

    // Calculating the maximum
    // absolute difference
    for (int i = 0; i < n - 1; i++) {
        int diff = Math.abs(arr[i] - arr[i + 1]);

        if (diff > max_diff)
            max_diff = diff;
    }

    // Return the maximum absolute difference
    return max_diff;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { -1, -1, 11, -1, 3, -1 };
    int n = arr.length;

    // Function call
    System.out.print(maximumAbsolute(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the minimum value
# of maximum absolute difference of
# all adjacent pairs in an Array

# Function to find the minimum possible
# value of the maximum absolute difference.
def maximumAbsolute(arr, n):

    # To store minimum and maximum elements
    mn = 10**9
    mx = -10**9

    for i in range(n):

        # If right side element is equals -1
        # and left side is not equals -1
        if (i > 0
            and arr[i] == -1
            and arr[i - 1] != -1):
            mn = min(mn, arr[i - 1])
            mx = max(mx, arr[i - 1])

        # If left side element is equals -1
        # and right side is not equals -1
        if (i < n - 1
            and arr[i] == -1
            and arr[i + 1] != -1):
            mn = min(mn, arr[i + 1])
            mx = max(mx, arr[i + 1])

    # Calculating the common integer
    # which needs to be replaced with
    common_integer = (mn + mx) // 2

    # Replace all -1 elements
    # with the common integer
    for i in range(n):
        if (arr[i] == -1):
            arr[i] = common_integer

    max_diff = 0

    # Calculating the maximum
    # absolute difference
    for i in range(n-1):
        diff = abs(arr[i] - arr[i + 1])

        if (diff > max_diff):
            max_diff = diff

    # Return the maximum absolute difference
    return max_diff

# Driver Code
if __name__ == '__main__':
    arr=[-1, -1, 11, -1, 3, -1]
    n = len(arr)

    # Function call
    print(maximumAbsolute(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the minimum value
// of maximum absolute difference of
// all adjacent pairs in an Array
using System;

class GFG{

    // Function to find the minimum possible
    // value of the maximum absolute difference.
    static int maximumAbsolute(int []arr, int n)
    {
        // To store minimum and maximum elements
        int mn = int.MaxValue;
        int mx = int.MinValue;

        for (int i = 0; i < n; i++) {

            // If right side element is equals -1
            // and left side is not equals -1
            if (i > 0
                && arr[i] == -1
                && arr[i - 1] != -1) {
                mn = Math.Min(mn, arr[i - 1]);
                mx = Math.Max(mx, arr[i - 1]);
            }

            // If left side element is equals -1
            // and right side is not equals -1
            if (i < n - 1
                && arr[i] == -1
                && arr[i + 1] != -1) {
                mn = Math.Min(mn, arr[i + 1]);
                mx = Math.Max(mx, arr[i + 1]);
            }
        }

        // Calculating the common integer
        // which needs to be replaced with
        int common_integer = (mn + mx) / 2;

        // Replace all -1 elements
        // with the common integer
        for (int i = 0; i < n; i++) {
            if (arr[i] == -1)
                arr[i] = common_integer;
        }

        int max_diff = 0;

        // Calculating the maximum
        // absolute difference
        for (int i = 0; i < n - 1; i++) {
            int diff = Math.Abs(arr[i] - arr[i + 1]);

            if (diff > max_diff)
                max_diff = diff;
        }

        // Return the maximum absolute difference
        return max_diff;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int []arr = { -1, -1, 11, -1, 3, -1 };
        int n = arr.Length;

        // Function call
        Console.Write(maximumAbsolute(arr, n));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript program to find the minimum value
// of maximum absolute difference of
// all adjacent pairs in an Array

// Function to find the minimum possible
// value of the maximum absolute difference.
function maximumAbsolute(arr, n)
{

    // To store minimum and maximum elements
    var mn = Number.MAX_VALUE;
    var mx = Number.MIN_VALUE;

    for(i = 0; i < n; i++)
    {

        // If right side element is equals -1
        // and left side is not equals -1
        if (i > 0 && arr[i] == -1 &&
                     arr[i - 1] != -1)
        {
            mn = Math.min(mn, arr[i - 1]);
            mx = Math.max(mx, arr[i - 1]);
        }

        // If left side element is equals -1
        // and right side is not equals -1
        if (i < n - 1 && arr[i] == -1 &&
                         arr[i + 1] != -1)
        {
            mn = Math.min(mn, arr[i + 1]);
            mx = Math.max(mx, arr[i + 1]);
        }
    }

    // Calculating the common integer
    // which needs to be replaced with
    var common_integer = (mn + mx) / 2;

    // Replace all -1 elements
    // with the common integer
    for(i = 0; i < n; i++)
    {
        if (arr[i] == -1)
            arr[i] = common_integer;
    }

    var max_diff = 0;

    // Calculating the maximum
    // absolute difference
    for(i = 0; i < n - 1; i++)
    {
        var diff = Math.abs(arr[i] - arr[i + 1]);

        if (diff > max_diff)
            max_diff = diff;
    }

    // Return the maximum absolute difference
    return max_diff;
}

// Driver Code
var arr = [ -1, -1, 11, -1, 3, -1 ];
var n = arr.length;

// Function call
document.write(maximumAbsolute(arr, n));

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*

***辅助空间:**O(1)*T4】