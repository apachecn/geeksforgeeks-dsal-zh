# 检查是否可以通过双倍或三倍

使数组相等

> 原文:[https://www . geesforgeks . org/check-可能-使-数组-相等-加倍-加倍/](https://www.geeksforgeeks.org/check-possible-make-array-equal-doubling-tripling/)

给定 n 个元素的数组。您可以将数组中的元素增加两倍或三倍任意次数。完成所有操作后，检查是否有可能使数组中的所有元素相等。

**例:**

```
Input : A[] = {75, 150, 75, 50}
Output : Yes
Explanation : Here, 75 should be doubled twice and 
150 should be doubled once and 50 should be doubled
once and tripled once.Then, all the elements will 
be equal to 300.

Input : A[] = {100, 151, 200}
Output : No
Explanation : No matter what we do all elements in
the array could not be equal.

```

这个想法是重复地将每个元素除以 2 和 3，直到这个元素可以被整除。在这一步之后，如果所有元素都变得相同，那么答案是肯定的。

这是如何工作的？我们知道每一个整数都可以表示为质数**2<sup>a</sup>. 3<sup>b</sup>. 5<sup>c</sup>. 7<sup>d</sup>…..**。所以，在我们的问题中，我们可以通过加倍(*2)或三倍(*3)来增加 a 和 b。我们可以通过乘以 2 或 3 使数组中所有元素的 a 和 b 相等。但是这些数在它们的乘积表示中也有其他质数，我们不能改变它们的幂。所以为了使所有的数相等，它们应该从一开始就对其他质数具有相等的幂。我们可以通过将所有的数字尽可能多地除以二或三来检查它。那么他们都应该是平等的。

## c++

```
// C++ program to check if all numbers can
// be made equal by repeated division of 2
// and 3
#include <bits/stdc++.h>
using namespace std;

bool canMakeEqual(int a[], int n)
{
    for (int i = 0; i < n; i++) {

        // continuously divide every number by 2 
        while (a[i] % 2 == 0)
            a[i] = a[i] / 2;

       // continuously divide every number by 3
        while (a[i] % 3 == 0)
            a[i] = a[i] / 3;
    }

    // Check if all numbers same
    for (int i = 1; i < n; i++)
        if (a[i] != a[0])
           return false;

    return true;
}

// Driver Code
int main()
{
    int A[] = { 75, 150, 75, 50 };
    int n = sizeof(A) / sizeof(A[0]);
    if (canMakeEqual(A, n))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java

```
// Java program to check if all numbers can
// be made equal by repeated division of 2
// and 3
import java.util.*;

class GFG {

static Boolean canMakeEqual(int a[], int n)
{
    for (int i = 0; i < n; i++) {

        // Continuously divide every number by 2
        while (a[i] % 2 == 0)
            a[i] = a[i] / 2;

    // Continuously divide every number by 3
        while (a[i] % 3 == 0)
            a[i] = a[i] / 3;
    }

    // Check if all numbers same
    for (int i = 1; i < n; i++)
        if (a[i] != a[0])
        return false;

    return true;
}

// Driver Code
public static void main(String[] args)
{
int A[] = { 75, 150, 75, 50 };
    int n = A.length;
    if (canMakeEqual(A, n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
    }

// This code is contributed by 'Gitanjali'.
```

## python 3

T2

## c#

T31

```
// C# program to check if all numbers can
// be made equal by repeated division of 2
// and 3
using System;

class GFG {

    static Boolean canMakeEqual(int []a, int n)
    {
        for (int i = 0; i < n; i++) {

            // Continuously divide every number by 2
            while (a[i] % 2 == 0)
                a[i] = a[i] / 2;

            // Continuously divide every number by 3
            while (a[i] % 3 == 0)
                a[i] = a[i] / 3;
        }

        // Check if all numbers same
        for (int i = 1; i < n; i++)
            if (a[i] != a[0])
                return false;

        return true;
    }

    // Driver Code
    public static void Main()
    {

        int []A = { 75, 150, 75, 50 };
        int n = A.Length;

        if (canMakeEqual(A, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by 'vt_m'.
```

PHPT4T37】JavascriptT40

**输出:**

```
  Yes
```