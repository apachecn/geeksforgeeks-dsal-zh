# 划分成两个相等和的相邻元素子阵列

> 原文:[https://www . geeksforgeeks . org/等和分割成两个连续元素子数组/](https://www.geeksforgeeks.org/partitioning-into-two-contiguous-element-subarray-with-equal-sums/)

给定 n 个正整数的数组。找到要添加到数组中的一个索引的最小正元素，以便它可以被划分为两个相等和的连续子数组。输出要添加的最小元素及其位置。如果可能有多个位置，则返回最少的一个。
**例:**

> 输入:arr[] = { 10，1，2，3，4 }
> 输出:0 0
> **解释:**数组已经可以划分为两个相邻的子数组，即{10}和{ 1，2，3，4 }的和相等。所以我们需要在任何位置加 0。(最小位置为 0)
> 
> 输入:arr[] = { 5，4 }
> 输出:1 1
> **解释:**我们需要添加 1 到 4，这样两个子数组为{5}，{5}因此输出为 1 1(最小元素及其要添加的位置。

**先决条件:** [前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
**方法 1(简单):**一种天真的方法是计算从(arr[0]到 arr[i])和(arr[i+1]到 arr[n-1])的元素和，并在每一步找到这两个和之间的差，最小差将给出要添加的元素。
**方法 2(高效)**:仔细分析建议可以使用前缀和后缀和的概念。计算两者并找出前缀 Sum[i](其中前缀 Sum[i]是到第一个位置的数组元素的总和)和后缀 Sum[i + 1](其中后缀 Sum[i + 1]是从第(i + 1)个位置到最后一个位置的数组元素的总和)之间的绝对差。
**例如**

```
arr              10    1    2    3    4
prefixSum        10    11   13   16   20
suffixSum        20    10   9    7    4

Absolute difference between suffixSum[i + 1] and prefixSum[i]
10 - 10 = 0 // minimum
11 - 9  = 1
13 - 7  = 6
16 - 4  = 12
Thus, minimum element is 0, for position,
if prefixSum[i] is greater than suffixSum[i + 1], then position is "i + 1".
else it's is "i".
```

下面是上述方法的实现。

## C++

```
// CPP Program to find the minimum element to
// be added such that the array can be partitioned
// into two contiguous subarrays with equal sums
#include <bits/stdc++.h>

using namespace std;

// Structure to store the minimum element
// and its position
struct data {
    int element;
    int position;
};

struct data findMinElement(int arr[], int n)
{
    struct data result;

    // initialize prefix and suffix sum arrays with 0
    int prefixSum[n] = { 0 };
    int suffixSum[n] = { 0 };

    prefixSum[0] = arr[0];
    for (int i = 1; i < n; i++) {
        // add current element to Sum
        prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    suffixSum[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        // add current element to Sum
        suffixSum[i] = suffixSum[i + 1] + arr[i];
    }

    // initialize the minimum element to be a large value
    int min = suffixSum[0];
    int pos;

    for (int i = 0; i < n - 1; i++) {
        // check for the minimum absolute difference
        // between current prefix sum and the next
        // suffix sum element
        if (abs(suffixSum[i + 1] - prefixSum[i]) < min) {
            min = abs(suffixSum[i + 1] - prefixSum[i]);

            // if prefixsum has a greater value then position
            // is the next element, else it's the same element.
            if (suffixSum[i + 1] < prefixSum[i]) pos = i + 1;
            else     pos = i;
        }
    }

    // return the data in struct.
    result.element = min;
    result.position = pos;
    return result;
}

// Driver Code
int main()
{
    int arr[] = { 10, 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    struct data values;

    values = findMinElement(arr, n);
    cout << "Minimum element : " << values.element
        << endl << "Position : " << values.position;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum element to
// be added such that the array can be partitioned
// into two contiguous subarrays with equal sums
import java.util.*;

class GFG
{

// Structure to store the minimum element
// and its position
static class data
{
    int element;
    int position;
};

static data findMinElement(int arr[], int n)
{
    data result=new data();

    // initialize prefix and suffix sum arrays with 0
    int []prefixSum = new int[n];
    int []suffixSum = new int[n];

    prefixSum[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        // add current element to Sum
        prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    suffixSum[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
    {
        // add current element to Sum
        suffixSum[i] = suffixSum[i + 1] + arr[i];
    }

    // initialize the minimum element to be a large value
    int min = suffixSum[0];
    int pos=0;

    for (int i = 0; i < n - 1; i++)
    {
        // check for the minimum absolute difference
        // between current prefix sum and the next
        // suffix sum element
        if (Math.abs(suffixSum[i + 1] - prefixSum[i]) < min)
        {
            min = Math.abs(suffixSum[i + 1] - prefixSum[i]);

            // if prefixsum has a greater value then position
            // is the next element, else it's the same element.
            if (suffixSum[i + 1] < prefixSum[i]) pos = i + 1;
            else     pos = i;
        }
    }

    // return the data in struct.
    result.element = min;
    result.position = pos;
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 10, 1, 2, 3, 4 };
    int n = arr.length;
    data values;

    values = findMinElement(arr, n);
    System.out.println("Minimum element : " + values.element
        + "\nPosition : " + values.position);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python Program to find the minimum element to
# be added such that the array can be partitioned
# into two contiguous subarrays with equal sums

# Class to store the minimum element
# and its position
class Data:
    def __init__(self):
        self.element = -1
        self.position = -1

def findMinElement(arr, n):
    result = Data()

    # initialize prefix and suffix sum arrays with 0
    prefixSum = [0]*n
    suffixSum = [0]*n

    prefixSum[0] = arr[0]
    for i in range(1, n):

        # add current element to Sum
        prefixSum[i] = prefixSum[i-1] + arr[i]\

    suffixSum[n-1] = arr[n-1]
    for i in range(n-2, -1, -1):

        # add current element to Sum
        suffixSum[i] = suffixSum[i+1] + arr[i]

    # initialize the minimum element to be a large value
    mini = suffixSum[0]
    pos = 0
    for i in range(n-1):

        # check for the minimum absolute difference
        # between current prefix sum and the next
        # suffix sum element
        if abs(suffixSum[i+1]-prefixSum[i]) < mini:
            mini = abs(suffixSum[i+1] - prefixSum[i])

            # if prefixsum has a greater value then position
            # is the next element, else it's the same element.
            if suffixSum[i+1] < prefixSum[i]:
                pos = i+1
            else:
                pos = i

    # return the data in class.
    result.element = mini
    result.position = pos

    return result

# Driver Code
if __name__ == "__main__":
    arr = [10, 1, 2, 3, 4]
    n = len(arr)
    values = Data()

    values = findMinElement(arr, n)

    print("Minimum element :", values.element, "\nPosition :", values.position)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# Program to find the minimum element
// to be added such that the array can be
// partitioned into two contiguous subarrays
// with equal sums
using System;

class GFG
{

// Structure to store the minimum element
// and its position
public class data
{
    public int element;
    public int position;
};

static data findMinElement(int []arr, int n)
{
    data result = new data();

    // initialize prefix and suffix
    // sum arrays with 0
    int []prefixSum = new int[n];
    int []suffixSum = new int[n];

    prefixSum[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        // add current element to Sum
        prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    suffixSum[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
    {
        // add current element to Sum
        suffixSum[i] = suffixSum[i + 1] + arr[i];
    }

    // initialize the minimum element
    // to be a large value
    int min = suffixSum[0];
    int pos = 0;

    for (int i = 0; i < n - 1; i++)
    {
        // check for the minimum absolute difference
        // between current prefix sum and the next
        // suffix sum element
        if (Math.Abs(suffixSum[i + 1] -
                     prefixSum[i]) < min)
        {
            min = Math.Abs(suffixSum[i + 1] -
                           prefixSum[i]);

            // if prefixsum has a greater value then position
            // is the next element, else it's the same element.
            if (suffixSum[i + 1] < prefixSum[i])
                pos = i + 1;
            else    
                pos = i;
        }
    }

    // return the data in struct.
    result.element = min;
    result.position = pos;
    return result;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 10, 1, 2, 3, 4 };
    int n = arr.Length;
    data values;

    values = findMinElement(arr, n);
    Console.WriteLine("Minimum element : " +
                            values.element +
                           "\nPosition : " +
                           values.position);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript Program to find the minimum element to
// be added such that the array can be partitioned
// into two contiguous subarrays with equal sums

// Structure to store the minimum element
// and its position
class data
{
    constructor(element, position){
        this.element = element;
        this.position = position;
    }
};

function findMinElement(arr, n)
{
    let result = new data();

    // initialize prefix and suffix sum arrays with 0
    let prefixSum = new Array(n);
    let suffixSum = new Array(n);

    prefixSum[0] = arr[0];
    for (let i = 1; i < n; i++)
    {
        // add current element to Sum
        prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    suffixSum[n - 1] = arr[n - 1];
    for (let i = n - 2; i >= 0; i--)
    {
        // add current element to Sum
        suffixSum[i] = suffixSum[i + 1] + arr[i];
    }

    // initialize the minimum element to be a large value
    let min = suffixSum[0];
    let pos=0;

    for (let i = 0; i < n - 1; i++)
    {
        // check for the minimum absolute difference
        // between current prefix sum and the next
        // suffix sum element
        if (Math.abs(suffixSum[i + 1] - prefixSum[i]) < min)
        {
            min = Math.abs(suffixSum[i + 1] - prefixSum[i]);

            // if prefixsum has a greater value then position
            // is the next element, else it's the same element.
            if (suffixSum[i + 1] < prefixSum[i]) pos = i + 1;
            else     pos = i;
        }
    }

    // return the data in struct.
    result.element = min;
    result.position = pos;
    return result;
}

// Driver Code

    let arr = [ 10, 1, 2, 3, 4 ];
    let n = arr.length;
    let values;

    values = findMinElement(arr, n);
    document.write("Minimum element : " +
    values.element + "<br>Position : " + values.position);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Minimum element : 0
Position : 0
```