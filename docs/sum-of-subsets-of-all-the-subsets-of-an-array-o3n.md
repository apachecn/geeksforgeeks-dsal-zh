# 一个数组的所有子集的子集之和| O(3^N)

> 原文:[https://www . geesforgeks . org/数组所有子集之和-o3n/](https://www.geeksforgeeks.org/sum-of-subsets-of-all-the-subsets-of-an-array-o3n/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找出该数组所有子集的子集的总和。
**例:**

> **输入:** arr[] = {1，1}
> **输出:** 6
> 所有可能的子集:
> **a) {} : 0**
> 该子集
> 的所有可能子集将为{}，Sum = 0
> **b){1}:1**
> 该子集
> 的所有可能子集将为{}和{ 1 }， Sum = 0+1 = 1
> **c){1}:1**
> 该子集
> 的所有可能子集将为{}和{1}，Sum = 0 + 1 = 1
> **d) {1，1} : 4**
> 该子集
> 的所有可能子集将为{}、{1}、{1}和{ 1，1 }，Sum = 0+1+2 = 4
> 因此，ans = 0 + 1

**方法:**在本文中，将讨论一种具有 **O(3 <sup>N</sup> )** 时间复杂度的方法来解决给定的问题。
首先，生成数组所有可能的子集。总共会有 **2 <sup>N</sup>** 个子集。然后对于每个子集，求其所有子集的和。
现在，让我们了解一下这个解决方案的时间复杂性。
有 <sup>N</sup> C <sub>k</sub> 长度的子集 **K** 而找到长度数组子集的时间 **K** 是**2<sup>K</sup>T24】。
总时间=(<sup>N</sup>C<sub>1</sub>* 2<sup>1</sup>)+(<sup>N</sup>C<sub>2</sub>* 2<sup>2</sup>)+……+(<sup>N</sup>C<sub>K</sub>*<sup>K</sup>)= 3<sup>K</sup>T46】以下为上述执行情况**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to sum of all subsets of a
// given array
void subsetSum(vector<int>& c, int i,
               int& ans, int curr)
{
    // Base case
    if (i == c.size()) {
        ans += curr;
        return;
    }

    // Recursively calling subsetSum
    subsetSum(c, i + 1, ans, curr + c[i]);
    subsetSum(c, i + 1, ans, curr);
}

// Function to generate the subsets
void subsetGen(int* arr, int i, int n,
               int& ans, vector<int>& c)
{
    // Base-case
    if (i == n) {

        // Finding the sum of all the subsets
        // of the generated subset
        subsetSum(c, 0, ans, 0);
        return;
    }

    // Recursively accepting and rejecting
    // the current number
    subsetGen(arr, i + 1, n, ans, c);
    c.push_back(arr[i]);
    subsetGen(arr, i + 1, n, ans, c);
    c.pop_back();
}

// Driver code
int main()
{
    int arr[] = { 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    // To store the final ans
    int ans = 0;
    vector<int> c;

    subsetGen(arr, 0, n, ans, c);
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static Vector<Integer> c = new Vector<>();

    // To store the final ans
    static int ans = 0;

    // Function to sum of all subsets of a
    // given array
    static void subsetSum(int i, int curr)
    {

        // Base case
        if (i == c.size())
        {
            ans += curr;
            return;
        }

        // Recursively calling subsetSum
        subsetSum(i + 1, curr + c.elementAt(i));
        subsetSum(i + 1, curr);
    }

    // Function to generate the subsets
    static void subsetGen(int[] arr, int i, int n)
    {

        // Base-case
        if (i == n)
        {

            // Finding the sum of all the subsets
            // of the generated subset
            subsetSum(0, 0);
            return;
        }

        // Recursively accepting and rejecting
        // the current number
        subsetGen(arr, i + 1, n);
        c.add(arr[i]);
        subsetGen(arr, i + 1, n);
        c.remove(c.size() - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 1 };
        int n = arr.length;

        subsetGen(arr, 0, n);
        System.out.println(ans);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to sum of all subsets
# of a given array
c = []
ans = 0

def subsetSum(i, curr):
    global ans, c

    # Base case
    if (i == len(c)):
        ans += curr
        return

    # Recursively calling subsetSum
    subsetSum(i + 1, curr + c[i])
    subsetSum(i + 1, curr)

# Function to generate the subsets
def subsetGen(arr, i, n):
    global ans, c

    # Base-case
    if (i == n):

        # Finding the sum of all the subsets
        # of the generated subset
        subsetSum(0, 0)
        return

    # Recursively accepting and rejecting
    # the current number
    subsetGen(arr, i + 1, n)
    c.append(arr[i])
    subsetGen(arr, i + 1, n)
    del c[-1]

# Driver code
arr = [1, 1]
n = len(arr)

subsetGen(arr, 0, n)

print(ans)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static List<int> c = new List<int>();

    // To store the readonly ans
    static int ans = 0;

    // Function to sum of all subsets of a
    // given array
    static void subsetSum(int i, int curr)
    {

        // Base case
        if (i == c.Count)
        {
            ans += curr;
            return;
        }

        // Recursively calling subsetSum
        subsetSum(i + 1, curr + c[i]);
        subsetSum(i + 1, curr);
    }

    // Function to generate the subsets
    static void subsetGen(int[] arr, int i, int n)
    {

        // Base-case
        if (i == n)
        {

            // Finding the sum of all the subsets
            // of the generated subset
            subsetSum(0, 0);
            return;
        }

        // Recursively accepting and rejecting
        // the current number
        subsetGen(arr, i + 1, n);
        c.Add(arr[i]);
        subsetGen(arr, i + 1, n);
        c.RemoveAt(c.Count - 1);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 1 };
        int n = arr.Length;

        subsetGen(arr, 0, n);
        Console.WriteLine(ans);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var ans = 0;

var c = [];

// Function to sum of all subsets of a
// given array
function subsetSum(i, curr)
{
    // Base case
    if (i == c.length) {
        ans += curr;
        return;
    }

    // Recursively calling subsetSum
    subsetSum( i + 1, curr + c[i]);
    subsetSum(i + 1, curr);
}

// Function to generate the subsets
function subsetGen(arr, i, n, ans)
{
    // Base-case
    if (i == n) {

        // Finding the sum of all the subsets
        // of the generated subset
        subsetSum(0, ans, 0);
        return;
    }

    // Recursively accepting and rejecting
    // the current number
    subsetGen(arr, i + 1, n, ans);
    c.push(arr[i]);
    subsetGen(arr, i + 1, n, ans);
    c.pop();
}

// Driver code
var arr = [1, 1 ];
var n = arr.length;
// To store the final ans
var ans = 0;
var c = [];
subsetGen(arr, 0, n, ans);
document.write( ans);

</script>
```

**Output:** 

```
6
```