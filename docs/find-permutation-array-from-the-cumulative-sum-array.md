# 从累计和数组

中找到置换数组

> 原文:[https://www . geeksforgeeks . org/find-array-from-累计和-array/](https://www.geeksforgeeks.org/find-permutation-array-from-the-cumulative-sum-array/)

给定一个由 **N** 元素组成的数组 **arr[]** ，其中每个 **arr[i]** 是另一个数组 **P[]** 的子数组 **P[0…i]** 的累积和，其中 **P** 是从 **1** 到 **N** 的整数排列。任务是找到数组 **P[]** ，如果没有这样的 **P** 则打印 **-1** 。
**举例:**

> **输入:** arr[] = {2，3，6}
> **输出:** 2 1 3
> **输入:** arr[] = {1，2，2，4}
> **输出:** -1

**进场:**

*   累积数组的第一个元素必须是置换数组的第一个元素，位于**I<sup>th</sup>T3】位置的元素将是**arr[I]–arr[I–1]**，因为 **arr[]** 是置换数组的累积和数组。**
*   因此，从累积和数组中找到数组，然后标记从 **1** 到 **N** 的每个元素在生成的数组中的出现。
*   如果任何元素出现不止一次，则该排列无效，否则打印该排列。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the valid permutation
void getPermutation(int a[], int n)
{

    // Find the array from the cumulative sum
    vector<int> ans(n);
    ans[0] = a[0];
    for (int i = 1; i < n; i++)
        ans[i] = a[i] - a[i - 1];

    // To mark the occurrence of an element
    bool present[n + 1] = { false };
    for (int i = 0; i < ans.size(); i++) {

        // If current element has already
        // been seen previously
        if (present[ans[i]]) {
            cout << "-1";
            return;
        }

        // Mark the current element's occurrence
        else
            present[ans[i]] = true;
    }

    // Print the required permutation
    for (int i = 0; i < n; i++)
        cout << ans[i] << " ";
}

// Driver code
int main()
{
    int a[] = { 2, 3, 6 };
    int n = sizeof(a) / sizeof(a[0]);

    getPermutation(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the valid permutation
static void getPermutation(int a[], int n)
{

    // Find the array from the cumulative sum
    int []ans = new int[n];
    ans[0] = a[0];
    for (int i = 1; i < n; i++)
        ans[i] = a[i] - a[i - 1];

    // To mark the occurrence of an element
    boolean []present = new boolean[n + 1];
    for (int i = 0; i < ans.length; i++)
    {

        // If current element has already
        // been seen previously
        if (present[ans[i]])
        {
            System.out.print("-1");
            return;
        }

        // Mark the current element's occurrence
        else
            present[ans[i]] = true;
    }

    // Print the required permutation
    for (int i = 0; i < n; i++)
        System.out.print(ans[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 3, 6 };
    int n = a.length;

    getPermutation(a, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the valid permutation
def getPermutation(a, n) :

    # Find the array from the cumulative sum
    ans = [0] * n;
    ans[0] = a[0];
    for i in range(1, n) :
        ans[i] = a[i] - a[i - 1];

    # To mark the occurrence of an element
    present = [0] * (n + 1);

    for i in range(n) :

        # If current element has already
        # been seen previously
        if (present[ans[i]]) :
            print("-1", end = "");
            return;

        # Mark the current element's occurrence
        else :
            present[ans[i]] = True;

    # Print the required permutation
    for i in range(n) :
        print(ans[i], end = " ");

# Driver code
if __name__ == "__main__" :

    a = [ 2, 3, 6 ];
    n = len(a);

    getPermutation(a, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the valid permutation
static void getPermutation(int [] a, int n)
{

    // Find the array from the cumulative sum
    List<int> ans = new List<int>();
    ans.Add(a[0]);
    for (int i = 1; i < n; i++)
        ans.Add(a[i] - a[i - 1]);

    // To mark the occurrence of an element
    List<int> present = new List<int>();

    for (int i = 0; i < n+1; i++)
        present.Add(0);

    for (int i = 0; i < ans.Count; i++)
    {

        // If current element has already
        // been seen previously
        if (present[ans[i]] == 1)
        {
            Console.Write("-1");
            return;
        }

        // Mark the current element's occurrence
        else
            present[ans[i]] = 1;
    }

    // Print the required permutation
    for (int i = 0; i < n; i++)
        Console.Write(ans[i] + " ");
}

// Driver code
static public void Main()
{
    int[] a = { 2,3,6};
    int n = a.Length;
    getPermutation(a, n);
}
}

// This code is ontributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the valid permutation
function getPermutation(a, n)
{

    // Find the array from the cumulative sum
    var ans = Array(n);
    ans[0] = a[0];
    for (var i = 1; i < n; i++)
        ans[i] = a[i] - a[i - 1];

    // To mark the occurrence of an element
    var present = Array(n+1).fill(false);
    for (var i = 0; i < ans.length; i++) {

        // If current element has already
        // been seen previously
        if (present[ans[i]]) {
            document.write( "-1");
            return;
        }

        // Mark the current element's occurrence
        else
            present[ans[i]] = true;
    }

    // Print the required permutation
    for (var i = 0; i < n; i++)
        document.write( ans[i] + " ");
}

// Driver code
var a = [2, 3, 6];
var n = a.length;
getPermutation(a, n);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2 1 3
```