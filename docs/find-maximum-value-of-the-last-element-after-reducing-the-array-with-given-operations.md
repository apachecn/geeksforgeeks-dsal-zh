# 用给定的运算缩小数组后，求最后一个元素的最大值

> 原文:[https://www . geeksforgeeks . org/find-通过给定操作减少数组后的最后一个元素的最大值/](https://www.geeksforgeeks.org/find-maximum-value-of-the-last-element-after-reducing-the-array-with-given-operations/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，您必须对给定的数组执行以下操作，直到该数组简化为单个元素，

1.  选择两个指数 **i** 和 **j** ，这样 **i！= j** 。
2.  将 **arr[i]** 替换为**arr[I]–arr[j]**，并从阵列中移除 **arr[j]** 。

任务是最大化并打印数组最后剩余元素的值。
**例:**

> **输入:** arr[] = {20，3，-15，7}
> 输出: 45
> 第一步:我们可以去掉 7，用-22 替换-15。
> 第二步:我们可以去掉 3，用-25 替换-22。
> 第三步:我们可以去掉-25，用 45 替换 20。
> 所以 45 是我们能得到的最大值。
> **输入:** arr[] = {5，4，6，2}
> **输出:** 13

**进场:**为了最大化最后剩余元素的价值，有三种情况:

1.  **数组有负数也有正数:**首先我们将负数减去所有正数(除了一个)。在这之后，我们只会剩下一个正数和一个负数。现在，我们将从正数中减去负数，最后得到一个正数。因此，在这种情况下，结果是数组元素绝对值的总和。
2.  **数组只包含正数:**首先我们找到最小的数，然后从中减去除一个正数以外的所有正数。在这之后，我们只得到一个正数和一个负数，现在我们将从正数中减去负数，最后得到一个正数。这里我们可以观察到最小的
    数已经消失，并且该值基本上是从下一个更大的元素中切出来的，这与情况 1 不同。因此，在这种情况下，结果是数组元素绝对值的总和–2 *最小元素。
3.  **数组只包含负数:**首先我们找到最大的数，然后从中减去除一个负数以外的所有负数。在这之后，我们只得到一个负数和一个正数，现在我们将从正数中减去负数，最后得到一个正数。在这里，我们可以观察到最大的数字已经消失，并且该值基本上是从与情况 1 不同的下一个更大的元素中剪切出来的。因此在这种情况下，结果是数组元素的绝对值之和–最大元素的 2 *绝对值。这里我们把最大值作为负数情况下最大值和最小值的绝对值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized value
int find_maximum_value(int a[], int n)
{
    int sum = 0;
    int minimum = INT_MAX;
    int pos = 0, neg = 0;

    for (int i = 0; i < n; i++) {

        // Overall minimum absolute value
        // of some element from the array
        minimum = min(minimum, abs(a[i]));

        // Add all absolute values
        sum += abs(a[i]);

        // Count positive and negative elements
        if (a[i] >= 0)
            pos += 1;
        else
            neg += 1;
    }

    // Both positive and negative
    // values are present
    if (pos > 0 && neg > 0)
        return sum;

    // Only positive or negative
    // values are present
    return (sum - 2 * minimum);
}

// Driver code
int main()
{
    int a[] = { 5, 4, 6, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << find_maximum_value(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

    // Function to return the maximized value
    static int find_maximum_value(int a[], int n)
    {
        int sum = 0;
        int minimum = Integer.MAX_VALUE;
        int pos = 0, neg = 0;

        for (int i = 0; i < n; i++)
        {

            // Overall minimum absolute value
            // of some element from the array
            minimum = Math.min(minimum, Math.abs(a[i]));

            // Add all absolute values
            sum += Math.abs(a[i]);

            // Count positive and negative elements
            if (a[i] >= 0)
                pos += 1;
            else
                neg += 1;
        }

        // Both positive and negative
        // values are present
        if (pos > 0 && neg > 0)
            return sum;

        // Only positive or negative
        // values are present
        return (sum - 2 * minimum);
    }

    // Driver code
    public static void main (String[] args)
    {

        int []a = { 5, 4, 6, 2 };
        int n = a.length;

        System.out.println(find_maximum_value(a, n));
    }
}

// This code is contributed by ajit
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the maximized value
def find_maximum_value(a, n):

    sum = 0
    minimum = 10**9
    pos = 0
    neg = 0

    for i in range(n):

        # Overall minimum absolute value
        # of some element from the array
        minimum = min(minimum, abs(a[i]))

        # Add all absolute values
        sum += abs(a[i])

        # Count positive and negative elements
        if (a[i] >= 0):
            pos += 1
        else:
            neg += 1

    # Both positive and negative
    # values are present
    if (pos > 0 and neg > 0):
        return sum

    # Only positive or negative
    # values are present
    return (sum - 2 * minimum)

# Driver code

a= [5, 4, 6, 2]
n = len(a)

print(find_maximum_value(a, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximized value
    static int find_maximum_value(int []a, int n)
    {
        int sum = 0;
        int minimum = int.MaxValue;
        int pos = 0, neg = 0;

        for (int i = 0; i < n; i++)
        {

            // Overall minimum absolute value
            // of some element from the array
            minimum = Math.Min(minimum, Math.Abs(a[i]));

            // Add all absolute values
            sum += Math.Abs(a[i]);

            // Count positive and negative elements
            if (a[i] >= 0)
                pos += 1;
            else
                neg += 1;
        }

        // Both positive and negative
        // values are present
        if (pos > 0 && neg > 0)
            return sum;

        // Only positive or negative
        // values are present
        return (sum - 2 * minimum);
    }

    // Driver code
    static public void Main ()
    {
        int []a = { 5, 4, 6, 2 };
        int n = a.Length;

        Console.WriteLine(find_maximum_value(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the maximized value
    function find_maximum_value(a , n) {
        var sum = 0;
        var minimum = Number.MAX_VALUE;
        var pos = 0, neg = 0;

        for (i = 0; i < n; i++) {

            // Overall minimum absolute value
            // of some element from the array
            minimum = Math.min(minimum, Math.abs(a[i]));

            // Add all absolute values
            sum += Math.abs(a[i]);

            // Count positive and negative elements
            if (a[i] >= 0)
                pos += 1;
            else
                neg += 1;
        }

        // Both positive and negative
        // values are present
        if (pos > 0 && neg > 0)
            return sum;

        // Only positive or negative
        // values are present
        return (sum - 2 * minimum);
    }

    // Driver code
        var a = [ 5, 4, 6, 2 ];
        var n = a.length;

        document.write(find_maximum_value(a, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
13
```

**时间复杂度:** O(N)