# 查找矩阵中两个单元格之间是否有路径

> 原文:[https://www . geesforgeks . org/find-when-path-two-cells-matrix/](https://www.geeksforgeeks.org/find-whether-path-two-cells-matrix/)

给定 N×N 矩阵，用 1，0，2，3 填充。查找从源到目的地是否有可能的路径，仅遍历空白单元格。你可以上下左右移动。

*   单元格 **1** 的值表示来源。
*   单元格 **2** 的值表示目的地。
*   单元格 **3** 的值表示空白单元格。
*   单元格 **0** 的值表示空白墙。

注意:只有一个源和一个目标(接收器)。

**示例:**

> **输入:**
> M[3][3] = {{ 0，3，2 }，
> { 3，3，0 }，
> { 1，3，0 } }；
> **输出:**是
> **说明:**
> 
> ![](img/ee04296cbd643e6545a058ca6b6c0282.png)
> 
> **输入:**
> M[4][4] = {{ 0，3，1，0 }，
> { 3，0，3，3 }，
> { 2，3，0，3 }，
> { 0，3，3，3 } }；
> **输出:**是
> **说明:**
> 
> ![](img/3d697308a05396dfd784266e5bc93381.png)

问于: [Adobe 面试](https://www.geeksforgeeks.org/adobe-interview-experience-set-41-software-engineer/)

**<u>简单解法:</u>** 递归。
**方法:**在每个矩阵中找到单元格的源索引，然后递归地在矩阵中找到从源索引到目的地的路径。该算法包括递归查找所有路径，直到找到到达目的地的最终路径。

**算法:**

1.  遍历矩阵，找到矩阵的起始索引。
2.  创建一个接受索引和访问矩阵的递归函数。
3.  标记当前单元格，并检查当前单元格是否是目标单元格。如果当前单元格是目标单元格，则返回 true。
4.  为所有相邻的空单元格和未访问的单元格调用递归函数。
5.  如果任何递归函数返回 true，则取消单元格标记并返回 true，否则取消单元格标记并返回 false。

## C++

```
// C++ program to find path between two
// cell in matrix
#include <iostream>
using namespace std;
#define N 4

// Method for checking boundaries
bool isSafe(int i, int j, int matrix[][N])
{
  if (i >= 0 && i < N && j >= 0 && j < N)
    return true;
  return false;
}

// Returns true if there is a
// path from a source (a
// cell with value 1) to a
// destination (a cell with
// value 2)
bool isPath(int matrix[][N], int i, int j,
            bool visited[][N])
{
  // Checking the boundaries, walls and
  // whether the cell is unvisited
  if (isSafe(i, j, matrix) && matrix[i][j] != 0
      && !visited[i][j])
  {
    // Make the cell visited
    visited[i][j] = true;

    // if the cell is the required
    // destination then return true
    if (matrix[i][j] == 2)
      return true;

    // traverse up
    bool up = isPath(matrix, i - 1, j, visited);

    // if path is found in up
    // direction return true
    if (up)
      return true;

    // traverse left
    bool left = isPath(matrix, i, j - 1, visited);

    // if path is found in left
    // direction return true
    if (left)
      return true;

    // traverse down
    bool down = isPath(matrix, i + 1, j, visited);

    // if path is found in down
    // direction return true
    if (down)
      return true;

    // traverse right
    bool right = isPath(matrix, i, j + 1, visited);

    // if path is found in right
    // direction return true
    if (right)
      return true;
  }

  // no path has been found
  return false;
}

// Method for finding and printing
// whether the path exists or not
void isPath(int matrix[][N])
{

  // Defining visited array to keep
  // track of already visited indexes
  bool visited[N][N];

  // Flag to indicate whether the
  // path exists or not
  bool flag = false;
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < N; j++)
    {
      // if matrix[i][j] is source
      // and it is not visited
      if (matrix[i][j] == 1 && !visited[i][j])

        // Starting from i, j and
        // then finding the path
        if (isPath(matrix, i, j, visited))
        {

          // if path exists
          flag = true;
          break;
        }
    }
  }
  if (flag)
    cout << "YES";
  else
    cout << "NO";
}

// Driver program to
// check above function
int main()
{
  int matrix[N][N] = { { 0, 3, 0, 1 },
                      { 3, 0, 3, 3 },
                      { 2, 3, 3, 3 },
                      { 0, 3, 3, 3 } };

  // calling isPath method
  isPath(matrix);
  return 0;
}

// This code is contributed by sudhanshugupta2019a.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find path between two
// cell in matrix
class Path {

    // Method for finding and printing
    // whether the path exists or not
    public static void isPath(
        int matrix[][], int n)
    {
        // Defining visited array to keep
        // track of already visited indexes
        boolean visited[][]
            = new boolean[n][n];

        // Flag to indicate whether the
        // path exists or not
        boolean flag = false;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                // if matrix[i][j] is source
                // and it is not visited
                if (
                    matrix[i][j] == 1
                    && !visited[i][j])

                    // Starting from i, j and
                    // then finding the path
                    if (isPath(
                            matrix, i, j, visited)) {
                        // if path exists
                        flag = true;
                        break;
                    }
            }
        }
        if (flag)
            System.out.println("YES");
        else
            System.out.println("NO");
    }

    // Method for checking boundaries
    public static boolean isSafe(
        int i, int j,
        int matrix[][])
    {

        if (
            i >= 0 && i < matrix.length
            && j >= 0
            && j < matrix[0].length)
            return true;
        return false;
    }

    // Returns true if there is a
    // path from a source (a
    // cell with value 1) to a
    // destination (a cell with
    // value 2)
    public static boolean isPath(
        int matrix[][],
        int i, int j,
        boolean visited[][])
    {

        // Checking the boundaries, walls and
        // whether the cell is unvisited
        if (
            isSafe(i, j, matrix)
            && matrix[i][j] != 0
            && !visited[i][j]) {
            // Make the cell visited
            visited[i][j] = true;

            // if the cell is the required
            // destination then return true
            if (matrix[i][j] == 2)
                return true;

            // traverse up
            boolean up = isPath(
                matrix, i - 1,
                j, visited);

            // if path is found in up
            // direction return true
            if (up)
                return true;

            // traverse left
            boolean left
                = isPath(
                    matrix, i, j - 1, visited);

            // if path is found in left
            // direction return true
            if (left)
                return true;

            // traverse down
            boolean down = isPath(
                matrix, i + 1, j, visited);

            // if path is found in down
            // direction return true
            if (down)
                return true;

            // traverse right
            boolean right
                = isPath(
                    matrix, i, j + 1,
                    visited);

            // if path is found in right
            // direction return true
            if (right)
                return true;
        }
        // no path has been found
        return false;
    }

    // driver program to
    // check above function
    public static void main(String[] args)
    {

        int matrix[][] = { { 0, 3, 0, 1 },
                           { 3, 0, 3, 3 },
                           { 2, 3, 3, 3 },
                           { 0, 3, 3, 3 } };

        // calling isPath method
        isPath(matrix, 4);
    }
}

/* This code is contributed by Madhu Priya */
```

## 蟒蛇 3

```
# Python3 program to find
# path between two cell in matrix

# Method for finding and printing
# whether the path exists or not
def isPath(matrix, n):

    # Defining visited array to keep
    # track of already visited indexes
    visited = [[False for x in range (n)]
                      for y in range (n)]

    # Flag to indicate whether the
    # path exists or not
    flag = False

    for i in range (n):
        for j in range (n):

            # If matrix[i][j] is source
            # and it is not visited
            if (matrix[i][j] == 1 and not
                visited[i][j]):

                # Starting from i, j and
                # then finding the path
                if (checkPath(matrix, i,
                              j, visited)):

                    # If path exists
                    flag = True
                    break
    if (flag):
        print("YES")
    else:
        print("NO")

# Method for checking boundaries
def isSafe(i, j, matrix):

    if (i >= 0 and i < len(matrix) and
        j >= 0 and j < len(matrix[0])):
        return True
    return False

# Returns true if there is a
# path from a source(a
# cell with value 1) to a
# destination(a cell with
# value 2)
def checkPath(matrix, i, j,
              visited):

    # Checking the boundaries, walls and
    # whether the cell is unvisited
    if (isSafe(i, j, matrix) and
        matrix[i][j] != 0 and not
        visited[i][j]):

        # Make the cell visited
        visited[i][j] = True

        # If the cell is the required
        # destination then return true
        if (matrix[i][j] == 2):
           return True

        # traverse up
        up = checkPath(matrix, i - 1,
                       j, visited)

        # If path is found in up
        # direction return true
        if (up):
           return True

        # Traverse left
        left = checkPath(matrix, i,
                         j - 1, visited)

        # If path is found in left
        # direction return true
        if (left):
           return True

        # Traverse down
        down = checkPath(matrix, i + 1,
                         j, visited)

        # If path is found in down
        # direction return true
        if (down):
           return True

        # Traverse right
        right = checkPath(matrix, i,
                          j + 1, visited)

        # If path is found in right
        # direction return true
        if (right):
           return True

    # No path has been found
    return False

# Driver code
if __name__ == "__main__":

    matrix = [[0, 3, 0, 1],
              [3, 0, 3, 3],
              [2, 3, 3, 3],
              [0, 3, 3, 3]]

    # calling isPath method
    isPath(matrix, 4)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find path between two
// cell in matrix
using System;

class GFG{

// Method for finding and printing
// whether the path exists or not
static void isPath(int[,] matrix, int n)
{

    // Defining visited array to keep
    // track of already visited indexes
    bool[,] visited = new bool[n, n];

    // Flag to indicate whether the
    // path exists or not
    bool flag = false;

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // If matrix[i][j] is source
            // and it is not visited
            if (matrix[i, j] == 1 &&
              !visited[i, j])

                // Starting from i, j and
                // then finding the path
                if (isPath(matrix, i, j,
                           visited))
                {

                    // If path exists
                    flag = true;
                    break;
                }
        }
    }
    if (flag)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}

// Method for checking boundaries
public static bool isSafe(int i, int j,
                          int[,] matrix)
{
    if (i >= 0 && i < matrix.GetLength(0) &&
        j >= 0 && j < matrix.GetLength(1))
        return true;

    return false;
}

// Returns true if there is a path from
// a source (a cell with value 1) to a
// destination (a cell with value 2)
public static bool isPath(int[,] matrix, int i,
                          int j, bool[,] visited)
{

    // Checking the boundaries, walls and
    // whether the cell is unvisited
    if (isSafe(i, j, matrix) &&
           matrix[i, j] != 0 &&
         !visited[i, j])
    {

        // Make the cell visited
        visited[i, j] = true;

        // If the cell is the required
        // destination then return true
        if (matrix[i, j] == 2)
            return true;

        // Traverse up
        bool up = isPath(matrix, i - 1,
                         j, visited);

        // If path is found in up
        // direction return true
        if (up)
            return true;

        // Traverse left
        bool left = isPath(matrix, i,
                           j - 1, visited);

        // If path is found in left
        // direction return true
        if (left)
            return true;

        // Traverse down
        bool down = isPath(matrix, i + 1,
                           j, visited);

        // If path is found in down
        // direction return true
        if (down)
            return true;

        // Traverse right
        bool right = isPath(matrix, i, j + 1,
                            visited);

        // If path is found in right
        // direction return true
        if (right)
            return true;
    }

    // No path has been found
    return false;
}

// Driver code  
static void Main()
{
    int[,] matrix = { { 0, 3, 0, 1 },
                      { 3, 0, 3, 3 },
                      { 2, 3, 3, 3 },
                      { 0, 3, 3, 3 } };

    // Calling isPath method
    isPath(matrix, 4);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program to find path between two
// cell in matrix

    // Method for finding and printing
    // whether the path exists or not
function isPath(matrix,n)
{

    // Defining visited array to keep
        // track of already visited indexes
        let visited = new Array(n);
            for(let i=0;i<n;i++)
            {
                visited[i]=new Array(n);
                for(let j=0;j<n;j++)
                {
                    visited[i][j]=false;
                }
            }

        // Flag to indicate whether the
        // path exists or not
        let flag = false;

        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {
                // if matrix[i][j] is source
                // and it is not visited
                if (
                    matrix[i][j] == 1
                    && !visited[i][j])

                    // Starting from i, j and
                    // then finding the path
                    if (checkPath(
                            matrix, i, j, visited)) {
                        // if path exists
                        flag = true;
                        break;
                    }
            }
        }
        if (flag)
            document.write("YES<br>");
        else
            document.write("NO<br>");
}

// Method for checking boundaries
function isSafe(i,j,matrix)
{
    if (
            i >= 0 && i < matrix.length
            && j >= 0
            && j < matrix[0].length)
            return true;
        return false;
}

// Returns true if there is a
    // path from a source (a
    // cell with value 1) to a
    // destination (a cell with
    // value 2)
function checkPath(matrix,i,j,visited)
{
    // Checking the boundaries, walls and
        // whether the cell is unvisited
        if (
            isSafe(i, j, matrix)
            && matrix[i][j] != 0
            && !visited[i][j]) {
            // Make the cell visited
            visited[i][j] = true;

            // if the cell is the required
            // destination then return true
            if (matrix[i][j] == 2)
                return true;

            // traverse up
            let up = checkPath(
                matrix, i - 1,
                j, visited);

            // if path is found in up
            // direction return true
            if (up)
                return true;

            // traverse left
            let left
                = checkPath(
                    matrix, i, j - 1, visited);

            // if path is found in left
            // direction return true
            if (left)
                return true;

            // traverse down
            let down = checkPath(
                matrix, i + 1, j, visited);

            // if path is found in down
            // direction return true
            if (down)
                return true;

            // traverse right
            let right
                = checkPath(
                    matrix, i, j + 1,
                    visited);

            // if path is found in right
            // direction return true
            if (right)
                return true;
        }
        // no path has been found
        return false;
}

// driver program to
// check above function
let matrix= [[ 0, 3, 0, 1 ],
             [ 3, 0, 3, 3 ],
             [ 2, 3, 3, 3 ],
             [ 0, 3, 3, 3 ]];

        // calling isPath method
        isPath(matrix, 4);

// This code is contributed by ab2127

</script>
```

**Output**

```
YES
```