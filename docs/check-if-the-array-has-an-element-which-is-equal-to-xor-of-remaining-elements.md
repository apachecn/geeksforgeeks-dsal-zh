# 检查数组中是否有一个元素等于剩余元素的异或

> 原文:[https://www . geesforgeks . org/check-如果数组有一个等于剩余元素异或的元素/](https://www.geeksforgeeks.org/check-if-the-array-has-an-element-which-is-equal-to-xor-of-remaining-elements/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是检查该数组中是否有一个元素等于所有剩余元素的异或。
**例:**

> **输入:** arr[] = { 8，2，4，15，1 }
> **输出:** Yes
> 8 是必需元素，因为 2 ^ 4 ^ 15 ^ 1 = 8。
> **输入:** arr[] = {4，2，3}
> **输出:**否

**方法:**首先，对数组的所有元素进行异或运算，并将其存储在变量 **xorArr** 中。现在再次遍历整个数组，对于每个元素，计算数组元素的 xor，不包括当前元素 **arr[i]** ，即 **x = xorArr ^ arr[i]** 。
如果 **x = arr[i]** ，则 **arr[i]** 是必需元素，因此打印**是**。如果没有找到这样的元素，则打印**否**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the array
// contains an element which is equal to
// the XOR of the remaining elements
bool containsElement(int arr[], int n)
{

    // To store the XOR of all
    // the array elements
    int xorArr = 0;
    for (int i = 0; i < n; ++i)
        xorArr ^= arr[i];

    // For every element of the array
    for (int i = 0; i < n; ++i) {

        // Take the XOR after excluding
        // the current element
        int x = xorArr ^ arr[i];

        // If the XOR of the remaining elements
        // is equal to the current element
        if (arr[i] == x)
            return true;
    }

    // If no such element is found
    return false;
}

// Driver code
int main()
{
    int arr[] = { 8, 2, 4, 15, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (containsElement(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if the array
// contains an element which is equal to
// the XOR of the remaining elements
static boolean containsElement(int [] arr, int n)
{

    // To store the XOR of all
    // the array elements
    int xorArr = 0;
    for (int i = 0; i < n; ++i)
        xorArr ^= arr[i];

    // For every element of the array
    for (int i = 0; i < n; ++i)
    {

        // Take the XOR after excluding
        // the current element
        int x = xorArr ^ arr[i];

        // If the XOR of the remaining elements
        // is equal to the current element
        if (arr[i] == x)
            return true;
    }

    // If no such element is found
    return false;
}

// Driver code
public static void main (String[] args)
{
    int [] arr = { 8, 2, 4, 15, 1 };
    int n = arr.length;

    if (containsElement(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the array
# contains an element which is equal to
# the XOR of the remaining elements
def containsElement(arr, n):

    # To store the XOR of all
    # the array elements
    xorArr = 0
    for i in range(n):
        xorArr ^= arr[i]

    # For every element of the array
    for i in range(n):

        # Take the XOR after excluding
        # the current element
        x = xorArr ^ arr[i]

        # If the XOR of the remaining elements
        # is equal to the current element
        if (arr[i] == x):
            return True

    # If no such element is found
    return False

# Driver Code
arr = [8, 2, 4, 15, 1]
n = len(arr)

if (containsElement(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function that returns true if the array
// contains an element which is equal to
// the XOR of the remaining elements
static bool containsElement(int [] arr, int n)
{

    // To store the XOR of all
    // the array elements
    int xorArr = 0;
    for (int i = 0; i < n; ++i)
        xorArr ^= arr[i];

    // For every element of the array
    for (int i = 0; i < n; ++i)
    {

        // Take the XOR after excluding
        // the current element
        int x = xorArr ^ arr[i];

        // If the XOR of the remaining elements
        // is equal to the current element
        if (arr[i] == x)
            return true;
    }

    // If no such element is found
    return false;
}

// Driver code
public static void Main ()
{
    int [] arr = { 8, 2, 4, 15, 1 };
    int n = arr.Length;

    if (containsElement(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if the array
// contains an element which is equal to
// the XOR of the remaining elements
function containsElement(arr, n)
{

    // To store the XOR of all
    // the array elements
    let xorArr = 0;
    for (let i = 0; i < n; ++i)
        xorArr ^= arr[i];

    // For every element of the array
    for (let i = 0; i < n; ++i) {

        // Take the XOR after excluding
        // the current element
        let x = xorArr ^ arr[i];

        // If the XOR of the remaining elements
        // is equal to the current element
        if (arr[i] == x)
            return true;
    }

    // If no such element is found
    return false;
}

// Driver code
    let arr = [ 8, 2, 4, 15, 1 ];
    let n = arr.length;

    if (containsElement(arr, n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Yes
```