# 图中与 k 条边精确连接的所有顶点对

> 原文:[https://www . geeksforgeeks . org/全顶点对-图中精确 k 边连通/](https://www.geeksforgeeks.org/all-vertex-pairs-connected-with-exactly-k-edges-in-a-graph/)

给定一个用邻接矩阵和整数“k”表示的有向图，任务是找出所有与“k”边精确相连的顶点对。
此外，找出两个顶点在 k 条边上链接的方法。

**示例:**

```
Input : k = 3 and graph :
0 1 0 0 0 
0 0 1 0 0 
0 0 0 1 1 
1 0 0 0 0 
0 0 1 0 0 
Output :
1 -> 4 in 1 way(s)
1 -> 5 in 1 way(s)
2 -> 1 in 1 way(s)
2 -> 3 in 1 way(s)
3 -> 2 in 1 way(s)
3 -> 4 in 1 way(s)
3 -> 5 in 1 way(s)
4 -> 3 in 1 way(s)
5 -> 1 in 1 way(s)
5 -> 3 in 1 way(s)

Input : k = 2 and graph :
0 0 0 
1 0 1 
0 1 0 
Output :
2 -> 2 in 1 way(s)
3 -> 1 in 1 way(s)
3 -> 3 in 1 way(s)
```

**进场:**

*   我们将把邻接矩阵乘以它自己的 k 次。
*   在结果矩阵中，res[i][j]将是从正好覆盖“k”边的顶点“I”到达顶点“j”的方式数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to multiply two square matrices
vector<vector<int>> multiplyMatrices(
  vector<vector<int>> arr1,
  vector<vector<int>> arr2)
{
  int order = arr1.size();
  vector<vector<int>> ans(order, vector<int>(order));

  for(int i = 0; i < order; i++)
  {
    for(int j = 0; j < order; j++)
    {
      for(int k = 0; k < order; k++)
      {
        ans[i][j] += arr1[i][k] * arr2[k][j];
      }
    }
  }
  return ans;
}

// Function to find all the pairs that
// can be connected with exactly 'k' edges
void solve(vector<vector<int>> arr, int k)
{
  vector<vector<int>> res(
    arr.size(), vector<int>(arr[0].size()));

  // Copying arr to res,
  // which is the result for k=1
  for(int i = 0; i < res.size(); i++)
    for(int j = 0; j < res.size(); j++)
      res[i][j] = arr[i][j];

  // Multiplying arr with itself
  // the required number of times
  for(int i = 2; i <= k; i++)
    res = multiplyMatrices(res, arr);

  for(int i = 0; i < res.size(); i++)
    for(int j = 0; j < res.size(); j++)

      // If there is a path between 'i'
      // and 'j' in exactly 'k' edges
      if (res[i][j] > 0)
      {
        cout << i << " -> " << j
             << " in " << res[i][j]
             << " way(s)" << endl;
      }
}

// Driver code
int main(int argc, char const *argv[])
{
  vector<vector<int>> arr(5, vector<int>(5));
  arr[0][1] = 1;
  arr[1][2] = 1;
  arr[2][3] = 1;
  arr[2][4] = 1;
  arr[3][0] = 1;
  arr[4][2] = 1;
  int k = 3;

  solve(arr, k);
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class KPaths {

    // Function to multiply two square matrices
    static int[][] multiplyMatrices(int[][] arr1, int[][] arr2)
    {
        int order = arr1.length;
        int[][] ans = new int[order][order];
        for (int i = 0; i < order; i++) {
            for (int j = 0; j < order; j++) {
                for (int k = 0; k < order; k++) {
                    ans[i][j] += arr1[i][k] * arr2[k][j];
                }
            }
        }
        return ans;
    }

    // Function to find all the pairs that
    // can be connected with exactly 'k' edges
    static void solve(int[][] arr, int k)
    {
        int[][] res = new int[arr.length][arr[0].length];

        // copying arr to res,
        // which is the result for k=1
        for (int i = 0; i < res.length; i++)
            for (int j = 0; j < res.length; j++)
                res[i][j] = arr[i][j];

        // multiplying arr with itself
        // the required number of times
        for (int i = 2; i <= k; i++)
            res = multiplyMatrices(res, arr);

        for (int i = 0; i < res.length; i++)
            for (int j = 0; j < res.length; j++)

                // if there is a path between 'i'
                // and 'j' in exactly 'k' edges
                if (res[i][j] > 0)
                    System.out.println(i + " -> " + j + " in " + res[i][j] + " way(s)");
    }

    // Driver code
    public static void main(String[] args)
    {
        int[][] arr = new int[5][5];
        arr[0][1] = 1;
        arr[1][2] = 1;
        arr[2][3] = 1;
        arr[2][4] = 1;
        arr[3][0] = 1;
        arr[4][2] = 1;
        int k = 3;
        solve(arr, k);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to multiply two square matrices
def multiplyMatrices(arr1, arr2):

    order = len(arr1)
    ans = [[0 for i in range(order)] for j in range(order)]

    for i in range(order):
        for j in range(order):
            for k in range(order):
                ans[i][j] += arr1[i][k] * arr2[k][j]

    return ans

# Function to find all the pairs that
# can be connected with exactly 'k' edges
def solve(arr, k):
    res = [[0 for i in range(len(arr))] for j in range(len(arr))]

    # Copying arr to res,
    # which is the result for k=1
    for i in range(len(arr)):
        for j in range(len(arr)):
            res[i][j] = arr[i][j]

    # Multiplying arr with itself
    # the required number of times
    for i in range(2, k+1):
        res = multiplyMatrices(res, arr)

    for i in range(len(arr)):
        for j in range(len(arr)):

            # If there is a path between 'i'
            # and 'j' in exactly 'k' edges
            if (res[i][j] > 0):
                print(i, "->", j, "in", res[i][j], "way(s)")

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4]
    arr = [[0 for i in range(5)] for j in range(5)]
    arr[0][1] = 1
    arr[1][2] = 1
    arr[2][3] = 1
    arr[2][4] = 1
    arr[3][0] = 1
    arr[4][2] = 1
    k = 3

    solve(arr, k)

# This code is contributed by kirtishsurangalikar
```

## C#

```
// C# implementation of the approach
using System;

class KPaths
{

// Function to multiply two square matrices
static int[,] multiplyMatrices(int[,] arr1,
                               int[,] arr2)
{
    int order = arr1.GetLength(0);
    int[,] ans = new int[order, order];
    for (int i = 0; i < order; i++)
    {
        for (int j = 0; j < order; j++)
        {
            for (int k = 0; k < order; k++)
            {
                ans[i, j] += arr1[i, k] *
                             arr2[k, j];
            }
        }
    }
    return ans;
}

// Function to find all the pairs that
// can be connected with exactly 'k' edges
static void solve(int[,] arr, int k)
{
    int[,] res = new int[arr.GetLength(0),
                         arr.GetLength(1)];

    // copying arr to res,
    // which is the result for k = 1
    for (int i = 0; i < res.GetLength(0); i++)
        for (int j = 0; j < res.GetLength(1); j++)
            res[i, j] = arr[i, j];

    // multiplying arr with itself
    // the required number of times
    for (int i = 2; i <= k; i++)
        res = multiplyMatrices(res, arr);

    for (int i = 0; i < res.GetLength(0); i++)
        for (int j = 0; j < res.GetLength(1); j++)

            // if there is a path between 'i'
            // and 'j' in exactly 'k' edges
            if (res[i,j] > 0)
                Console.WriteLine(i + " -> " + j + " in " +
                                    res[i, j] + " way(s)");
}

// Driver code
public static void Main(String[] args)
{
    int[,] arr = new int[5, 5];
    arr[0, 1] = 1;
    arr[1, 2] = 1;
    arr[2, 3] = 1;
    arr[2, 4] = 1;
    arr[3, 0] = 1;
    arr[4, 2] = 1;
    int k = 3;
    solve(arr, k);
}
}

// This code is contributed by Rajput-Ji
```

**Output**

```
0 -> 3 in 1 way(s)
0 -> 4 in 1 way(s)
1 -> 0 in 1 way(s)
1 -> 2 in 1 way(s)
2 -> 1 in 1 way(s)
2 -> 3 in 1 way(s)
2 -> 4 in 1 way(s)
3 -> 2 in 1 way(s)
4 -> 0 in 1 way(s)
4 -> 2 in 1 way(s)
```

通过使用[矩阵指数化](https://www.geeksforgeeks.org/matrix-exponentiation/)，对于 k 的大值，可以降低上述代码的时间复杂度。复杂度可以从 **O(n^3 * k)** 变为 **O(n^3 * log k)**

## Java 语言(一种计算机语言，尤用于创建网站)

```
class KPaths {

    // Function to multiply two square matrices
    static int[][] multiplyMatrices(int[][] arr1, int[][] arr2)
    {
        int order = arr1.length;
        int[][] ans = new int[order][order];
        for (int i = 0; i < order; i++) {
            for (int j = 0; j < order; j++) {
                for (int k = 0; k < order; k++) {
                    ans[i][j] += arr1[i][k] * arr2[k][j];
                }
            }
        }
        return ans;
    }

    // Function to find all the pairs that
    // can be connected with exactly 'k' edges
    static void solve(int[][] arr, int k)
    {
        int[][] res = new int[arr.length][arr[0].length];

        res = power(arr, k, arr[0].length);
        for (int i = 0; i < res.length; i++)
            for (int j = 0; j < res.length; j++)

                // if there is a path between 'i'
                // and 'j' in exactly 'k' edges
                if (res[i][j] > 0)
                    System.out.println(i + " -> " + j + " in " + res[i][j] + " way(s)");
    }

    static int[][] power(int x[][], int y, int n)
    {
        // MATRIX EXPONENTIATION
        // Initialize result
        int res[][] = identity(n);

        while (y > 0) {

            if ((y & 1) == 1)
                res = multiplyMatrices(res, x);

            // y must be even now
            // y = y / 2
            y = y >> 1;
            x = multiplyMatrices(x, x);
        }
        return res;
    }
    static int[][] identity(int n)
    {
        // returns identity matrix of order n
        int r[][] = new int[n][n];
        for (int i = 0; i < n; i++)
            r[i][i] = 1;

        return r;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[][] arr = new int[5][5];
        arr[0][1] = 1;
        arr[1][2] = 1;
        arr[2][3] = 1;
        arr[2][4] = 1;
        arr[3][0] = 1;
        arr[4][2] = 1;
        int k = 3;
        solve(arr, k);
    }
}
```

## C#

```
// C# implementation of the above approach:
using System;

class KPaths
{

    // Function to multiply two square matrices
    static int[,] multiplyMatrices(int[,] arr1,
                                   int[,] arr2)
    {
        int order = arr1.GetLength(0);
        int[,] ans = new int[order,order];
        for (int i = 0; i < order; i++)
        {
            for (int j = 0; j < order; j++)
            {
                for (int k = 0; k < order; k++)
                {
                    ans[i, j] += arr1[i, k] *
                                 arr2[k, j];
                }
            }
        }
        return ans;
    }

    // Function to find all the pairs that
    // can be connected with exactly 'k' edges
    static void solve(int[,] arr, int k)
    {
        int[,] res = new int[arr.GetLength(0),
                             arr.GetLength(1)];

        res = power(arr, k, arr.GetLength(0));
        for (int i = 0; i < res.GetLength(0); i++)
            for (int j = 0; j < res.GetLength(1); j++)

                // if there is a path between 'i'
                // and 'j' in exactly 'k' edges
                if (res[i, j] > 0)
                    Console.WriteLine(i + " -> " + j + 
                      " in " + res[i, j] + " way(s)");
    }

    static int[,] power(int [,]x, int y, int n)
    {

        // MATRIX EXPONENTIATION
        // Initialize result
        int [,]res = identity(n);

        while (y > 0)
        {

            if ((y & 1) == 1)
                res = multiplyMatrices(res, x);

            // y must be even now
            // y = y / 2
            y = y >> 1;
            x = multiplyMatrices(x, x);
        }
        return res;
    }

    static int[,] identity(int n)
    {
        // returns identity matrix of order n
        int [,]r = new int[n, n];
        for (int i = 0; i < n; i++)
            r[i, i] = 1;

        return r;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[,] arr = new int[5, 5];
        arr[0, 1] = 1;
        arr[1, 2] = 1;
        arr[2, 3] = 1;
        arr[2, 4] = 1;
        arr[3, 0] = 1;
        arr[4, 2] = 1;
        int k = 3;
        solve(arr, k);
    }
}

// This code is contributed by PrinciRaj1992
```