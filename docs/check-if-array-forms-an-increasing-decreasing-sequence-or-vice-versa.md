# 检查数组是否形成递增-递减序列，反之亦然

> 原文:[https://www . geeksforgeeks . org/check-if-array-forms-递增-递减-序列-反之亦然/](https://www.geeksforgeeks.org/check-if-array-forms-an-increasing-decreasing-sequence-or-vice-versa/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出该数组是否可以分成 2 个子数组，使得第一个子数组严格递增，第二个子数组严格递减，反之亦然。如果给定的数组可以分割，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:** arr[] = {3，1，-2，-2，-1，3}
> **输出:**是
> **说明:**
> 严格递减的第一子阵{3，1，-2}，严格递增的第二子阵是{-2，1，3}。
> 
> **输入:** arr[] = {1，1，2，3，4，5}
> **输出:**否
> **说明:**
> 全阵在增加。

**天真方法:**天真的想法是在每一个可能的索引处将阵列分成两个子阵列，并明确检查第一个[子阵列是否严格增加](https://www.geeksforgeeks.org/longest-increasing-subarray/)，第二个子阵列是否严格减少，反之亦然。如果我们能打破任何一个子阵列，那么打印**“是”**否则打印**“否”**。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，遍历数组并检查严格递增的序列，然后检查严格递减的子序列，反之亦然。以下是步骤:

1.  如果 arr[1] > arr[0]，则检查严格递增然后严格递减，如下所示:
    *   检查每一个连续的对，直到在任何索引 i arr[i + 1]小于 arr[i]。
    *   现在从索引 i + 1 开始，检查每个连续的对，检查 arr[i + 1]是否小于 arr[i],直到数组结束。如果在任何索引 I 处， **arr[i]小于 arr[i + 1]** ，则中断循环。
    *   如果我们在上述步骤中到达终点，则打印**“是”**否则打印**“否”**。
2.  如果 arr[1] < arr[0]，则检查严格递减然后严格递增，如下所示:
    *   检查每一个连续的对，直到在任何索引 i arr[i + 1]大于 arr[i]。
    *   现在从索引 i + 1 开始，检查每个连续的对，检查 arr[i + 1]是否大于 arr[i],直到数组结束。如果在任何索引 I 处， **arr[i]大于 arr[i + 1]** ，则中断循环。
    *   如果我们在上述步骤中到达终点，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given array
// forms an increasing decreasing
// sequence or vice versa
bool canMake(int n, int ar[])
{
    // Base Case
    if (n == 1)
        return true;
    else {

        // First subarray is
        // stricly increasing
        if (ar[0] < ar[1]) {

            int i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n
                   && ar[i - 1] < ar[i]) {
                i++;
            }

            // Check for strictly
            // decreasing condition
            // & find the break point
            while (i + 1 < n
                   && ar[i] > ar[i + 1]) {
                i++;
            }

            // If i is equal to
            // length of array
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // First subarray is
        // strictly Decreasing
        else if (ar[0] > ar[1]) {
            int i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n
                   && ar[i - 1] > ar[i]) {
                i++;
            }

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i + 1 < n
                   && ar[i] < ar[i + 1]) {
                i++;
            }

            // If i is equal to
            // length of array - 1
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // Condition if ar[0] == ar[1]
        else {
            for (int i = 2; i < n; i++) {
                if (ar[i - 1] <= ar[i])
                    return false;
            }
            return true;
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    if (canMake(n, arr)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to check if the given array
// forms an increasing decreasing
// sequence or vice versa
static boolean canMake(int n, int ar[])
{
    // Base Case
    if (n == 1)
        return true;
    else
    {

        // First subarray is
        // stricly increasing
        if (ar[0] < ar[1])
        {

            int i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n && ar[i - 1] < ar[i])
            {
                i++;
            }

            // Check for strictly
            // decreasing condition
            // & find the break point
            while (i + 1 < n && ar[i] > ar[i + 1])
            {
                i++;
            }

            // If i is equal to
            // length of array
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // First subarray is
        // strictly Decreasing
        else if (ar[0] > ar[1])
        {
            int i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n && ar[i - 1] > ar[i])
            {
                i++;
            }

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i + 1 < n && ar[i] < ar[i + 1])
            {
                i++;
            }

            // If i is equal to
            // length of array - 1
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // Condition if ar[0] == ar[1]
        else
        {
            for (int i = 2; i < n; i++)
            {
                if (ar[i - 1] <= ar[i])
                    return false;
            }
            return true;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;

    // Function Call
    if (!canMake(n, arr)) {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given array
# forms an increasing decreasing
# sequence or vice versa
def canMake(n, ar):

    # Base Case
    if (n == 1):
        return True;
    else:

        # First subarray is
        # stricly increasing
        if (ar[0] < ar[1]):

            i = 1;

            # Check for strictly
            # increasing condition
            # & find the break point
            while (i < n and ar[i - 1] < ar[i]):
                i += 1;

            # Check for strictly
            # decreasing condition
            # & find the break point
            while (i + 1 < n and ar[i] > ar[i + 1]):
                i += 1;

            # If i is equal to
            # length of array
            if (i >= n - 1):
                return True;
            else:
                return False;

        # First subarray is
        # strictly Decreasing
        elif (ar[0] > ar[1]):
            i = 1;

            # Check for strictly
            # increasing condition
            # & find the break point
            while (i < n and ar[i - 1] > ar[i]):
                i += 1;

            # Check for strictly
            # increasing condition
            # & find the break point
            while (i + 1 < n and ar[i] < ar[i + 1]):
                i += 1;

            # If i is equal to
            # length of array - 1
            if (i >= n - 1):
                return True;
            else:
                return False;

        # Condition if ar[0] == ar[1]
        else:
            for i in range(2, n):
                if (ar[i - 1] <= ar[i]):
                    return False;

            return True;

# Driver Code

# Given array arr
arr = [1, 2, 3, 4, 5];
n = len(arr);

# Function Call
if (canMake(n, arr)==False):
    print("Yes");
else:
    print("No");

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if the given array
// forms an increasing decreasing
// sequence or vice versa
static bool canMake(int n, int []ar)
{
    // Base Case
    if (n == 1)
        return true;
    else
    {

        // First subarray is
        // stricly increasing
        if (ar[0] < ar[1])
        {

            int i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n && ar[i - 1] < ar[i])
            {
                i++;
            }

            // Check for strictly
            // decreasing condition
            // & find the break point
            while (i + 1 < n && ar[i] > ar[i + 1])
            {
                i++;
            }

            // If i is equal to
            // length of array
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // First subarray is
        // strictly Decreasing
        else if (ar[0] > ar[1])
        {
            int i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n && ar[i - 1] > ar[i])
            {
                i++;
            }

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i + 1 < n && ar[i] < ar[i + 1])
            {
                i++;
            }

            // If i is equal to
            // length of array - 1
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // Condition if ar[0] == ar[1]
        else
        {
            for (int i = 2; i < n; i++)
            {
                if (ar[i - 1] <= ar[i])
                    return false;
            }
            return true;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;

    // Function Call
    if (!canMake(n, arr))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the given array
// forms an increasing decreasing
// sequence or vice versa
function canMake(n, ar)
{

    // Base Case
    if (n == 1)
        return true;
    else
    {

        // First subarray is
        // stricly increasing
        if (ar[0] < ar[1])
        {
            let i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n && ar[i - 1] < ar[i])
            {
                i++;
            }

            // Check for strictly
            // decreasing condition
            // & find the break point
            while (i + 1 < n && ar[i] > ar[i + 1])
            {
                i++;
            }

            // If i is equal to
            // length of array
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // First subarray is
        // strictly Decreasing
        else if (ar[0] > ar[1])
        {
            let i = 1;

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i < n && ar[i - 1] > ar[i])
            {
                i++;
            }

            // Check for strictly
            // increasing condition
            // & find the break point
            while (i + 1 < n && ar[i] < ar[i + 1])
            {
                i++;
            }

            // If i is equal to
            // length of array - 1
            if (i >= n - 1)
                return true;
            else
                return false;
        }

        // Condition if ar[0] == ar[1]
        else
        {
            for(let i = 2; i < n; i++)
            {
                if (ar[i - 1] <= ar[i])
                    return false;
            }
            return true;
        }
    }
}

// Driver Code

// Given array arr[]
let arr = [ 1, 2, 3, 4, 5 ];
let n = arr.length;

// Function Call
if (!canMake(n, arr))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*