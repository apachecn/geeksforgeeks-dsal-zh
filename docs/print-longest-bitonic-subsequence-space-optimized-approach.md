# 打印最长的双音素子序列(空间优化方法)

> 原文:[https://www . geesforgeks . org/print-long-bitonic-subsequence-space-optimized-approach/](https://www.geeksforgeeks.org/print-longest-bitonic-subsequence-space-optimized-approach/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是打印给定数组中最长的双音素子序列。
**注意:**如果多个解决方案退出，则打印任何解决方案。

**示例:**

> **输入:** arr[] = {1，1 1，2，10，4，5，2，1}
> **输出:** 1 11 10 5 2 1
> **解释:**
> 上述数组中所有可能的最长双音素子序列为{1，2，10，4，2，1}、{1，11，10，5，2，1}、{1，2，4，5，2，1}。
> 因此，打印它们中的任何一个来获得答案。
> 
> **输入:** arr[] = {80，60，30，40，20，10}
> **输出:** 80 60 30 20 10

**使用额外空间的动态规划方法:**关于解决问题的 2D 动态规划方法，请参考[上一篇文章](https://www.geeksforgeeks.org/printing-longest-bitonic-subsequence/)。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**空间优化方式:**上述方式使用的辅助空间可以通过**1D**T4**动态规划**T7】进行优化。按照以下步骤解决问题。

1.  创建两个数组 **lis[]** 和 **lds[]** ，以在每个 i <sup>第</sup>索引处分别存储以元素**arr【I】**结束的最长递增和递减子序列的长度。
2.  一旦计算出来，找到包含最大值**lis[I]+LDS[I]–1**的 **i <sup>第</sup>指数**
3.  创建 **res[]** 以按元素降序存储最长双音素序列的所有元素，然后按元素升序存储。
4.  打印 **res[]** 数组。

下面是实施上述方法:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the longest
// bitonic subsequence
void printRes(vector<int>& res)
{
    int n = res.size();
    for (int i = 0; i < n; i++) {
        cout << res[i] << " ";
    }
}

// Function to generate the longest
// bitonic subsequence
void printLBS(int arr[], int N)
{

    // Store the lengths of LIS
    // ending at every index
    int lis[N];

    // Store the lengths of LDS
    // ending at every index
    int lds[N];

    for (int i = 0; i < N; i++) {
        lis[i] = lds[i] = 1;
    }

    // Compute LIS for all indices
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < i; j++) {

            if (arr[j] < arr[i]) {

                if (lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;
            }
        }
    }

    // Compute LDS for all indices
    for (int i = N - 1; i >= 0; i--) {

        for (int j = N - 1; j > i; j--) {
            if (arr[j] < arr[i]) {

                if (lds[i] < lds[j] + 1)
                    lds[i] = lds[j] + 1;
            }
        }
    }

    // Find the index having
    // maximum value of
    // lis[i] + lds[i] - 1
    int MaxVal = arr[0], inx = 0;
    for (int i = 0; i < N; i++) {

        if (MaxVal < lis[i] + lds[i] - 1) {
            MaxVal = lis[i] + lds[i] - 1;
            inx = i;
        }
    }

    // Stores the count of elements in
    // increasing order in Bitonic subsequence
    int ct1 = lis[inx];
    vector<int> res;

    // Store the increasing subsequence
    for (int i = inx; i >= 0 && ct1 > 0; i--) {

        if (lis[i] == ct1) {

            res.push_back(arr[i]);

            ct1--;
        }
    }

    // Sort the bitonic subsequence
    // to arrange smaller elements
    // at the beginning
    reverse(res.begin(), res.end());

    // Stores the count of elements in
    // decreasing order in Bitonic subsequence
    int ct2 = lds[inx] - 1;
    for (int i = inx; i < N && ct2 > 0; i++) {

        if (lds[i] == ct2) {

            res.push_back(arr[i]);

            ct2--;
        }
    }

    // Print the longest
    // bitonic sequence
    printRes(res);
}

// Driver Code
int main()
{

    int arr[] = { 80, 60, 30, 40, 20, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printLBS(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG {

// Function to print the longest
// bitonic subsequence
static void printRes(Vector<Integer> res)
{
    Enumeration enu = res.elements();
    while (enu.hasMoreElements())
    {
        System.out.print(enu.nextElement() + " ");
    }
}

// Function to generate the longest
// bitonic subsequence
static void printLBS(int arr[], int N)
{

    // Store the lengths of LIS
    // ending at every index
    int lis[] = new int[N];

    // Store the lengths of LDS
    // ending at every index
    int lds[] = new int[N];

    for(int i = 0; i < N; i++)
    {
        lis[i] = lds[i] = 1;
    }

    // Compute LIS for all indices
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < i; j++)
        {
            if (arr[j] < arr[i])
            {
                if (lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;
            }
        }
    }

    // Compute LDS for all indices
    for(int i = N - 1; i >= 0; i--)
    {
        for(int j = N - 1; j > i; j--)
        {
            if (arr[j] < arr[i])
            {
                if (lds[i] < lds[j] + 1)
                    lds[i] = lds[j] + 1;
            }
        }
    }

    // Find the index having
    // maximum value of
    // lis[i] + lds[i] - 1
    int MaxVal = arr[0], inx = 0;
    for(int i = 0; i < N; i++)
    {
        if (MaxVal < lis[i] + lds[i] - 1)
        {
            MaxVal = lis[i] + lds[i] - 1;
            inx = i;
        }
    }

    // Stores the count of elements in
    // increasing order in Bitonic subsequence
    int ct1 = lis[inx];
    Vector<Integer> res = new Vector<Integer>();

    // Store the increasing subsequence
    for(int i = inx; i >= 0 && ct1 > 0; i--)
    {
        if (lis[i] == ct1)
        {
            res.add(arr[i]);

            ct1--;
        }
    }

    // Sort the bitonic subsequence
    // to arrange smaller elements
    // at the beginning
    Collections.reverse(res);

    // Stores the count of elements in
    // decreasing order in Bitonic subsequence
    int ct2 = lds[inx] - 1;
    for(int i = inx; i < N && ct2 > 0; i++)
    {
        if (lds[i] == ct2)
        {
            res.add(arr[i]);
            ct2--;
        }
    }

    // Print the longest
    // bitonic sequence
    printRes(res);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 80, 60, 30, 40, 20, 10 };
    int N = arr.length;

    printLBS(arr, N);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the longest
# bitonic subsequence
def printRes(res):

    n = len(res)
    for i in range(n):
        print(res[i], end = " ")

# Function to generate the longest
# bitonic subsequence
def printLBS(arr, N):

    # Store the lengths of LIS
    # ending at every index
    lis = [0] * N

    # Store the lengths of LDS
    # ending at every index
    lds = [0] * N

    for i in range(N):
        lis[i] = lds[i] = 1

    # Compute LIS for all indices
    for i in range(N):
        for j in range(i):
            if arr[j] < arr[i]:
                if lis[i] < lis[j] + 1:
                    lis[i] = lis[j] + 1

    # Compute LDS for all indices
    for i in range(N - 1, -1, -1):
        for j in range(N - 1, i, -1):
            if arr[j] < arr[i]:
                if lds[i] < lds[j] + 1:
                    lds[i] = lds[j] + 1

    # Find the index having
    # maximum value of
    # lis[i]+lds[i]+1
    MaxVal = arr[0]
    inx = 0

    for i in range(N):
        if MaxVal < lis[i] + lds[i] - 1:
            MaxVal = lis[i] + lds[i] - 1
            inx = i

    # Stores the count of elements in
    # increasing order in Bitonic subsequence
    ct1 = lis[inx]
    res = []

    i = inx

    # Store the increasing subsequence
    while i >= 0 and ct1 > 0:
        if lis[i] == ct1:
            res.append(arr[i])
            ct1 -= 1

        i -= 1

    # Sort the bitonic subsequence
    # to arrange smaller elements
    # at the beginning
    res.reverse()

    # Stores the count of elements in
    # decreasing order in Bitonic subsequence
    ct2 = lds[inx] - 1
    i = inx

    while i < N and ct2 > 0:
        if lds[i] == ct2:
            res.append(arr[i])
            ct2 -= 1

        i += 1

    # Print the longest
    # bitonic sequence
    printRes(res)

# Driver code
arr = [ 80, 60, 30, 40, 20, 10 ]
N = len(arr)

printLBS(arr, N)

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

    // Function to print the longest
    // bitonic subsequence
    static void printRes(List<int> res)
    {
        foreach(int enu in res)
        {
            Console.Write(enu + " ");
        }
    }

    // Function to generate the longest
    // bitonic subsequence
    static void printLBS(int[] arr, int N)
    {

        // Store the lengths of LIS
        // ending at every index
        int[] lis = new int[N];

        // Store the lengths of LDS
        // ending at every index
        int[] lds = new int[N];

        for (int i = 0; i < N; i++)
        {
            lis[i] = lds[i] = 1;
        }

        // Compute LIS for all indices
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < i; j++)
            {
                if (arr[j] < arr[i])
                {
                    if (lis[i] < lis[j] + 1)
                        lis[i] = lis[j] + 1;
                }
            }
        }

        // Compute LDS for all indices
        for (int i = N - 1; i >= 0; i--)
        {
            for (int j = N - 1; j > i; j--)
            {
                if (arr[j] < arr[i])
                {
                    if (lds[i] < lds[j] + 1)
                        lds[i] = lds[j] + 1;
                }
            }
        }

        // Find the index having
        // maximum value of
        // lis[i] + lds[i] - 1
        int MaxVal = arr[0], inx = 0;
        for (int i = 0; i < N; i++)
        {
            if (MaxVal < lis[i] + lds[i] - 1)
            {
                MaxVal = lis[i] + lds[i] - 1;
                inx = i;
            }
        }

        // Stores the count of elements in
        // increasing order in Bitonic subsequence
        int ct1 = lis[inx];
        List<int> res = new List<int>();

        // Store the increasing subsequence
        for (int i = inx; i >= 0 && ct1 > 0; i--)
        {
            if (lis[i] == ct1)
            {
                res.Add(arr[i]);
                ct1--;
            }
        }

        // Sort the bitonic subsequence
        // to arrange smaller elements
        // at the beginning
        res.Reverse();

        // Stores the count of elements in
        // decreasing order in Bitonic subsequence
        int ct2 = lds[inx] - 1;
        for (int i = inx; i < N && ct2 > 0; i++)
        {
            if (lds[i] == ct2)
            {
                res.Add(arr[i]);
                ct2--;
            }
        }

        // Print the longest
        // bitonic sequence
        printRes(res);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = {80, 60, 30, 40, 20, 10};
        int N = arr.Length;
        printLBS(arr, N);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to print the longest
// bitonic subsequence
function printRes( res)
{
    var n = res.length;
    for (var i = 0; i < n; i++) {
        document.write( res[i] + " ");
    }
}

// Function to generate the longest
// bitonic subsequence
function printLBS(arr, N)
{

    // Store the lengths of LIS
    // ending at every index
    var lis = Array(N);

    // Store the lengths of LDS
    // ending at every index
    var lds = Array(N);

    for (var i = 0; i < N; i++) {
        lis[i] = lds[i] = 1;
    }

    // Compute LIS for all indices
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < i; j++) {

            if (arr[j] < arr[i]) {

                if (lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;
            }
        }
    }

    // Compute LDS for all indices
    for (var i = N - 1; i >= 0; i--) {

        for (var j = N - 1; j > i; j--) {
            if (arr[j] < arr[i]) {

                if (lds[i] < lds[j] + 1)
                    lds[i] = lds[j] + 1;
            }
        }
    }

    // Find the index having
    // maximum value of
    // lis[i] + lds[i] - 1
    var MaxVal = arr[0], inx = 0;
    for (var i = 0; i < N; i++) {

        if (MaxVal < lis[i] + lds[i] - 1) {
            MaxVal = lis[i] + lds[i] - 1;
            inx = i;
        }
    }

    // Stores the count of elements in
    // increasing order in Bitonic subsequence
    var ct1 = lis[inx];
    var res = [];

    // Store the increasing subsequence
    for (var i = inx; i >= 0 && ct1 > 0; i--) {

        if (lis[i] == ct1) {

            res.push(arr[i]);

            ct1--;
        }
    }

    // Sort the bitonic subsequence
    // to arrange smaller elements
    // at the beginning
    res.reverse();

    // Stores the count of elements in
    // decreasing order in Bitonic subsequence
    var ct2 = lds[inx] - 1;
    for (var i = inx; i < N && ct2 > 0; i++) {

        if (lds[i] == ct2) {

            res.push(arr[i]);

            ct2--;
        }
    }

    // Print the longest
    // bitonic sequence
    printRes(res);
}

// Driver Code

var arr = [80, 60, 30, 40, 20, 10];
var N = arr.length;
printLBS(arr, N);

</script>
```

**Output:** 

```
80 60 30 20 10
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*