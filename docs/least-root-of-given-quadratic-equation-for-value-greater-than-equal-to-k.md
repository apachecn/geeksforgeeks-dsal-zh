# 大于等于 K 的给定二次方程的最小根

> 原文:[https://www . geesforgeks . org/给定二次方程的最小根大于等于 k/](https://www.geeksforgeeks.org/least-root-of-given-quadratic-equation-for-value-greater-than-equal-to-k/)

给定二次方程 **F(x) = Ax <sup>2</sup> + Bx + C** 为 **A、B、C** 和一个整数 **K** ，任务是求根 **x** 的最小值使得 **F(x) ≥ K** 和 **x > 0** 。如果不存在这样的值，则打印**-1”**。给出 **F(x)** 是单调递增函数。

**示例:**

> **输入:** A = 3，B = 4，C = 5，K = 6
> **输出:** 1
> **说明:**
> 对于给定值 F(x)= 3x<sup>2</sup>+4x+5 x 的最小值为 1，F(x) = 12，大于给定值 **K** 。
> 
> **输入:** A = 3，B = 4，C = 5，K = 150
> **输出:** 7
> **说明:**
> 对于给定值 F(x)= 3x<sup>2</sup>+4x+5 x 的最小值为 7，F(x) = 180，大于给定值 **K** 。

**逼近:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)求 **x** 的最小值。以下是步骤:

*   要得到等于或大于 **K、**的值， **x** 的值必须在**【1，sqrt(K)】**的范围内，因为这是一个二次方程。
*   现在，基本上需要在范围内搜索适当的元素，因此为此实现了二分搜索法。
*   计算 **F(中间)**，其中**中间**是范围**【1，sqrt(K)】**的中间值。以下三种情况是可能的:
    *   如果 **F(中)≥ K & & F(中)< K:** 这意味着当前的 mid 是要求的答案。
    *   如果 **F(mid) < K:** 这意味着 mid 的当前值小于 x 的要求值，那么，向右移动，即在后半部分，因为 **F(x)** 是一个递增函数。
    *   如果 **F(mid) > K:** 这意味着 mid 的当前值大于 x 的要求值，那么，向左移动，即前半部分作为 **F(x)** 是递增函数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate value of
// quadratic equation for some x
int func(int A, int B, int C, int x)
{
    return (A * x * x + B * x + C);
}

// Function to calculate the minimum
// value of x such that F(x) >= K using
// binary search
int findMinx(int A, int B, int C, int K)
{

    // Start and end value for
    // binary search
    int start = 1;
    int end = ceil(sqrt(K));

    // Binary Search
    while (start <= end) {
        int mid = start + (end - start) / 2;

        // Computing F(mid) and F(mid-1)
        int x = func(A, B, C, mid);
        int Y = func(A, B, C, mid - 1);

        // Checking the three cases

        // If F(mid) >= K  and
        // F(mid-1) < K return mid
        if (x >= K && Y < K) {
            return mid;
        }

        // If F(mid) < K go to mid+1 to end
        else if (x < K) {
            start = mid + 1;
        }

        // If F(mid) > K go to start to mid-1
        else {
            end = mid - 1;
        }
    }

    // If no such value exist
    return -1;
}

// Driver Code
int main()
{
    // Given coefficients of Equations
    int A = 3, B = 4, C = 5, K = 6;

    // Find minimum value of x
    cout << findMinx(A, B, C, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate value of
// quadratic equation for some x
static int func(int A, int B, int C, int x)
{
    return (A * x * x + B * x + C);
}

// Function to calculate the minimum
// value of x such that F(x) >= K using
// binary search
static int findMinx(int A, int B, int C, int K)
{

    // Start and end value for
    // binary search
    int start = 1;
    int end = (int)Math.ceil(Math.sqrt(K));

    // Binary Search
    while (start <= end)
    {
        int mid = start + (end - start) / 2;

        // Computing F(mid) and F(mid-1)
        int x = func(A, B, C, mid);
        int Y = func(A, B, C, mid - 1);

        // Checking the three cases
        // If F(mid) >= K and
        // F(mid-1) < K return mid
        if (x >= K && Y < K)
        {
            return mid;
        }

        // If F(mid) < K go to mid+1 to end
        else if (x < K)
        {
            start = mid + 1;
        }

        // If F(mid) > K go to start to mid-1
        else
        {
            end = mid - 1;
        }
    }

    // If no such value exist
    return -1;
}

// Driver code
public static void main(String[] args)
{

    // Given coefficients of Equations
    int A = 3, B = 4, C = 5, K = 6;

    // Find minimum value of x
    System.out.println(findMinx(A, B, C, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to calculate value of
# quadratic equation for some x
def func(A, B, C, x):

    return (A * x * x + B * x + C)

# Function to calculate the minimum
# value of x such that F(x) >= K using
# binary search
def findMinx(A, B, C, K):

    # Start and end value for
    # binary search
    start = 1
    end = math.ceil(math.sqrt(K))

    # Binary Search
    while (start <= end):
        mid = start + (end - start) // 2

        # Computing F(mid) and F(mid-1)
        x = func(A, B, C, mid)
        Y = func(A, B, C, mid - 1)

        # Checking the three cases

        # If F(mid) >= K and
        # F(mid-1) < K return mid
        if (x >= K and Y < K):
            return mid

        # If F(mid) < K go to mid+1 to end
        elif (x < K):
            start = mid + 1

        # If F(mid) > K go to start to mid-1
        else:
            end = mid - 1

    # If no such value exist
    return -1

# Driver Code

# Given coefficients of Equations
A = 3
B = 4
C = 5
K = 6

# Find minimum value of x
print(findMinx(A, B, C, K))

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to calculate value of
// quadratic equation for some x
static int func(int A, int B, int C, int x)
{
    return (A * x * x + B * x + C);
}

// Function to calculate the minimum
// value of x such that F(x) >= K using
// binary search
static int findMinx(int A, int B, int C, int K)
{

    // Start and end value for
    // binary search
    int start = 1;
    int end = (int)Math.Ceiling(Math.Sqrt(K));

    // Binary Search
    while (start <= end)
    {
        int mid = start + (end - start) / 2;

        // Computing F(mid) and F(mid-1)
        int x = func(A, B, C, mid);
        int Y = func(A, B, C, mid - 1);

        // Checking the three cases
        // If F(mid) >= K and
        // F(mid-1) < K return mid
        if (x >= K && Y < K)
        {
            return mid;
        }

        // If F(mid) < K go to mid+1 to end
        else if (x < K)
        {
            start = mid + 1;
        }

        // If F(mid) > K go to start to mid-1
        else
        {
            end = mid - 1;
        }
    }

    // If no such value exist
    return -1;
}

// Driver code
public static void Main(String[] args)
{

    // Given coefficients of Equations
    int A = 3, B = 4, C = 5, K = 6;

    // Find minimum value of x
    Console.WriteLine(findMinx(A, B, C, K));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to calculate value of
// quadratic equation for some x
function func(A , B , C , x)
{
    return (A * x * x + B * x + C);
}

// Function to calculate the minimum
// value of x such that F(x) >= K using
// binary search
function findMinx(A , B , C , K)
{

    // Start and end value for
    // binary search
    var start = 1;
    var end = parseInt(Math.ceil(Math.sqrt(K)));

    // Binary Search
    while (start <= end)
    {
        var mid = start + parseInt((end - start) / 2);

        // Computing F(mid) and F(mid-1)
        var x = func(A, B, C, mid);
        var Y = func(A, B, C, mid - 1);

        // Checking the three cases
        // If F(mid) >= K and
        // F(mid-1) < K return mid
        if (x >= K && Y < K)
        {
            return mid;
        }

        // If F(mid) < K go to mid+1 to end
        else if (x < K)
        {
            start = mid + 1;
        }

        // If F(mid) > K go to start to mid-1
        else
        {
            end = mid - 1;
        }
    }

    // If no such value exist
    return -1;
}

// Driver code

// Given coefficients of Equations
var A = 3, B = 4, C = 5, K = 6;

// Find minimum value of x
document.write(findMinx(A, B, C, K));

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(log(sqrt(K))*
T5】辅助空间: *O(1)*