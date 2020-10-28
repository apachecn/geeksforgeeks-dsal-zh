# 在给定范围内翻转 Q 查询的子矩阵后的二进制矩阵

给定尺寸为 **M x N** 和 **Q** 尺寸为[ **x1，y1，x2，y2）的二进制矩阵 **arr [] []**** ，其中（[ **x1，y1** ）和（ **x2，y2** ）表示需要翻转的子矩阵的左上和右下索引（将 0s 转换为 1s 反之亦然）。 任务是打印执行给定的 **Q** 查询

**后获得的最终矩阵。示例**：

> **输入**：arr [] [] = {{0，1，0}，{1，1，0}}，查询[] [] = {{1，1，2，3}}
> **输出**：[[1、0、1]，[0、0、1]]
> **说明**：
> 要翻转的子矩阵等于{ {0，1，0}，{1，1，0}}。
> 翻转后的矩阵为{{1，0，1}，{0，0，1}}。
> 
> **输入**：arr [] [] = {{0，1，0}，{1，1，0}}，查询[] [] = {{1，1，2，3}，{ 1，1，1，1]，{1,2,2,3}}
> **输出**：[[0，1，0]，[0，1，0]]
> **解释**：
> 查询 1：
> 要翻转的子矩阵= [[0，1，0]，[1，1，0]]
> 翻转的子矩阵是[[1，0 ，1]，[0、0、1]。
> 因此，修改后的矩阵是[[1，0，1]，[0，0，1]]。
> 查询 2：
> 要翻转的子矩阵= [[1]]
> 翻转的子矩阵为[[0]]
> 因此，矩阵为[[0，0，1]，[0，0 ，1]]。
> 查询 3：
> 要翻转的子矩阵= [[0，1]，[0，1]]
> 翻转的子矩阵为[[1，0]，[1，0]]
> 因此 ，修改后的矩阵为[[0，1，0]，[0，1，0]]。

**天真的方法**：解决每个查询问题的最简单方法是遍历给定的子矩阵，并针对每个元素检查其是否为 0 或 1，然后进行相应翻转。 完成所有查询的这些操作后，打印获得的最终矩阵。

下面是上述方法的实现：

## Java

```java

// Java program to implement
// the above approach 
import java.util.*;
import java.lang.*;
class GFG{

// Function to flip a submatrices
static void manipulation(int[][] matrix,
                         int[] q)
{
  // Boundaries of the submatrix
  int x1 = q[0], y1 = q[1], 
      x2 = q[2], y2 = q[3];

  // Iterate over the submatrix
  for(int i = x1 - 1; i < x2; i++)
  {
    for(int j = y1 - 1; j < y2; j++)
    {
      // Check for 1 or 0
      // and flip accordingly
      if (matrix[i][j] == 1)
        matrix[i][j] = 0;
      else
        matrix[i][j] = 1;
    }
  }
}

// Function to perform the queries
static void queries_fxn(int[][] matrix,
                        int[][] queries)
{
  for(int[] q : queries)
    manipulation(matrix, q);        
}

// Driver code
public static void main (String[] args)
{
  int[][] matrix = {{0, 1, 0}, {1, 1, 0}};
  int[][] queries = {{1, 1, 2, 3}, 
                     {1, 1, 1, 1}, 
                     {1, 2, 2, 3}};

  // Function call
  queries_fxn(matrix, queries);
  System.out.print("[");

  for(int i = 0; i < matrix.length; i++)
  {
    System.out.print("[");  
    for(int j = 0; j < matrix[i].length; j++)
      System.out.print(matrix[i][j] + " ");

    if(i == matrix.length - 1)
      System.out.print("]");
    else
      System.out.print("], ");
  }
  System.out.print("]"); 
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 Program to implement
# the above approach

# Function to flip a submatrices
def manipulation(matrix, q):

    # Boundaries of the submatrix
    x1, y1, x2, y2 = q

    # Iterate over the submatrix
    for i in range(x1-1, x2):
        for j in range(y1-1, y2):

            # Check for 1 or 0
            # and flip accordingly
            if matrix[i][j]:
                matrix[i][j] = 0
            else:
                matrix[i][j] = 1

# Function to perform the queries
def queries_fxn(matrix, queries):
    for q in queries:
        manipulation(matrix, q)

# Driver Code
matrix = [[0, 1, 0], [1, 1, 0]]
queries = [[1, 1, 2, 3], \
           [1, 1, 1, 1], \
           [1, 2, 2, 3]]

# Function call
queries_fxn(matrix, queries)
print(matrix)

```

## C#

```cs

// C# program to implement
// the above approach
using System;

class GFG{

// Function to flip a submatrices
static void manipulation(int[,] matrix,
                         int[] q)
{

    // Boundaries of the submatrix
    int x1 = q[0], y1 = q[1], 
        x2 = q[2], y2 = q[3];

    // Iterate over the submatrix
    for(int i = x1 - 1; i < x2; i++)
    {
        for(int j = y1 - 1; j < y2; j++)
        {

            // Check for 1 or 0
            // and flip accordingly
            if (matrix[i, j] == 1)
                matrix[i, j] = 0;
            else
                matrix[i, j] = 1;
        }
    }
}

public static int[] GetRow(int[,] matrix, int row)
{
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for(var i = 0; i < rowLength; i++)
        rowVector[i] = matrix[row, i];

    return rowVector;
}

// Function to perform the queries
static void queries_fxn(int[,] matrix,
                        int[,] queries)
{
    for(int i = 0; i < queries.GetLength(0); i++)
        manipulation(matrix, GetRow(queries, i));        
}

// Driver code
public static void Main(String[] args)
{
    int[,] matrix = { { 0, 1, 0 },
                      { 1, 1, 0 } };
    int[,] queries = { { 1, 1, 2, 3 }, 
                       { 1, 1, 1, 1 }, 
                       { 1, 2, 2, 3 } };

    // Function call
    queries_fxn(matrix, queries);
    Console.Write("[");

    for(int i = 0; i < matrix.GetLength(0); i++)
    {
        Console.Write("[");  
        for(int j = 0; j < matrix.GetLength(1); j++)
            Console.Write(matrix[i, j] + ", ");

        if (i == matrix.Length - 1)
            Console.Write("]");
        else
            Console.Write("], ");
    }
    Console.Write("]"); 
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
[[0, 1, 0], [0, 1, 0]]

```

***时间复杂度**：O（N * M * Q）*

***辅助空间**：O（1）*

**有效方法**：可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)和[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术来优化上述方法。 标记每个查询中涉及的子矩阵的边界，然后计算矩阵中涉及的运算的**前缀总和**，并相应地更新矩阵。 请按照以下步骤解决问题：

*   初始化 2D 状态空间表 **dp [] []** ，以将翻转计数存储在矩阵的各个索引处

*   对于每个查询{x1，y1，x2，y2，K}，通过以下操作更新 dp [] []矩阵：

    *   dp [x1] [y1] + = 1

    *   dp [x2 + 1] [y1]-= 1

    *   dp [x2 +1] [y2 +1] + = 1

    *   dp [x1] [y2 + 1]-= 1

*   现在，遍历 dp [] []矩阵，并通过以下关系计算行和列以及对角线的前缀和，从而更新 dp [i] [j]：

> dp [i] [j] = dp [i] [j] + dp [i-1] [j] + dp [i] [j – 1] – dp [i – 1] [j – 1]

*   如果发现 dp [i] [j]为奇数，则将 mat [i – 1] [j – 1]减 1。

*   最后，打印更新后的矩阵 mat [] []作为结果。

下面是上述方法的实现：

## Python3

```py

# Python3 program to implement
# the above approach

# Function to modify dp[][] array by
# generating prefix sum
def modifyDP(matrix, dp):

    for j in range(1, len(matrix)+1):

        for k in range(1, len(matrix[0])+1):

            # Update the tabular data
            dp[j][k] = dp[j][k] + dp[j-1][k] \
            + dp[j][k-1]-dp[j-1][k-1]

            # If the count of flips is even
            if dp[j][k] % 2 != 0:
                matrix[j-1][k-1] = int(matrix[j-1][k-1]) ^ 1

# Function to update dp[][] matrix
# for each query
def queries_fxn(matrix, queries, dp):
    for q in queries:
        x1, y1, x2, y2 = q

        # Update the table
        dp[x1][y1] += 1
        dp[x2 + 1][y2 + 1] += 1
        dp[x1][y2 + 1] -= 1
        dp[x2 + 1][y1] -= 1

    modifyDP(matrix, dp)

# Driver Code
matrix = [[0, 1, 0], [1, 1, 0]]
queries = [[1, 1, 2, 3], \
           [1, 1, 1, 1], \
           [1, 2, 2, 3]]

# Initialize dp table
dp = [[0 for i in range(len(matrix[0])+2)] \
for j in range(len(matrix)+2)]

queries_fxn(matrix, queries, dp)
print(matrix)

```

**Output:** 

```
[[0, 1, 0], [0, 1, 0]]

```

***时间复杂度**：O（N * M）*

***辅助空间**：O（N * M）*



* * *

* * *



