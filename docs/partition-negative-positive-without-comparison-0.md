# 划分正负，不与 0 比较

> 原文:[https://www . geesforgeks . org/partition-negative-positive-不带比较-0/](https://www.geeksforgeeks.org/partition-negative-positive-without-comparison-0/)

给定一个 n 个整数的数组，包括负数和正数，将它们分成两个不同的数组，不要将任何元素与 0 进行比较。

**示例:**

```
Input : arr[] = [1, -2, 6, -7, 8]
Output : a[] = [1, 6, 8] 
         b[] = [-2, -7]
```

**算法:**

1.  初始化两个空向量。将数组的第一个元素推入两个向量中的任何一个。假设第一个向量。让它用 x 表示。
2.  对于每隔一个元素，arr[1]到 arr[n-1]，检查它的符号和 x 的符号是否相同。如果符号相同，则将元素推入同一向量。否则，将元素推入另一个向量。
3.  完成两个向量的遍历后，打印两个向量。

如何检查它们的标志是否相反？
让检查的整数用 x 和 y 表示，负数的符号位是 1，正数的符号位是 0。当且仅当 x 和 y 的符号相反时，它们的异或符号位为 1。换句话说，当且仅当 x 和 y 符号相反时，x 和 y 的异或将是负数。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to rearrange positive and
// negative numbers without comparison
// with 0.
#include <bits/stdc++.h>
using namespace std;

bool oppositeSigns(int x, int y)
{
    return ((x ^ y) < 0);
}

void partitionNegPos(int arr[], int n)
{
    vector<int> a, b;

    // Push first element to a.
    a.push_back(arr[0]);

    // Now put all elements of same sign
    // in a[] and opposite sign in b[]
    for (int i = 1; i < n; i++) {
        if (oppositeSigns(a[0], arr[i]))
            b.push_back(arr[i]);
        else
            a.push_back(arr[i]);
    }

    // Print a[] and b[]
    for (int i = 0; i < a.size(); i++)
        cout << a[i] << ' ';
    cout << '\n';
    for (int i = 0; i < b.size(); i++)
        cout << b[i] << ' ';
}

int main()
{
    int arr[] = { 1, -2, 6, -7, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    partitionNegPos(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange positive and
// negative numbers without comparison
// with 0.
import java.util.*;

class GFG
{

static boolean oppositeSigns(int x, int y)
{
    return ((x ^ y) < 0);
}

static void partitionNegPos(int arr[], int n)
{
    Vector<Integer> a = new Vector<Integer>();
    Vector<Integer> b = new Vector<Integer>();

    // Push first element to a.
    a.add(arr[0]);

    // Now put all elements of same sign
    // in a[] and opposite sign in b[]
    for (int i = 1; i < n; i++)
    {
        if (oppositeSigns(a.get(0), arr[i]))
            b.add(arr[i]);
        else
            a.add(arr[i]);
    }

    // Print a[] and b[]
    for (int i = 0; i < a.size(); i++)
        System.out.print(a.get(i) + " ");
    System.out.println("");
    for (int i = 0; i < b.size(); i++)
        System.out.print(b.get(i) + " ");
}

public static void main(String[] args)
{
    int arr[] = { 1, -2, 6, -7, 8 };
    int n = arr.length;
    partitionNegPos(arr, n);
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to rearrange positive
# and negative numbers without comparison
# with 0.

def oppositeSigns(x, y):

    return ((x ^ y) < 0)

def partitionNegPos(arr, n):

    a = []
    b = []

    # Push first element to a.
    a = a + [arr[0]]

    # Now put all elements of same sign
    # in a[] and opposite sign in b[]
    for i in range(1, n) :
        if (oppositeSigns(a[0], arr[i])):
            b = b + [arr[i]]
        else:
            a = a + [arr[i]]

    # Print a[] and b[]
    for i in range(0, len(a)):
        print(a[i], end = ' ')
    print("")

    for i in range(0, len(b)):
        print(b[i], end = ' ')

# Driver code
arr = [1, -2, 6, -7, 8 ]
n = len(arr)
partitionNegPos(arr, n)

# This code is contributed by Smitha
```

## C#

```
// C# program to rearrange positive and
// negative numbers without comparison
// with 0.
using System;
using System.Collections.Generic;

class GFG
{

static bool oppositeSigns(int x, int y)
{
    return ((x ^ y) < 0);
}

static void partitionNegPos(int []arr, int n)
{
    List<int> a = new List<int> ();
    List<int> b = new List<int> ();

    // Push first element to a.
    a.Add(arr[0]);

    // Now put all elements of same sign
    // in a[] and opposite sign in b[]
    for (int i = 1; i < n; i++)
    {
        if (oppositeSigns(a[0], arr[i]))
            b.Add(arr[i]);
        else
            a.Add(arr[i]);
    }

    // Print a[] and b[]
    for (int i = 0; i < a.Count; i++)
        Console.Write(a[i] + " ");
    Console.WriteLine("");
    for (int i = 0; i < b.Count; i++)
        Console.Write(b[i] + " ");
}

// Driver code
public static void Main()
{
    int []arr = { 1, -2, 6, -7, 8 };
    int n = arr.Length;
    partitionNegPos(arr, n);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to rearrange positive and
// negative numbers without comparison
// with 0.

function oppositeSigns(x, y)
{
    return ((x ^ y) < 0);
}

function partitionNegPos(arr, n)
{
    var a = [], b = [];

    // Push first element to a.
    a.push(arr[0]);

    // Now put all elements of same sign
    // in a[] and opposite sign in b[]
    for (var i = 1; i < n; i++) {
        if (oppositeSigns(a[0], arr[i]))
            b.push(arr[i]);
        else
            a.push(arr[i]);
    }

    // Print a[] and b[]
    for (var i = 0; i < a.length; i++)
        document.write( a[i] + ' ');
    document.write( "<br>" );
    for (var i = 0; i < b.length; i++)
        document.write( b[i] + ' ');
}

var arr = [1, -2, 6, -7, 8];
var n = arr.length;
partitionNegPos(arr, n);

</script>
```

**输出:**

```
1 6 8
-2 -7
```