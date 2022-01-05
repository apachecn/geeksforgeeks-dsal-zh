# 二维差分阵列

> 原文:[https://www . geesforgeks . org/二维差分阵列/](https://www.geeksforgeeks.org/two-dimensional-difference-array/)

给定维度为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)和具有形式为 **{k，r1，c1，r2，c2}** 的每个查询的 2D 数组**查询[][]** ，任务是将 **k** 添加到子矩阵 **(r1，c1)** 到 **(r2，c2)** 中的所有c单元

**示例:**

> **输入:** A[][] = {{1，2，3}，{1，1，0}，{4，-2，2}}，查询[][] = {{2，0，0，1，1，1}，{-1，1，0，2，2}}
> **输出:**
> 3 4 3
> 2-1
> 3-3 1
> **解释:**
> 查询 1:矩阵修改为{{3，4，1
> 
> **输入:** A[][] = {{1，2，3}，{ 4，5，6}，{7，8，9}}，查询[][] = {{1，1，1，2，2}，{2，0，1，0，2 } }
> T3】输出:T5】1 4 5
> 4 6 7
> 7 9 10

**方法:**思路基于 O(1) 中的[差阵|范围更新查询。按照以下步骤解决问题:](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)

*   初始化一个 2D 差分数组 **D[][]** ，这样 **D[i][j]** 存储**A[I][j]–A[I][j–1]**(对于 **0 ≤ i ≤ N 和 0 < j < M** )或者 **D[i][j] = A[i][j]** 否则。
*   遍历每一行，计算并存储相邻元素之间的差异。
*   要更新子矩阵 **(r1，c1)** 到 **(r2，c2)** ，从 **r1** 遍历到 **r2** (假设 r1 < r2 和 c1 < c2)并更新 **D[i][c1] = D[i][c1] + k** 和**D[I][C2+1]= D[I][C2+1]–k**。
*   最后，将修改后的数组打印为 **j > 0** 的 **D[i][j] + A[i][j-1]** 或 **D[i][j]** 的 **j = 0** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

#define N 3
#define M 3

// Function to initialize the difference array
void intializeDiff(int D[N][M + 1],
                   int A[N][M])
{
    for (int i = 0; i < N; i++) {
        D[i][0] = A[i][0];
        D[i][M] = 0;
    }
    for (int i = 0; i < N; i++) {
        for (int j = 1; j < M; j++)
            D[i][j] = A[i][j] - A[i][j - 1];
    }
}

// Function to add k to the specified
// submatrix (r1, c1) to (r2, c2)
void update(int D[N][M + 1], int k,
            int r1, int c1, int r2,
            int c2)
{
    for (int i = r1; i <= r2; i++) {
        D[i][c1] += k;
        D[i][c2 + 1] -= k;
    }
}

// Function to print the modified array
void printArray(int A[N][M], int D[N][M + 1])
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if (j == 0)
                A[i][j] = D[i][j];
            else
                A[i][j] = D[i][j] + A[i][j - 1];
            cout << A[i][j] << " ";
        }
        cout << endl;
    }
}

// Function to perform the given queries
void performQueries(int A[N][M],
                    vector<vector<int> > Queries)
{
    // Difference array
    int D[N][M + 1];

    // Function to initialize
    // the difference array
    intializeDiff(D, A);

    // Count of queries
    int Q = Queries.size();

    // Perform Queries
    for (int i = 0; i < Q; i++) {
        update(D, Queries[i][0],
               Queries[i][1], Queries[i][2],
               Queries[i][3], Queries[i][4]);
    }

    printArray(A, D);
}

// Driver Code
int main()
{

    // Given Matrix
    int A[N][M] = { { 1, 2, 3 },
                    { 1, 1, 0 },
                    { 4, -2, 2 } };

    // Given Queries
    vector<vector<int> > Queries
        = { { 2, 0, 0, 1, 1 },
            { -1, 1, 0, 2, 2 } };

    performQueries(A, Queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int N = 3;
static int M = 3;

// Function to initialize the difference array
static void intializeDiff(int D[][], int A[][])
{
    for(int i = 0; i < N; i++)
    {
        D[i][0] = A[i][0];
        D[i][M] = 0;
    }
    for(int i = 0; i < N; i++)
    {
        for(int j = 1; j < M; j++)
            D[i][j] = A[i][j] - A[i][j - 1];
    }
}

// Function to add k to the specified
// submatrix (r1, c1) to (r2, c2)
static void update(int D[][], int k,
                   int r1, int c1,
                   int r2, int c2)
{
    for(int i = r1; i <= r2; i++)
    {
        D[i][c1] += k;
        D[i][c2 + 1] -= k;
    }
}

// Function to print the modified array
static void printArray(int A[][], int D[][])
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            if (j == 0)
                A[i][j] = D[i][j];
            else
                A[i][j] = D[i][j] + A[i][j - 1];

            System.out.print(A[i][j] + " ");
        }
        System.out.println();
    }
}

// Function to perform the given queries
static void performQueries(int A[][],
                           Vector<Vector<Integer>> Queries)
{

    // Difference array
    int D[][] = new int[N][M + 1];

    // Function to initialize
    // the difference array
    intializeDiff(D, A);

    // Count of queries
    int Q = Queries.size();

    // Perform Queries
    for(int i = 0; i < Q; i++)
    {
        update(D, Queries.get(i).get(0),
                  Queries.get(i).get(1),
                  Queries.get(i).get(2),
                  Queries.get(i).get(3),
                  Queries.get(i).get(4));
    }
    printArray(A, D);
}

// Driver Code
public static void main(String[] args)
{

    // Given Matrix
    int A[][] = { { 1, 2, 3 },
                  { 1, 1, 0 },
                  { 4, -2, 2 } };

    // Given Queries
    Vector<Vector<Integer>> Queries = new Vector<Vector<Integer>>();
    Vector<Integer> list1 = new Vector<Integer>();
    list1.add(2);
    list1.add(0);
    list1.add(0);
    list1.add(1);
    list1.add(1);

    Vector<Integer> list2 = new Vector<Integer>();
    list2.add(-1);
    list2.add(1);
    list2.add(0);
    list2.add(2);
    list2.add(2);

    Queries.add(list1);
    Queries.add(list2);

    performQueries(A, Queries);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
N = 3
M = 3

# Function to initialize the difference array
def intializeDiff(D, A):
    for i in range(N):       
        D[i][0] = A[i][0];
        D[i][M] = 0;  
    for i in range(N):
        for j in range(1, M):
            D[i][j] = A[i][j] - A[i][j - 1];

# Function to add k to the specified
# submatrix (r1, c1) to (r2, c2)
def update(D, k, r1, c1, r2, c2):
    for i in range(r1, r2 + 1):
        D[i][c1] += k;
        D[i][c2 + 1] -= k;

# Function to print the modified array
def printArray(A, D):  
    for i in range(N):
        for j in range(M):  
            if (j == 0):
                A[i][j] = D[i][j];
            else:
                A[i][j] = D[i][j] + A[i][j - 1];               
            print(A[i][j], end = ' ')
        print()

# Function to perform the given queries
def performQueries(A, Queries):

    # Difference array
    D = [[0 for j in range(M + 1)] for i in range(N)]

    # Function to initialize
    # the difference array
    intializeDiff(D, A);

    # Count of queries
    Q = len(Queries)

    # Perform Queries
    for i in range(Q):   
        update(D, Queries[i][0],
               Queries[i][1], Queries[i][2],
               Queries[i][3], Queries[i][4]);

    printArray(A, D);

# Driver Code
if __name__=='__main__':

    # Given Matrix
    A = [ [ 1, 2, 3 ],
                    [ 1, 1, 0 ],
                    [ 4, -2, 2 ] ];

    # Given Queries
    Queries = [ [ 2, 0, 0, 1, 1 ],[ -1, 1, 0, 2, 2 ] ];

    performQueries(A, Queries);

  # This code is contributed by Pratham76
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static int N = 3;
static int M = 3;

// Function to initialize the difference array
static void intializeDiff(int[,] D, int[,] A)
{
    for(int i = 0; i < N; i++)
    {
        D[i, 0] = A[i, 0];
        D[i, M] = 0;
    }
    for(int i = 0; i < N; i++)
    {
        for(int j = 1; j < M; j++)
            D[i, j] = A[i, j] - A[i, j - 1];
    }
}

// Function to add k to the specified
// submatrix (r1, c1) to (r2, c2)
static void update(int[,] D, int k,
                   int r1, int c1,
                   int r2, int c2)
{
    for(int i = r1; i <= r2; i++)
    {
        D[i, c1] += k;
        D[i, c2 + 1] -= k;
    }
}

// Function to print the modified array
static void printArray(int[,] A, int[,] D)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            if (j == 0)
                A[i, j] = D[i, j];
            else
                A[i, j] = D[i, j] + A[i, j - 1];

            Console.Write(A[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Function to perform the given queries
static void performQueries(int[,] A,
                 List<List<int>> Queries)
{

    // Difference array
    int[,] D = new int[N, M + 1];

    // Function to initialize
    // the difference array
    intializeDiff(D, A);

    // Count of queries
    int Q = Queries.Count;

    // Perform Queries
    for(int i = 0; i < Q; i++)
    {
        update(D, Queries[i][0],
                  Queries[i][1], Queries[i][2],
                  Queries[i][3], Queries[i][4]);
    }
    printArray(A, D);
}

// Driver Code
static void Main()
{

    // Given Matrix
    int[,] A = { { 1, 2, 3 },
                 { 1, 1, 0 },
                 { 4, -2, 2 } };

    // Given Queries
    List<List<int>> Queries = new List<List<int>>();
    Queries.Add(new List<int>{ 2, 0, 0, 1, 1 });
    Queries.Add(new List<int>{ -1, 1, 0, 2, 2 });

    performQueries(A, Queries);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach
var N = 3;
var M = 3;

// Function to initialize the difference array
function intializeDiff(D,
                    A)
{
    for (var i = 0; i < N; i++) {
        D[i][0] = A[i][0];
        D[i][M] = 0;
    }
    for (var i = 0; i < N; i++) {
        for (var j = 1; j < M; j++)
            D[i][j] = A[i][j] - A[i][j - 1];
    }
}

// Function to add k to the specified
// submatrix (r1, c1) to (r2, c2)
function update( D,  k, r1, c1, r2, c2)
{
    for (var i = r1; i <= r2; i++) {
        D[i][c1] += k;
        D[i][c2 + 1] -= k;
    }
}

// Function to print the modified array
function printArray(A, D)
{
  var str = "";
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < M; j++) {
            if (j == 0)
                A[i][j] = D[i][j];
            else
                A[i][j] = D[i][j] + A[i][j - 1];

            str += A[i][j] + " ";

        }
        console.log(str );
        str="";
    }
}

// Function to perform the given queries
function performQueries( A,
                     Queries)
{
    // Difference array
    var D = new Array(N);
    for (var i =0 ; i< N;i++)
      D[i] = new Array(M + 1);

    // Function to initialize
    // the difference array
    intializeDiff(D, A);

    // Count of queries
    var Q = Queries.length;

    // Perform Queries
    for (var i = 0; i < Q; i++) {
        update(D, Queries[i][0],
               Queries[i][1], Queries[i][2],
               Queries[i][3], Queries[i][4]);
    }

    printArray(A, D);
}

// Driver Code

// Given Matrix
var A = [[ 1, 2, 3 ],
                [ 1, 1, 0 ],
                [ 4, -2, 2 ]];

// Given Queries
var Queries
    = [[ 2, 0, 0, 1, 1 ],
        [ -1, 1, 0, 2, 2 ]];

performQueries(A, Queries);

// This code is contributed by ukasp.   

</script>
```

**输出:**

```
3 4 3
2 2 -1
3 -3 1
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*