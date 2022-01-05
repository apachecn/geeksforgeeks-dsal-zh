# 查询给定范围内是否存在给定数字

> 原文:[https://www . geesforgeks . org/query-to-check-给定范围内是否存在给定数字/](https://www.geeksforgeeks.org/queries-to-check-whether-a-given-digit-is-present-in-the-given-range/)

**先决条件:** [分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

给定一组数字 **arr[]** 。给定一个范围[L，R]和每个范围的一个数字 X。任务是检查每个给定的范围[L，R]中的数字 X 是否出现在数组 arr[]的该范围内。

**示例:**

```
Input : arr = [1, 3, 3, 9, 8, 7]
        l1=0, r1=3, x=2   // Range 1
        l1=2, r1=5, x=3   // Range 2
Output : NO  
         YES
For Range 1: The digit 2 is not present within
             range [0, 3] in the array.
For Range 2: The digit 3 is present within the range
             [2, 5] at index 2 in the given array.

```

**天真方法**:天真方法是遍历数组中每个给定范围的数字，检查数字是否存在。

时间复杂度:每个查询的 O(N)。

**更好的方法**:更好的方法是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。由于从(0-9)开始只有 10 个数字，因此段树的每个节点将包含该节点范围内的所有数字。我们将在每个节点使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)数据结构来存储数字。Set 是一种特殊的数据结构，它删除冗余元素并以升序存储它们。我们使用了集合数据结构，因为合并两个子节点更容易得到段树中的父节点。我们将插入父集中子节点中出现的所有数字，它将自动删除冗余数字。因此，在每个集合(节点)中最多有 10 个元素(0-9 个数字)。

还有内置的计数函数，它返回集合中存在的元素的计数，这将有助于查询函数检查节点上是否存在数字。如果计数大于 0，这意味着元素存在于集合中，我们将返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// CPP program to answer Queries to check whether
// a given digit is present in the given range

#include <bits/stdc++.h>
using namespace std;

#define N 6

// Segment Tree with set at each node
set<int> Tree[6 * N];

// Funtiom to build the segment tree
void buildTree(int* arr, int idx, int s, int e)
{
    if (s == e) {
        Tree[idx].insert(arr[s]);
        return;
    }

    int mid = (s + e) >> 1;

    // Left child node
    buildTree(arr, 2 * idx, s, mid);

    // Right child node
    buildTree(arr, 2 * idx + 1, mid + 1, e);

    // Merging child nodes to get parent node.
    // Since set is used, it will remove
    // redundant digits.
    for (auto it : Tree[2 * idx]) {
        Tree[idx].insert(it);
    }
    for (auto it : Tree[2 * idx + 1]) {
        Tree[idx].insert(it);
    }
}

// Function to query a range
bool query(int idx, int s, int e, int qs, int qe, int x)
{
    // Complete Overlapp condition
    // return true if digit is present.
    // else false.
    if (qs <= s && e <= qe) {
        if (Tree[idx].count(x) != 0) {
            return true;
        }
        else
            return false;
    }

    // No Overlapp condition
    // Return false
    if (qe < s || e < qs) {
        return false;
    }

    int mid = (s + e) >> 1;

    // If digit is found in any child
    // return true, else False
    bool LeftAns = query(2 * idx, s, mid, qs, qe, x);
    bool RightAns = query(2 * idx + 1, mid + 1, e, qs, qe, x);

    return LeftAns or RightAns;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 3, 9, 8, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build the tree
    buildTree(arr, 1, 0, n - 1);

    int l, r, x;

    // Query 1
    l = 0, r = 3, x = 2;
    if (query(1, 0, n - 1, l, r, x))
        cout << "YES" << '\n';
    else
        cout << "NO" << '\n';

    // Query 2
    l = 2, r = 5, x = 3;
    if (query(1, 0, n - 1, l, r, x))
        cout << "YES" << '\n';
    else
        cout << "NO" << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer Queries to check whether 
// a given digit is present in the given range 
import java.io.*;
import java.util.*;

class GFG 
{
    static int N = 6;

    // Segment Tree with set at each node
    @SuppressWarnings("unchecked")
    static HashSet<Integer>[] Tree = new HashSet[6 * N];
    static 
    {
        for (int i = 0; i < 6 * N; i++)
            Tree[i] = new HashSet<>();
    }

    // Funtiom to build the segment tree
    static void buildTree(int[] arr, int idx, int s, int e) 
    {
        if (s == e) 
        {
            Tree[idx].add(arr[s]);
            return;
        }

        int mid = (s + e) / 2;

        // Left child node
        buildTree(arr, 2 * idx, s, mid);

        // Right child node
        buildTree(arr, 2 * idx + 1, mid + 1, e);

        // Merging child nodes to get parent node.
        // Since set is used, it will remove
        // redundant digits.
        for (int it : Tree[2 * idx])
            Tree[idx].add(it);
        for (int it : Tree[2 * idx + 1])
            Tree[idx].add(it);
    }

    // Function to query a range
    static boolean query(int idx, int s, int e,
                        int qs, int qe, int x) 
    {

        // Complete Overlapp condition
        // return true if digit is present.
        // else false.
        if (qs <= s && e <= qe)
        {
            if (Collections.frequency(Tree[idx], x) != 0)
                return true;
            else
                return false;
        }

        // No Overlapp condition
        // Return false
        if (qe < s || e < qs)
            return false;

        int mid = (s + e) / 2;

        // If digit is found in any child
        // return true, else False
        boolean LeftAns = query(2 * idx, s, mid, qs, qe, x);
        boolean RightAns = query(2 * idx + 1, mid + 1, e, qs, qe, x);

        return (LeftAns || RightAns);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 1, 3, 3, 9, 8, 7 };
        int n = arr.length;

        // Build the tree
        buildTree(arr, 1, 0, n - 1);

        int l, r, x;

        // Query 1
        l = 0;
        r = 3;
        x = 2;
        if (query(1, 0, n - 1, l, r, x))
            System.out.println("Yes");
        else
            System.out.println("No");

        // Query 2
        l = 2;
        r = 5;
        x = 3;
        if (query(1, 0, n - 1, l, r, x))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to answer Queries to check whether
# a given digit is present in the given range
N = 6

# Segment Tree with set at each node
Tree = [0] * (6 * N)
for i in range(6 * N):
    Tree[i] = set()

# Funtiom to build the segment tree
def buildTree(arr: list, idx: int,
                   s: int, e: int) -> None:
    global Tree
    if s == e:
        Tree[idx].add(arr[s])
        return

    mid = (s + e) // 2

    # Left child node
    buildTree(arr, 2 * idx, s, mid)

    # Right child node
    buildTree(arr, 2 * idx + 1, mid + 1, e)

    # Merging child nodes to get parent node.
    # Since set is used, it will remove
    # redundant digits.
    for it in Tree[2 * idx]:
        Tree[idx].add(it)

    for it in Tree[2 * idx + 1]:
        Tree[idx].add(it)

# Function to query a range
def query(idx: int, s: int, e: int, 
          qs: int, qe: int, x: int) -> bool:
    global Tree

    # Complete Overlapp condition
    # return true if digit is present.
    # else false.
    if qs <= s and e <= qe:
        if list(Tree[idx]).count(x) != 0:
            return True
        else:
            return False

    # No Overlapp condition
    # Return false
    if qe < s or e < qs:
        return False

    mid = (s + e) // 2

    # If digit is found in any child
    # return true, else False
    leftAns = query(2 * idx, s, mid, qs, qe, x)
    rightAns = query(2 * idx + 1, 
                         mid + 1, e, qs, qe, x)

    return (leftAns or rightAns)

# Driver Code
if __name__ == "__main__":
    arr = [1, 3, 3, 9, 8, 7]
    n = len(arr)

    # Build the tree
    buildTree(arr, 1, 0, n - 1)

    # Query 1
    l = 0
    r = 3
    x = 2
    if query(1, 0, n - 1, l, r, x):
        print("YES")
    else:
        print("NO")

    # Query 2
    l = 2
    r = 5
    x = 3
    if query(1, 0, n - 1, l, r, x):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to answer Queries to check whether 
// a given digit is present in the given range 
using System;
using System.Collections.Generic;

class GFG 
{
    static int N = 6;

    // Segment Tree with set at each node
    static SortedSet<int>[] Tree = new SortedSet<int>[6 * N];

    // Funtiom to build the segment tree
    static void buildTree(int[] arr, int idx, int s, int e) 
    {
        if (s == e) 
        {
            Tree[idx].Add(arr[s]);
            return;
        }

        int mid = (s + e) / 2;

        // Left child node
        buildTree(arr, 2 * idx, s, mid);

        // Right child node
        buildTree(arr, 2 * idx + 1, mid + 1, e);

        // Merging child nodes to get parent node.
        // Since set is used, it will remove
        // redundant digits.
        foreach (int it in Tree[2 * idx])
            Tree[idx].Add(it);
        foreach (int it in Tree[2 * idx + 1])
            Tree[idx].Add(it);
    }

    // Function to query a range
    static bool query(int idx, int s, int e,
                        int qs, int qe, int x) 
    {

        // Complete Overlapp condition
        // return true if digit is present.
        // else false.
        if (qs <= s && e <= qe)
        {
            if (Tree[idx].Contains(x))
                return true;
            else
                return false;
        }

        // No Overlapp condition
        // Return false
        if (qe < s || e < qs)
            return false;

        int mid = (s + e) / 2;

        // If digit is found in any child
        // return true, else False
        bool LeftAns = query(2 * idx, s, mid, qs, qe, x);
        bool RightAns = query(2 * idx + 1, mid + 1, e, qs, qe, x);

        return (LeftAns || RightAns);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        int[] arr = { 1, 3, 3, 9, 8, 7 };
        int n = arr.Length;
        for (int i = 0; i < 6 * N; i++)
            Tree[i] = new SortedSet<int>();

        // Build the tree
        buildTree(arr, 1, 0, n - 1);

        int l, r, x;

        // Query 1
        l = 0;
        r = 3;
        x = 2;
        if (query(1, 0, n - 1, l, r, x))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        // Query 2
        l = 2;
        r = 5;
        x = 3;
        if (query(1, 0, n - 1, l, r, x))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
NO
YES

```

**时间复杂度:** O(N)一次用于构建段树，然后 O(logN)用于每个查询。