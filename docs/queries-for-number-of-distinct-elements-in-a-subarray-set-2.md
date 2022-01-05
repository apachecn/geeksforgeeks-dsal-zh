# 查询子阵列中不同元素的数量|集合 2

> 原文:[https://www . geesforgeks . org/query-for-number-of-distinct-elements-in-a-subarray-set-2/](https://www.geeksforgeeks.org/queries-for-number-of-distinct-elements-in-a-subarray-set-2/)

给定一个由 **N** 整数和 **Q** 查询组成的数组 **arr[]** 。每个查询可以用两个整数 **L** 和 **R** 来表示。任务是找到子阵列**arr【L】**到**arr【R】**中不同整数的计数。
**示例:**

> **输入:** arr[] = {1，1，3，3，5，5，7，7，9，9 }，L = 0，R = 4
> **输出:** 3
> **输入:** arr[] = { 1，1，2，1，3 }，L = 1，R = 3
> **输出:** 2

**天真的方法:**在这种方法中，我们将遍历范围 l，r，并使用一个集合来查找范围中所有不同的元素并打印它们。
**时间复杂度:** O(q*n)
**高效方法:**思路是形成[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，其中节点将存储范围内所有不同的元素。为此，我们可以在 C++中使用自平衡 BST 或“set”数据结构。
每个查询都会返回集合的大小。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Each segment of the segment tree would be a set
// to maintain distinct elements
set<int>* segment;

// Build the segment tree
// i denotes current node, s denotes start and
// e denotes the end of range for current node
void build(int i, int s, int e, int arr[])
{

    // If start is equal to end then
    // insert the array element
    if (s == e) {
        segment[i].insert(arr[s]);
        return;
    }

    // Else divide the range into two halves
    // (start to mid) and (mid+1 to end)
    // first half will be the left node
    // and the second half will be the right node
    build(2 * i, s, (s + e) / 2, arr);
    build(1 + 2 * i, 1 + (s + e) / 2, e, arr);

    // Insert the sets of right and left
    // node of the segment tree
    segment[i].insert(segment[2 * i].begin(),
                      segment[2 * i].end());

    segment[i].insert(segment[2 * i + 1].begin(),
                      segment[2 * i + 1].end());
}

// Query in an range a to b
set<int> query(int node, int l, int r, int a, int b)
{
    set<int> left, right, result;

    // If the range is out of the bounds
    // of this segment
    if (b < l || a > r)
        return result;

    // If the range lies in this segment
    if (a <= l && r <= b)
        return segment[node];

    // Else query for the right and left
    // leaf node of this subtree
    // and insert them into the set
    left = query(2 * node, l, (l + r) / 2, a, b);
    result.insert(left.begin(), left.end());

    right = query(1 + 2 * node, 1 + (l + r) / 2, r, a, b);
    result.insert(right.begin(), right.end());

    // Return the result
    return result;
}

// Initialize the segment tree
void init(int n)
{
    // Get the height of the segment tree
    int h = (int)ceil(log2(n));
    h = (2 * (pow(2, h))) - 1;

    // Initialize the segment tree
    segment = new set<int>[h];
}

// Function to get the result for the
// subarray from arr[l] to arr[r]
void getDistinct(int l, int r, int n)
{
    // Query for the range set
    set<int> ans = query(1, 0, n - 1, l, r);

    cout << ans.size() << endl;
}

// Driver code
int main()
{

    int arr[] = { 1, 1, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    init(n);

    // Build the segment tree
    build(1, 0, n - 1, arr);

    // Query in range 0 to 4
    getDistinct(0, 4, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Each segment of the segment tree would be a set
    // to maintain distinct elements
    static HashSet<Integer>[] segment;

    // Build the segment tree
    // i denotes current node, s denotes start and
    // e denotes the end of range for current node
    static void build(int i, int s, int e, int[] arr)
    {

        // If start is equal to end then
        // insert the array element
        if (s == e)
        {
            segment[i].add(arr[s]);
            return;
        }

        // Else divide the range into two halves
        // (start to mid) and (mid+1 to end)
        // first half will be the left node
        // and the second half will be the right node
        build(2 * i, s, (s + e) / 2, arr);
        build(1 + 2 * i, 1 + (s + e) / 2, e, arr);

        // Insert the sets of right and left
        // node of the segment tree
        segment[i].addAll(segment[2 * i]);
        segment[i].addAll(segment[2 * i + 1]);
    }

    // Query in an range a to b
    static HashSet<Integer> query(int node, int l,
                                int r, int a, int b)
    {
        HashSet<Integer> left = new HashSet<>();
        HashSet<Integer> right = new HashSet<>();
        HashSet<Integer> result = new HashSet<>();

        // If the range is out of the bounds
        // of this segment
        if (b < l || a > r)
            return result;

        // If the range lies in this segment
        if (a <= l && r <= b)
            return segment[node];

        // Else query for the right and left
        // leaf node of this subtree
        // and insert them into the set
        left = query(2 * node, l, (l + r) / 2, a, b);
        result.addAll(left);

        right = query(1 + 2 * node, 1 + (l + r) / 2, r, a, b);
        result.addAll(right);

        // Return the result
        return result;
    }

    // Initialize the segment tree
    @SuppressWarnings("unchecked")
    static void init(int n)
    {

        // Get the height of the segment tree
        int h = (int) Math.ceil(Math.log(n) / Math.log(2));
        h = (int) (2 * Math.pow(2, h)) - 1;

        // Initialize the segment tree
        segment = new HashSet[h];
        for (int i = 0; i < h; i++)
            segment[i] = new HashSet<>();
    }

    // Function to get the result for the
    // subarray from arr[l] to arr[r]
    static void getDistinct(int l, int r, int n)
    {

        // Query for the range set
        HashSet<Integer> ans = query(1, 0, n - 1, l, r);

        System.out.println(ans.size());
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 1, 2, 1, 3 };
        int n = arr.length;

        init(n);

        // Build the segment tree
        build(1, 0, n - 1, arr);

        // Query in range 0 to 4
        getDistinct(0, 4, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# python3 implementation of above approach
from math import ceil,log,floor

# Each segment of the segment tree would be a set
# to maintain distinct elements
segment=[[] for i in range(1000)]

# Build the segment tree
# i denotes current node, s denotes start and
# e denotes the end of range for current node
def build(i, s, e, arr):

    # If start is equal to end then
    # append the array element
    if (s == e):
        segment[i].append(arr[s])
        return

    # Else divide the range into two halves
    # (start to mid) and (mid+1 to end)
    # first half will be the left node
    # and the second half will be the right node
    build(2 * i, s, (s + e) // 2, arr)
    build(1 + 2 * i, 1 + (s + e) // 2, e, arr)

    # Insert the sets of right and left
    # node of the segment tree
    segment[i].append(segment[2 * i])

    segment[i].append(segment[2 * i + 1])

# Query in an range a to b
def query(node, l, r, a, b):
    left, right, result=[],[],[]

    # If the range is out of the bounds
    # of this segment
    if (b < l or a > r):
        return result

    # If the range lies in this segment
    if (a <= l and r <= b):
        return segment[node]

    # Else query for the right and left
    # leaf node of this subtree
    # and append them into the set
    left = query(2 * node, l, (l + r) // 2, a, b)
    result.append(left)

    right = query(1 + 2 * node, 1 + (l + r) // 2, r, a, b)
    result.append(right)

    # Return the result
    return result
def answer(ans):
    d = {}
    for i in str(ans):
        if i not in ['[',',',']',' ']:
            d[i]=1
    return len(d)

# Initialize the segment tree
def init(n):

    # Get the height of the segment tree
    h = ceil(log(n, 2))
    h = (2 * (pow(2, h))) - 1

# Function to get the result for the
# subarray from arr[l] to arr[r]
def getDistinct(l, r, n):

    # Query for the range set
    ans = query(1, 0, n - 1, l, r)

    print(answer(str(ans)))

# Driver code
arr=[1, 1, 2, 1, 3]
n = len(arr)

init(n)

# Build the segment tree
build(1, 0, n - 1, arr)

# Query in range 0 to 4
getDistinct(0, 4, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG{

// Each segment of the segment
// tree would be a set to maintain
// distinct elements
static HashSet<int>[] segment;

// Build the segment tree
// i denotes current node,
// s denotes start and
// e denotes the end of
// range for current node
static void build(int i, int s,
                  int e, int[] arr)
{
  // If start is equal to end then
  // insert the array element
  if (s == e)
  {
    segment[i].Add(arr[s]);
    return;
  }

  // Else divide the range
  // into two halves (start
  // to mid) and (mid+1 to end)
  // first half will be the left
  // node and the second half
  // will be the right node
  build(2 * i, s,
        (s + e) / 2, arr);
  build(1 + 2 * i,
        1 + (s + e) / 2,
        e, arr);

  // Insert the sets of
  // right and left node
  // of the segment tree
  foreach(int x in segment[2 * i])
  {
    segment[i].Add(x);   
  }

  foreach(int x in segment[2 * i + 1])
  {
    segment[i].Add(x);   
  }
}

// Query in an range a to b
static HashSet<int> query(int node, int l,
                          int r, int a, int b)
{
  HashSet<int> left = new HashSet<int>();
  HashSet<int> right = new HashSet<int>();
  HashSet<int> result = new HashSet<int>();

  // If the range is out
  // of the bounds
  // of this segment
  if (b < l || a > r)
    return result;

  // If the range lies
  // in this segment
  if (a <= l && r <= b)
    return segment[node];

  // Else query for the right and left
  // leaf node of this subtree
  // and insert them into the set
  left = query(2 * node,
               l, (l + r) / 2,
               a, b);
  foreach(int x in left)
  {
    result.Add(x);   
  }

  right = query(1 + 2 * node,
                1 + (l + r) / 2,
                r, a, b);
  foreach(int x in right)
  {
    result.Add(x);   
  }

  // Return the result
  return result;
}

// Initialize the segment tree
static void init(int n)
{

  // Get the height of the segment tree
  int h = (int) Math.Ceiling(Math.Log(n) /
                             Math.Log(2));
  h = (int) (2 * Math.Pow(2, h)) - 1;

  // Initialize the segment tree
  segment = new HashSet<int>[h];

  for (int i = 0; i < h; i++)
    segment[i] = new HashSet<int>();
}

// Function to get the result for the
// subarray from arr[l] to arr[r]
static void getDistinct(int l,
                        int r, int n)
{
  // Query for the range set
  HashSet<int> ans = query(1, 0,
                           n - 1,
                           l, r);

  Console.Write(ans.Count);
}

// Driver Code
public static void Main(string[] args)
{
  int[] arr = {1, 1, 2, 1, 3};
  int n = arr.Length;
  init(n);

  // Build the segment tree
  build(1, 0, n - 1, arr);

  // Query in range 0 to 4
  getDistinct(0, 4, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Each segment of the segment tree would be a set
    // to maintain distinct elements
let segment;

 // Build the segment tree
    // i denotes current node, s denotes start and
    // e denotes the end of range for current node
function build(i,s,e,arr)
{
    // If start is equal to end then
        // insert the array element
        if (s == e)
        {
            segment[i].push(arr[s]);
            return;
        }

        // Else divide the range into two halves
        // (start to mid) and (mid+1 to end)
        // first half will be the left node
        // and the second half will be the right node
        build(2 * i, s, Math.floor((s + e) / 2), arr);
        build(1 + 2 * i, 1 + Math.floor((s + e) / 2), e, arr);

        // Insert the sets of right and left
        // node of the segment tree
        segment[i].push(segment[2 * i]);
        segment[i].push(segment[2 * i + 1]);
}

// Query in an range a to b
function query(node,l,r,a,b)
{
     let left = [];
        let right = [];
        let result = [];

        // If the range is out of the bounds
        // of this segment
        if (b < l || a > r)
            return result;

        // If the range lies in this segment
        if (a <= l && r <= b)
            return segment[node];

        // Else query for the right and left
        // leaf node of this subtree
        // and insert them into the set
        left = query(2 * node, l, Math.floor((l + r) / 2), a, b);
        result.push(left);

        right = query(1 + 2 * node, 1 + Math.floor((l + r) / 2), r, a, b);
        result.push(right);

        // Return the result
        return result;
}

// Initialize the segment tree
function init(n)
{
    // Get the height of the segment tree
        let h = Math.floor( Math.ceil(Math.log(n) / Math.log(2)));
        h = Math.floor (2 * Math.pow(2, h)) - 1;

        // Initialize the segment tree
        segment = new Array(h);
        for (let i = 0; i < h; i++)
            segment[i] = [];
}

// Function to get the result for the
    // subarray from arr[l] to arr[r]
function getDistinct(l,r,n)
{
    // Query for the range set
        let ans = query(1, 0, n - 1, l, r);
        ans=ans.join("")   
        let answer=new Set();
        for(let i=0;i<ans.length;i++)
        {
            if(!['[',',',']',' '].includes(ans[i]))
                answer.add(ans[i]);

        }
        document.write(answer.size)

}

 // Driver Code
 let arr=[1, 1, 2, 1, 3];
 let n = arr.length;
 init(n);

        // Build the segment tree
        build(1, 0, n - 1, arr);

        // Query in range 0 to 4
        getDistinct(0, 4, n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(q*n*log(n))