# 使用 Map

查找一个数组是否是另一个数组的子集

> 原文:[https://www . geeksforgeeks . org/find-一个数组是否是另一个数组的子集-使用-map/](https://www.geeksforgeeks.org/find-whether-an-array-is-subset-of-another-array-using-map/)

给定两个数组:arr1[0..m-1]和 arr2[0..n-1]。查找 arr2[]是否是 arr1[]的子集。两个数组都不是按排序顺序排列的。可以假设两个数组中的元素是不同的。
**例:**

```
Input: arr1[] = {11, 1, 13, 21, 3, 7},  arr2[] = {11, 3, 7, 1}
Output: arr2[] is a subset of arr1[]

Input: arr1[] = {1, 2, 3, 4, 5, 6},  arr2[] = {1, 2, 4}
Output: arr2[] is a subset of arr1[]

Input: arr1[] = {10, 5, 2, 23, 19},  arr2[] = {19, 5, 3}
Output: arr2[] is not a subset of arr1[]
```

**简单方法:**简单的方法是运行两个嵌套循环。外循环逐个挑选 B[]的所有元素。内部循环线性搜索由外部循环在[A]中拾取的元素。如果找到所有元素，则打印是，否则打印否。您可以在此查看解决方案。
**高效方法:**创建一个地图，存储每个不同数字在 A[]中出现的频率。然后我们将检查地图中是否存在每个数字 B[]。如果出现在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，我们会将该数字的频率值减少 1，并检查下一个数字。如果任何数字的地图值变为零，我们将从地图中删除它。如果在地图中找不到任何数量的 B[]，我们将设置标志值并打破循环并打印否。否则，我们将打印是。

## C++

```
// C++ program to check if an array is
// subset of another array

#include <bits/stdc++.h>
using namespace std;

// Function to check if an array is
// subset of another array

int isSubset(int a[], int b[], int m, int n)
{

    // map to store the values of array a[]
    map<int, int> mp1;

    for (int i = 0; i < m; i++)
        mp1[a[i]]++;

    // flag value
    int f = 0;

    for (int i = 0; i < n; i++) {
        // if b[i] is not present in map
        // then array b[] can not be a
        // subset of array a[]

        if (mp1.find(b[i]) == mp1.end()) {
            f = 1;
            break;
        }

        // if if b[i] is present in map
        // decrement by one
        else {
            mp1[b[i]]--;

            if (mp1[b[i]] == 0)
                mp1.erase(mp1.find(b[i]));
        }
    }

    return f;
}

// Driver code
int main()
{
    int arr1[] = { 11, 1, 13, 21, 3, 7 };
    int arr2[] = { 11, 3, 7, 1 };

    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);

    if (!isSubset(arr1, arr2, m, n))
        cout<<"arr2[] is subset of arr1[] ";
    else
        cout<<"arr2[] is not a subset of arr1[]";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if an array is
// subset of another array
import java.util.*;

class GFG
{

    // Function to check if an array is
    // subset of another array
    static int isSubset(int a[], int b[], int m, int n)
    {

        // map to store the values of array a[]
        HashMap<Integer, Integer> mp1 = new
                HashMap<Integer, Integer>();

        for (int i = 0; i < m; i++)
            if (mp1.containsKey(a[i]))
            {
                mp1.put(a[i], mp1.get(a[i]) + 1);
            }
            else
            {
                mp1.put(a[i], 1);
            }

        // flag value
        int f = 0;

        for (int i = 0; i < n; i++)
        {
            // if b[i] is not present in map
            // then array b[] can not be a
            // subset of array a[]
            if (!mp1.containsKey(b[i]))
            {
                f = 1;
                break;
            }

            // if if b[i] is present in map
            // decrement by one
            else
            {
                mp1.put(b[i], mp1.get(b[i]) - 1);

                if (mp1.get(b[i]) == 0)
                    mp1.remove(b[i]);
            }
        }

        return f;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = { 11, 1, 13, 21, 3, 7 };
        int arr2[] = { 11, 3, 7, 1 };

        int m = arr1.length;
        int n = arr2.length;

        if (isSubset(arr1, arr2, m, n)!=1)
            System.out.print("arr2[] is subset of arr1[] ");
        else
            System.out.print("arr2[] is not a subset of arr1[]");
    }
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program to check if an array is
# subset of another array

# Function to check if an array is
# subset of another array
def isSubset(a, b, m, n) :

    # map to store the values of array a
    mp1 = {}
    for i in range(m):
        if a[i] not in mp1:
            mp1[a[i]] = 0
        mp1[a[i]] += 1

    # flag value
    f = 0
    for i in range(n):

        # if b[i] is not present in map
        # then array b can not be a
        # subset of array a
        if b[i] not in mp1:
            f = 1
            break

        # if if b[i] is present in map
        # decrement by one
        else :
            mp1[b[i]] -= 1

            if (mp1[b[i]] == 0):
                mp1.pop(b[i])
    return f

# Driver code
arr1 = [11, 1, 13, 21, 3, 7 ]
arr2 = [11, 3, 7, 1 ]

m = len(arr1)
n = len(arr2)

if (not isSubset(arr1, arr2, m, n)):
    print("arr2[] is subset of arr1[] ")
else:
    print("arr2[] is not a subset of arr1[]")

# This code is contributed by Shubhamsingh10
```

## C#

```
// C# program to check if an array is
// subset of another array
using System;
using System.Collections.Generic;

class GFG
{

    // Function to check if an array is
    // subset of another array
    static int isSubset(int []a, int []b, int m, int n)
    {

        // map to store the values of array []a
        Dictionary<int, int> mp1 = new
                Dictionary<int, int>();

        for (int i = 0; i < m; i++)
            if (mp1.ContainsKey(a[i]))
            {
                mp1[a[i]] = mp1[a[i]] + 1;
            }
            else
            {
                mp1.Add(a[i], 1);
            }

        // flag value
        int f = 0;

        for (int i = 0; i < n; i++)
        {
            // if b[i] is not present in map
            // then array []b can not be a
            // subset of array []a
            if (!mp1.ContainsKey(b[i]))
            {
                f = 1;
                break;
            }

            // if if b[i] is present in map
            // decrement by one
            else
            {
                mp1[b[i]] = mp1[b[i]] - 1;

                if (mp1[b[i]] == 0)
                    mp1.Remove(b[i]);
            }
        }

        return f;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr1 = {11, 1, 13, 21, 3, 7};
        int []arr2 = {11, 3, 7, 1};

        int m = arr1.Length;
        int n = arr2.Length;

        if (isSubset(arr1, arr2, m, n) != 1)
            Console.Write("arr2[] is subset of arr1[] ");
        else
            Console.Write("arr2[] is not a subset of arr1[]");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to check if an array is
// subset of another array

// Function to check if an array is
// subset of another array

function isSubset(a, b, m, n) {

    // map to store the values of array a[]
    let mp = new Map();

    for (let i = 0; i < m; i++) {
         if (mp.has(a[i])) {
            mp.set(a[i], mp.get(a[i]) + 1)
        } else {
            mp.set(a[i], 1)
        }
    }

    // flag value
    let f = 0;

    for (let i = 0; i < n; i++) {
        // if b[i] is not present in map
        // then array b[] can not be a
        // subset of array a[]

        if (!mp.has(b[i])) {
            f = 1;
            break;
        }

        // if if b[i] is present in map
        // decrement by one
        else {
            mp.set(b[i], mp.get(b[i]) - 1);

            if (mp.get(b[i]) == 0)
                mp.delete(b[i]);
        }
    }

    return f;
}

// Driver code

let arr1 = [11, 1, 13, 21, 3, 7];
let arr2 = [11, 3, 7, 1];

let m = arr1.length;
let n = arr2.length;

if (!isSubset(arr1, arr2, m, n))
    document.write("arr2[] is subset of arr1[] ");
else
    document.write("arr2[] is not a subset of arr1[]");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
arr2[] is subset of arr1[]
```

**时间复杂度:** O (n)