# 元素可以混洗时数组中面积最大的方块

> 原文:[https://www . geeksforgeeks . org/最大面积正方形阵列-当元素可以被混洗时/](https://www.geeksforgeeks.org/largest-area-square-in-an-array-when-elements-can-be-shuffled/)

给定一个由 **N** 整数组成的数组**arr【】**，其中**arr【I】**是 **i <sup>th</sup>** 巧克力的高度，所有巧克力都是 **1** 单位宽，当巧克力可以以任何顺序排列时，任务是找到由巧克力制成的任何方块的最大面积。
**示例:**

> **输入:** arr[] = {1，3，4，5，5}
> **输出:** 9
> 边= 3 的正方形可以从{3，4，5}或{4，5，5}中获得
> 。
> **输入:** arr[] = {6，1，6，6，6}
> **输出:** 16

**方法:**如果数组中至少存在一个等于或大于 **a** 的 **a** 元素，则可以获得一个正方形的边 **a** 。二分搜索法可以用来寻找在 **0** 到 **N** 范围内可以达到的正方形的最大边。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it
// is possible to make a square
// with side equal to l
bool isSquarePossible(int arr[], int n, int l)
{

    // To store the count of elements
    // greater than or equal to l
    int cnt = 0;
    for (int i = 0; i < n; i++) {

        // Increment the count
        if (arr[i] >= l)
            cnt++;

        // If the count becomes greater
        // than or equal to l
        if (cnt >= l)
            return true;
    }

    return false;
}

// Function to return the
// maximum area of the square
// that can be obtained
int maxArea(int arr[], int n)
{
    int l = 0, r = n;
    int len = 0;
    while (l <= r) {
        int m = l + ((r - l) / 2);

        // If square is possible with
        // side length m
        if (isSquarePossible(arr, n, m)) {
            len = m;
            l = m + 1;
        }

        // Try to find a square with
        // smaller side length
        else
            r = m - 1;
    }

    // Return the area
    return (len * len);
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 4, 5, 5 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxArea(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if it
    // is possible to make a square
    // with side equal to l
    static boolean isSquarePossible(int arr[],
                                    int n, int l)
    {

        // To store the count of elements
        // greater than or equal to l
        int cnt = 0;
        for (int i = 0; i < n; i++)
        {

            // Increment the count
            if (arr[i] >= l)
                cnt++;

            // If the count becomes greater
            // than or equal to l
            if (cnt >= l)
                return true;
        }
        return false;
    }

    // Function to return the
    // maximum area of the square
    // that can be obtained
    static int maxArea(int arr[], int n)
    {
        int l = 0, r = n;
        int len = 0;
        while (l <= r)
        {
            int m = l + ((r - l) / 2);

            // If square is possible with
            // side length m
            if (isSquarePossible(arr, n, m))
            {
                len = m;
                l = m + 1;
            }

            // Try to find a square with
            // smaller side length
            else
                r = m - 1;
        }

        // Return the area
        return (len * len);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 3, 4, 5, 5 };
        int n = arr.length;

        System.out.println(maxArea(arr, n));
    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it
# is possible to make a square
# with side equal to l
def isSquarePossible(arr, n, l) :

    # To store the count of elements
    # greater than or equal to l
    cnt = 0
    for i in range(n) :

        # Increment the count
        if arr[i] >= l :
            cnt += 1

        # If the count becomes greater
        # than or equal to l
        if cnt >= l :
            return True

    return False

# Function to return the
# maximum area of the square
# that can be obtained
def maxArea(arr, n) :

    l , r = 0, n
    len = 0
    while l <= r :
        m = l + ((r - l) // 2)

        # If square is possible with
        # side length m
        if isSquarePossible(arr, n, m) :
            len = m
            l = m + 1

        # Try to find a square with
        # smaller side length
        else :
            r = m - 1

    # Return the area
    return (len * len)

# Driver code
arr = [ 1, 3, 4, 5, 5 ]
n = len(arr)

print(maxArea(arr, n))

# This code is contributed by divyamohan
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if it
    // is possible to make a square
    // with side equal to l
    static bool isSquarePossible(int []arr,
                                 int n, int l)
    {

        // To store the count of elements
        // greater than or equal to l
        int cnt = 0;
        for (int i = 0; i < n; i++)
        {

            // Increment the count
            if (arr[i] >= l)
                cnt++;

            // If the count becomes greater
            // than or equal to l
            if (cnt >= l)
                return true;
        }
        return false;
    }

    // Function to return the
    // maximum area of the square
    // that can be obtained
    static int maxArea(int []arr, int n)
    {
        int l = 0, r = n;
        int len = 0;
        while (l <= r)
        {
            int m = l + ((r - l) / 2);

            // If square is possible with
            // side length m
            if (isSquarePossible(arr, n, m))
            {
                len = m;
                l = m + 1;
            }

            // Try to find a square with
            // smaller side length
            else
                r = m - 1;
        }

        // Return the area
        return (len * len);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 3, 4, 5, 5 };
        int n = arr.Length;

        Console.WriteLine(maxArea(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if it
// is possible to make a square
// with side equal to l
function isSquarePossible(arr, n, l) {

    // To store the count of elements
    // greater than or equal to l
    let cnt = 0;
    for (let i = 0; i < n; i++) {

        // Increment the count
        if (arr[i] >= l)
            cnt++;

        // If the count becomes greater
        // than or equal to l
        if (cnt >= l)
            return true;
    }

    return false;
}

// Function to return the
// maximum area of the square
// that can be obtained
function maxArea(arr, n) {
    let l = 0, r = n;
    let len = 0;
    while (l <= r) {
        let m = l + Math.floor((r - l) / 2);

        // If square is possible with
        // side length m
        if (isSquarePossible(arr, n, m)) {
            len = m;
            l = m + 1;
        }

        // Try to find a square with
        // smaller side length
        else
            r = m - 1;
    }

    // Return the area
    return (len * len);
}

// Driver code

let arr = [1, 3, 4, 5, 5];
let n = arr.length;

document.write(maxArea(arr, n));

</script>
```

**Output:** 

```
9
```