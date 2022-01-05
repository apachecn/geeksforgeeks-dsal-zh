# 查找未排序数组中缺失的最小正数|集合 3

> 原文:[https://www . geeksforgeeks . org/find-最小正数-未排序数组集缺失-3/](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array-set-3/)

给定一个包含正负元素的未排序数组。任务是找出数组中缺失的最小正数。

**示例:**

> **输入:** arr[] = {2，3，7，6，8，-1，-10，15}
> **输出:** 1
> 
> **输入:** arr[] = { 2，3，-7，6，8，1，-10，15 }
> **输出:** 4
> 
> **输入:** arr[] = {1，1，0，-1，-2}
> **输出:** 2

**方法:**
我们已经讨论了一些技术来寻找未排序数组中缺失的最小正数。
[查找未排序数组中缺失的最小正数|集合 1](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)
[查找未排序数组中缺失的最小正数|集合 2](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)
这里，我们使用[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储所有正整数，并查找第一个缺失的正整数。

## C++

```
// CPP program to find the smallest
// positive missing number
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// positive missing number
int findMissingPositive(int arr[], int n)
{
    // Default smallest Positive Integer
    int m = 1;

    // Store values in set which are
    // greater than variable m
    set<int> x;

    for (int i = 0; i < n; i++) {
        // Store value when m is less than
        // current index of given array
        if (m < arr[i]) {
            x.insert(arr[i]);
        }
        else if (m == arr[i]) {
            // Increment m when it is equal
            // to current element
            m = m + 1;

            while (x.count(m)) {
                x.erase(m);

                // Increment m when it is one of the
                // element of the set
                m = m + 1;
            }
        }
    }

    // Return the required answer
    return m;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, -7, 6, 8, 1, -10, 15 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << findMissingPositive(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// positive missing number
import java.util.*;

class GFG
{

// Function to find the smallest
// positive missing number
static int findMissingPositive(int arr[], int n)
{
    // Default smallest Positive Integer
    int m = 1;

    // Store values in set which are
    // greater than variable m
    HashSet<Integer> x = new HashSet<Integer>();

    for (int i = 0; i < n; i++)
    {
        // Store value when m is less than
        // current index of given array
        if (m < arr[i])
        {
            x.add(arr[i]);
        }
        else if (m == arr[i])
        {
            // Increment m when it is equal
            // to current element
            m = m + 1;

            while (x.contains(m))
            {
                x.remove(m);

                // Increment m when it is one of the
                // element of the set
                m = m + 1;
            }
        }
    }

    // Return the required answer
    return m;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, -7, 6, 8, 1, -10, 15 };

    int n = arr.length;

    // Function call
    System.out.println(findMissingPositive(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the smallest
# positive missing number

# Function to find the smallest
# positive missing number
def findMissingPositive(arr, n):

    # Default smallest Positive Integer
    m = 1

    # Store values in set which are
    # greater than variable m
    x = []
    for i in range(n):

        # Store value when m is less than
        # current index of given array
        if (m < arr[i]):
            x.append(arr[i])

        elif (m == arr[i]):

            # Increment m when it is equal
            # to current element
            m = m + 1

            while (x.count(m)):
                x.remove(m)

                # Increment m when it is one of the
                # element of the set
                m = m + 1

    # Return the required answer
    return m

# Driver code
if __name__ == '__main__':
    arr = [2, 3, -7, 6, 8, 1, -10, 15]

    n = len(arr)

    # Function call
    print(findMissingPositive(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the smallest
// positive missing number
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the smallest
// positive missing number
static int findMissingPositive(int []arr, int n)
{
    // Default smallest Positive Integer
    int m = 1;

    // Store values in set which are
    // greater than variable m
    HashSet<int> x = new HashSet<int>();

    for (int i = 0; i < n; i++)
    {
        // Store value when m is less than
        // current index of given array
        if (m < arr[i])
        {
            x.Add(arr[i]);
        }

        else if (m == arr[i])
        {
            // Increment m when it is equal
            // to current element
            m = m + 1;

            while (x.Contains(m))
            {
                x.Remove(m);

                // Increment m when it is one of the
                // element of the set
                m = m + 1;
            }
        }
    }

    // Return the required answer
    return m;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, -7, 6, 8, 1, -10, 15 };

    int n = arr.Length;

    // Function call
    Console.WriteLine(findMissingPositive(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the smallest
// positive missing number

// Function to find the smallest
// positive missing number
function findMissingPositive(arr, n)
{
    // Default smallest Positive integer
    let m = 1;

    // Store values in set which are
    // greater than variable m
    let x = new Set();

    for (let i = 0; i < n; i++) {
        // Store value when m is less than
        // current index of given array
        if (m < arr[i]) {
            x.add(arr[i]);
        }
        else if (m == arr[i]) {
            // Increment m when it is equal
            // to current element
            m = m + 1;

            while (x.has(m)) {
                x.delete(m);

                // Increment m when it is one of the
                // element of the set
                m = m + 1;
            }
        }
    }

    // Return the required answer
    return m;
}

// Driver code

let arr = [2, 3, -7, 6, 8, 1, -10, 15];

let n = arr.length;

// Function call
document.write(findMissingPositive(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4
```