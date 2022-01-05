# 对给定范围内存在的矩阵的行和列的总和进行计数的查询

> 原文:[https://www . geeksforgeeks . org/查询-计数-给定范围内存在的矩阵的行和列的总和/](https://www.geeksforgeeks.org/queries-to-count-sum-of-rows-and-columns-of-a-matrix-present-in-given-ranges/)

给定大小为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **A[][]** 和由 **{L，R}** 形式的 **Q** 查询组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **查询[][]** ，任务是统计[行和列和](https://www.geeksforgeeks.org/program-to-find-the-sum-of-each-row-and-each-column-of-a-matrix/)的数量，它们是从**【L，R】**范围内的整数。

**示例:**

> **输入:** N = 2，M = 2，A[][] = {{1，4}，{2，5}}，Q = 2，查询[][] = {{3，7}，{3，9}}
> **输出:** 3 4
> **解释:**
> 第一行之和= 1 + 4 = 5。
> 第二行之和= 2 + 5 = 7。
> 第一列之和= 1 + 2 = 3。
> 第二列之和= 4 + 5 = 9。
> 
> 查询 1: L = 3，R = 7:
> 范围内出现的列和= 3。
> 范围内的行总和= {5，7}。
> 因此，计数为 3。
> 查询 2: L = 3，R = 9:
> 列总和出现在= {3，9}的范围内。
> 范围内的行总和= {5，7}。
> 因此，计数为 4。
> 
> **输入:** N = 3，M = 2，A[][] = {{13，3}，{9，4}，{6，10}}，Q = 2，查询[][] = {{10，20}，{25，35}}
> **输出:** 4 1

**高效方法**:思路是[逐行逐列](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)遍历矩阵，分别预先计算每行每列的和。[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **查询【】【】**并使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)计算给定范围内存在的行和或列和的数量。按照以下步骤解决问题:

1.  初始化两个辅助[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说**row _ sum[]**&**col _ sum[]**，来[存储行和列的总和。](https://www.geeksforgeeks.org/program-to-find-the-sum-of-each-row-and-each-column-of-a-matrix/)
2.  初始化另一个数组，比如 **sum_list[]，**来存储所有行和列和元素的组合。
3.  [按升序排列数组**sum _ list[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
4.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **查询[]** ，对于每个查询:
    *   执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到索引，说出最左边和的 **i，**，即 **L.**
    *   再次执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到最右边和的指标 **j** ，即 **R**
    *   打印**j–I+1**作为查询结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to search for the
// leftmost index of given number
int left_search(vector<int> A, int num)
{
    // Initialize low, high and ans
    int low = 0, high = A.size() - 1;
    int ans = 0;

    while (low <= high)
    {

        // Stores mid
        int mid = low + (high - low) / 2;

        // If A[mid] >= num
        if (A[mid] >= num)
        {

            ans = mid;
            high = mid - 1;
        }
        else
        {
            low = mid + 1;
        }
    }
    return ans;
}

// Function to search for the
// rightmost index of given number
int right_search(vector<int> A, int num)
{
    // Initialise low, high and ans
    int low = 0, high = A.size() - 1;
    int ans = high;

    while (low <= high)
    {

        // Stores mid
        int mid = low + (high - low) / 2;

        // If A[mid] <= num
        if (A[mid] <= num)
        {

            // Update ans
            ans = mid;

            // Update mid
            low = mid + 1;
        }
        else
        {

            // Update high
            high = mid - 1;
        }
    }

    return ans;
}

// Function to preprocess the matrix to execute the
// queries
void totalCount(vector<vector<int>> A, int N, int M, vector<vector<int>> queries, int Q)
{
    // Stores the sum of each row
    vector<int> row_sum(N);

    // Stores the sum of each col
    vector<int> col_sum(N);

    // Traverse the matrix and calculate
    // sum of each row and column
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            row_sum[i] += A[i][j];
            col_sum[j] += A[i][j];
        }
    }

    vector<int> sum_list;

    // Insert all row sums in sum_list
    for (int i = 0; i < N; i++)
        sum_list.push_back(row_sum[i]);

    // Insert all column sums in sum_list
    for (int i = 0; i < M; i++)
        sum_list.push_back(col_sum[i]);

    // Sort the array in ascending order
    sort(sum_list.begin(), sum_list.end());

    // Traverse the array queries[][]
    for (int i = 0; i < Q; i++)
    {
        int L = queries[i][0];
        int R = queries[i][1];

        // Search the leftmost index of L
        int l = left_search(sum_list, L);

        // Search the rightmost index of R
        int r = right_search(sum_list, R);

        cout << r - l + 1 << " ";
    }
}

// Driver Code
int main()
{
    // Given dimensions of matrix
    int N = 3, M = 2;

    // Given matrix
    vector<vector<int>> A = {{13, 3},
                             {9, 4},
                             {6, 10}};

    // Given number of queries
    int Q = 2;

    // Given queries
    vector<vector<int>> queries = {{10, 20}, {25, 35}};

    // Function call to count the
    // number row-sums and column-sums
    // present in the given ranges
    totalCount(A, N, M, queries, Q);
}

// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to preprocess the matrix to execute the
    // queries
    static void totalCount(int[][] A, int N,
                           int M, int[][] queries, int Q)
    {
        // Stores the sum of each row
        int row_sum[] = new int[N];

        // Stores the sum of each col
        int col_sum[] = new int[M];

        // Traverse the matrix and calculate
        // sum of each row and column
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {

                row_sum[i] += A[i][j];
                col_sum[j] += A[i][j];
            }
        }

        ArrayList<Integer> sum_list
            = new ArrayList<>();

        // Insert all row sums in sum_list
        for (int i = 0; i < N; i++)
            sum_list.add(row_sum[i]);

        // Insert all column sums in sum_list
        for (int i = 0; i < M; i++)
            sum_list.add(col_sum[i]);

        // Sort the array in ascending order
        Collections.sort(sum_list);

        // Traverse the array queries[][]
        for (int i = 0; i < Q; i++) {
            int L = queries[i][0];
            int R = queries[i][1];

            // Search the leftmost index of L
            int l = left_search(sum_list, L);

            // Search the rightmost index of R
            int r = right_search(sum_list, R);

            System.out.print(r - l + 1 + " ");
        }
    }

    // Function to search for the
    // leftmost index of given number
    static int left_search(
        ArrayList<Integer> A,
        int num)
    {
        // Initialize low, high and ans
        int low = 0, high = A.size() - 1;
        int ans = 0;

        while (low <= high) {

            // Stores mid
            int mid = low + (high - low) / 2;

            // If A[mid] >= num
            if (A.get(mid) >= num) {

                ans = mid;
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return ans;
    }

    // Function to search for the
    // rightmost index of given number
    static int right_search(
        ArrayList<Integer> A,
        int num)
    {
        // Initialise low, high and ans
        int low = 0, high = A.size() - 1;
        int ans = high;

        while (low <= high) {

            // Stores mid
            int mid = low + (high - low) / 2;

            // If A[mid] <= num
            if (A.get(mid) <= num) {

                // Update ans
                ans = mid;

                // Update mid
                low = mid + 1;
            }
            else {

                // Update high
                high = mid - 1;
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given dimensions of matrix
        int N = 3, M = 2;

        // Given matrix
        int A[][] = { { 13, 3 },
                      { 9, 4 },
                      { 6, 10 } };

        // Given number of queries
        int Q = 2;

        // Given queries
        int queries[][] = { { 10, 20 }, { 25, 35 } };

        // Function call to count the
        // number row-sums and column-sums
        // present in the given ranges
        totalCount(A, N, M, queries, Q);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque
from bisect import bisect_left, bisect_right

# Function to preprocess the matrix to execute the
# queries
def totalCount(A, N, M, queries, Q):

    # Stores the sum of each row
    row_sum = [0]*N

    # Stores the sum of each col
    col_sum = [0]*M

    # Traverse the matrix and calculate
    # sum of each row and column
    for i in range(N):
        for j in range(M):
            row_sum[i] += A[i][j]
            col_sum[j] += A[i][j]

    sum_list = []

    # Insert all row sums in sum_list
    for i in range(N):
        sum_list.append(row_sum[i])

    # Insert all column sums in sum_list
    for i in range(M):
        sum_list.append(col_sum[i])

    # Sort the array in ascending order
    sum_list = sorted(sum_list)

    # Traverse the array queries[][]
    for i in range(Q):
        L = queries[i][0]
        R = queries[i][1]

        # Search the leftmost index of L
        l = left_search(sum_list, L)

        # Search the rightmost index of R
        r = right_search(sum_list, R)
        print(r - l + 1, end = " ")

# Function to search for the
# leftmost index of given number
def left_search(A, num):

    # Initialize low, high and ans
    low, high = 0, len(A) - 1
    ans = 0
    while (low <= high):

        # Stores mid
        mid = low + (high - low) // 2

        # If A[mid] >= num
        if (A[mid] >= num):
            ans = mid
            high = mid - 1
        else:
            low = mid + 1
    return ans

# Function to search for the
# rightmost index of given number
def right_search(A, num):

    # Initialise low, high and ans
    low, high = 0, len(A) - 1
    ans = high
    while (low <= high):

        # Stores mid
        mid = low + (high - low) // 2

        # If A[mid] <= num
        if (A[mid] <= num):
            # Update ans
            ans = mid

            # Update mid
            low = mid + 1
        else:

            # Update high
            high = mid - 1

    return ans

# Driver Code
if __name__ == '__main__':

    # Given dimensions of matrix
    N, M = 3, 2

    # Given matrix
    A = [ [ 13, 3 ],
          [ 9, 4 ],
          [ 6, 10 ] ]

    # Given number of queries
    Q = 2

    # Given queries
    queries= [ [ 10, 20 ], [ 25, 35 ] ]

    # Function call to count the
    # number row-sums and column-sums
    # present in the given ranges
    totalCount(A, N, M, queries, Q)

# This code is contributed by mohit kumar 29.
```

## C#

```
using System;
using System.Collections.Generic;
class GFG
{

    // Function to preprocess the matrix to execute the
    // queries
    static void totalCount(int[,] A, int N, int M,
                           int[,] queries, int Q)
    {

        // Stores the sum of each row
        int []row_sum = new int[N];

        // Stores the sum of each col
        int []col_sum = new int[M];

        // Traverse the matrix and calculate
        // sum of each row and column
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {

                row_sum[i] += A[i,j];
                col_sum[j] += A[i,j];
            }
        }

        List<int> sum_list = new List<int>();

        // Insert all row sums in sum_list
        for (int i = 0; i < N; i++)
            sum_list.Add(row_sum[i]);

        // Insert all column sums in sum_list
        for (int i = 0; i < M; i++)
            sum_list.Add(col_sum[i]);

        // Sort the array in ascending order
        sum_list.Sort();

        // Traverse the array queries[][]
        for (int i = 0; i < Q; i++) {
            int L = queries[i,0];
            int R = queries[i,1];

            // Search the leftmost index of L
            int l = left_search(sum_list, L);

            // Search the rightmost index of R
            int r = right_search(sum_list, R);

           Console.Write(r - l + 1 + " ");
        }
    }

    // Function to search for the
    // leftmost index of given number
    static int left_search(List<int> A, int num)
    {

        // Initialize low, high and ans
        int low = 0, high = A.Count- 1;
        int ans = 0;
        while (low <= high)
        {

            // Stores mid
            int mid = low + (high - low) / 2;

            // If A[mid] >= num
            if (A[mid] >= num) {

                ans = mid;
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return ans;
    }

    // Function to search for the
    // rightmost index of given number
    static int right_search( List<int> A,int num)
    {
        // Initialise low, high and ans
        int low = 0, high = A.Count- 1;
        int ans = high;

        while (low <= high) {

            // Stores mid
            int mid = low + (high - low) / 2;

            // If A[mid] <= num
            if (A[mid] <= num) {

                // Update ans
                ans = mid;

                // Update mid
                low = mid + 1;
            }
            else {

                // Update high
                high = mid - 1;
            }
        }

        return ans;
    }

//driver code
static void Main()
{
       int N = 3, M = 2;

        // Given matrix
        int [,]A = new int[,]{ { 13, 3 },{ 9, 4 },{ 6, 10 } };

        // Given number of queries
        int Q = 2;

        // Given queries
        int [,]queries = new int[,]{ { 10, 20 }, { 25, 35 } };

        // Function call to count the
        // number row-sums and column-sums
        // present in the given ranges
        totalCount(A, N, M, queries, Q);
    }
}

//This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to preprocess the matrix to execute the
    // queries
function totalCount(A,N,M,queries,Q)
{
    // Stores the sum of each row
        let row_sum = new Array(N);

        // Stores the sum of each col
        let col_sum = new Array(M);

        for(let i=0;i<N;i++)
            row_sum[i]=0;
        for(let j=0;j<M;j++)
            col_sum[j]=0;
        // Traverse the matrix and calculate
        // sum of each row and column
        for (let i = 0; i < N; i++) {
            for (let j = 0; j < M; j++) {

                row_sum[i] += A[i][j];
                col_sum[j] += A[i][j];
            }
        }

        let sum_list=[];

        // Insert all row sums in sum_list
        for (let i = 0; i < N; i++)
            sum_list.push(row_sum[i]);

        // Insert all column sums in sum_list
        for (let i = 0; i < M; i++)
            sum_list.push(col_sum[i]);

        // Sort the array in ascending order
        (sum_list).sort(function(a,b){return a-b;});

        // Traverse the array queries[][]
        for (let i = 0; i < Q; i++) {
            let L = queries[i][0];
            let R = queries[i][1];

            // Search the leftmost index of L
            let l = left_search(sum_list, L);

            // Search the rightmost index of R
            let r = right_search(sum_list, R);

            document.write(r - l + 1 + " ");
        }
}

// Function to search for the
    // leftmost index of given number
function left_search(A,num)
{
    // Initialize low, high and ans
        let low = 0, high = A.length - 1;
        let ans = 0;

        while (low <= high) {

            // Stores mid
            let mid = low + Math.floor((high - low) / 2);

            // If A[mid] >= num
            if (A[mid] >= num) {

                ans = mid;
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return ans;
}

// Function to search for the
    // rightmost index of given number
function right_search(A,num)
{
    // Initialise low, high and ans
        let low = 0, high = A.length - 1;
        let ans = high;

        while (low <= high) {

            // Stores mid
            let mid = low + Math.floor((high - low) / 2);

            // If A[mid] <= num
            if (A[mid] <= num) {

                // Update ans
                ans = mid;

                // Update mid
                low = mid + 1;
            }
            else {

                // Update high
                high = mid - 1;
            }
        }

        return ans;
}

 // Given dimensions of matrix
let N = 3, M = 2;

        // Given matrix
let A=[[ 13, 3 ],[ 9, 4 ],[ 6, 10 ] ];

// Given number of queries
let  Q = 2;

let queries=[[ 10, 20 ], [ 25, 35 ]];
// Function call to count the
// number row-sums and column-sums
// present in the given ranges
totalCount(A, N, M, queries, Q);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4 1
```

***时间复杂度:**O(Q * log(N * M))*
***辅助空间:** O(N * M)*