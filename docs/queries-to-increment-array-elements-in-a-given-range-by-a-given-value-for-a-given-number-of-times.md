# 查询给定次数给定范围内的数组元素增加给定值

> 原文:[https://www . geeksforgeeks . org/query-to-increment-array-elements-in-a-给定范围-a-给定值-a-给定次数/](https://www.geeksforgeeks.org/queries-to-increment-array-elements-in-a-given-range-by-a-given-value-for-a-given-number-of-times/)

给定一个由正整数 **N** 和形式为 **{a，b，val，f}** 的 **M** 查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** 。任务是执行每次查询后打印数组，将**【a，b】**范围内的数组元素增加一个值 **val** **f** 的次数。

**示例:**

> **输入:** arr[] = {1，2，3}，M=3，Q[][] = {{1，2，1，4}，{1，3，2，3}，{2，3，4，5}}
> 输出:11 32 29
> T6】解释:
> 应用第一次查询 4 次后，
> 数组为:5 6 3
> 应用第二次查询 3 次后，
> 数组为:11
> 
> **输入:** arr[] = {1}，M = 1，Q[][] = {{1，1，1，1}}
> **输出:** 2
> **解释:**
> 应用第一次也是唯一一次后只查询 1 次。
> 阵将:2

**<u>朴素方法</u> :** 最简单的方法是对给定数组执行每个查询，即对于每个查询 **{a，b，val，f}** [在范围**【a，b】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将每个元素增加值 **val** 到 **f** 的次数。执行每个查询后打印数组。

***时间复杂度:**O(N * M * max(Freq))*
***辅助空间:** O(1)*

**<u>更好的接近</u> :** 这个想法基于[差阵](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)，可以用在范围更新操作中。以下是步骤:

1.  [求给定数组**的差异数组**](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)**D[]**A[]定义为**D[I]=(A[I]–A[I–1])**(0<I<N)和 **D[0] = A[0]** 考虑 **0** 基索引。
2.  将 **val** 加到**D【a–1】**上，从**D【(b–1)+1】**中减去，即**D【a–1】+= val，D【(b–1)+1】-= val。**执行此操作 **Freq** 次。
3.  现在使用差异数组更新给定的数组。将 **A[0]** 更新为 **D[0]** 并打印。对于其余元素，执行 **A[i] = A[i-1] + D[i]** 。
4.  完成上述步骤后，打印结果数组。

***时间复杂度:**O(N+M * max(Freq))*
***辅助空间:** O(N)* 差阵额外空间

**<u>高效方法</u> :** 这种方法与之前的方法相似，但是是差异数组应用的扩展版本。之前的任务是通过**值**、 **f** 次数更新指数 **a** 到 **b** 的值。这里不要多次调用范围更新函数 **f** ，每次查询只调用一次:

1.  通过 **val*f** 更新从索引 **a** 到 **b** 的值，每次查询只更新一次。
2.  在**D【a–1】**上加上 **val*f** ，从**D【(b–1)+1】**上减去，即增加**D【a–1】**为 **val*f** ，减少**D【b】**为 **val*f** 。
3.  现在使用差异数组更新主数组。将 **A[0]** 更新为 **D[0]** 并打印。
4.  对于其余元素，通过 **(A[i-1] + D[i])** 更新 **A[i]** 。
5.  完成上述步骤后，打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that creates a difference
// array D[] for A[]
vector<int> initializeDiffArray(
    vector<int>& A)
{
    int N = A.size();

    // Stores the difference array
    vector<int> D(N + 1);

    D[0] = A[0], D[N] = 0;

    // Update difference array D[]
    for (int i = 1; i < N; i++)
        D[i] = A[i] - A[i - 1];

    // Return difference array
    return D;
}

// Function that performs the range
// update queries
void update(vector<int>& D, int l,
            int r, int x)
{
    // Update the ends of the range
    D[l] += x;
    D[r + 1] -= x;
}

// Function that perform all query
// once with modified update Call
void UpdateDiffArray(vector<int>& DiffArray,
                     int Start, int End,
                     int Val, int Freq)
{
    // For range update, difference
    // array is modified
    update(DiffArray, Start - 1,
           End - 1, Val * Freq);
}

// Function to take queries
void queriesInput(vector<int>& DiffArray,
                  int Q[][4], int M)
{
    // Traverse the query
    for (int i = 0; i < M; i++) {

        // Function Call for updates
        UpdateDiffArray(DiffArray, Q[i][0],
                        Q[i][1], Q[i][2],
                        Q[i][3]);
    }
}

// Function to updates the array
// using the difference array
void UpdateArray(vector<int>& A,
                 vector<int>& D)
{
    // Traverse the array A[]
    for (int i = 0; i < A.size(); i++) {

        // 1st Element
        if (i == 0) {
            A[i] = D[i];
        }

        // A[0] or D[0] decides values
        // of rest of the elements
        else {
            A[i] = D[i] + A[i - 1];
        }
    }
}

// Function that prints the array
void PrintArray(vector<int>& A)
{
    // Print the element
    for (int i = 0; i < A.size(); i++) {
        cout << A[i] << " ";
    }

    return;
}

// Function that print the array
// after performing all queries
void printAfterUpdate(vector<int>& A,
                      int Q[][4], int M)
{
    // Create and fill difference
    // array for range updates
    vector<int> DiffArray
        = initializeDiffArray(A);

    queriesInput(DiffArray, Q, M);

    // Now update Array A using
    // Difference Array
    UpdateArray(A, DiffArray);

    // Print updated Array A
    // after M queries
    PrintArray(A);
}

// Driver Code
int main()
{
    // N = Array size, M = Queries
    int N = 3, M = 3;

    // Given array A[]
    vector<int> A{ 1, 2, 3 };

    // Queries
    int Q[][4] = { { 1, 2, 1, 4 },
                   { 1, 3, 2, 3 },
                   { 2, 3, 4, 5 } };

    // Function Call
    printAfterUpdate(A, Q, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// N = Array size,
// M = Queries
static int N = 3, M = 3;

static int []A = new int[N];

//Stores the difference array
static int []D = new int[N + 1];

// Function that creates
// a difference array D[]
// for A[]
static void initializeDiffArray()
{
  D[0] = A[0];
  D[N] = 0;

  // Update difference array D[]
  for (int i = 1; i < N; i++)
    D[i] = A[i] - A[i - 1];
}

// Function that performs
// the range update queries
static void update(int l,
                   int r, int x)
{
  // Update the ends
  // of the range
  D[l] += x;
  D[r + 1] -= x;
}

// Function that perform all query
// once with modified update Call
static void UpdateDiffArray(int Start, int End,
                            int Val, int Freq)
{
  // For range update, difference
  // array is modified
  update(Start - 1,
         End - 1, Val * Freq);
}

// Function to take queries
static void queriesInput(  int Q[][])
{
  // Traverse the query
  for (int i = 0; i < M; i++)
  {
    // Function Call for updates
    UpdateDiffArray(Q[i][0], Q[i][1],
                    Q[i][2], Q[i][3]);
  }
}

// Function to updates the array
// using the difference array
static void UpdateArray()
{
  // Traverse the array A[]
  for (int i = 0; i < N; i++)
  {
    // 1st Element
    if (i == 0)
    {
      A[i] = D[i];
    }

    // A[0] or D[0] decides
    // values of rest of
    // the elements
    else
    {
      A[i] = D[i] + A[i - 1];
    }
  }
}

// Function that prints
// the array
static void PrintArray()
{
  // Print the element
  for (int i = 0; i < N; i++)
  {
    System.out.print(A[i] + i +
                     1 + " ");
  }
  return;
}

// Function that print the array
// after performing all queries
static void printAfterUpdate(int []A,
                             int Q[][], int M)
{
  // Create and fill difference
  // array for range updates
  initializeDiffArray();

  queriesInput( Q);

  // Now update Array
  // A using Difference
  // Array
  UpdateArray();

  // Print updated Array A
  // after M queries
  PrintArray();
}

// Driver Code
public static void main(String[] args)
{
  // Given array A[]
  int []A = {1, 2, 3};

  // Queries
  int [][]Q = {{1, 2, 1, 4},
               {1, 3, 2, 3},
               {2, 3, 4, 5}};

  // Function Call
  printAfterUpdate(A, Q, M);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that creates a difference
# array D[] for A[]
def initializeDiffArray(A):

    N = len(A)

    # Stores the difference array
    D = [0] * (N + 1)

    D[0] = A[0]
    D[N] = 0

    # Update difference array D[]
    for i in range(1, N):
        D[i] = A[i] - A[i - 1]

    # Return difference array
    return D

# Function that performs the range
# update queries
def update(D, l, r, x):

    # Update the ends of the range
    D[l] += x
    D[r + 1] -= x

# Function that perform all query
# once with modified update Call
def UpdateDiffArray(DiffArray, Start,
                    End, Val, Freq):

    # For range update, difference
    # array is modified
    update(DiffArray, Start - 1,
           End - 1, Val * Freq)

# Function to take queries
def queriesInput(DiffArray, Q, M):

    # Traverse the query
    for i in range(M):

        # Function Call for updates
        UpdateDiffArray(DiffArray, Q[i][0],
                          Q[i][1], Q[i][2],
                          Q[i][3])

# Function to updates the array
# using the difference array
def UpdateArray(A, D):

    # Traverse the array A[]
    for i in range(len(A)):

        # 1st Element
        if (i == 0):
            A[i] = D[i]

        # A[0] or D[0] decides values
        # of rest of the elements
        else:
            A[i] = D[i] + A[i - 1]

# Function that prints the array
def PrintArray(A):

    # Print the element
    for i in range(len(A)):
        print(A[i], end = " ")

    return

# Function that print the array
# after performing all queries
def printAfterUpdate(A, Q, M):

    # Create and fill difference
    # array for range updates
    DiffArray = initializeDiffArray(A)

    queriesInput(DiffArray, Q, M)

    # Now update Array A using
    # Difference Array
    UpdateArray(A, DiffArray)

    # Prupdated Array A
    # after M queries
    PrintArray(A)

# Driver Code
if __name__ == '__main__':

    # N = Array size, M = Queries
    N = 3
    M = 3

    # Given array A[]
    A = [ 1, 2, 3 ]

    # Queries
    Q = [ [ 1, 2, 1, 4 ],
          [ 1, 3, 2, 3 ],
          [ 2, 3, 4, 5 ] ]

    # Function call
    printAfterUpdate(A, Q, M)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// N = Array size,
// M = Queries
static int N = 3, M = 3;

static int[] A = new int[N];

// Stores the difference array
static int[] D = new int[N + 1];

// Function that creates
// a difference array D[]
// for A[]
static void initializeDiffArray()
{
  D[0] = A[0];
  D[N] = 0;

  // Update difference array D[]
  for (int i = 1; i < N; i++)
    D[i] = A[i] - A[i - 1];
}

// Function that performs
// the range update queries
static void update(int l,
                   int r, int x)
{
  // Update the ends
  // of the range
  D[l] += x;
  D[r + 1] -= x;
}

// Function that perform all query
// once with modified update Call
static void UpdateDiffArray(int Start, int End,
                            int Val, int Freq)
{
  // For range update, difference
  // array is modified
  update(Start - 1,
         End - 1, Val * Freq);
}

// Function to take queries
static void queriesInput(int[, ] Q)
{
  // Traverse the query
  for (int i = 0; i < M; i++)
  {
    // Function Call for updates
    UpdateDiffArray(Q[i, 0], Q[i, 1],
                    Q[i, 2], Q[i, 3]);
  }
}

// Function to updates the array
// using the difference array
static void UpdateArray()
{
  // Traverse the array A[]
  for (int i = 0; i < N; i++)
  {
    // 1st Element
    if (i == 0)
    {
      A[i] = D[i];
    }

    // A[0] or D[0] decides
    // values of rest of
    // the elements
    else
    {
      A[i] = D[i] + A[i - 1];
    }
  }
}

// Function that prints
// the array
static void PrintArray()
{
  // Print the element
  for (int i = 0; i < N; i++)
  {
    Console.Write(A[i] + i +
                  1 + " ");
  }
  return;
}

// Function that print the array
// after performing all queries
static void printAfterUpdate(int[] A,
                             int[, ] Q, int M)
{
  // Create and fill difference
  // array for range updates
  initializeDiffArray();

  queriesInput(Q);

  // Now update Array
  // A using Difference
  // Array
  UpdateArray();

  // Print updated Array A
  // after M queries
  PrintArray();
}

// Driver Code
public static void Main(String[] args)
{
  // Given array A[]
  int[] A = {1, 2, 3};

  // Queries
  int[, ] Q = {{1, 2, 1, 4},
               {1, 3, 2, 3},
               {2, 3, 4, 5}};

  // Function Call
  printAfterUpdate(A, Q, M);
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// N = Array size,
// M = Queries
let N = 3, M = 3;

let A = new Array(N).fill(0);

//Stores the difference array
let D = new Array(N+1).fill(0);

// Function that creates
// a difference array D[]
// for A[]
function initializeDiffArray()
{
  D[0] = A[0];
  D[N] = 0;

  // Update difference array D[]
  for (let i = 1; i < N; i++)
    D[i] = A[i] - A[i - 1];
}

// Function that performs
// the range update queries
function update(l, r, x)
{
  // Update the ends
  // of the range
  D[l] += x;
  D[r + 1] -= x;
}

// Function that perform all query
// once with modified update Call
function UpdateDiffArray(Start, End, Val, Freq)
{
  // For range update, difference
  // array is modified
  update(Start - 1,
         End - 1, Val * Freq);
}

// Function to take queries
function queriesInput(Q)
{
  // Traverse the query
  for (let i = 0; i < M; i++)
  {
    // Function Call for updates
    UpdateDiffArray(Q[i][0], Q[i][1],
                    Q[i][2], Q[i][3]);
  }
}

// Function to updates the array
// using the difference array
function UpdateArray()
{
  // Traverse the array A[]
  for (let i = 0; i < N; i++)
  {
    // 1st Element
    if (i == 0)
    {
      A[i] = D[i];
    }

    // A[0] or D[0] decides
    // values of rest of
    // the elements
    else
    {
      A[i] = D[i] + A[i - 1];
    }
  }
}

// Function that print
// the array
function PrintArray()
{
  // Print the element
  for (let i = 0; i < N; i++)
  {
    document.write(A[i] + i +
                     1 + " ");
  }
  return;
}

// Function that print the array
// after performing all queries
function printAfterUpdate(A, Q, M)
{
  // Create and fill difference
  // array for range updates
  initializeDiffArray();

  queriesInput( Q);

  // Now update Array
  // A using Difference
  // Array
  UpdateArray();

  // Print updated Array A
  // after M queries
  PrintArray();
}

// Driver Code

     // Given array A[]
  let a = [1, 2, 3];

  // Queries
  let Q = [[1, 2, 1, 4],
               [1, 3, 2, 3],
               [2, 3, 4, 5]];

  // Function Call
  printAfterUpdate(a, Q, M);

</script>
```

**Output**

```
11 32 29 
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*