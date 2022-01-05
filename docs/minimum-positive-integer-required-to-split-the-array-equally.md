# 等分数组所需的最小正整数

> 原文:[https://www . geesforgeks . org/minimum-正整数-需要平均拆分数组/](https://www.geeksforgeeks.org/minimum-positive-integer-required-to-split-the-array-equally/)

给定一个由 N 个正整数组成的数组，任务是找到可以放在数组任意两个元素之间的**最小的**正整数，这样，出现在它之前的子数组中的元素之和**等于出现在它之后的子数组中的元素之和**，新放置的整数包含在两个子数组中的任何一个中。
**例:**

```
Input : arr = { 3, 2, 1, 5, 7, 8 }
Output : 4
Explanation
The smallest possible number that can be inserted is 4 between elements 5 and 7 
as part of the first subarray so that the sum of the two subarrays becomes 
equal i.e, 3 + 2 + 1 + 5 + 4 = 15 and 7 + 8 = 15.

Input : arr = { 3, 2, 2, 3 }
Output : No Extra Element required
Explanation
Equal sum of 5 is obtained by adding the first two elements and last two elements 
as separate subarrays without inserting any extra number.
```

**逼近:**让整个数组的和除以 s，想法是找到左和直到索引 I(包括它)。设这个和为 l，现在是子阵的和 <sub>i + 1 ……。N</sub> 是**S–L**。让这个和为 R。因为两个子阵列的和应该相等，所以上面获得的两个和 L 和 R 中的较大者应该减少到这两者中较小者的值，并且较大者和较小者之间的差将是所需正整数的值，这需要最小化。
穿越时有两种情况:

1.  **L > R** :使左右子阵列之和相等所需的元素值将为**L–R**，如果该值小于之前计算的最小元素值，则该值成为所需的最小元素。显然，这个元素将是具有较小总和的子阵列的一部分，也就是说，在这种情况下是正确的子阵列
2.  **R > L** :使左右子阵列之和相等所需的元素值将为**R–L**，如果该值小于之前计算的最小元素值，则该值成为所需的最小元素。显然，这个元素将是具有较小总和的子阵列的一部分，即左子阵列就是这种情况

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum non-negative
// element required to split the array
// into two subarrays with equal sum
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum positive integer
// required to split array into two subarrays with equal sums
int findMinimumSplit(int arr[], int n)
{

    // Find the sum of whole array
    int totalSum = 0;
    for (int i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    // leftSubarraySum stores the sum of arr[0....i] and
    // rightSubarraySum stores the sum of arr[i + 1....n]
    int leftSubarraySum = 0;
    int rightSubarraySum = 0;
    int minimumElement = INT_MAX;

    for (int i = 0; i < n - 1; i++) {
        // Find the left subarray sum and
        // corresponding right subarray sum
        leftSubarraySum += arr[i];
        rightSubarraySum = totalSum - leftSubarraySum;

        // if left subarray has larger sum, find the
        // element to be included in the right subarray
        // to make their sums equal
        if (leftSubarraySum > rightSubarraySum) {
            int element = leftSubarraySum - rightSubarraySum;
            if (element < minimumElement) {
                minimumElement = element;
            }
        }
        // the Right subarray has larger sum,
        // find the element to be included in
        // the left subarray to make their sums equal
        else {
            int element = rightSubarraySum - leftSubarraySum;
            if (element < minimumElement) {
                minimumElement = element;
            }
        }
    }

    return minimumElement;
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, 1, 5, 7, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int minimumElement = findMinimumSplit(arr, n);

    // If 0 then no insertion is required
    if (minimumElement == 0) {
        cout << "No Extra Element Required" << endl;
    }
    else {
        cout << minimumElement << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum non-negative
// element required to split the array
// into two subarrays with equal sum
import java.util.*;

class solution
{

// Function to return the minimum positive integer
// required to split array into two subarrays with equal sums
static int findMinimumSplit(int arr[], int n)
{

    // Find the sum of whole array
    int totalSum = 0;
    for (int i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    // leftSubarraySum stores the sum of arr[0....i] and
    // rightSubarraySum stores the sum of arr[i + 1....n]
    int leftSubarraySum = 0;
    int rightSubarraySum = 0;
    int minimumElement = Integer.MAX_VALUE;

    for (int i = 0; i < n - 1; i++) {
        // Find the left subarray sum and
        // corresponding right subarray sum
        leftSubarraySum += arr[i];
        rightSubarraySum = totalSum - leftSubarraySum;

        // if left subarray has larger sum, find the
        // element to be included in the right subarray
        // to make their sums equal
        if (leftSubarraySum > rightSubarraySum) {
            int element = leftSubarraySum - rightSubarraySum;
            if (element < minimumElement) {
                minimumElement = element;
            }
        }
        // the Right subarray has larger sum,
        // find the element to be included in
        // the left subarray to make their sums equal
        else {
            int element = rightSubarraySum - leftSubarraySum;
            if (element < minimumElement) {
                minimumElement = element;
            }
        }
    }

    return minimumElement;
}

// Driver Code
public static void main(String args[])
{

    int arr[] = { 3, 2, 1, 5, 7, 8 };
    int n = arr.length;

    int minimumElement = findMinimumSplit(arr, n);

    // If 0 then no insertion is required
    if (minimumElement == 0) {
        System.out.println("No Extra Element Required");
    }
    else {
        System.out.println(minimumElement);
    }

}

}
// This code is contributed by
// Sanjit_Prasad
```

## 蟒蛇 3

```
# Python 3 program to find the minimum
# non-negative element required to split
# the array into two subarrays with equal sum
import sys

# Function to return the minimum positive
# integer required to split array into two
# subarrays with equal sums
def findMinimumSplit(arr, n):

    # Find the sum of whole array
    totalSum = 0
    for i in range(n):
        totalSum += arr[i]

    # leftSubarraySum stores the sum of
    # arr[0....i] and rightSubarraySum
    # stores the sum of arr[i + 1....n]
    leftSubarraySum = 0
    rightSubarraySum = 0
    minimumElement = sys.maxsize

    for i in range(n - 1):

        # Find the left subarray sum and
        # corresponding right subarray sum
        leftSubarraySum += arr[i]
        rightSubarraySum = totalSum - leftSubarraySum

        # if left subarray has larger sum, find the
        # element to be included in the right
        # subarray to make their sums equal
        if (leftSubarraySum > rightSubarraySum):
            element = leftSubarraySum - rightSubarraySum
            if (element < minimumElement) :
                minimumElement = element

        # the Right subarray has larger sum,
        # find the element to be included in
        # the left subarray to make their sums equal
        else :
            element = rightSubarraySum - leftSubarraySum
            if (element < minimumElement) :
                minimumElement = element

    return minimumElement

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 2, 1, 5, 7, 8 ]
    n = len(arr)

    minimumElement = findMinimumSplit(arr, n)

    # If 0 then no insertion is required
    if (minimumElement == 0):
        print( "No Extra Element Required" )

    else :
        print(minimumElement)

# This code is contributed by ita_c
```

## C#

```
// C# program to find the
// minimum non-negative
// element required to split
// the array into two
// subarrays with equal sum
using System;

class GFG
{

// Function to return the
// minimum positive integer
// required to split array
// into two subarrays with
// equal sums
static int findMinimumSplit(int []arr,
                            int n)
{

    // Find the sum
    // of whole array
    int totalSum = 0;
    for (int i = 0; i < n; i++)
    {
        totalSum += arr[i];
    }

    // leftSubarraySum stores
    // the sum of arr[0....i]
    // and rightSubarraySum
    // stores the sum of
    // arr[i + 1....n]
    int leftSubarraySum = 0;
    int rightSubarraySum = 0;
    int minimumElement = int.MaxValue;

    for (int i = 0; i < n - 1; i++)
    {
        // Find the left subarray
        // sum and corresponding
        // right subarray sum
        leftSubarraySum += arr[i];
        rightSubarraySum = totalSum -
                           leftSubarraySum;

        // if left subarray has
        // larger sum, find the
        // element to be included
        // in the right subarray
        // to make their sums equal
        if (leftSubarraySum >
            rightSubarraySum)
        {
            int element = leftSubarraySum -
                          rightSubarraySum;
            if (element < minimumElement)
            {
                minimumElement = element;
            }
        }

        // the Right subarray has
        // larger sum, find the
        // element to be included
        // in the left subarray to
        // make their sums equal
        else
        {
            int element = rightSubarraySum -
                          leftSubarraySum;
            if (element < minimumElement)
            {
                minimumElement = element;
            }
        }
    }

    return minimumElement;
}

// Driver Code
public static void Main ()
{
    int []arr = {3, 2, 1, 5, 7, 8};
    int n = arr.Length;

    int minimumElement =
        findMinimumSplit(arr, n);

    // If 0 then no
    // insertion is required
    if (minimumElement == 0)
    {
        Console.WriteLine("No Extra " +
                   "Element Required");
    }
    else
    {
        Console.WriteLine(minimumElement);
    }
}
}

// This code is contributed
// by anuj_67.
```

## java 描述语言

```
<script>
// Javascript program to find the minimum non-negative
// element required to split the array
// into two subarrays with equal sum

    // Function to return the minimum positive integer
    // required to split array into two subarrays with equal sums
    function findMinimumSplit(arr,n)
    {
        // Find the sum of whole array
    let totalSum = 0;
    for (let i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    // leftSubarraySum stores the sum of arr[0....i] and
    // rightSubarraySum stores the sum of arr[i + 1....n]
    let leftSubarraySum = 0;
    let rightSubarraySum = 0;
    let minimumElement = Number.MAX_VALUE;

    for (let i = 0; i < n - 1; i++) {
        // Find the left subarray sum and
        // corresponding right subarray sum
        leftSubarraySum += arr[i];
        rightSubarraySum = totalSum - leftSubarraySum;

        // if left subarray has larger sum, find the
        // element to be included in the right subarray
        // to make their sums equal
        if (leftSubarraySum > rightSubarraySum) {
            let element = leftSubarraySum - rightSubarraySum;
            if (element < minimumElement) {
                minimumElement = element;
            }
        }
        // the Right subarray has larger sum,
        // find the element to be included in
        // the left subarray to make their sums equal
        else {
            let element = rightSubarraySum - leftSubarraySum;
            if (element < minimumElement) {
                minimumElement = element;
            }
        }
    }

    return minimumElement;
    }

    // Driver Code
    let arr=[3, 2, 1, 5, 7, 8];
    let n = arr.length;
    let minimumElement = findMinimumSplit(arr, n);
    // If 0 then no insertion is required
    if (minimumElement == 0) {
        document.write("No Extra Element Required");
    }
    else {
        document.write(minimumElement);
    }

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)，其中 N 为数组中的元素个数。