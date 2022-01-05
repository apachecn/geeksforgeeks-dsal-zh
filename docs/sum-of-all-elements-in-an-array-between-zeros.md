# 零之间的数组中所有元素的总和

> 原文:[https://www . geesforgeks . org/全零数组元素之和/](https://www.geeksforgeeks.org/sum-of-all-elements-in-an-array-between-zeros/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出给定数组中两个零之间所有元素的[和。如果可能，那么打印所有的总和，否则打印 **"-1"** 。
**注意:**给定数组中没有连续的零。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = { 1，0，3，4，0，4，4，0，2，1，4，0，3 }
> **输出:** 7 8 7
> **解释:**
> 每 0 之间的元素之和为:
> 3 + 4 = 7
> 4 + 4 = 8
> 2 + 1 + 4 = 7
> 
> **输入:** arr[] = { 1，3，4，6，0}
> **输出:** -1

**进场:**

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，找到元素为 0 的第一个索引。
2.  如果值为零的任何元素出现，则开始将其后元素的总和存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)(比如 **A[]** )中，直到下一个零出现。
3.  对出现的每个零重复上述步骤。
4.  打印存储在[A]中的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to find the sum between two
// zeros in the given array arr[]
void sumBetweenZero(int arr[], int N)
{

    int i = 0;

    // To store the sum of element
    // between two zeros
    vector<int> A;

    // To store the sum
    int sum = 0;

    // Find first index of 0
    for (i = 0; i < N; i++) {
        if (arr[i] == 0) {
            i++;
            break;
        }
    }

    // Traverse the given array arr[]
    for (; i < N; i++) {

        // If 0 occurs then add it to A[]
        if (arr[i] == 0) {
            A.push_back(sum);
            sum = 0;
        }

        // Else add element to the sum
        else {
            sum += arr[i];
        }
    }

    // Print all the sum stored in A
    for (int i = 0; i < A.size(); i++) {
        cout << A[i] << ' ';
    }

    // If there is no such element print -1
    if (A.size() == 0)
        cout << "-1";
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 3, 4, 0, 4, 4,
                  0, 2, 1, 4, 0, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    sumBetweenZero(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the sum between two
// zeros in the given array arr[]
static void sumBetweenZero(int arr[], int N)
{
    int i = 0;

    // To store the sum of element
    // between two zeros
    Vector<Integer> A = new Vector<Integer>();

    // To store the sum
    int sum = 0;

    // Find first index of 0
    for(i = 0; i < N; i++)
    {
       if (arr[i] == 0)
       {
           i++;
           break;
       }
    }

    // Traverse the given array arr[]
    for(; i < N; i++)
    {

       // If 0 occurs then add it to A[]
       if (arr[i] == 0)
       {
           A.add(sum);
           sum = 0;
       }

       // Else add element to the sum
       else
       {
           sum += arr[i];
       }
    }

    // Print all the sum stored in A
    for(int j = 0; j < A.size(); j++)
    {
       System.out.print(A.get(j) + " ");
    }

    // If there is no such element print -1
    if (A.size() == 0)
        System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 3, 4, 0, 4, 4,
                  0, 2, 1, 4, 0, 3 };
    int N = arr.length;

    // Function call
    sumBetweenZero(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
#Python3 program for the above approach

# Function to find the sum between two
# zeros in the given array arr[]
def sumBetweenZero(arr, N):
    i = 0

    # To store the sum of the element
    # between two zeros
    A = []

    # To store the sum
    sum = 0

    # Find first index of 0
    for i in range(N):
        if (arr[i] == 0):
            i += 1
            break
    k = i

    # Traverse the given array arr[]
    for i in range(k, N, 1):

        # If 0 occurs then add it to A[]
        if (arr[i] == 0):
            A.append(sum)
            sum = 0

        # Else add element to the sum
        else:
            sum += arr[i]

    # Print all the sum stored in A
    for i in range(len(A)):
        print(A[i], end = ' ')

    # If there is no such element print -1
    if (len(A) == 0):
        print("-1")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 0, 3, 4, 0, 4, 4,
            0, 2, 1, 4, 0, 3 ]

    N = len(arr)

    # Function call
    sumBetweenZero(arr, N)

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the sum between two
// zeros in the given array []arr
static void sumBetweenZero(int []arr, int N)
{
    int i = 0;

    // To store the sum of element
    // between two zeros
    List<int> A = new List<int>();

    // To store the sum
    int sum = 0;

    // Find first index of 0
    for(i = 0; i < N; i++)
    {
       if (arr[i] == 0)
       {
           i++;
           break;
       }
    }

    // Traverse the given array []arr
    for(; i < N; i++)
    {

       // If 0 occurs then add it to []A
       if (arr[i] == 0)
       {
           A.Add(sum);
           sum = 0;
       }

       // Else add element to the sum
       else
       {
           sum += arr[i];
       }
    }

    // Print all the sum stored in A
    for(int j = 0; j < A.Count; j++)
    {
       Console.Write(A[j] + " ");
    }

    // If there is no such element print -1
    if (A.Count == 0)
        Console.Write("-1");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 3, 4, 0, 4, 4,
                  0, 2, 1, 4, 0, 3 };
    int N = arr.Length;

    // Function call
    sumBetweenZero(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the sum between two
// zeros in the given array arr[]
function sumBetweenZero(arr, N) {

    let i = 0;

    // To store the sum of element
    // between two zeros
    let A = new Array();

    // To store the sum
    let sum = 0;

    // Find first index of 0
    for (i = 0; i < N; i++) {
        if (arr[i] == 0) {
            i++;
            break;
        }
    }

    // Traverse the given array arr[]
    for (; i < N; i++) {

        // If 0 occurs then add it to A[]
        if (arr[i] == 0) {
            A.push(sum);
            sum = 0;
        }

        // Else add element to the sum
        else {
            sum += arr[i];
        }
    }

    // Print all the sum stored in A
    for (let i = 0; i < A.length; i++) {
        document.write(A[i] + ' ');
    }

    // If there is no such element print -1
    if (A.length == 0)
        document.write("-1");
}

// Driver Code

let arr = [1, 0, 3, 4, 0, 4, 4,
    0, 2, 1, 4, 0, 3];

let N = arr.length;

// Function call
sumBetweenZero(arr, N);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
7 8 7
```

**时间复杂度:** *O(N)* ，其中 N 为数组长度。