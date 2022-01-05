# 找到数组中除 Ai 以外的最大元素

> 原文:[https://www . geesforgeks . org/find-数组中最大元素非 ai/](https://www.geeksforgeeks.org/find-the-maximum-element-in-the-array-other-than-ai/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是为从 **1** 到 **N** 的每个 **i** 找到**N–1**元素中除**arr【I】**以外的最大元素。
**举例:**

> **输入:** arr[] = {2，5，6，1，3}
> **输出:**6 6 5 6
> T6】输入: arr[] = {1，2，3}
> **输出:** 3 3 2

**方法:**一种有效的方法是制作最大元素的前缀和后缀数组，并在除**arr【I】**之外的**N–1**元素中找到最大元素。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum element
// among (N - 1) elements other than
// a[i] for each i from 1 to N
int max_element(int a[], int n)
{
    // To store prefix max element
    int pre[n];

    pre[0] = a[0];
    for (int i = 1; i < n; i++)
        pre[i] = max(pre[i - 1], a[i]);

    // To store suffix max element
    int suf[n];

    suf[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suf[i] = max(suf[i + 1], a[i]);

    // Find the maximum element
    // in the array other than a[i]
    for (int i = 0; i < n; i++) {
        if (i == 0)
            cout << suf[i + 1] << " ";

        else if (i == n - 1)
            cout << pre[i - 1] << " ";

        else
            cout << max(pre[i - 1], suf[i + 1]) << " ";
    }
}

// Driver code
int main()
{
    int a[] = { 2, 5, 6, 1, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    max_element(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find maximum element
// among (N - 1) elements other than
// a[i] for each i from 1 to N
static void max_element(int a[], int n)
{
    // To store prefix max element
    int []pre = new int[n];

    pre[0] = a[0];
    for (int i = 1; i < n; i++)
        pre[i] = Math.max(pre[i - 1], a[i]);

    // To store suffix max element
    int []suf = new int[n];

    suf[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suf[i] = Math.max(suf[i + 1], a[i]);

    // Find the maximum element
    // in the array other than a[i]
    for (int i = 0; i < n; i++)
    {
        if (i == 0)
            System.out.print(suf[i + 1] + " ");

        else if (i == n - 1)
            System.out.print(pre[i - 1] + " ");

        else
            System.out.print(Math.max(pre[i - 1],
                              suf[i + 1]) + " ");
    }
}

// Driver code
public static void main(String []args)
{
    int a[] = { 2, 5, 6, 1, 3 };
    int n = a.length;

    max_element(a, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find maximum element
# among (N - 1) elements other than
# a[i] for each i from 1 to N
def max_element(a, n) :

    # To store prefix max element
    pre = [0] * n;

    pre[0] = a[0];
    for i in range(1, n) :
        pre[i] = max(pre[i - 1], a[i]);

    # To store suffix max element
    suf = [0] * n;

    suf[n - 1] = a[n - 1];
    for i in range(n - 2, -1, -1) :
        suf[i] = max(suf[i + 1], a[i]);

    # Find the maximum element
    # in the array other than a[i]
    for i in range(n) :
        if (i == 0) :
            print(suf[i + 1], end = " ");

        elif (i == n - 1) :
            print(pre[i - 1], end = " ");

        else :
            print(max(pre[i - 1],
                      suf[i + 1]), end = " ");

# Driver code
if __name__ == "__main__" :

    a = [ 2, 5, 6, 1, 3 ];
    n = len(a);

    max_element(a, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find maximum element
// among (N - 1) elements other than
// a[i] for each i from 1 to N
static void max_element(int []a, int n)
{
    // To store prefix max element
    int []pre = new int[n];

    pre[0] = a[0];
    for (int i = 1; i < n; i++)
        pre[i] = Math.Max(pre[i - 1], a[i]);

    // To store suffix max element
    int []suf = new int[n];

    suf[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suf[i] = Math.Max(suf[i + 1], a[i]);

    // Find the maximum element
    // in the array other than a[i]
    for (int i = 0; i < n; i++)
    {
        if (i == 0)
            Console.Write(suf[i + 1] + " ");

        else if (i == n - 1)
            Console.Write(pre[i - 1] + " ");

        else
            Console.Write(Math.Max(pre[i - 1],
                           suf[i + 1]) + " ");
    }
}

// Driver code
public static void Main(String []args)
{
    int []a = { 2, 5, 6, 1, 3 };
    int n = a.Length;

    max_element(a, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find maximum element
// among (N - 1) elements other than
// a[i] for each i from 1 to N
function max_element(a, n)
{

    // To store prefix max element
    let pre = new Array(n);

    pre[0] = a[0];
    for (let i = 1; i < n; i++)
        pre[i] = Math.max(pre[i - 1], a[i]);

    // To store suffix max element
    let suf = new Array(n);

    suf[n - 1] = a[n - 1];
    for (let i = n - 2; i >= 0; i--)
        suf[i] = Math.max(suf[i + 1], a[i]);

    // Find the maximum element
    // in the array other than a[i]
    for (let i = 0; i < n; i++) {
        if (i == 0)
            document.write(suf[i + 1] + " ");

        else if (i == n - 1)
            document.write(pre[i - 1] + " ");

        else
            document.write(Math.max(pre[i - 1], suf[i + 1]) + " ");
    }
}

// Driver code
let a = [2, 5, 6, 1, 3];
let n = a.length;
max_element(a, n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
6 6 5 6 6
```