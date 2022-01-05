# 有障碍物的网格中的唯一路径

> 原文:[https://www . geesforgeks . org/带障碍物的网格中的唯一路径/](https://www.geeksforgeeks.org/unique-paths-in-a-grid-with-obstacles/)

给定大小为 m * n 的网格，让我们假设您从(1，1)开始，并且您的目标是达到(m，n)。在任何情况下，如果您在(x，y)上，您可以转到(x，y + 1)或(x + 1，y)。
现在考虑网格中是否增加了一些障碍物。会有多少独特的路径？
网格中障碍物和空白区域分别标记为 1 和 0。

**示例:**

```
Input: [[0, 0, 0],
        [0, 1, 0],
        [0, 0, 0]]
Output : 2
There is only one obstacle in the middle.
```

我们讨论了一个问题，当网格中没有障碍物时，计算网格中唯一路径的数量。但这里的情况完全不同。在通过网格时，我们可以得到一些我们无法跳跃的障碍物，到达右下角的路被堵塞了。
这个问题最有效的解决方案可以通过动态规划来实现。像每个动态问题概念一样，我们不会重新计算子问题。将使用自下而上的方法构建临时 2D 矩阵并存储值。

### 方法

*   创建一个与给定矩阵相同大小的 2D 矩阵来存储结果。
*   逐行遍历创建的数组，并开始填充其中的值。
*   如果发现障碍物，将该值设置为 0。
*   对于第一行和第一列，如果没有发现障碍物，则将该值设置为 1。
*   如果给定矩阵中的相应位置不存在障碍物，则设置右值和上值之和
*   返回创建的 2d 矩阵的最后一个值

## C++

```
// C++ code to find number of unique paths
// in a Matrix
#include<bits/stdc++.h>
using namespace std;

int uniquePathsWithObstacles(vector<vector<int>>& A)
{

    int r = A.size(), c = A[0].size();

    // create a 2D-matrix and initializing
    // with value 0
    vector<vector<int>> paths(r, vector<int>(c, 0));

    // Initializing the left corner if
    // no obstacle there
    if (A[0][0] == 0)
        paths[0][0] = 1;

    // Initializing first column of
    // the 2D matrix
    for(int i = 1; i < r; i++)
    {
        // If not obstacle
        if (A[i][0] == 0)
            paths[i][0] = paths[i-1][0];
    }

    // Initializing first row of the 2D matrix
    for(int j = 1; j < c; j++)
    {

        // If not obstacle
        if (A[0][j] == 0)
            paths[0][j] = paths[0][j - 1];
    }  

    for(int i = 1; i < r; i++)
    {
        for(int j = 1; j < c; j++)
        {

            // If current cell is not obstacle
            if (A[i][j] == 0)
                paths[i][j] = paths[i - 1][j] +
                              paths[i][j - 1];
        } 
    }

    // Returning the corner value
    // of the matrix
    return paths[r - 1];
}

// Driver code
int main()
{
   vector<vector<int>> A = { { 0, 0, 0 },
                             { 0, 1, 0 },
                             { 0, 0, 0 } };

   cout << uniquePathsWithObstacles(A) << " \n";                                               
}

// This code is contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find number of unique paths
// in a Matrix
public class Main
{
  static int uniquePathsWithObstacles(int[][] A)
  {

    int r = 3, c = 3;

    // create a 2D-matrix and initializing
    // with value 0
    int[][] paths = new int[r];
    for(int i = 0; i < r; i++)
    {
      for(int j = 0; j < c; j++)
      {
        paths[i][j] = 0;
      }
    }

    // Initializing the left corner if
    // no obstacle there
    if (A[0][0] == 0)
      paths[0][0] = 1;

    // Initializing first column of
    // the 2D matrix
    for(int i = 1; i < r; i++)
    {
      // If not obstacle
      if (A[i][0] == 0)
        paths[i][0] = paths[i - 1][0];
    }

    // Initializing first row of the 2D matrix
    for(int j = 1; j < c; j++)
    {

      // If not obstacle
      if (A[0][j] == 0)
        paths[0][j] = paths[0][j - 1];
    }  

    for(int i = 1; i < r; i++)
    {
      for(int j = 1; j < c; j++)
      {

        // If current cell is not obstacle
        if (A[i][j] == 0)
          paths[i][j] = paths[i - 1][j] +
          paths[i][j - 1];
      } 
    }

    // Returning the corner value
    // of the matrix
    return paths[r - 1];
  }

  // Driver code
  public static void main(String[] args) {
    int[][] A = { { 0, 0, 0 },
                 { 0, 1, 0 },
                 { 0, 0, 0 } };

    System.out.print(uniquePathsWithObstacles(A));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 计算机编程语言

```
# Python code to find number of unique paths in a
# matrix with obstacles.

def uniquePathsWithObstacles(A):

    # create a 2D-matrix and initializing with value 0
    paths = [[0]*len(A[0]) for i in A]

    # initializing the left corner if no obstacle there
    if A[0][0] == 0:
        paths[0][0] = 1

    # initializing first column of the 2D matrix
    for i in range(1, len(A)):

        # If not obstacle
        if A[i][0] == 0:
            paths[i][0] = paths[i-1][0]

    # initializing first row of the 2D matrix
    for j in range(1, len(A[0])):

        # If not obstacle
        if A[0][j] == 0:
            paths[0][j] = paths[0][j-1]

    for i in range(1, len(A)):
        for j in range(1, len(A[0])):

            # If current cell is not obstacle
            if A[i][j] == 0:
                paths[i][j] = paths[i-1][j] + paths[i][j-1]

    # returning the corner value of the matrix
    return paths[-1][-1]

# Driver Code
A = [[0, 0, 0], [0, 1, 0], [0, 0, 0]]
print(uniquePathsWithObstacles(A))
```

## C#

```
// C# code to find number of unique paths
// in a Matrix
using System;
class GFG {

  static int uniquePathsWithObstacles(int[,] A)
  {

    int r = 3, c = 3;

    // create a 2D-matrix and initializing
    // with value 0
    int[,] paths = new int[r,c];
    for(int i = 0; i < r; i++)
    {
      for(int j = 0; j < c; j++)
      {
        paths[i, j] = 0;
      }
    }

    // Initializing the left corner if
    // no obstacle there
    if (A[0, 0] == 0)
      paths[0, 0] = 1;

    // Initializing first column of
    // the 2D matrix
    for(int i = 1; i < r; i++)
    {
      // If not obstacle
      if (A[i, 0] == 0)
        paths[i, 0] = paths[i - 1, 0];
    }

    // Initializing first row of the 2D matrix
    for(int j = 1; j < c; j++)
    {

      // If not obstacle
      if (A[0, j] == 0)
        paths[0, j] = paths[0, j - 1];
    }  

    for(int i = 1; i < r; i++)
    {
      for(int j = 1; j < c; j++)
      {

        // If current cell is not obstacle
        if (A[i, j] == 0)
          paths[i, j] = paths[i - 1, j] +
          paths[i, j - 1];
      } 
    }

    // Returning the corner value
    // of the matrix
    return paths[r - 1, c - 1];
  }

  // Driver code
  static void Main() {
    int[,] A = { { 0, 0, 0 },
                { 0, 1, 0 },
                { 0, 0, 0 } };

    Console.WriteLine(uniquePathsWithObstacles(A));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript code to find number of unique paths
    // in a Matrix

    function uniquePathsWithObstacles(A)
    {

      let r = 3, c = 3;

      // create a 2D-matrix and initializing
      // with value 0
      let paths = new Array(r);
      for(let i = 0; i < r; i++)
      {
          paths[i] = new Array(c);
        for(let j = 0; j < c; j++)
        {
          paths[i][j] = 0;
        }
      }

      // Initializing the left corner if
      // no obstacle there
      if (A[0][0] == 0)
        paths[0][0] = 1;

      // Initializing first column of
      // the 2D matrix
      for(let i = 1; i < r; i++)
      {
        // If not obstacle
        if (A[i][0] == 0)
          paths[i][0] = paths[i - 1][0];
      }

      // Initializing first row of the 2D matrix
      for(let j = 1; j < c; j++)
      {

        // If not obstacle
        if (A[0][j] == 0)
          paths[0][j] = paths[0][j - 1];
      } 

      for(let i = 1; i < r; i++)
      {
        for(let j = 1; j < c; j++)
        {

          // If current cell is not obstacle
          if (A[i][j] == 0)
            paths[i][j] = paths[i - 1][j] +
            paths[i][j - 1];
        }
      }

      // Returning the corner value
      // of the matrix
      return paths[r - 1];
    }

    let A = [ [ 0, 0, 0 ],
             [ 0, 1, 0 ],
             [ 0, 0, 0 ] ];

    document.write(uniquePathsWithObstacles(A));

    // This code is contributed by suresh07.
</script>
```

**Output**

```
2 
```

本文由  供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。

### 动力定位解的空间优化。

在这种方法中，我们将使用自下而上的方法，使用给定的“A”2D 矩阵来存储之前的答案。

**接近**

*   开始逐行遍历给定的“and 矩阵，并填充其中的值。
*   对于第一行和第一列，如果没有发现障碍物，则将该值设置为 1。
*   对于第一行和第一列，如果发现障碍，则开始填充 0，直到该特定行或列的最后一个索引。
*   现在从第二行和第二列开始遍历(例如:A[ 1 ][ 1 ])。
*   如果发现障碍物，在特定网格处设置 0(例如:A[ i ][ j ])，否则在 A[ i ][ j ]处设置上限值和左限值之和。
*   返回 2D 矩阵的最后一个值。

下面是上述方法的实现。

## C++

```
// CPP program for the above approach

#include <bits/stdc++.h>
using namespace std;

int uniquePathsWithObstacles(vector<vector<int> >& A)
{

    int r = A.size();
    int c = A[0].size();

    // If obstacle is at starting position
    if (A[0][0])
        return 0;

    //  Initializing starting position
    A[0][0] = 1;

    // first row all are '1' until obstacle
    for (int j = 1; j < c; j++) {

        if (A[0][j] == 0) {
            A[0][j] = A[0][j - 1];
        }
        else {
            // No ways to reach at this index
            A[0][j] = 0;
        }
    }

    // first column all are '1' until obstacle
    for (int i = 1; i < r; i++) {

        if (A[i][0] == 0) {
            A[i][0] = A[i - 1][0];
        }
        else {
            // No ways to reach at this index
            A[i][0] = 0;
        }
    }

    for (int i = 1; i < r; i++) {

        for (int j = 1; j < c; j++) {
            // If current cell has no obstacle
            if (A[i][j] == 0) {

                A[i][j] = A[i - 1][j] + A[i][j - 1];
            }
            else {
                // No ways to reach at this index
                A[i][j] = 0;
            }
        }
    }

    // returning the bottom right
    // corner of Grid
    return A[r - 1];
}

// Driver Code

int main()
{

    vector<vector<int> > A
        = { { 0, 0, 0 }, { 0, 1, 0 }, { 0, 0, 0 } };

    cout << uniquePathsWithObstacles(A) << "\n";

    return 0;
}
// This code is contributed by hemantraj712
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    static int uniquePathsWithObstacles(int[][] A)
    {

        int r = A.length;
        int c = A[0].length;

        // If obstacle is at starting position
        if (A[0][0] != 0)
            return 0;

        //  Initializing starting position
        A[0][0] = 1;

        // first row all are '1' until obstacle
        for (int j = 1; j < c; j++) {

            if (A[0][j] == 0) {
                A[0][j] = A[0][j - 1];
            }
            else {
                // No ways to reach at this index
                A[0][j] = 0;
            }
        }

        // first column all are '1' until obstacle
        for (int i = 1; i < r; i++) {

            if (A[i][0] == 0) {
                A[i][0] = A[i - 1][0];
            }
            else {
                // No ways to reach at this index
                A[i][0] = 0;
            }
        }

        for (int i = 1; i < r; i++)
        {

            for (int j = 1; j < c; j++)
            {

                // If current cell has no obstacle
                if (A[i][j] == 0) {

                    A[i][j] = A[i - 1][j] + A[i][j - 1];
                }
                else {
                    // No ways to reach at this index
                    A[i][j] = 0;
                }
            }
        }

        // returning the bottom right
        // corner of Grid
        return A[r - 1];
    }

  // Driver code
    public static void main(String[] args)
    {
        int[][] A
            = { { 0, 0, 0 }, { 0, 1, 0 }, { 0, 0, 0 } };

        System.out.print(uniquePathsWithObstacles(A));
    }
}

// This code is contributed by rajsanghavi9.
```

**Output**

```
2
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(1)