# 构造对角线和的奇偶性与矩阵大小相同的方阵

> 原文:[https://www . geesforgeks . org/construct-a-square-matrix-其对角线和的奇偶性与矩阵的大小相同/](https://www.geeksforgeeks.org/construct-a-square-matrix-whose-parity-of-diagonal-sum-is-same-as-size-of-matrix/)

给定一个表示矩阵大小的整数 **N** ，任务是构造一个正方形矩阵 **N * N** ，它具有从 **1 到 N<sup>2</sup>T7】的元素，使得它的对角线之和的奇偶性等于整数 **N** 的奇偶性。**

**示例:**

> **输入:** N = 4
> **输出:**
> 1 2 3 4
> 8 7 6 5
> 9 10 11 12
> 16 15 14 13
> **说明:**
> 对角线= 32 和 36 之和与整数 N = 4，所有的数都是偶数即相同的奇偶性。
> 
> **输入:** N = 3
> **输出:**
> 1 2 3
> 6 5 4
> 7 8 9
> **说明:**
> 对角线之和= 15，整数 N = 3，所有数字都是奇数即相同奇偶性。

**方法:**想法是观察在以**替代方式**填充矩阵中的元素时， **N** 的奇偶性和对角线的和是相同的。从 1 开始计数，然后从 **0 到 N–1**依次填充第一行，然后从索引**N–1 到 0** 填充第二行，以此类推。以这种交替的方式从数值 **1 到数值 <sup>2</sup>** 填充每个元素，以获得所需的矩阵。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to construct a N * N
// matrix based on the given condition
void createMatrix(int N)
{
    // Matrix with given sizM
    int M[N][N];

    // Counter to insert elements
    // from 1 to N * N
    int count = 1;
    for (int i = 0; i < N; i++) {

        // Check if it is first row
        // or odd row of the matrix
        if (i % 2 == 0) {

            for (int j = 0; j < N; j++) {
                M[i][j] = count;
                count++;
            }
        }
        else
        {
            // Insert elements from
            // right to left
            for (int j = N - 1;j >= 0; j--){
                M[i][j] = count;
                count += 1;
            }
        }
    }

    // Print the matrix
    for (int i = 0; i < N; i++) {

        // Traverse column
        for (int j = 0; j < N; j++) {
            cout << M[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given size of matrix N
    int N = 3;

    // Function Call
    createMatrix(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to construct a N * N
// matrix based on the given condition
static void createMatrix(int N)
{
    // Matrix with given sizM
    int M[][] = new int[N][N];

    // Counter to insert elements
    // from 1 to N * N
    int count = 1;
    for (int i = 0; i < N; i++)
    {

        // Check if it is first row
        // or odd row of the matrix
        if (i % 2 == 0)
        {

            for (int j = 0; j < N; j++)
            {
                M[i][j] = count;
                count++;
            }
        }
        else
        {
            // Insert elements from
            // right to left
            for(int j = N - 1; j >= 0; j--){
                M[i][j] = count;
                count += 1 ;
            }
        }
    }

    // Print the matrix
    for (int i = 0; i < N; i++)
    {

        // Traverse column
        for (int j = 0; j < N; j++)
        {
            System.out.print(M[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given size of matrix N
    int N = 3;

    // Function Call
    createMatrix(N);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to construct a N * N
# matrix based on the given condition
def createMatrix(N):

    # Matrix with given size
    M = [[0] * N for i in range(N)]

    # Counter to insert elements
    # from 1 to N * N
    count = 1

    for i in range(N):

        # Check if it is first row
        # or odd row of the matrix
        if (i % 2 == 0):
            for j in range(N):

                # Insert elements from
                # left to right
                M[i][j] = count
                count += 1

        # Condition if it is second
        # row or even row
        else:

            # Insert elements from
            # right to left
            for j in range(N - 1, -1, -1):
                M[i][j] = count
                count += 1

    # Print the matrix
    for i in range(N):

        # Traverse column
        for j in range(N):
            print(M[i][j], end = " ")

        print()

# Driver Code
if __name__ == '__main__':

    # Given size of matrix N
    N = 3

    # Function call
    createMatrix(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to construct a N * N
// matrix based on the given condition
static void createMatrix(int N)
{
  // Matrix with given sizM
  int[,] M = new int[N, N];

  // Counter to insert elements
  // from 1 to N * N
  int count = 1;
  for (int i = 0; i < N; i++)
  {
    // Check if it is first row
    // or odd row of the matrix
    if (i % 2 == 0)
    {

      for (int j = 0; j < N; j++)
      {
        M[i, j] = count;
        count++;
      }
    }
    else
    {
      // Insert elements from
      // right to left
      for(int j = N - 1; j >= 0; j--)
      {
        M[i, j] = count;
        count += 1;
      }
    }
  }

  // Print the matrix
  for (int i = 0; i < N; i++)
  {
    // Traverse column
    for (int j = 0; j < N; j++)
    {
      Console.Write(M[i, j] + " ");
    }
    Console.WriteLine();
  }
}

// Driver Code
public static void Main()
{
  // Given size of matrix N
  int N = 3;

  // Function Call
  createMatrix(N);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to construct a N * N
// matrix based on the given condition
function createMatrix(N)
{
    // Matrix with given sizM
    var M = Array(N).fill(0).map(x => Array(N).fill(0));

    // Counter to insert elements
    // from 1 to N * N
    var count = 1;
    for (i = 0; i < N; i++)
    {

        // Check if it is first row
        // or odd row of the matrix
        if (i % 2 == 0)
        {

            for (j = 0; j < N; j++)
            {
                M[i][j] = count;
                count++;
            }
        }
        else
        {
            // Insert elements from
            // right to left
            for(j = N - 1; j >= 0; j--){
                M[i][j] = count;
                count += 1 ;
            }
        }
    }

    // Prvar the matrix
    for (i = 0; i < N; i++)
    {

        // Traverse column
        for (j = 0; j < N; j++)
        {
            document.write(M[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code
var N = 3;

// Function Call
createMatrix(N);

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
1 2 3 
6 5 4 
7 8 9
```

***时间复杂度:** O(N*N)*
***辅助空间:** O(1)*