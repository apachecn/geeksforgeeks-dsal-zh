# 通过从任一端移除元素来查找最小可能数组和的查询

> 原文:[https://www . geesforgeks . org/query-to-find-通过从任一端移除元素来最小化总和/](https://www.geeksforgeeks.org/queries-to-find-minimum-sum-by-removing-elements-from-either-end/)

给定一个由 **N** 不同的**T7】整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个表示查询的数组**Q【】**，每个查询的任务 **Q[i]** 是通过从任一端移除数组元素来找到可能的最小和，直到获得 **Q[i]** 。**

**示例:**

> **输入:** arr[] = {2，3，6，7，4，5，1}，Q[] = {7，6}
> **输出:** 17 11
> **解释:**
> **查询 1:** 通过从末尾弹出元素，求和= 1 + 5 + 4 + 7 = 17。
> **查询 2:** 从前面弹出元素，总和= 2 + 3 + 6 = 11。
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10}，Q[] = {4，6，3}
> **输出:** 10 21 6

**朴素方法:**解决给定问题的最简单方法是[从两端遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)进行每个查询 **Q[i]** 并打印从两次遍历中获得的最小和，直到获得值为 **Q[i]** 的元素。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum for
// each query after removing elements
// from either ends
void minSum(int arr[], int N, int Q[],
            int M)
{
    // Traverse the query array
    for (int i = 0; i < M; i++) {
        int val = Q[i];

        int front = 0, rear = 0;

        // Traverse the array from
        // the front
        for (int j = 0; j < N; j++) {
            front += arr[j];

            // If element equals val,
            // then break out of loop
            if (arr[j] == val) {
                break;
            }
        }

        // Traverse the array from rear
        for (int j = N - 1; j >= 0; j--) {
            rear += arr[j];

            // If element equals val, break
            if (arr[j] == val) {
                break;
            }
        }

        // Print the minimum of the
        // two as the answer
        cout << min(front, rear) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 6, 7, 4, 5, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q[] = { 7, 6 };
    int M = sizeof(Q) / sizeof(Q[0]);

    // Function Call
    minSum(arr, N, Q, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the minimum sum for
// each query after removing elements
// from either ends
static void minSum(int arr[], int N, int Q[],
            int M)
{

    // Traverse the query array
    for (int i = 0; i < M; i++)
    {
        int val = Q[i];
        int front = 0, rear = 0;

        // Traverse the array from
        // the front
        for (int j = 0; j < N; j++)
        {
            front += arr[j];

            // If element equals val,
            // then break out of loop
            if (arr[j] == val)
            {
                break;
            }
        }

        // Traverse the array from rear
        for (int j = N - 1; j >= 0; j--)
        {
            rear += arr[j];

            // If element equals val, break
            if (arr[j] == val)
            {
                break;
            }
        }

        // Print the minimum of the
        // two as the answer
        System.out.print(Math.min(front, rear) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 6, 7, 4, 5, 1 };
    int N = arr.length;
    int Q[] = { 7, 6 };
    int M = Q.length;

    // Function Call
    minSum(arr, N, Q, M);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum sum for
# each query after removing elements
# from either ends
def minSum(arr, N, Q, M):

    # Traverse the query array
    for i in range(M):
        val = Q[i]

        front, rear = 0, 0

        # Traverse the array from
        # the front
        for j in range(N):
            front += arr[j]

            # If element equals val,
            # then break out of loop
            if (arr[j] == val):
                break

        # Traverse the array from rear
        for j in range(N - 1, -1, -1):
            rear += arr[j]

            # If element equals val, break
            if (arr[j] == val):
                break

        # Print the minimum of the
        # two as the answer
        print(min(front, rear), end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 6, 7, 4, 5, 1]
    N = len(arr)
    Q = [7, 6]
    M = len(Q)

    # Function Call
    minSum(arr, N, Q, M)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum sum for
// each query after removing elements
// from either ends
static void minSum(int[] arr, int N, int[] Q,
                   int M)
{

    // Traverse the query array
    for(int i = 0; i < M; i++)
    {
        int val = Q[i];
        int front = 0, rear = 0;

        // Traverse the array from
        // the front
        for(int j = 0; j < N; j++)
        {
            front += arr[j];

            // If element equals val,
            // then break out of loop
            if (arr[j] == val)
            {
                break;
            }
        }

        // Traverse the array from rear
        for(int j = N - 1; j >= 0; j--)
        {
            rear += arr[j];

            // If element equals val, break
            if (arr[j] == val)
            {
                break;
            }
        }

        // Print the minimum of the
        // two as the answer
        Console.Write(Math.Min(front, rear) + " ");
    }
}

// Driver Code
static public void Main()
{
    int[] arr = { 2, 3, 6, 7, 4, 5, 1 };
    int N = arr.Length;
    int[] Q = { 7, 6 };
    int M = Q.Length;

    // Function Call
    minSum(arr, N, Q, M);
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum sum for
// each query after removing elements
// from either ends
function minSum(arr,  N, Q, M)
{
    // Traverse the query array
    for (var i = 0; i < M; i++) {
        var val = Q[i];

        var front = 0, rear = 0;

        // Traverse the array from
        // the front
        for (var j = 0; j < N; j++) {
            front += arr[j];

            // If element equals val,
            // then break out of loop
            if (arr[j] == val) {
                break;
            }
        }

        // Traverse the array from rear
        for (var j = N - 1; j >= 0; j--) {
            rear += arr[j];

            // If element equals val, break
            if (arr[j] == val) {
                break;
            }
        }

        // Print the minimum of the
        // two as the answer
        document.write( Math.min(front, rear) + " ");
    }
}

var arr = [ 2, 3, 6, 7, 4, 5, 1 ];
var N = arr.length;
var Q = [ 7, 6 ];
var M = Q.length;

    // Function Call
    minSum(arr, N, Q, M);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
17 11
```

**时间复杂度:** *O(N*M)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，思路是使用[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术来解决这个问题。按照以下步骤解决问题:

*   创建两个辅助[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **M1** 和 **M2** 。
*   [从前面遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，将计算出的当前总和连同元素一起插入到地图 **M1** 中的每个索引处。
*   同样，从后面遍历数组，将计算出的当前总和连同元素一起插入到地图中的每个索引 **M2** 处。
*   遍历数组 **Q[]** ，对于每个元素 **Q[i]** ，打印最小的**M1【Q[I]】**和**M2【Q[I]】**作为最小可能和。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum
// for each query after removing
// element from either ends till each
// value Q[i]
void minOperations(int arr[], int N,
                   int Q[], int M)
{
    // Stores the prefix sum from
    // both the ends of the array
    map<int, int> m1, m2;

    int front = 0, rear = 0;

    // Traverse the array from front
    for (int i = 0; i < N; i++) {
        front += arr[i];

        // Insert it into the map m1
        m1.insert({ arr[i], front });
    }

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--) {
        rear += arr[i];

        // Insert it into the map m2
        m2.insert({ arr[i], rear });
    }

    // Traverse the query array
    for (int i = 0; i < M; i++) {

        // Print the minimum of the
        // two values as the answer
        cout << min(m1[Q[i]], m2[Q[i]])
             << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 6, 7, 4, 5, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q[] = { 7, 6 };
    int M = sizeof(Q) / sizeof(Q[0]);

    // Function Call
    minOperations(arr, N, Q, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum sum
// for each query after removing
// element from either ends till each
// value Q[i]
static void minOperations(int[] arr, int N,
                          int[] Q, int M)
{

    // Stores the prefix sum from
    // both the ends of the array
    Map<Integer,
        Integer> m1 = new HashMap<Integer,
                                  Integer>();
    Map<Integer,
        Integer> m2 = new HashMap<Integer,
                                  Integer>();

    int front = 0, rear = 0;

    // Traverse the array from front
    for(int i = 0; i < N; i++)
    {
        front += arr[i];

        // Insert it into the map m1
        m1.put(arr[i], front);
    }

    // Traverse the array in reverse
    for(int i = N - 1; i >= 0; i--)
    {
        rear += arr[i];

        // Insert it into the map m2
        m2.put(arr[i], rear);
    }

    // Traverse the query array
    for(int i = 0; i < M; i++)
    {

        // Print the minimum of the
        // two values as the answer
        System.out.print(Math.min(m1.get(Q[i]),
                                  m2.get(Q[i])) + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 6, 7, 4, 5, 1 };
    int N = arr.length;
    int[] Q = { 7, 6 };
    int M = Q.length;

    // Function Call
    minOperations(arr, N, Q, M);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum sum
# for each query after removing
# element from either ends till each
# value Q[i]
def minOperations(arr, N, Q, M):

    # Stores the prefix sum from
    # both the ends of the array
    m1 = {}
    m2 = {}
    front = 0
    rear = 0

    # Traverse the array from front
    for i in range(N):
        front += arr[i]

        # Insert it into the map m1
        m1[arr[i]] = front

    # Traverse the array in reverse
    for i in range(N - 1, -1, -1):
        rear += arr[i]

        # Insert it into the map m2
        m2[arr[i]] = rear

    # Traverse the query array
    for i in range(M):

        # Print the minimum of the
        # two values as the answer
        print(min(m1[Q[i]], m2[Q[i]]),end=" ")

# Driver Code
arr = [2, 3, 6, 7, 4, 5, 1 ]
N = len(arr)
Q = [7,6]
M = len(Q)

# Function Call
minOperations(arr, N, Q, M)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum sum
// for each query after removing
// element from either ends till each
// value Q[i]
static void minOperations(int[] arr, int N,
                          int[] Q, int M)
{

    // Stores the prefix sum from
    // both the ends of the array
    Dictionary<int,
               int> m1 = new Dictionary<int,
                                        int>();
    Dictionary<int,
               int> m2 = new Dictionary<int,
                                        int>();

    int front = 0, rear = 0;

    // Traverse the array from front
    for(int i = 0; i < N; i++)
    {
        front += arr[i];

        // Insert it into the map m1
        m1[arr[i]] = front;
    }

    // Traverse the array in reverse
    for(int i = N - 1; i >= 0; i--)
    {
        rear += arr[i];

        // Insert it into the map m2
        m2[arr[i]] = rear;
    }

    // Traverse the query array
    for(int i = 0; i < M; i++)
    {

        // Print the minimum of the
        // two values as the answer
        Console.Write(Math.Min(m1[Q[i]],
                               m2[Q[i]]) + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 3, 6, 7, 4, 5, 1 };
    int N = arr.Length;
    int[] Q = { 7, 6 };
    int M = Q.Length;

    // Function Call
    minOperations(arr, N, Q, M);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find the minimum sum
// for each query after removing
// element from either ends till each
// value Q[i]
function minOperations(arr, N, Q, M)
{
    // Stores the prefix sum from
    // both the ends of the array

    var m1 = new Map();
    var m2 = new Map();

    var front = 0, rear = 0;
    var i;
    // Traverse the array from front
    for (i = 0; i < N; i++) {
        front += arr[i];

        // Insert it into the map m1
        m1.set(arr[i],front);
    }

    // Traverse the array in reverse
    for (i = N - 1; i >= 0; i--) {
        rear += arr[i];

        // Insert it into the map m2
        m2.set(arr[i], rear);
    }

    // Traverse the query array
    for (i = 0; i < M; i++) {

        // Print the minimum of the
        // two values as the answer
        document.write(Math.min(m1.get(Q[i]), m2.get(Q[i])) + " ");
    }
}

// Driver Code
    var arr = [2, 3, 6, 7, 4, 5, 1];
    var N = arr.length;
    var Q = [7, 6];
    var M = Q.length;

    // Function Call
    minOperations(arr, N, Q, M);

 // This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
17 11
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*