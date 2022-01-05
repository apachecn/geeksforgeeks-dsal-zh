# 数组逆时针旋转 K 次的范围和查询

> 原文:[https://www . geeksforgeeks . org/range-sum-query-for-array-rotations-by-k-indexs/](https://www.geeksforgeeks.org/range-sum-queries-for-anticlockwise-rotations-of-array-by-k-indices/)

给定由以下两种类型的 **N** 元素和 **Q** 查询组成的数组 **arr** :

*   **1 K** :对于这种类型的查询，需要将数组从当前状态逆时针[旋转](https://www.geeksforgeeks.org/array-rotation/)**K**个索引。
*   **2 L R** :对于这个查询，需要计算索引**【L，R】**中存在的数组元素之和。

**示例:**

> **输入:** arr = {1，2，3，4，5，6 }，查询= { {2，1，3}，{ 1，3}，{2，0，3}，{ 1，4}，{2，3，5} }
> **输出:**
> 9
> 16
> 12
> **解释:**
> 对于第一个查询{2，1，3} - >索引中的元素之和
> 对于第二个查询{1，3} - >逆时针旋转 3 位后的修改数组为{ 4，5，6，1，2，3 }
> 对于第三个查询{2，0，3} - >索引[0，3] = 4 + 5 + 6 + 1 = 16 中的元素之和。
> 对于第四个查询{1，4} - >逆时针旋转 4 位后的修改数组为{2，3，4，5，6，1 }
> 对于第五个查询{ 2，3，5} - >索引[3，5]中元素的总和= 5 + 6 + 1 = 12。

**进场:**

*   创建一个 [**前缀数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) ，其大小是 **arr** 的两倍，并将 **arr** 的**I<sup>th</sup>T9】索引处的元素复制到**I<sup>th</sup>T15】和**N+I<sup>th</sup>T19】索引处的元素，用于**【0，N】**中的所有 I。******
*   预计算该数组每个索引的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，并存储在**前缀**中。
*   将指针**开始**设置在 **0** 处，表示初始数组的开始索引。
*   对于类型 1 的查询，将**切换到**开始

```
((start + K) % N)th position
```

*   对于类型 2 的查询，计算

```
prefix[start + R]
 - prefix[start + L- 1 ]
```

*   如果**开始+ L > = 1** 或打印的值

```
prefix[start + R]
```

*   否则。

下面的代码是上述方法的实现:

## C++

```
// C++ Program to calculate range sum
// queries for anticlockwise
// rotations of array by K

#include <bits/stdc++.h>
using namespace std;

// Function to execute the queries
void rotatedSumQuery(
    int arr[], int n,
    vector<vector<int> >& query,
    int Q)
{
    // Construct a new array
    // of size 2*N to store
    // prefix sum of every index
    int prefix[2 * n];

    // Copy elements to the new array
    for (int i = 0; i < n; i++) {
        prefix[i] = arr[i];
        prefix[i + n] = arr[i];
    }

    // Calculate the prefix sum
    // for every index
    for (int i = 1; i < 2 * n; i++)
        prefix[i] += prefix[i - 1];

    // Set start pointer as 0
    int start = 0;

    for (int q = 0; q < Q; q++) {

        // Query to perform
        // anticlockwise rotation
        if (query[q][0] == 1) {
            int k = query[q][1];
            start = (start + k) % n;
        }

        // Query to answer range sum
        else if (query[q][0] == 2) {

            int L, R;
            L = query[q][1];
            R = query[q][2];

            // If pointing to 1st index
            if (start + L == 0)

                // Display the sum upto start + R
                cout << prefix[start + R] << endl;

            else

                // Subtract sum upto start + L - 1
                // from sum upto start + R
                cout << prefix[start + R]
                            - prefix[start + L - 1]
                     << endl;
        }
    }
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6 };

    // Number of query
    int Q = 5;

    // Store all the queries
    vector<vector<int> > query
        = { { 2, 1, 3 },
            { 1, 3 },
            { 2, 0, 3 },
            { 1, 4 },
            { 2, 3, 5 } };

    int n = sizeof(arr) / sizeof(arr[0]);
    rotatedSumQuery(arr, n, query, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate range sum
// queries for anticlockwise
// rotations of array by K
class GFG{

// Function to execute the queries
static void rotatedSumQuery(int arr[], int n,
                            int [][]query, int Q)
{

    // Construct a new array
    // of size 2*N to store
    // prefix sum of every index
    int []prefix = new int[2 * n];

    // Copy elements to the new array
    for(int i = 0; i < n; i++)
    {
        prefix[i] = arr[i];
        prefix[i + n] = arr[i];
    }

    // Calculate the prefix sum
    // for every index
    for(int i = 1; i < 2 * n; i++)
        prefix[i] += prefix[i - 1];

    // Set start pointer as 0
    int start = 0;

    for(int q = 0; q < Q; q++)
    {

        // Query to perform
        // anticlockwise rotation
        if (query[q][0] == 1)
        {
            int k = query[q][1];
            start = (start + k) % n;
        }

        // Query to answer range sum
        else if (query[q][0] == 2)
        {
            int L, R;
            L = query[q][1];
            R = query[q][2];

            // If pointing to 1st index
            if (start + L == 0)

                // Display the sum upto start + R
                System.out.print(prefix[start + R] + "\n");

            else

                // Subtract sum upto start + L - 1
                // from sum upto start + R
                System.out.print(prefix[start + R] -
                                 prefix[start + L - 1] +
                                 "\n");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };

    // Number of query
    int Q = 5;

    // Store all the queries
    int [][]query = { { 2, 1, 3 },
                      { 1, 3 },
                      { 2, 0, 3 },
                      { 1, 4 },
                      { 2, 3, 5 } };

    int n = arr.length;
    rotatedSumQuery(arr, n, query, Q);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to calculate range sum
# queries for anticlockwise
# rotations of the array by K

# Function to execute the queries
def rotatedSumQuery(arr, n, query, Q):

    # Construct a new array
    # of size 2*N to store
    # prefix sum of every index
    prefix = [0] * (2 * n)

    # Copy elements to the new array
    for i in range(n):
        prefix[i] = arr[i]
        prefix[i + n] = arr[i]

    # Calculate the prefix sum
    # for every index
    for i in range(1, 2 * n):
        prefix[i] += prefix[i - 1];

    # Set start pointer as 0
    start = 0;

    for q in range(Q):

        # Query to perform
        # anticlockwise rotation
        if (query[q][0] == 1):
            k = query[q][1]
            start = (start + k) % n;

        # Query to answer range sum
        elif (query[q][0] == 2):
            L = query[q][1]
            R = query[q][2]

            # If pointing to 1st index
            if (start + L == 0):

                # Display the sum upto start + R
                print(prefix[start + R])

            else:

                # Subtract sum upto start + L - 1
                # from sum upto start + R
                print(prefix[start + R]-
                      prefix[start + L - 1])

# Driver code
arr = [ 1, 2, 3, 4, 5, 6 ];

# Number of query
Q = 5

# Store all the queries
query= [ [ 2, 1, 3 ],
         [ 1, 3 ],
         [ 2, 0, 3 ],
         [ 1, 4 ],
         [ 2, 3, 5 ] ]

n = len(arr);
rotatedSumQuery(arr, n, query, Q);

# This code is contributed by ankitkumar34
```

## C#

```
// C# program to calculate range sum
// queries for anticlockwise
// rotations of array by K
using System;

class GFG{

// Function to execute the queries
static void rotatedSumQuery(int[] arr, int n,
                            int[,] query, int Q)
{

    // Construct a new array
    // of size 2*N to store
    // prefix sum of every index
    int[] prefix = new int[2 * n];

    // Copy elements to the new array
    for(int i = 0; i < n; i++)
    {
        prefix[i] = arr[i];
        prefix[i + n] = arr[i];
    }

    // Calculate the prefix sum
    // for every index
    for(int i = 1; i < 2 * n; i++)
        prefix[i] += prefix[i - 1];

    // Set start pointer as 0
    int start = 0;

    for(int q = 0; q < Q; q++)
    {

        // Query to perform
        // anticlockwise rotation
        if (query[q, 0] == 1)
        {
            int k = query[q, 1];
            start = (start + k) % n;
        }

        // Query to answer range sum
        else if (query[q, 0] == 2)
        {
            int L, R;
            L = query[q, 1];
            R = query[q, 2];

            // If pointing to 1st index
            if (start + L == 0)

                // Display the sum upto start + R
                Console.Write(prefix[start + R] + "\n");

            else

                // Subtract sum upto start + L - 1
                // from sum upto start + R
                Console.Write(prefix[start + R] -
                              prefix[start + L - 1] +
                              "\n");
        }
    }
}

// Driver code
public static void Main()
{
    int[] arr = new int[] { 1, 2, 3, 4, 5, 6 };

    // Number of query
    int Q = 5;

    // Store all the queries
    int[,] query = new int[,] { { 2, 1, 3 },
                                { 1, 3, 0 },
                                { 2, 0, 3 },
                                { 1, 4, 0 },
                                { 2, 3, 5 } };

    int n = arr.Length;
    rotatedSumQuery(arr, n, query, Q);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to calculate range sum
// queries for anticlockwise
// rotations of array by K

// Function to execute the queries
function rotatedSumQuery(arr, n,
                            query, Q)
{

    // Construct a new array
    // of size 2*N to store
    // prefix sum of every index
    let prefix = [];

    // Copy elements to the new array
    for(let i = 0; i < n; i++)
    {
        prefix[i] = arr[i];
        prefix[i + n] = arr[i];
    }

    // Calculate the prefix sum
    // for every index
    for(let i = 1; i < 2 * n; i++)
        prefix[i] += prefix[i - 1];

    // Set start pointer as 0
    let start = 0;

    for(let q = 0; q < Q; q++)
    {

        // Query to perform
        // anticlockwise rotation
        if (query[q][0] == 1)
        {
            let k = query[q][1];
            start = (start + k) % n;
        }

        // Query to answer range sum
        else if (query[q][0] == 2)
        {
            let L, R;
            L = query[q][1];
            R = query[q][2];

            // If pointing to 1st index
            if (start + L == 0)

                // Display the sum upto start + R
                document.write(prefix[start + R] + "<br/>");

            else

                // Subtract sum upto start + L - 1
                // from sum upto start + R
                document.write(prefix[start + R] -
                                 prefix[start + L - 1] +
                                 "<br/>");
        }
    }
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5, 6 ];

    // Number of query
    let Q = 5;

    // Store all the queries
    let query = [[ 2, 1, 3 ],
                      [ 1, 3 ],
                      [ 2, 0, 3 ],
                      [ 1, 4 ],
                      [ 2, 3, 5 ]];

    let n = arr.length;
    rotatedSumQuery(arr, n, query, Q);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
9
16
12
```

**时间复杂度:** *O(1)* 对于每个查询。
**辅助空间复杂度:** *O(N)*