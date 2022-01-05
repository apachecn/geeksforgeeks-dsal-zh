# 两个相等和段范围查询

> 原文:[https://www . geesforgeks . org/two-equal-sum-segment-range-query/](https://www.geeksforgeeks.org/two-equal-sum-segment-range-queries/)

给定一个由 **N** 正整数组成的数组 **arr[]** ，以及一些由范围**【L，R】**组成的查询，任务是找出给定索引范围内的子数组是否可以分成长度非零且和相等的两个连续部分。
**举例:**

> **输入:** arr[] = {1，1，2，3}，q[] = {{0，1}，{1，3}，{1，2}}
> **输出:**
> 是
> 是
> 否
> q[0]:子阵列可以拆分为{1}、{1}。
> q[1]:子阵列可以拆分为{1，2}，{3}。
> q[2]:子阵列不能拆分成两个相等的段。
> **输入:** arr[] = {2，1，3，4，1，2}，q[] = {{0，5}，{1，3}}
> **输出:**
> 否
> 是

一个**简单的解决方案**将是迭代整个范围并计算该范围的**和**。然后，我们将再次遍历整个数组。我们将从索引“L”开始总结元素。如果在任何一步，我们发现当前总和是范围总和的一半，则范围所代表的子阵列可以被分成两个相等的一半。使用这种方法回答查询可能需要多达 O(n)个时间。
更好的解决方案**是使用前缀和数组。首先，我们创建一个 arr 的前缀和数组 **p_arr** 。现在，使用“p_arr”，我们可以在 O(1)时间内确定“L”到“R”范围内所有元素的总和。一旦我们有了我们的和，我们需要确定是否存在从 **L 到 R-1** 的索引‘I’，使得原始数组的 L 到 I 之间的所有数字的和是范围和的一半。为此，我们可以简单地在无序映射中插入前缀和数组“p_arr”中的所有值。** 

> 如果 sum 的值为偶数且图中存在 **p_arr[l-1] + sum/2** ，则数组可以拆分为两个等和的段。

因此，回答查询的时间复杂度变成了 O(1)。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required prefix sum
void prefixSum(int* p_arr, int* arr, int n)
{
    p_arr[0] = arr[0];
    for (int i = 1; i < n; i++)
        p_arr[i] = arr[i] + p_arr[i - 1];
}

// Function to hash all the values of prefix
// sum array in an unordered map
void hashPrefixSum(int* p_arr, int n, unordered_set<int>& q)
{
    for (int i = 0; i < n; i++)
        q.insert(p_arr[i]);
}

// Function to check if a range
// can be divided into two equal parts
void canDivide(int* p_arr, int n,
               unordered_set<int>& q, int l, int r)
{
    // To store the value of sum
    // of entire range
    int sum;

    if (l == 0)
        sum = p_arr[r];
    else
        sum = p_arr[r] - p_arr[l - 1];

    // If value of sum is odd
    if (sum % 2 == 1) {
        cout << "No" << endl;
        return;
    }

    // To store p_arr[l-1]
    int beg = 0;

    if (l != 0)
        beg = p_arr[l - 1];

    // If the value exists in the map
    if (q.find(beg + sum / 2) != q.end())
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // prefix-sum array
    int p_arr[n];

    prefixSum(p_arr, arr, n);

    // Map to store the values of prefix-sum
    unordered_set<int> q;

    hashPrefixSum(p_arr, n, q);

    // Perform queries
    canDivide(p_arr, n, q, 0, 1);
    canDivide(p_arr, n, q, 1, 3);
    canDivide(p_arr, n, q, 1, 2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

// Function to find the required prefix sum
static void prefixSum(int[] p_arr, int[] arr, int n)
{
    p_arr[0] = arr[0];
    for (int i = 1; i < n; i++)
        p_arr[i] = arr[i] + p_arr[i - 1];
}

// Function to q all the values of prefix
// sum array in an unordered map
static void qPrefixSum(int[]p_arr, int n, HashSet<Integer>q)
{
    for (int i = 0; i < n; i++)
        q.add(p_arr[i]);
}

// Function to check if a range
// can be divided into two equal parts
static void canDivide(int[] p_arr, int n,
               HashSet<Integer>q, int l, int r)
{
    // To store the value of sum
    // of entire range
    int sum;

    if (l == 0)
        sum = p_arr[r];
    else
        sum = p_arr[r] - p_arr[l - 1];

    // If value of sum is odd
    if (sum % 2 == 1) {
        System.out.println("No");
        return;
    }

    // To store p_arr[l-1]
    int beg = 0;

    if (l != 0)
        beg = p_arr[l - 1];

    // If the value exists in the map
    if(q.contains(beg + sum / 2) && (beg + sum / 2)!=(int)q.toArray()[ q.size()-1 ] )
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
 public static void main(String[] args) {
   int arr[] = { 1, 1, 2, 3 };
    int n = arr.length;

    // prefix-sum array
    int p_arr[] = new int[n];

    prefixSum(p_arr, arr, n);

    // Map to store the values of prefix-sum
    HashSet<Integer> q = new HashSet<>();

    qPrefixSum(p_arr, n, q);

    // Perform queries
    canDivide(p_arr, n, q, 0, 1);
    canDivide(p_arr, n, q, 1, 3);
    canDivide(p_arr, n, q, 1, 2);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required prefix Sum
def prefixSum(p_arr, arr, n):

    p_arr[0] = arr[0]
    for i in range(1, n):
        p_arr[i] = arr[i] + p_arr[i - 1]

# Function to hash all the values of
# prefix Sum array in an unordered map
def hashPrefixSum(p_arr, n, q):

    for i in range(n):
        q[p_arr[i]] = 1

# Function to check if a range
# can be divided into two equal parts
def canDivide(p_arr, n, q, l, r):

    # To store the value of Sum
    # of entire range
    Sum = 0

    if (l == 0):
        Sum = p_arr[r]
    else:
        Sum = p_arr[r] - p_arr[l - 1]

    # If value of Sum is odd
    if (Sum % 2 == 1):
        print("No")
        return

    # To store p_arr[l-1]
    beg = 0

    if (l != 0):
        beg = p_arr[l - 1]

    # If the value exists in the map
    if (beg + Sum // 2 in q.keys()):
        print("Yes")
    else:
        print("No")

# Driver code
arr = [1, 1, 2, 3]
n = len(arr)

# prefix-Sum array
p_arr = [0 for i in range(n)]

prefixSum(p_arr, arr, n)

# Map to store the values
# of prefix-Sum
q = dict()

hashPrefixSum(p_arr, n, q)

# Perform queries
canDivide(p_arr, n, q, 0, 1)
canDivide(p_arr, n, q, 1, 3)
canDivide(p_arr, n, q, 1, 2)

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the required prefix sum
static void prefixSum(int[] p_arr, int[] arr, int n)
{
    p_arr[0] = arr[0];
    for (int i = 1; i < n; i++)
        p_arr[i] = arr[i] + p_arr[i - 1];
}

// Function to q all the values of prefix
// sum array in an unordered map
static void qPrefixSum(int[]p_arr, int n, HashSet<int>q)
{
    for (int i = 0; i < n; i++)
        q.Add(p_arr[i]);
}

// Function to check if a range
// can be divided into two equal parts
static void canDivide(int[] p_arr, int n,
            HashSet<int>q, int l, int r)
{
    // To store the value of sum
    // of entire range
    int sum;

    if (l == 0)
        sum = p_arr[r];
    else
        sum = p_arr[r] - p_arr[l - 1];

    // If value of sum is odd
    if (sum % 2 == 1)
    {
        Console.WriteLine("No");
        return;
    }

    // To store p_arr[l-1]
    int beg = 0;

    if (l != 0)
        beg = p_arr[l - 1];

    // If the value exists in the map
    if(q.Contains(beg + sum / 2) )
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 2, 3 };
    int n = arr.Length;

    // prefix-sum array
    int []p_arr = new int[n];

    prefixSum(p_arr, arr, n);

    // Map to store the values of prefix-sum
    HashSet<int> q = new HashSet<int> ();

    qPrefixSum(p_arr, n, q);

    // Perform queries
    canDivide(p_arr, n, q, 0, 1);
    canDivide(p_arr, n, q, 1, 3);
    canDivide(p_arr, n, q, 1, 2);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the required prefix sum
function prefixSum(p_arr, arr, n)
{
    p_arr[0] = arr[0];
    for (var i = 1; i < n; i++)
        p_arr[i] = arr[i] + p_arr[i - 1];
}

// Function to hash all the values of prefix
// sum array in an unordered map
function hashPrefixSum(p_arr, n, q)
{
    for (var i = 0; i < n; i++)
        q.add(p_arr[i]);
}

// Function to check if a range
// can be divided into two equal parts
function canDivide(p_arr, n, q, l, r)
{
    // To store the value of sum
    // of entire range
    var sum;

    if (l == 0)
        sum = p_arr[r];
    else
        sum = p_arr[r] - p_arr[l - 1];

    // If value of sum is odd
    if (sum % 2 == 1) {
        document.write( "No" );
        return;
    }

    // To store p_arr[l-1]
    var beg = 0;

    if (l != 0)
        beg = p_arr[l - 1];

    // If the value exists in the map
    if (q.has((beg + sum / 2)))
        document.write( "Yes<br>" );
    else
        document.write( "No<br>" );
}

// Driver code
var arr = [1, 1, 2, 3 ];
var n = arr.length;

// prefix-sum array
var p_arr = Array(n);
prefixSum(p_arr, arr, n);

// Map to store the values of prefix-sum
var q = new Set();
hashPrefixSum(p_arr, n, q);

// Perform queries
canDivide(p_arr, n, q, 0, 1);
canDivide(p_arr, n, q, 1, 3);
canDivide(p_arr, n, q, 1, 2);

</script>
```

**Output:** 

```
Yes
Yes
No
```