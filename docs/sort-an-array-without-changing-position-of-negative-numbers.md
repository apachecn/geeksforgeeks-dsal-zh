# 在不改变负数位置的情况下对数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-array-of-not-changed-position-of-negative-numbers/](https://www.geeksforgeeks.org/sort-an-array-without-changing-position-of-negative-numbers/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是在不改变负数(如果有的话)位置的情况下对数组进行排序，即负数不需要排序。
**例:**

> **输入:** arr[] = {2，-6，-3，8，4，1}
> **输出:** 1 -6 -3 2 4 8
> **输入:** arr[] = {-2，-6，-3，-8，4，1}
> **输出:** -2 -6 -3 -8 1 4

**方法:**将数组的所有非负元素存储在另一个向量中，并对这个向量进行排序。现在，用这些排序后的值替换原始数组中的所有非负值。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the array such that
// negative values do not get affected
void sortArray(int a[], int n)
{

    // Store all non-negative values
    vector<int> ans;
    for (int i = 0; i < n; i++) {
        if (a[i] >= 0)
            ans.push_back(a[i]);
    }

    // Sort non-negative values
    sort(ans.begin(), ans.end());

    int j = 0;
    for (int i = 0; i < n; i++) {

        // If current element is non-negative then
        // update it such that all the
        // non-negative values are sorted
        if (a[i] >= 0) {
            a[i] = ans[j];
            j++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 2, -6, -3, 8, 4, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    sortArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to sort the array such that
// negative values do not get affected
static void sortArray(int a[], int n)
{

    // Store all non-negative values
    Vector<Integer> ans = new Vector<>();
    for (int i = 0; i < n; i++)
    {
        if (a[i] >= 0)
            ans.add(a[i]);
    }

    // Sort non-negative values
    Collections.sort(ans);

    int j = 0;
    for (int i = 0; i < n; i++)
    {

        // If current element is non-negative then
        // update it such that all the
        // non-negative values are sorted
        if (a[i] >= 0)
        {
            a[i] = ans.get(j);
            j++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < n; i++)
        System.out.print(a[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, -6, -3, 8, 4, 1 };

    int n = arr.length;

    sortArray(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to sort the array such that
# negative values do not get affected
def sortArray(a, n):

    # Store all non-negative values
    ans=[]
    for i in range(n):
        if (a[i] >= 0):
            ans.append(a[i])

    # Sort non-negative values
    ans = sorted(ans)

    j = 0
    for i in range(n):

        # If current element is non-negative then
        # update it such that all the
        # non-negative values are sorted
        if (a[i] >= 0):
            a[i] = ans[j]
            j += 1

    # Print the sorted array
    for i in range(n):
        print(a[i],end = " ")

# Driver code

arr = [2, -6, -3, 8, 4, 1]

n = len(arr)

sortArray(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System.Collections.Generic;
using System;

class GFG
{

// Function to sort the array such that
// negative values do not get affected
static void sortArray(int []a, int n)
{

    // Store all non-negative values
    List<int> ans = new List<int>();
    for (int i = 0; i < n; i++)
    {
        if (a[i] >= 0)
            ans.Add(a[i]);
    }

    // Sort non-negative values
    ans.Sort();

    int j = 0;
    for (int i = 0; i < n; i++)
    {

        // If current element is non-negative then
        // update it such that all the
        // non-negative values are sorted
        if (a[i] >= 0)
        {
            a[i] = ans[j];
            j++;
        }
    }

    // Print the sorted array
    for (int i = 0; i < n; i++)
        Console.Write(a[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, -6, -3, 8, 4, 1 };

    int n = arr.Length;

    sortArray(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to sort the array such that
// negative values do not get affected
function sortArray(a, n)
{

    // Store all non-negative values
    var ans = [];
    for (var i = 0; i < n; i++) {
        if (a[i] >= 0)
            ans.push(a[i]);
    }

    // Sort non-negative values
    ans.sort((a,b)=> a-b);

    var j = 0;
    for (var i = 0; i < n; i++) {

        // If current element is non-negative then
        // update it such that all the
        // non-negative values are sorted
        if (a[i] >= 0) {
            a[i] = ans[j];
            j++;
        }
    }

    // Print the sorted array
    for (var i = 0; i < n; i++)
        document.write( a[i] + " ");
}

// Driver code
var arr = [2, -6, -3, 8, 4, 1];
var n = arr.length;
sortArray(arr, n);

</script>
```

**Output:** 

```
1 -6 -3 2 4 8
```

***时间复杂度:** O(n ** log n *)*

***辅助空间:** O(n)*