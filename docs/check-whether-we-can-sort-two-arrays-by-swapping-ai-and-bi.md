# 检查我们是否可以通过交换 A[i]和 B[i]

来对两个数组进行排序

> 原文:[https://www . geeksforgeeks . org/check-we-能否通过交换对两个数组进行排序-ai-and-bi/](https://www.geeksforgeeks.org/check-whether-we-can-sort-two-arrays-by-swapping-ai-and-bi/)

给定两个数组，我们必须检查是否可以通过交换 A[i]和 B[i]以严格的升序对两个数组进行排序。

**示例:**

> **输入:** A[ ]={ 1，4，3，5，7}，B[ ]={ 2，2，5，8，9}
> **输出:**真
> 交换 A[1]和 B[1]后，两个数组都排序。
> 
> **输入:** A[ ]={ 1，4，5，5，7}，B[ ]={ 2，2，5，8，9}
> **输出:**假
> 不可能让两个数组都用任意数量的互换排序。

给我们两个数组，我们可以用 B[i]交换 A[i]，这样我们就可以严格按照升序对两个数组进行排序，所以我们必须以 A[i] < A[i+1] and B[i] < B[i+1]. 
的方式对数组进行排序，我们将使用贪婪的方法来解决这个问题。
我们将得到 A[i]和 B[i]的最小值和最大值，并将最小值分配给 B[i]，将最大值分配给 A[i]。
现在，我们将检查数组 A 和数组 B 是否严格递增。
让我们考虑我们的方法是不正确的，(有可能安排但我们的方法给出假的)，这意味着任何一个或多个位置被切换。

这意味着 a[i-1]不小于 a[i]或 a[i+1]不大于 a[i]。现在如果 a[i]不大于 a[i-1]，我们就不能用 b[i]来交换 a[i]，因为 b[i]总是小于 a[i]。现在让我们假设 a[i+1]不大于 a[i]，这样我们就可以将 a[i]与 b[i]交换为 a[i] > b[i]，但作为 a[i] > b[i]和 a[i+1]> b[i+1]和 a[i]>a[i+1]，所以 a[i]永远不能小于 b[i+1]，所以没有可能的交换。我们同样可以证明 b[i]。

因此，证明了当输出为是时，排列数组可能有更多可能的组合，但是当输出为否时，没有可能根据约束排列数组

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Function to check whether both the array can be
// sorted in (strictly increasing ) ascending order
bool IsSorted(int A[], int B[], int n)
{
    // Traverse through the array
    // and find out the min and max
    // variable at each position
    // make one array of min variables
    // and another of maximum variable
    for (int i = 0; i < n; i++) {
        int x, y;

        // Maximum and minimum variable
        x = max(A[i], B[i]);
        y = min(A[i], B[i]);

        // Assign min value to
        // B[i] and max value to A[i]
        A[i] = x;
        B[i] = y;
    }

    // Now check whether the array is
    // sorted or not
    for (int i = 1; i < n; i++) {
        if (A[i] <= A[i - 1] || B[i] <= B[i - 1])
            return false;
    }

    return true;
}

// Driver code
int main()
{
    int A[] = { 1, 4, 3, 5, 7 };
    int B[] = { 2, 2, 5, 8, 9 };
    int n = sizeof(A) / sizeof(int);

    cout << (IsSorted(A, B, n) ? "True" : "False");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

// Function to check whether both the array can be
// sorted in (strictly increasing ) ascending order
static boolean IsSorted(int []A, int []B, int n)
{
    // Traverse through the array
    // and find out the min and max
    // variable at each position
    // make one array of min variables
    // and another of maximum variable
    for (int i = 0; i < n; i++)
    {
        int x, y;

        // Maximum and minimum variable
        x = Math.max(A[i], B[i]);
        y = Math.min(A[i], B[i]);

        // Assign min value to
        // B[i] and max value to A[i]
        A[i] = x;
        B[i] = y;
    }

    // Now check whether the array is
    // sorted or not
    for (int i = 1; i < n; i++)
    {
        if (A[i] <= A[i - 1] || B[i] <= B[i - 1])
            return false;
    }

    return true;
}

// Driver code
public static void main (String[] args)
{

    int []A = { 1, 4, 3, 5, 7 };
    int []B = { 2, 2, 5, 8, 9 };
    int n = A.length;

    if(IsSorted(A, B, n) == true)
    {
        System.out.println("True");
    }
    else
    {
        System.out.println("False");
    }
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to check whether both the array can be
# sorted in (strictly increasing ) ascending order
def IsSorted(A, B, n) :

    # Traverse through the array
    # and find out the min and max
    # variable at each position
    # make one array of min variables
    # and another of maximum variable
    for i in range(n) :

        # Maximum and minimum variable
        x = max(A[i], B[i]);
        y = min(A[i], B[i]);

        # Assign min value to
        # B[i] and max value to A[i]
        A[i] = x;
        B[i] = y;

    # Now check whether the array is
    # sorted or not
    for i in range(1, n) :
        if (A[i] <= A[i - 1] or B[i] <= B[i - 1]) :
            return False;

    return True;

# Driver code
if __name__ == "__main__" :

    A = [ 1, 4, 3, 5, 7 ];
    B = [ 2, 2, 5, 8, 9 ];

    n = len(A);

    if (IsSorted(A, B, n)) :
        print(True)
    else :
        print(False)

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to check whether both the array can be
// sorted in (strictly increasing ) ascending order
static bool IsSorted(int []A, int []B, int n)
{
    // Traverse through the array
    // and find out the min and max
    // variable at each position
    // make one array of min variables
    // and another of maximum variable
    for (int i = 0; i < n; i++) {
        int x, y;

        // Maximum and minimum variable
        x = Math.Max(A[i], B[i]);
        y = Math.Min(A[i], B[i]);

        // Assign min value to
        // B[i] and max value to A[i]
        A[i] = x;
        B[i] = y;
    }

    // Now check whether the array is
    // sorted or not
    for (int i = 1; i < n; i++) {
        if (A[i] <= A[i - 1] || B[i] <= B[i - 1])
            return false;
    }

    return true;
}

// Driver code
public static void Main()
{
    int []A = { 1, 4, 3, 5, 7 };
    int []B = { 2, 2, 5, 8, 9 };
    int n = A.Length;

    if(IsSorted(A, B, n) == true)
    {
        Console.Write("True");
    }
    else
    {
        Console.Write("False");
    }
}
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check whether both the
// array can be sorted in (strictly
// increasing) ascending order
function IsSorted(A, B, n)
{

    // Traverse through the array
    // and find out the min and max
    // variable at each position
    // make one array of min variables
    // and another of maximum variable
    for(var i = 0; i < n; i++)
    {
        var x, y;

        // Maximum and minimum variable
        x = Math.max(A[i], B[i]);
        y = Math.min(A[i], B[i]);

        // Assign min value to
        // B[i] and max value to A[i]
        A[i] = x;
        B[i] = y;
    }

    // Now check whether the array is
    // sorted or not
    for(var i = 1; i < n; i++)
    {
        if (A[i] <= A[i - 1] ||
            B[i] <= B[i - 1])
            return false;
    }
    return true;
}

// Driver Code
var A = [ 1, 4, 3, 5, 7 ];
var B = [ 2, 2, 5, 8, 9 ];
var n = A.length;

document.write(IsSorted(A, B, n) ?
               "True" : "False");

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
True
```

**时间复杂度:** O(N)