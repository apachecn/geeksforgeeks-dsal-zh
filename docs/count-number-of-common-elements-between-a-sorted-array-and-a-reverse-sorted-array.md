# 计算排序数组和反向排序数组之间的公共元素数量

> 原文:[https://www . geeksforgeeks . org/count-排序数组和反向排序数组之间的公共元素数/](https://www.geeksforgeeks.org/count-number-of-common-elements-between-a-sorted-array-and-a-reverse-sorted-array/)

给定两个由 **N** 不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，使得数组 **A[]** 和 **B[]** 分别按升序和降序排序，任务是找出两个数组中共有的值的数量。

**示例:**

> **输入:** A[] = {1，10，100}，B[] = {200，20，2 }
> T3】输出: 0
> 
> **输入:** A[] = {2，4，5，8，12，13，17，18，20，22，309，999}，B[] = {109，99，68，54，22，19，17，13，11，5，3，1}
> **输出:** 4

**方法:**给定的问题可以通过使用[双指针方法](https://www.geeksforgeeks.org/tag/two-pointer-algorithm/)来解决。按照以下步骤解决问题:

*   初始化两个变量，先将**表示为 **0** ，将**表示为**(N–1)**，分别用于从前面和**后面**遍历数组 **A[]** 和 **B[]** 。****
*   初始化一个变量，比如说**计数**为 **0** ，存储数组中常见的数字计数 **A[]** 和 **B[]** 。
*   [重复一个循环，直到](https://www.geeksforgeeks.org/range-based-loop-c/) **第一个< N** 和**第二个> = 0** 并执行以下步骤:
    *   如果 **A【第一次】**的值等于 **B【第二次】**，则递增**计数**和**第一次**的值，递减**第二次**的值。
    *   如果 **A【第一次】**的值小于 **B【第二次】**，则增加**第一次**的值。
    *   如果 **A【第一个】**的值大于 **B【第二个】**，则递减**第二个**的值。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// elements common in both the arrays
int countEqual(int A[], int B[], int N)
{
    // Used to traverse array A[] and
    // B[] from the front and the back
    int first = 0;
    int second = N - 1;

    // Stores the count of numbers
    // common in both array
    int count = 0;

    while (first < N && second >= 0) {

        // If A[first] is less than
        // B[second]
        if (A[first] < B[second]) {

            // Increment the value
            // of first
            first++;
        }

        // IF B[second] is less
        // than A[first]
        else if (B[second] < A[first]) {

            // Decrement the value
            // of second
            second--;
        }

        // A[first] is equal to
        // B[second]
        else {

            // Increment the value
            // of count
            count++;

            // Increment the value
            // of first
            first++;

            // Decrement the value
            // of second
            second--;
        }
    }

    // Return the value of count
    return count;
}

// Driver Code
int main()
{
    int A[] = { 2, 4, 5, 8, 12, 13, 17,
                18, 20, 22, 309, 999 };
    int B[] = { 109, 99, 68, 54, 22, 19,
                17, 13, 11, 5, 3, 1 };
    int N = sizeof(A) / sizeof(int);
    cout << countEqual(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{

// Function to count the number of
// elements common in both the arrays
static int countEqual(int A[], int B[], int N)
{

    // Used to traverse array A[] and
    // B[] from the front and the back
    int first = 0;
    int second = N - 1;

    // Stores the count of numbers
    // common in both array
    int count = 0;

    while (first < N && second >= 0) {

        // If A[first] is less than
        // B[second]
        if (A[first] < B[second]) {

            // Increment the value
            // of first
            first++;
        }

        // IF B[second] is less
        // than A[first]
        else if (B[second] < A[first]) {

            // Decrement the value
            // of second
            second--;
        }

        // A[first] is equal to
        // B[second]
        else {

            // Increment the value
            // of count
            count++;

            // Increment the value
            // of first
            first++;

            // Decrement the value
            // of second
            second--;
        }
    }

    // Return the value of count
    return count;
}

    // Driver Code
    public static void main(String[] args)
    {

        int A[] = { 2, 4, 5, 8, 12, 13, 17,
                18, 20, 22, 309, 999 };
    int B[] = { 109, 99, 68, 54, 22, 19,
                17, 13, 11, 5, 3, 1 };
    int N = A.length;
    System.out.println(countEqual(A, B, N));
    }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the number of
# elements common in both the arrays
def countEqual(A, B, N) :

    # Used to traverse array A[] and
    # B[] from the front and the back
    first = 0
    second = N - 1

    # Stores the count of numbers
    # common in both array
    count = 0

    while (first < N and second >= 0) :

        # If A[first] is less than
        # B[second]
        if (A[first] < B[second]) :

            # Increment the value
            # of first
            first += 1

        # IF B[second] is less
        # than A[first]
        elif (B[second] < A[first]) :

            # Decrement the value
            # of second
            second -= 1

        # A[first] is equal to
        # B[second]
        else :

            # Increment the value
            # of count
            count += 1

            # Increment the value
            # of first
            first += 1

            # Decrement the value
            # of second
            second -= 1

    # Return the value of count
    return count

# Driver Code

A= [ 2, 4, 5, 8, 12, 13, 17,
                18, 20, 22, 309, 999 ]
B = [ 109, 99, 68, 54, 22, 19,
                17, 13, 11, 5, 3, 1 ]
N = len(A)
print(countEqual(A, B, N))

# This code is contributed by sanjou_62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// elements common in both the arrays
static int countEqual(int[] A, int[] B, int N)
{

    // Used to traverse array A[] and
    // B[] from the front and the back
    int first = 0;
    int second = N - 1;

    // Stores the count of numbers
    // common in both array
    int count = 0;

    while (first < N && second >= 0)
    {

        // If A[first] is less than
        // B[second]
        if (A[first] < B[second])
        {

            // Increment the value
            // of first
            first++;
        }

        // IF B[second] is less
        // than A[first]
        else if (B[second] < A[first])
        {

            // Decrement the value
            // of second
            second--;
        }

        // A[first] is equal to
        // B[second]
        else
        {

            // Increment the value
            // of count
            count++;

            // Increment the value
            // of first
            first++;

            // Decrement the value
            // of second
            second--;
        }
    }

    // Return the value of count
    return count;
}

// Driver code
static void Main()
{
    int[] A = { 2, 4, 5, 8, 12, 13,
                17, 18, 20, 22, 309, 999 };
    int[] B = { 109, 99, 68, 54, 22, 19,
                17, 13, 11, 5, 3, 1 };
    int N = A.Length;

    Console.WriteLine(countEqual(A, B, N));
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number of
// elements common in both the arrays
function countEqual(A, B, N)
{

    // Used to traverse array A[] and
    // B[] from the front and the back
    let first = 0;
    let second = N - 1;

    // Stores the count of numbers
    // common in both array
    let count = 0;

    while (first < N && second >= 0) {

        // If A[first] is less than
        // B[second]
        if (A[first] < B[second]) {

            // Increment the value
            // of first
            first++;
        }

        // IF B[second] is less
        // than A[first]
        else if (B[second] < A[first]) {

            // Decrement the value
            // of second
            second--;
        }

        // A[first] is equal to
        // B[second]
        else {

            // Increment the value
            // of count
            count++;

            // Increment the value
            // of first
            first++;

            // Decrement the value
            // of second
            second--;
        }
    }

    // Return the value of count
    return count;
}

// Driver Code

let A = [2, 4, 5, 8, 12, 13, 17,
    18, 20, 22, 309, 999];
let B = [109, 99, 68, 54, 22, 19,
    17, 13, 11, 5, 3, 1];
let N = A.length;
document.write(countEqual(A, B, N));

// This code is contributed _saurabh_jaiswal
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)