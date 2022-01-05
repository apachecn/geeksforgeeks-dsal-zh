# 检查数组是否可以通过交换与最小数组元素数量相等的设置位计数的 GCD 对进行排序

> 原文:[https://www . geesforgeks . org/check-if-array-can-sort-by-switching-pairs-with-gcd-set-bits-count-等于最小数组元素数/](https://www.geeksforgeeks.org/check-if-array-can-be-sorted-by-swapping-pairs-with-gcd-of-set-bits-count-equal-to-that-of-the-smallest-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查是否有可能使用以下交换操作对数组进行[排序:](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)

> 只有当两个数的[设定位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)等于数组最小元素的设定位数时，两个数的交换才有效。

如果可以通过仅执行上述交换来对阵列进行排序，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {2，3，5，7，6}
> **输出:**是
> **说明:**
> 需要交换 7 和 6 才能使数组排序。
> 7 有 3 个设置位，6 有 2 个设置位。
> 由于 GCD(2，3) = 1，等于数组中最小整数的设定位数，即 2 (1 个设定位)。
> 因此，可以通过交换(7，6)对数组进行排序。
> 
> **输入:** arr[] = {3，3，15，7}
> **输出:**否
> **说明:**
> 需要交换 15 和 7 才能使数组排序。
> 15 有 4 个设置位，7 有 3 个设置位。GCD(4，3) = 1，不等于数组中最小整数的设置位数，即 3(2 个设置位)。
> 因此，数组无法排序。

**方法:**按照以下步骤解决问题:

1.  [对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，并将其存储在辅助数组中(比如 **dup[]** )。
2.  [迭代数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，检查它在**arr【】**和**dup【】**中是否在同一索引处。如果发现是真的，继续下一个索引。
3.  否则，如果在**arr【】**中需要交换第 i <sup>个</sup>和第 j <sup>个</sup>位置元素，则计算**arr【I】**的设置位与**arr【j】**的设置位的 **GCD** ，并检查其是否等于数组最小元素中的设置位的计数。
4.  如果不允许这样的交换，打印**“否”**。否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of set
// bits in an integer
int calculateSetBit(int n)
{
    int count = 0;

    // Traverse every bits
    for (int i = 0; i < 32; i++) {
        if (n & 1)
            count++;

        // Right shift by 1
        n = n >> 1;
    }

    return count;
}

// Function to check if sorting the
// given array is possible or not
void sortPossible(int arr[], int n)
{
    // Duplicate array
    int dup[n];

    for (int i = 0; i < n; i++)
        dup[i] = arr[i];

    // Sorted array to check if the
    // original array can be sorted
    sort(dup, dup + n);

    // Flag variable to check
    // if possible to sort
    bool flag = 1;

    // Calculate bits of smallest
    // array element
    int bit = calculateSetBit(dup[0]);

    // Check every wrong placed
    // integer in the array
    for (int i = 0; i < n; i++) {
        if (arr[i] != dup[i]) {

            // Swapping only if GCD of set
            // bits is equal to set bits in
            // smallest integer
            if (__gcd(
                    calculateSetBit(arr[i]),
                    bit)
                != bit) {
                flag = 0;
                break;
            }
        }
    }

    // Print the result
    if (flag) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return;
}

// Driver Code
int main()
{
    int arr[] = { 3, 9, 12, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortPossible(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{

    // Everything divides 0 
    if (a == 0)
        return b;
    if (b == 0)
         return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to count number of set
// bits in an integer
static int calculateSetBit(int n)
{
    int count = 0;

    // Traverse every bits
    for(int i = 0; i < 32; i++)
    {
        if ((n & 1) != 0)
            count++;

        // Right shift by 1
        n = n >> 1;
    }
    return count;
}

// Function to check if sorting the
// given array is possible or not
static void sortPossible(int arr[], int n)
{

    // Duplicate array
    int dup[] = new int[n];

    for(int i = 0; i < n; i++)
        dup[i] = arr[i];

    // Sorted array to check if the
    // original array can be sorted
    Arrays.sort(dup);

    // Flag variable to check
    // if possible to sort
    int flag = 1;

    // Calculate bits of smallest
    // array element
    int bit = calculateSetBit(dup[0]);

    // Check every wrong placed
    // integer in the array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != dup[i])
        {

            // Swapping only if GCD of set
            // bits is equal to set bits in
            // smallest integer
            if (gcd(calculateSetBit(
                arr[i]), bit) != bit)
            {
                flag = 0;
                break;
            }
        }
    }

    // Print the result
    if (flag != 0)
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
    return;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 9, 12, 6 };

    int N = arr.length;

    // Function call
    sortPossible(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import gcd

# Function to count number of set
# bits in an eger
def calculateSetBit(n):

    count = 0

    # Traverse every bits
    for i in range(32):
        if (n & 1):
            count += 1

        # Right shift by 1
        n = n >> 1

    return count

# Function to check if sorting the
# given array is possible or not
def sortPossible(arr, n):

    # Duplicate array
    dup = [0] * n

    for i in range(n):
        dup[i] = arr[i]

    # Sorted array to check if the
    # original array can be sorted
    dup = sorted(dup)

    # Flag variable to check
    # if possible to sort
    flag = 1

    # Calculate bits of smallest
    # array element
    bit = calculateSetBit(dup[0])

    # Check every wrong placed
    # eger in the array
    for i in range(n):
        if (arr[i] != dup[i]):

            # Swapping only if GCD of set
            # bits is equal to set bits in
            # smallest eger
            if (gcd(calculateSetBit(arr[i]), bit) != bit):
                flag = 0
                break

    # Print the result
    if (flag):
        print("Yes")
    else:
        print("No")

    return

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 9, 12, 6 ]

    N = len(arr)

    # Function call
    sortPossible(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{

    // Everything divides 0 
    if (a == 0)
        return b;
    if (b == 0)
         return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to count number of set
// bits in an integer
static int calculateSetBit(int n)
{
    int count = 0;

    // Traverse every bits
    for(int i = 0; i < 32; i++)
    {
        if ((n & 1) != 0)
            count++;

        // Right shift by 1
        n = n >> 1;
    }
    return count;
}

// Function to check if sorting the
// given array is possible or not
static void sortPossible(int[] arr, int n)
{

    // Duplicate array
    int[] dup = new int[n];

    for(int i = 0; i < n; i++)
        dup[i] = arr[i];

    // Sorted array to check if the
    // original array can be sorted
    Array.Sort(dup);

    // Flag variable to check
    // if possible to sort
    int flag = 1;

    // Calculate bits of smallest
    // array element
    int bit = calculateSetBit(dup[0]);

    // Check every wrong placed
    // integer in the array
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != dup[i])
        {

            // Swapping only if GCD of set
            // bits is equal to set bits in
            // smallest integer
            if (gcd(calculateSetBit(
                arr[i]), bit) != bit)
            {
                flag = 0;
                break;
            }
        }
    }

    // Print the result
    if (flag != 0)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }

    return;
}

// Driver Code
public static void Main()
{
    int[] arr = { 3, 9, 12, 6 };

    int N = arr.Length;

    // Function call
    sortPossible(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Recursive function to return
// gcd of a and b
function gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
         return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);
}

// Function to count number of set
// bits in an integer
function calculateSetBit(n)
{
    let count = 0;

    // Traverse every bits
    for(let i = 0; i < 32; i++)
    {
        if ((n & 1) != 0)
            count++;

        // Right shift by 1
        n = n >> 1;
    }
    return count;
}

// Function to check if sorting the
// given array is possible or not
function sortPossible(arr, n)
{

    // Duplicate array
    let dup = [];

    for(let i = 0; i < n; i++)
        dup[i] = arr[i];

    // Sorted array to check if the
    // original array can be sorted
    dup.sort();

    // Flag variable to check
    // if possible to sort
    let flag = 1;

    // Calculate bits of smallest
    // array element
    let bit = calculateSetBit(dup[0]);

    // Check every wrong placed
    // integer in the array
    for(let i = 0; i < n; i++)
    {
        if (arr[i] != dup[i])
        {

            // Swapping only if GCD of set
            // bits is equal to set bits in
            // smallest integer
            if (gcd(calculateSetBit(
                arr[i]), bit) != bit)
            {
                flag = 0;
                break;
            }
        }
    }

    // Print the result
    if (flag != 0)
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }
    return;
}

// Driver code
    let arr = [ 3, 9, 12, 6 ];
    let N = arr.length;

    // Function call
    sortPossible(arr, N);

     // This code is contributed by target_2.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)