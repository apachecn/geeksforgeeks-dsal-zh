# 检查一个排序数组的末尾是否可以通过重复跳转一个以上、一个以下或与前一次跳转相同数量的索引来到达

> 原文:[https://www . geeksforgeeks . org/check-如果一个排序数组的末尾可以通过重复跳转一个多一个少或相同数量的索引来达到，则与上一次跳转相同/](https://www.geeksforgeeks.org/check-if-end-of-a-sorted-array-can-be-reached-by-repeated-jumps-of-one-more-one-less-or-same-number-of-indices-as-previous-jump/)

给定一个大小为 **N** 的排序后的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过在每次移动中跳转**arr[I]+k–1**、 **arr[i] + k、**或 **arr[i] + k + 1** 来检查是否有可能从 **arr[1]** 到达给定数组的末尾，其中 **k** 表示索引的数量最初考虑 **K = 1** 。如果可能，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {0，1，3，5，6，8，12，17}
> **输出:**是
> **解释:**
> 第一步:采取(k + 1 = 2)步移至包含 A[1] + 2 = 3 的索引
> 第二步:采取(k = 2)步移至包含 A[2] + 2 = 5 的索引。
> 第三步:采取(k + 1 = 3)步移至包含 A[3] + 3 = 8 的索引
> 第四步:采取(k + 1 = 4)步移至包含 A[5] + 4 = 12 的索引
> 第四步:采取(k + 1 = 5)步移至包含 A[6] + 5 = 17 的索引
> 由于最后一个数组索引包含 17，因此到达数组的末尾。
> 
> **输入:** arr[] = {0，1，2，3，4，8，9，11}
> **输出:**否

**天真方法:**想法是使用[递归](https://www.geeksforgeeks.org/recursion/)。从索引 **i** ，递归移动到具有值**A[I]+K–1、A[i] + K** 或 **A[i] + K + 1、**的索引，并检查是否有可能到达终点。如果存在到达终点的路径，则打印**“是”**否则打印**“否”**。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。创建一个 [2D 表**备忘录【N】【N】**来存储记忆的结果](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)。对于任何索引 **(i，j)** ，**备忘录【I】【j】**表示是否有可能从索引 **i** 移动到结束 **(N-1)** 和先前采取的 **j** 步骤。 **memo[i][j] = 1** 表示可能， **memo[i][j] = 0** 表示不可能。按照以下步骤解决问题:

*   创建一个大小为 **N*N** 的记忆表**备忘录[][]** 。
*   对于任何索引 **(i，j)** 更新**备忘录【】【】**表格，如下所示:
    *   如果 **i** 等于**(N–1)**，到达终点位置时返回 1。
    *   如果**备忘录【I】【j】**已经计算，则返回**备忘录【I】【j】**。
    *   检查任何具有 **A[i] + j，A[I]+j–1**或 **A[i] + j + 1** 值的索引，并递归检查是否有可能到达终点。
    *   将该值存储在**备忘录【I】【j】**中并返回该值。
*   如果有可能到达终点，打印**“是”**。
*   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define N 8

// Utility function to check if it is
// possible to move from index 1 to N-1
int check(int memo[][N], int i,
          int j, int* A)
{
    // memo[i][j]: Stores if it is
    // possible to move from index i
    // to end(N-1) previously j steps

    // Successfully reached end index
    if (i == N - 1)
        return 1;

    // memo[i][j] is already calculated
    if (memo[i][j] != -1)
        return memo[i][j];

    // Check if there is any index
    // having value of A[i]+j-1,
    // A[i]+j or A[i]+j+1
    int flag = 0, k;
    for (k = i + 1; k < N; k++) {

        // If A[k] > A[i] + j + 1,
        // can't make a move further
        if (A[k] - A[i] > j + 1)
            break;

        // It's possible to move A[k]
        if (A[k] - A[i] >= j - 1
            && A[k] - A[i] <= j + 1)

            // Check is it possible to
            // move from index k
            // having previously taken
            // A[k] - A[i] steps
            flag = check(memo, k,
                         A[k] - A[i], A);

        // If yes then break the loop
        if (flag)
            break;
    }

    // Store value of flag in memo
    memo[i][j] = flag;

    // Return memo[i][j]
    return memo[i][j];
}

// Function to check if it is possible
// to move from index 1 to N-1
void checkEndReach(int A[], int K)
{

    // Stores the memoized state
    int memo[N][N];

    // Initialize all values as -1
    memset(memo, -1, sizeof(memo));

    // Initially, starting index = 1
    int startIndex = 1;

    // Function call
    if (check(memo, startIndex, K, A))
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    int A[] = { 0, 1, 3, 5, 6,
                8, 12, 17 };
    int K = 1;

    // Function Call
    checkEndReach(A, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

static int N = 8;

// Utility function to check if it is
// possible to move from index 1 to N-1
static int check(int[][] memo, int i,
                 int j, int[] A)
{

    // memo[i][j]: Stores if it is
    // possible to move from index i
    // to end(N-1) previously j steps

    // Successfully reached end index
    if (i == N - 1)
        return 1;

    // memo[i][j] is already calculated
    if (memo[i][j] != -1)
        return memo[i][j];

    // Check if there is any index
    // having value of A[i]+j-1,
    // A[i]+j or A[i]+j+1
    int flag = 0, k;

    for(k = i + 1; k < N; k++)
    {

        // If A[k] > A[i] + j + 1,
        // can't make a move further
        if (A[k] - A[i] > j + 1)
            break;

        // It's possible to move A[k]
        if (A[k] - A[i] >= j - 1 &&
            A[k] - A[i] <= j + 1)

            // Check is it possible to
            // move from index k
            // having previously taken
            // A[k] - A[i] steps
            flag = check(memo, k, A[k] - A[i], A);

        // If yes then break the loop
        if (flag != 0)
            break;
    }

    // Store value of flag in memo
    memo[i][j] = flag;

    // Return memo[i][j]
    return memo[i][j];
}

// Function to check if it is possible
// to move from index 1 to N-1
static void checkEndReach(int A[], int K)
{

    // Stores the memoized state
    int[][] memo = new int[N][N];

    // Initialize all values as -1
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {
            memo[i][j] = -1;
        }
    }

    // Initially, starting index = 1
    int startIndex = 1;

    // Function call
    if (check(memo, startIndex, K, A) != 0)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String[] args)
{
    int[] A = { 0, 1, 3, 5, 6, 8, 12, 17 };
    int K = 1;

    // Function Call
    checkEndReach(A, K);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach
N = 8

# Utility function to check if it is
# possible to move from index 1 to N-1
def check(memo, i, j, A):

  # memo[i][j]: Stores if it is
  # possible to move from index i
  # to end(N-1) previously j steps

  # Successfully reached end index
  if (i == N - 1):
    return 1

  # memo[i][j] is already calculated
  if (memo[i][j] != -1):
    return memo[i][j]

  # Check if there is any index
  # having value of A[i]+j-1,
  # A[i]+j or A[i]+j+1
  flag = 0

  for k in range(i + 1, N):

    # If A[k] > A[i] + j + 1,
    # can't make a move further
    if (A[k] - A[i] > j + 1):
      break

    # It's possible to move A[k]
    if (A[k] - A[i] >= j - 1 and
        A[k] - A[i] <= j + 1):

      # Check is it possible to
      # move from index k
      # having previously taken
      # A[k] - A[i] steps
      flag = check(memo, k,
                   A[k] - A[i], A)

      # If yes then break the loop
      if (flag != 0):
        break

  # Store value of flag in memo
  memo[i][j] = flag

  # Return memo[i][j]
  return memo[i][j]

# Function to check if it is possible
# to move from index 1 to N-1
def checkEndReach(A, K):

  # Stores the memoized state
  memo = [[0] * N] * N

  # Initialize all values as -1
  for i in range(0, N):
    for j in range(0, N):
      memo[i][j] = -1

  # Initially, starting index = 1
  startIndex = 1

  # Function call
  if (check(memo, startIndex, K, A) != 0):
    print("Yes")
  else:
    print("No")

# Driver Code
if __name__  == '__main__':

  A = [ 0, 1, 3, 5, 6, 8, 12, 17 ]
  K = 1

  # Function Call
  checkEndReach(A, K)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int N = 8;
// Utility function to check if it is
// possible to move from index 1 to N-1
static int check(int[,] memo, int i,
                 int j, int[] A)
{

    // memo[i][j]: Stores if it is
    // possible to move from index i
    // to end(N-1) previously j steps

    // Successfully reached end index
    if (i == N - 1)
        return 1;

    // memo[i][j] is already calculated
    if (memo[i, j] != -1)
        return memo[i, j];

    // Check if there is any index
    // having value of A[i]+j-1,
    // A[i]+j or A[i]+j+1
    int flag = 0, k;
    for(k = i + 1; k < N; k++)
    {

        // If A[k] > A[i] + j + 1,
        // can't make a move further
        if (A[k] - A[i] > j + 1)
            break;

        // It's possible to move A[k]
        if (A[k] - A[i] >= j - 1 &&
            A[k] - A[i] <= j + 1)

            // Check is it possible to
            // move from index k
            // having previously taken
            // A[k] - A[i] steps
            flag = check(memo, k, A[k] - A[i], A);

        // If yes then break the loop
        if (flag != 0)
            break;
    }

    // Store value of flag in memo
    memo[i, j] = flag;

    // Return memo[i][j]
    return memo[i, j];
}

// Function to check if it is possible
// to move from index 1 to N-1
static void checkEndReach(int[] A, int K)
{

    // Stores the memoized state
    int[,] memo = new int[N, N];

    // Initialize all values as -1
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {
            memo[i, j] = -1;
        }
    }

    // Initially, starting index = 1
    int startIndex = 1;

    // Function call
    if (check(memo, startIndex, K, A) != 0)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main()
{
    int[] A = { 0, 1, 3, 5, 6, 8, 12, 17 };
    int K = 1;

    // Function Call
    checkEndReach(A, K);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
let N = 8;

// Utility function to check if it is
// possible to move from index 1 to N-1
function check(memo, i, j, A)
{

    // memo[i][j]: Stores if it is
    // possible to move from index i
    // to end(N-1) previously j steps

    // Successfully reached end index
    if (i == N - 1)
        return 1;

    // memo[i][j] is already calculated
    if (memo[i][j] != -1)
        return memo[i][j];

    // Check if there is any index
    // having value of A[i]+j-1,
    // A[i]+j or A[i]+j+1
    let flag = 0, k;

    for(k = i + 1; k < N; k++)
    {

        // If A[k] > A[i] + j + 1,
        // can't make a move further
        if (A[k] - A[i] > j + 1)
            break;

        // It's possible to move A[k]
        if (A[k] - A[i] >= j - 1 &&
            A[k] - A[i] <= j + 1)

            // Check is it possible to
            // move from index k
            // having previously taken
            // A[k] - A[i] steps
            flag = check(memo, k, A[k] - A[i], A);

        // If yes then break the loop
        if (flag != 0)
            break;
    }

    // Store value of flag in memo
    memo[i][j] = flag;

    // Return memo[i][j]
    return memo[i][j];
}

// Function to check if it is possible
// to move from index 1 to N-1
function checkEndReach(A, K)
{

    // Stores the memoized state
    let memo = new Array(N);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < memo.length; i++)
    {
        memo[i] = new Array(2);
    }   

    // Initialize all values as -1
    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < N; j++)
        {
            memo[i][j] = -1;
        }
    }

    // Initially, starting index = 1
    let startIndex = 1;

    // Function call
    if (check(memo, startIndex, K, A) != 0)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
let A = [ 0, 1, 3, 5, 6, 8, 12, 17 ];
let K = 1;

// Function Call
checkEndReach(A, K);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*