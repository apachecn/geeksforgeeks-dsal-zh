# 最大子集，其和小于或等于各个指数的和

> 原文:[https://www . geeksforgeeks . org/最大子集具有小于等于各自指数总和的总和/](https://www.geeksforgeeks.org/largest-subset-having-with-sum-less-than-equal-to-sum-of-respective-indices/)

给定一个数组 **arr[]** ，任务是找到元素之和小于或等于其索引之和的最大子集的长度(基于 1 的索引)。

**示例:**

> **输入:** arr[] = {1，7，3，5，9，6，6}
> **输出:** 5
> **解释:**
> 最大子集是{1，3，5，6，6}
> 指数之和= 1 + 3 + 4 + 6 + 7 = 21
> 元素之和= 1 + 3 + 5 + 6 + 6 = 21
> 
> **输入:** arr[] = {4，1，6，7，8，2 }
> T3】输出: 3

**天真方法:**
解决问题最简单的方法是生成所有可能的子集，并计算元素之和小于或等于其各自索引之和的子集的长度。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**
按照以下步骤解决问题:

*   迭代所有索引，只考虑那些值大于或等于存储在其中的相应值的索引。
*   不断更新上一步得到的差值的**和**。
*   对于其余的元素，用它们各自的索引存储它们的差异。理清分歧。
*   将元素一个接一个地包含到子集中，并从**和**中减去差值。保持包含，直到遇到一个元素，该元素与其索引的差值超过剩余的**和**或者所有数组元素都已经包含。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length
// of the longest subset
int findSubset(int* a, int n)
{
    // Stores the sum of differences
    // between elements and
    // their respective index
    int sum = 0;

    // Stores the size of
    // the subset
    int cnt = 0;

    vector<int> v;

    // Iterate over the array
    for (int i = 1; i <= n; i++) {

        // If an element which is
        // smaller than or equal
        // to its index is encountered
        if (a[i - 1] - i <= 0) {

            // Increase count and sum
            sum += a[i - 1] - i;
            cnt += 1;
        }

        // Store the difference with
        // index of the remaining
        // elements
        else {
            v.push_back(a[i - 1] - i);
        }
    }

    // Sort the differences
    // in increasing order
    sort(v.begin(), v.end());

    int ptr = 0;

    // Include the differences while
    // sum remains positive or
    while (ptr < v.size()
           && sum + v[ptr] <= 0) {
        cnt += 1;
        ptr += 1;
        sum += v[ptr];
    }

    // Return the size
    return cnt;
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 6, 7,
                  8, 2 };

    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function Calling
    cout << findSubset(arr, n)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the length
// of the longest subset
public static int findSubset(int[] a, int n)
{

    // Stores the sum of differences
    // between elements and
    // their respective index
    int sum = 0;

    // Stores the size of
    // the subset
    int cnt = 0;

    Vector<Integer> v = new Vector<>();

    // Iterate over the array
    for(int i = 1; i <= n; i++)
    {

        // If an element which is
        // smaller than or equal
        // to its index is encountered
        if (a[i - 1] - i <= 0)
        {

            // Increase count and sum
            sum += a[i - 1] - i;
            cnt += 1;
        }

        // Store the difference with
        // index of the remaining
        // elements
        else
        {
            v.add(a[i - 1] - i);
        }
    }

    // Sort the differences
    // in increasing order
    Collections.sort(v);

    int ptr = 0;

    // Include the differences while
    // sum remains positive or
    while (ptr < v.size() &&
           sum + v.get(ptr) <= 0)
    {
        cnt += 1;
        ptr += 1;
        sum += v.get(ptr);
    }

    // Return the size
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 1, 6, 7, 8, 2 };
    int n = arr.length;

    // Function Calling
    System.out.println(findSubset(arr, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach

# Function to find the length 
# of the longest subset
def findSubset(a, n):

    # Stores the sum of differences 
    # between elements and 
    # their respective index 
    sum = 0

    # Stores the size of 
    # the subset 
    cnt = 0

    v = [] 

    # Iterate over the array 
    for i in range(1, n + 1):

        # If an element which is 
        # smaller than or equal 
        # to its index is encountered 
        if (a[i - 1] - i <= 0):

            # Increase count and sum 
            sum += a[i - 1] - i 
            cnt += 1

        # Store the difference with 
        # index of the remaining 
        # elements 
        else:
            v.append(a[i - 1] - i)

    # Sort the differences 
    # in increasing order 
    v.sort()

    ptr = 0

    # Include the differences while 
    # sum remains positive or 
    while (ptr < len(v) and
           sum + v[ptr] <= 0):
        cnt += 1
        ptr += 1 
        sum += v[ptr] 

    # Return the size 
    return cnt

# Driver code
if __name__=="__main__":

    arr = [ 4, 1, 6, 7, 8, 2 ] 
    n = len(arr)

    # Function calling 
    print(findSubset(arr, n))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the length
// of the longest subset
public static int findSubset(int[] a, int n)
{

    // Stores the sum of differences
    // between elements and
    // their respective index
    int sum = 0;

    // Stores the size of
    // the subset
    int cnt = 0;

    List<int> v = new List<int>();

    // Iterate over the array
    for(int i = 1; i <= n; i++)
    {

        // If an element which is
        // smaller than or equal
        // to its index is encountered
        if (a[i - 1] - i <= 0)
        {

            // Increase count and sum
            sum += a[i - 1] - i;
            cnt += 1;
        }

        // Store the difference with
        // index of the remaining
        // elements
        else
        {
            v.Add(a[i - 1] - i);
        }
    }

    // Sort the differences
    // in increasing order
    v.Sort();

    int ptr = 0;

    // Include the differences while
    // sum remains positive or
    while (ptr < v.Count &&
           sum + v[ptr] <= 0)
    {
        cnt += 1;
        ptr += 1;
        sum += v[ptr];
    }

    // Return the size
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 1, 6, 7, 8, 2 };
    int n = arr.Length;

    // Function calling
    Console.WriteLine(findSubset(arr, n));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the length
// of the longest subset
function findSubset(a, n)
{

    // Stores the sum of differences
    // between elements and
    // their respective index
    let sum = 0;

    // Stores the size of
    // the subset
    let cnt = 0;

    let v = [];

    // Iterate over the array
    for(let i = 1; i <= n; i++)
    {

        // If an element which is
        // smaller than or equal
        // to its index is encountered
        if (a[i - 1] - i <= 0)
        {

            // Increase count and sum
            sum += a[i - 1] - i;
            cnt += 1;
        }

        // Store the difference with
        // index of the remaining
        // elements
        else
        {
            v.push(a[i - 1] - i);
        }
    }

    // Sort the differences
    // in increasing order
    v.sort();

    let ptr = 0;

    // Include the differences while
    // sum remains positive or
    while (ptr < v.length &&
           sum + v[ptr] <= 0)
    {
        cnt += 1;
        ptr += 1;
        sum += v[ptr];
    }

    // Return the size
    return cnt;
}

// Driver Code

    let arr = [ 4, 1, 6, 7, 8, 2 ];
    let n = arr.length;

    // Function Calling
    document.write(findSubset(arr, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***空间复杂度:** O(N)*