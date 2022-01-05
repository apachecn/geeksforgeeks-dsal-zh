# 将数组变成从 1 到 n 的数字排列

> 原文:[https://www . geesforgeks . org/change-array-array-numbers-1-n/](https://www.geeksforgeeks.org/change-array-permutation-numbers-1-n/)

给定一个由 n 个元素组成的数组。我们需要使用数组中的最小替换将数组变成从 1 到 n 的数字排列。
**例:**

```
Input : A[] = {2, 2, 3, 3} 
Output : 2 1 3 4
Explanation:
To make it a permutation of 1 to 4, 1 and 4 are
missing from the array. So replace 2, 3 with 
1 and 4.

Input :  A[] = {1, 3, 2}
Output : 1 3 2

Input : A[] = {10, 1, 2}
Output : 3 1 2

```

**方法:**观察我们不需要改变在[1，n]范围内且不同的数字(只有一次出现)。所以，我们用贪婪的方法。如果我们遇到了以前从未遇到过的数字，并且这个数字在 1 和 n 之间，我们就不改变这个数字。并删除重复的元素，在[1，n]范围内添加缺失的元素。也替换数字，不在范围内。

## C++

```
// CPP program to make a permutation of numbers
// from 1 to n using minimum changes.
#include <bits/stdc++.h>
using namespace std;

void makePermutation(int a[], int n)
{
    // Store counts of all elements.
    unordered_map<int, int> count;
    for (int i = 0; i < n; i++)
        count[a[i]]++;

    int next_missing = 1;
    for (int i = 0; i < n; i++) {
        if (count[a[i]] != 1 || a[i] > n || a[i] < 1) {
            count[a[i]]--;

            // Find next missing element to put
            // in place of current element.
            while (count.find(next_missing) != count.end())
                next_missing++;

            // Replace with next missing and insert the
            // missing element in hash.
            a[i] = next_missing;
            count[next_missing] = 1;
        }
    }
}

// Driver Code
int main()
{
    int A[] = { 2, 2, 3, 3 };
    int n = sizeof(A) / sizeof(A[0]);
    makePermutation(A, n);
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make a permutation of numbers
// from 1 to n using minimum changes.
import java.util.*;

class GFG
{
static void makePermutation(int []a, int n)
{
    // Store counts of all elements.
    HashMap<Integer,
            Integer> count = new HashMap<Integer,
                                         Integer>();
    for (int i = 0; i < n; i++)
    {
        if(count.containsKey(a[i]))
        {
            count.put(a[i], count.get(a[i]) + 1);
        }
        else
        {
            count.put(a[i], 1);
        }
    }

    int next_missing = 1;
    for (int i = 0; i < n; i++)
    {
        if (count.containsKey(a[i]) &&
            count.get(a[i]) != 1 ||
            a[i] > n || a[i] < 1)
        {
            count.put(a[i], count.get(a[i]) - 1);

            // Find next missing element to put
            // in place of current element.
            while (count.containsKey(next_missing))
                next_missing++;

            // Replace with next missing and insert
            // the missing element in hash.
            a[i] = next_missing;
            count. put(next_missing, 1);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 2, 3, 3 };
    int n = A.length;
    makePermutation(A, n);
    for (int i = 0; i < n; i++)
        System.out.print(A[i] + " ");
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 code to make a permutation
# of numbers from 1 to n using
# minimum changes.

def makePermutation (a, n):

    # Store counts of all elements.
    count = dict()
    for i in range(n):
        if count.get(a[i]):
            count[a[i]] += 1
        else:
            count[a[i]] = 1;

    next_missing = 1
    for i in range(n):
        if count[a[i]] != 1 or a[i] > n or a[i] < 1:
            count[a[i]] -= 1

            # Find next missing element to put
            # in place of current element.
            while count.get(next_missing):
                next_missing+=1

            # Replace with next missing and
            # insert the missing element in hash.
            a[i] = next_missing
            count[next_missing] = 1

# Driver Code
A = [ 2, 2, 3, 3 ]
n = len(A)
makePermutation(A, n)

for i in range(n):
    print(A[i], end = " ")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to make a permutation of numbers
// from 1 to n using minimum changes.
using System;
using System.Collections.Generic;

class GFG
{
static void makePermutation(int []a, int n)
{
    // Store counts of all elements.
    Dictionary<int,
               int> count = new Dictionary<int,
                                           int>();
    for (int i = 0; i < n; i++)
    {
        if(count.ContainsKey(a[i]))
        {
            count[a[i]] = count[a[i]] + 1;
        }
        else
        {
            count.Add(a[i], 1);
        }
    }

    int next_missing = 1;
    for (int i = 0; i < n; i++)
    {
        if (count.ContainsKey(a[i]) &&
            count[a[i]] != 1 ||
            a[i] > n || a[i] < 1)
        {
            count[a[i]] = count[a[i]] - 1;

            // Find next missing element to put
            // in place of current element.
            while (count.ContainsKey(next_missing))
                next_missing++;

            // Replace with next missing and insert
            // the missing element in hash.
            a[i] = next_missing;
            count.Add(next_missing, 1);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 2, 3, 3 };
    int n = A.Length;
    makePermutation(A, n);
    for (int i = 0; i < n; i++)
        Console.Write(A[i] + " ");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to make a permutation of numbers
// from 1 to n using minimum changes.

function makePermutation(a, n)
{
    // Store counts of all elements.
    var count = new Map();
    for(var i = 0; i < n; i++)
    {
        if(count.has(a[i]))
            count.set(a[i], count.get(a[i])+1)
        else
            count.set(a[i], 1)
    }

    var next_missing = 1;
    for (var i = 0; i < n; i++) {
        if (count.get(a[i]) != 1 || a[i] > n || a[i] < 1) {

            count.set(a[i], count.get(a[i])-1);

            // Find next missing element to put
            // in place of current element.
            while (count.has(next_missing))
                next_missing++;

            // Replace with next missing and insert the
            // missing element in hash.
            a[i] = next_missing;
            count.set(next_missing,1);
        }
    }
}

// Driver Code

var A = [2, 2, 3, 3];
var n = A.length;
makePermutation(A, n);
for(var i = 0; i < n; i++)
    document.write( A[i] + " ");

</script>
```

**输出:**

```
1 2 4 3
```