# 最后出现的阵元(最后出现的最早)

> 原文:[https://www . geesforgeks . org/last-seed-array-element-last-appearance-early/](https://www.geeksforgeeks.org/last-seen-array-element-last-appearance-earliest/)

给定一个可能包含重复项的数组，找到最后出现的元素。
**例:**

```
Input :  arr[] = {10, 30, 20, 10, 20}
Output : 30
Explanation: Below are indexes of last
appearances of all elements (0 based indexes)
10 last occurs at index 3
30 last occurs at index 1
20 last occurs at index 2
The element whose last appearance earliest
is 30.

Input : arr[] = {20, 10, 20, 20, 40, 10}
Output : 20
Explanation: 
Explanation: Below are indexes of last
appearances of all elements (0 based indexes)
20 last occurs at index 2
10 last occurs at index 5
40 last occurs at index 4
The element whose last appearance earliest
is 20.
```

一种**天真的方法**是取每个元素，迭代并将其最后一次出现与其他元素进行比较。这需要两个嵌套循环，并且需要 O(n*n)个时间。
一个**有效的方法**是使用哈希。我们将每个元素索引存储在它最后出现的地方，然后遍历所有可能的元素，并打印索引存储最少的元素，因为这将是从左向右遍历时最后看到的元素。

## C++

```
// C++ program to find last seen element in
// an array.
#include <bits/stdc++.h>
using namespace std;

// Returns last seen element in arr[]
int lastSeenElement(int a[], int n)
{
    // Store last occurrence index of
    // every element
    unordered_map<int, int> hash;
    for (int i = 0; i < n; i++)
        hash[a[i]] = i;

    // Find an element in hash with minimum
    // index value
    int res_ind = INT_MAX, res;
    for (auto x : hash)
    {
       if (x.second < res_ind)
       {
            res_ind = x.second;
            res = x.first;
       }
    }

    return res;
}

// driver program
int main()
{
    int a[] = { 2, 1, 2, 2, 4, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << lastSeenElement(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last seen element in
// an array.
import java.util.*;

class GFG
{

// Returns last seen element in arr[]
static int lastSeenElement(int a[], int n)
{
    // Store last occurrence index of
    // every element
    HashMap<Integer,
            Integer> hash = new HashMap<Integer,       
                                        Integer>();
    for (int i = 0; i < n; i++)
    {
        hash.put(a[i], i);
    }

    // Find an element in hash with minimum
    // index value
    int res_ind = Integer.MAX_VALUE, res = 0;
    for (Map.Entry<Integer,
                   Integer> x : hash.entrySet())
    {
        if (x.getValue() < res_ind)
        {
            res_ind = x.getValue();
            res = x.getKey();
        }  
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 2, 1, 2, 2, 4, 1 };
    int n = a.length;
    System.out.println(lastSeenElement(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find last seen
# element in an array.
import sys;

# Returns last seen element in arr[]
def lastSeenElement(a, n):

    # Store last occurrence index of
    # every element
    hash = {}

    for i in range(n):
        hash[a[i]] = i

    # Find an element in hash with minimum
    # index value
    res_ind = sys.maxsize
    res = 0

    for x, y in hash.items():
        if y < res_ind:
            res_ind = y
            res = x

    return res

# Driver code   
if __name__=="__main__":

    a = [ 2, 1, 2, 2, 4, 1 ]
    n = len(a)

    print(lastSeenElement(a,n))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find last seen element in
// an array.
using System;
using System.Collections.Generic;

class GFG
{

// Returns last seen element in arr[]
static int lastSeenElement(int []a, int n)
{
    // Store last occurrence index of
    // every element
    Dictionary<int,
               int> hash = new Dictionary<int,
                                          int>();
    for (int i = 0; i < n; i++)
    {
        if(hash.ContainsKey(a[i]))
        {
            hash[a[i]] = i;
        }
        else
        {
            hash.Add(a[i], i);
        }
    }

    // Find an element in hash with minimum
    // index value
    int res_ind = int.MaxValue, res = 0;
    foreach(KeyValuePair<int, int> x in hash)
    {
        if (x.Value < res_ind)
        {
            res_ind = x.Value;
            res = x.Key;
        }
    }
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 2, 1, 2, 2, 4, 1 };
    int n = a.Length;
    Console.WriteLine(lastSeenElement(a, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find last seen element in
// an array.

// Returns last seen element in arr[]
function lastSeenElement(a, n)
{
    // Store last occurrence index of
    // every element
    let hash = new Map();
    for (let i = 0; i < n; i++)
    {
        hash.set(a[i], i);
    }

    // Find an element in hash with minimum
    // index value
    let res_ind = Number.MAX_SAFE_INTEGER, res = 0;
    for (let x of hash)
    {
        if (x[1] < res_ind)
        {
            res_ind = x[1];
            res = x[0];
        }
    }
    return res;
}

// Driver Code

    let a = [ 2, 1, 2, 2, 4, 1 ];
    let n = a.length;
    document.write(lastSeenElement(a, n));

// This code is contributed by gfgking

</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n)

**辅助空间:** O(n)