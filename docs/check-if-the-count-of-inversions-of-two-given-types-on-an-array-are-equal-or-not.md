# 检查一个数组上两个给定类型的求逆计数是否相等

> 原文:[https://www . geesforgeks . org/check-如果数组上两个给定类型的倒计数相等或不相等/](https://www.geeksforgeeks.org/check-if-the-count-of-inversions-of-two-given-types-on-an-array-are-equal-or-not/)

给定一个数组 **a[]** ，在该数组上执行以下两种类型的反演:

*   成对指数 **(i，j)** 的计数，使得**A【I】>A【j】**和 **i < j**
*   指数对的计数 **(i，j)** 使得 **A[i] > A[j]** 和 **j = i + 1**

任务是检查两个反转的计数是否相等。如果相等，打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** a[] = {1，0，2}
> **输出:**是
> **解释:**
> 1 型反转计数= 1 [(i，j) : (0，1)]
> 2 型反转计数= 1 [(i，j) : (0，1)]
> **输入:** a[] = {1，2，0}
> **输出:**否
> **(1，2)]**

**方法:**
要解决这个问题，需要了解两个反演的区别:

*   对于**类型 2** ，如果 **j = 5，**那么 **i** 只能是 **4** 作为 **j = i + 1**
*   对于**1 型，**如果 **j = 5** ，那么 **i** 可以从 **0** 到 **4** ，因为 **i** 小于 **j** 。
*   因此**1 型**的反演基本上是【T12 型的反演，用**把所有对指标(I，j)** 和小于(**j–1**)的 **i** 和**a【I】>a【j】**相加。
*   所以，对于任何指标 **j** ，任务是检查是否有指标 **i** ，比 j–1 和**a【I】>a【j】**小**。如果找到任何一对这样的索引 **(i，j)** ，则打印“ **No** ”。否则，打印“**是**”。**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// count of inversion of two
// types are same or not
bool solve(int a[], int n)
{
    int mx = INT_MIN;

    for (int j = 1; j < n; j++) {

        // If maximum value is found
        // to be greater than a[j],
        // then that pair of indices
        // (i, j) will add extra value
        // to inversion of Type 1
        if (mx > a[j])

            return false;

        // Update max
        mx = max(mx, a[j - 1]);
    }

    return true;
}

// Driver code
int main()
{

    int a[] = { 1, 0, 2 };

    int n = sizeof(a) / sizeof(a[0]);

    bool possible = solve(a, n);

    if (possible)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to check if the
// count of inversion of two
// types are same or not
static boolean solve(int a[], int n)
{
    int mx = Integer.MIN_VALUE;

    for(int j = 1; j < n; j++)
    {

        // If maximum value is found
        // to be greater than a[j],
        // then that pair of indices
        // (i, j) will add extra value
        // to inversion of Type 1
        if (mx > a[j])
            return false;

        // Update max
        mx = Math.max(mx, a[j - 1]);
    }
    return true;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 0, 2 };

    int n = a.length;

    boolean possible = solve(a, n);

    if (possible)
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach
import sys

# Function to check if the
# count of inversion of two
# types are same or not
def solve(a, n):

    mx = -sys.maxsize - 1

    for j in range(1, n):

        # If maximum value is found
        # to be greater than a[j],
        # then that pair of indices
        # (i, j) will add extra value
        # to inversion of Type 1
        if (mx > a[j]):
            return False

        # Update max
        mx = max(mx, a[j - 1])

    return True

# Driver code
a = [ 1, 0, 2 ]

n = len(a)

possible = solve(a, n)

if (possible != 0):
    print("Yes")
else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement 
// the above approach
using System;

class GFG{

// Function to check if the
// count of inversion of two
// types are same or not
static bool solve(int[] a, int n)
{
    int mx = Int32.MinValue;

    for(int j = 1; j < n; j++)
    {

        // If maximum value is found
        // to be greater than a[j],
        // then that pair of indices
        // (i, j) will add extra value
        // to inversion of Type 1
        if (mx > a[j])
            return false;

        // Update max
        mx = Math.Max(mx, a[j - 1]);
    }
    return true;
}

// Driver code
public static void Main ()
{
    int[] a = { 1, 0, 2 };
    int n = a.Length;

    bool possible = solve(a, n);

    if (possible)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to check if the
// count of inversion of two
// types are same or not
function solve(a, n)
{
    let mx = 0;

    for(let j = 1; j < n; j++)
    {

        // If maximum value is found
        // to be greater than a[j],
        // then that pair of indices
        // (i, j) will add extra value
        // to inversion of Type 1
        if (mx > a[j])
            return false;

        // Update max
        mx = Math.max(mx, a[j - 1]);
    }
    return true;
}

  // Driver Code

    let a = [ 1, 0, 2 ];

    let n = a.length;

    let possible = solve(a, n);

    if (possible)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*