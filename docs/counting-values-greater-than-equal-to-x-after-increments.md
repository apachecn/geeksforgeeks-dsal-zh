# 递增后大于等于 x 的计数值

> 原文:[https://www . geesforgeks . org/counting-values-大于等于 x-after-increments/](https://www.geeksforgeeks.org/counting-values-greater-than-equal-to-x-after-increments/)

考虑一个大小为 n、初始值为 0 的数组。在执行 m 范围更新后，有多少索引将包含至少 x 的值？在他们的每个查询中，您都被赋予了一个从 L 到 R 的范围，并且您必须在从 L 到 R(包括 L 和 R)的每个索引中添加 1。现在，给你 q 个查询，每个查询中有一个数字 x。你的任务是找出有多少数组索引大于或等于 x(n，m，q 的值可以达到 10^6)

**例:**

```
Input :  n = 4
         l[] = {1, 1, 3};
         r[] = {3, 2, 4};         
         x[] = {1, 4, 2};
Output :
Number of indexes with atleast 1 is 4
Number of indexes with atleast 4 is 0
Number of indexes with atleast 2 is 3

Explanation :
Initial array is {0, 0, 0, 0}
After first update : {1, 1, 1, 0}
After second update : {2, 2, 1, 0}
After third update : {2, 2, 2, 1} 
```

**天真的方法**:想到的琐碎的解决方案是创建一个大小为 n 的数组，对于每个更新[L，R]，在这个范围内为每个数组索引添加 1。然后，对于每个 x，通过遍历整个数组来计数值大于或等于 x 的索引的数量。然而，我们被告知 n 和 q 的值非常大(直到 10^6)，因此对于每个查询，我们不能简单地遍历数组并找出有多少索引至少有 x 作为它们的值。在最坏的情况下，复杂度为 O(nq)，效率相当低。

**有效方法**:首先通过累加所有增量来计算数组的值(我们使用与[这篇](https://www.geeksforgeeks.org/print-modified-array-executing-commands-addition-subtraction/)文章相同的技术)。在找到元素之后，我们找到每个元素的频率。然后我们通过从右向左遍历来计算更大元素的频率。最后，我们可以在 O(1)时间内回答所有查询。

## c++

```
// C++ code to count element
// with values at least x.
#include<bits/stdc++.h>
using namespace std;

// For every query in x[0..q-1], count of values
// greater than or equal to query value are printed.
void coutIndices(int n, int l[], int r[], int m,
                 int x[], int q)
{
    // Start and end store frequencies of all
    // starting and ending points
    int start[n+1] = {0};
    int End[n+1] = {0};
    for (int i = 0; i < m; i++)
    {
        start[l[i]] += 1;
        End[r[i]] += 1;
    }

    // Find actual array values after m queries
    int compute[n+1] = {0};
    compute[1] = start[1];
    for (int i = 1; i <= n; i++)
        compute[i] =  compute[i - 1] + start[i] -
                      End[i - 1];

    // Find frequency of every element in compute[]
    int max = *max_element(compute, compute+n+1);
    int freq[max+1] = {0};
    for (int i=1; i<=n; i++)
        freq[compute[i]]++;

    // reverse cumulative sum of the freq array
    // because of atleast value of array
    // indices for each possible x
    for (int i = max-1; i >= 0; i--)
        freq[i] += freq[i + 1];

    // Solving queries
    for (int i = 0; i < q; i++)
    {
        cout << "number of indexes with atleast " <<
             x[i] << " is ";
        if (x[i] > max)
            cout << 0 << "\n";
        else
            cout << freq[x[i]] << endl;
    }
}

// Driver code
int main()
{
    // Number of elements in an array
    // with all initial 0 values
    int n = 7;

    // Subarrays that need to be incremented
    int l[] = {1, 2, 1, 5};
    int r[] = {3, 5, 2, 6};

    // Query values
    int x[] = {1, 7, 4, 2};

    int m = sizeof(l)/sizeof(l[0]);
    int q = sizeof(x)/sizeof(x[0]);
    coutIndices(n, l, r, m, x, q);

    return 0;
}
```

## Java

```
// Java code to count element
// with values at least x.
import java.io.*;
import java.util.*;

class GFG
{

// For every query in x[0..q-1],
// count of values greater than
// or equal to query value are
// printed.
static void coutIndices(int n, int l[],
                        int r[], int m,
                        int x[], int q)
{
    // Start and end store
    // frequencies of all
    // starting and ending points
    int []start = new int[n + 1];
    int End[] = new int[n + 1];

    for (int i = 0; i < m; i++)
    {
        start[l[i]] += 1;
        End[r[i]] += 1;
    }

    // Find actual array
    // values after m queries
    int compute[] = new int[n + 1];
    compute[1] = start[1];
    for (int i = 1; i <= n; i++)
        compute[i] = compute[i - 1] +
                           start[i] -
                           End[i - 1];

    // Find frequency of every
    // element in compute[]
    Arrays.sort(compute);
    int max = compute[n];
    int freq[] = new int[max + 1];

    for (int i = 1; i <= n; i++)
        freq[compute[i]]++;

    // reverse cumulative sum of
    // the freq array because of
    // atleast value of array
    // indices for each possible x
    for (int i = max - 1; i >= 0; i--)
        freq[i] += freq[i + 1];

    // Solving queries
    for (int i = 0; i < q; i++)
    {
        System.out.print("number of indexes " +
                               "with atleat " +
                                x[i] + " is ");
        if (x[i] > max)
            System.out.println("0");
        else
            System.out.println(freq[x[i]]);
    }
}

// Driver code
public static void main (String[] args)
{

// Number of elements in
// an array with all
// initial 0 values
int n = 7;

// Subarrays that need
// to be incremented
int l[] = {1, 2, 1, 5};
int r[] = {3, 5, 2, 6};

// Query values
int x[] = {1, 7, 4, 2};

int m = l.length;
int q = x.length;
coutIndices(n, l, r, m, x, q);
}
}

// This code has been
// contributed by anuj_67.
```

## python 3

T2

## c#

```
// C# code to count element
// with values at least x.
using System;

class GFG
{

// For every query in x[0..q-1],
// count of values greater than
// or equal to query value are
// printed.
static void coutIndices(int n, int []l,
                        int []r, int m,
                        int []x, int q)
{
    // Start and end store
    // frequencies of all
    // starting and ending points
    int []start = new int[n + 1];
    int []End = new int[n + 1];

    for (int i = 0; i < m; i++)
    {
        start[l[i]] += 1;
        End[r[i]] += 1;
    }

    // Find actual array
    // values after m queries
    int []compute = new int[n + 1];
    compute[1] = start[1];
    for (int i = 1; i <= n; i++)
        compute[i] = compute[i - 1] +
                       start[i] -
                         End[i - 1];

    // Find frequency of every
    // element in compute[]
    Array.Sort(compute);
    int max = compute[n];
    int []freq = new int[max + 1];

    for (int i = 1; i <= n; i++)
        freq[compute[i]]++;

    // reverse cumulative sum of
    // the freq array because of
    // atleast value of array
    // indices for each possible x
    for (int i = max - 1; i >= 0; i--)
        freq[i] += freq[i + 1];

    // Solving queries
    for (int i = 0; i < q; i++)
    {
        Console.Write("number of indexes " +
                            "with atleat " +
                             x[i] + " is ");
        if (x[i] > max)
            Console.WriteLine("0");
        else
            Console.WriteLine(freq[x[i]]);
    }
}

// Driver code
public static void Main ()
{

// Number of elements in
// an array with all
// initial 0 values
int n = 7;

// Subarrays that need
// to be incremented
int []l = {1, 2, 1, 5};
int []r = {3, 5, 2, 6};

// Query values
int []x = {1, 7, 4, 2};

int m = l.Length;
int q = x.Length;
coutIndices(n, l, r, m, x, q);
}
}

// This code has been
// contributed by anuj_67.
```

## Javascript

```
<script>
    // Javascript code to count element with values at least x.

    // For every query in x[0..q-1],
    // count of values greater than
    // or equal to query value are
    // printed.
    function coutIndices(n, l, r, m, x, q)
    {
        // Start and end store
        // frequencies of all
        // starting and ending points
        let start = new Array(n + 1);
        start.fill(0);
        let End = new Array(n + 1);
        End.fill(0);

        for (let i = 0; i < m; i++)
        {
            start[l[i]] += 1;
            End[r[i]] += 1;
        }

        // Find actual array
        // values after m queries
        let compute = new Array(n + 1);
        compute.fill(0);
        compute[1] = start[1];
        for (let i = 1; i <= n; i++)
            compute[i] = compute[i - 1] +
                           start[i] -
                             End[i - 1];

        // Find frequency of every
        // element in compute[]
        compute.sort();
        let max = compute[n];
        let freq = new Array(max + 1);
        freq.fill(0);

        for (let i = 1; i <= n; i++)
            freq[compute[i]]++;

        // reverse cumulative sum of
        // the freq array because of
        // atleast value of array
        // indices for each possible x
        for (let i = max - 1; i >= 0; i--)
            freq[i] += freq[i + 1];

        // Solving queries
        for (let i = 0; i < q; i++)
        {
            document.write("number of indexes " +
                                "with atleast " +
                                 x[i] + " is ");
            if (x[i] > max)
                document.write("0" + "</br>");
            else
                document.write(freq[x[i]] + "</br>");
        }
    }

    // Number of elements in
    // an array with all
    // initial 0 values
    let n = 7;

    // Subarrays that need
    // to be incremented
    let l = [1, 2, 1, 5];
    let r = [3, 5, 2, 6];

    // Query values
    let x = [1, 7, 4, 2];

    let m = l.length;
    let q = x.length;
    coutIndices(n, l, r, m, x, q);

</script>
```

T30】

**输出:**

```
number of indexes with atleast 1 is 6
number of indexes with atleast 7 is 0
number of indexes with atleast 4 is 0
number of indexes with atleast 2 is 4
```