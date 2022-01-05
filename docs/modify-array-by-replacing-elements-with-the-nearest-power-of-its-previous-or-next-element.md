# 通过用上一个或下一个元素的最近次幂替换元素来修改数组

> 原文:[https://www . geeksforgeeks . org/通过用上一个或下一个元素的最近幂替换元素来修改数组/](https://www.geeksforgeeks.org/modify-array-by-replacing-elements-with-the-nearest-power-of-its-previous-or-next-element/)

给定一个由正整数 **N** 组成的[圆形数组](https://www.geeksforgeeks.org/circular-array/)**arr【】**，任务是通过将每个数组元素替换为其前一个或下一个数组元素的最近幂来修改数组。

**示例:**

> **输入:** arr[] = {2，3，4，1，2}
> **输出:** {2，4，3，1，2}
> **解释:**
> 对于 arr[0](= 2):上一个和下一个数组元素分别为 2 和 3。所以，最近的动力是 2 <sup>1</sup> 。
> 对于 arr[1](= 3):上一个和下一个元素分别为 2 和 4。因此，最近的电源是 4 <sup>1</sup> 。
> 对于 arr[2](= 4):上一个和下一个元素分别为 3 和 1。因此，最近的电源是 3 <sup>1</sup> 。
> 对于 arr[3](= 1):上一个和下一个元素是 4 和 2。因此，最近的电源是 4 <sup>0</sup> 。
> 对于 arr[4](= 2):上一个和下一个元素是 1 和 2。因此，1 的最近幂是 2 <sup>1</sup> 。
> 
> **输入:** arr[] = {21，3，54，78，9}
> 输出: {27，1，78，81，1}

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并用其前一个元素或下一个数组元素的最近次幂替换每个数组元素。
按照以下步骤解决这个问题:

*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下步骤:
    *   找出**X<sup>K</sup>T5【最接近**y**的 **K** 的值**
    *   计算 **K** 取**原木 <sub>x</sub> (Y)的[楼层值](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)。**
    *   因此 **K** 和 **K + 1** 将是最接近幂的两个整数。
    *   计算**Y<sup>K</sup>T3**Y<sup>(K+1)</sup>**并检查哪个最接近 **X** 并用最接近的值更新数组元素 **arr[i]** 。**
*   完成以上步骤后，[打印数组**arr【】**T3】作为修改后的数组。](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the power
// of y which is nearest to x
int nearestPow(int x, int y)
{

    // Base Case
    if (y == 1)
        return 1;

    // Stores the logarithmic
    // value of x with base y
    int k = log10(x) / log10(y);

    if (abs(pow(y, k) - x) <
        abs(pow(y, (k + 1)) - x))
        return pow(y, k);

    return pow(y, (k + 1));
}

// Function to replace each array
// element by the nearest power of
// its previous or next element
void replacebyNearestPower(vector<int> arr)
{

    // Stores the previous
    // and next element
    int prev = arr[arr.size() - 1];
    int lastNext = arr[0];
    int next = 0;

    // Traverse the array
    for(int i = 0; i < arr.size(); i++)
    {
        int temp = arr[i];
        if (i == arr.size() - 1)
            next = lastNext;
        else
            next = arr[(i + 1) % arr.size()];

        // Calculate nearest power for
        // previous and next elements
        int prevPow = nearestPow(arr[i], prev);
        int nextPow = nearestPow(arr[i], next);

        // Replacing the array values
        if (abs(arr[i] - prevPow) <
            abs(arr[i] - nextPow))
            arr[i] = prevPow;
        else
            arr[i] = nextPow;

        prev = temp;
    }

    // Print the updated array
    for(int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr{ 2, 3, 4, 1, 2 };

    replacebyNearestPower(arr);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate the power
// of y which is nearest to x
static int nearestPow(int x, int y)
{

    // Base Case
    if (y == 1)
        return 1;

    // Stores the logarithmic
    // value of x with base y
    int k = (int)(Math.log10(x) /
                  Math.log10(y));

    if (Math.abs(Math.pow(y, k) - x) <
        Math.abs(Math.pow(y, (k + 1)) - x))
        return (int)(Math.pow(y, k));

    return (int)(Math.pow(y, (k + 1)));
}

// Function to replace each array
// element by the nearest power of
// its previous or next element
static void replacebyNearestPower(int[] arr)
{

    // Stores the previous
    // and next element
    int prev = arr[arr.length - 1];
    int lastNext = arr[0];
    int next = 0;

    // Traverse the array
    for(int i = 0; i < arr.length; i++)
    {
        int temp = arr[i];
        if (i == arr.length - 1)
            next = lastNext;
        else
            next = arr[(i + 1) % arr.length];

        // Calculate nearest power for
        // previous and next elements
        int prevPow = nearestPow(arr[i], prev);
        int nextPow = nearestPow(arr[i], next);

        // Replacing the array values
        if (Math.abs(arr[i] - prevPow) <
            Math.abs(arr[i] - nextPow))
            arr[i] = prevPow;
        else
            arr[i] = nextPow;

        prev = temp;
    }

    // Print the updated array
    for(int i = 0; i < arr.length; i++)
        System.out.print(arr[i] + " ");
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int[] arr = { 2, 3, 4, 1, 2 };

    replacebyNearestPower(arr);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

import math

# Function to calculate the power
# of y which is nearest to x
def nearestPow(x, y):

    # Base Case
    if y == 1:
        return 1

    # Stores the logarithmic
    # value of x with base y
    k = int(math.log(x, y))

    if abs(y**k - x) < abs(y**(k + 1) - x):
        return y**k

    return y**(k + 1)

# Function to replace each array
# element by the nearest power of
# its previous or next element
def replacebyNearestPower(arr):

    # Stores the previous
    # and next element
    prev = arr[-1]

    lastNext = arr[0]

    # Traverse the array
    for i in range(len(arr)):

        temp = arr[i]
        if i == len(arr)-1:
            next = lastNext
        else:
            next = arr[(i + 1) % len(arr)]

        # Calculate nearest power for
        # previous and next elements
        prevPow = nearestPow(arr[i], prev)
        nextPow = nearestPow(arr[i], next)

        # Replacing the array values
        if abs(arr[i]-prevPow) < abs(arr[i]-nextPow):
            arr[i] = prevPow
        else:
            arr[i] = nextPow
        prev = temp

    # Print the updated array
    print(arr)

# Driver Code

# Given array
arr = [2, 3, 4, 1, 2]

replacebyNearestPower(arr)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate the power
// of y which is nearest to x
static int nearestPow(int x, int y)
{

    // Base Case
    if (y == 1)
        return 1;

    // Stores the logarithmic
    // value of x with base y
    int k = (int)(Math.Log(x, y));

    if (Math.Abs(Math.Pow(y, k) - x) <
        Math.Abs(Math.Pow(y, (k + 1)) - x))
        return (int)(Math.Pow(y, k));

    return (int)(Math.Pow(y, (k + 1)));
}

// Function to replace each array
// element by the nearest power of
// its previous or next element
static void replacebyNearestPower(int[] arr)
{

    // Stores the previous
    // and next element
    int prev = arr[arr.Length - 1];
    int lastNext = arr[0];
    int next = 0;

    // Traverse the array
    for(int i = 0; i < arr.Length; i++)
    {
        int temp = arr[i];
        if (i == arr.Length - 1)
            next = lastNext;
        else
            next = arr[(i + 1) % arr.Length];

        // Calculate nearest power for
        // previous and next elements
        int prevPow = nearestPow(arr[i], prev);
        int nextPow = nearestPow(arr[i], next);

        // Replacing the array values
        if (Math.Abs(arr[i] - prevPow) <
            Math.Abs(arr[i] - nextPow))
            arr[i] = prevPow;
        else
            arr[i] = nextPow;

        prev = temp;
    }

    // Print the updated array
    for(int i = 0; i < arr.Length; i++)
        Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main()
{

    // Given array
    int[] arr = { 2, 3, 4, 1, 2 };

    replacebyNearestPower(arr);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the power
// of y which is nearest to x
function nearestPow(x, y) {

    // Base Case
    if (y == 1)
        return 1

    // Stores the logarithmic
    // value of x with base y
    var k = Math.floor(Math.log(x) / Math.log(y))

    if (Math.abs(Math.pow(y,k) - x) <
        Math.abs(Math.pow(y,(k + 1)) - x))
        return Math.pow(y,k)

    return Math.pow(y,(k + 1))
}

// Function to replace each array
// element by the nearest power of
// its previous or next element
function replacebyNearestPower(arr) {

    // Stores the previous
    // and next element
    var prev = arr[arr.length -1]

    var lastNext = arr[0]

    // Traverse the array
    for (var i = 0; i < arr.length; i++){

        var temp = arr[i]
        if (i == arr.length -1)
            var next = lastNext
        else
            var next = arr[(i + 1) % arr.length]

        // Calculate nearest power for
        // previous and next elements
        var prevPow = nearestPow(arr[i], prev)
        var nextPow = nearestPow(arr[i], next)

        // Replacing the array values
        if (Math.abs(arr[i]-prevPow) <
            Math.abs(arr[i]-nextPow))
            arr[i] = prevPow
        else
            arr[i] = nextPow

        prev = temp
    }

    // Print the updated array
    document.write(arr)
}
// Driver Code
// Given array
var arr = [2, 3, 4, 1, 2]

replacebyNearestPower(arr)

// This code is contributed by AnkThon

</script>
```

**Output:** 

```
[2, 4, 3, 1, 2]
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)