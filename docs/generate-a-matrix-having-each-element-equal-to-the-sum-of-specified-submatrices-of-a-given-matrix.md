# 生成一个矩阵，其每个元素等于给定矩阵的指定子矩阵之和

> 原文:[https://www . geesforgeks . org/generate-a-matrix-让每个元素等于给定矩阵的指定子矩阵之和/](https://www.geeksforgeeks.org/generate-a-matrix-having-each-element-equal-to-the-sum-of-specified-submatrices-of-a-given-matrix/)

给定一个维度为 **M*N** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】【】**和一个整数 **K** ，任务是生成一个矩阵**答案【】【】、**，其中**答案【I】【j】**等于所有元素**mat【r】**的和，使得**r∈I–K，i + K】，c∈j \u K，j + K】**

**示例:**

> **输入:** mat = {{1，2，3}，{4，5，6}，{7，8，9}}，K = 1
> **输出:** {{12，21，16}，{27，45，33}，{24，39，28}}
> **解释:**
> 答案[0][0]= mat[0][0]+mat[0][1]+mat[1][0]+mat[0]
> 答案[0][1]= mat[0][0]+mat[0][1]+mat[0][2]+mat[1][0]+mat[1][1]+mat[1][2]= 1+2+3+4+5+6 = 21。
> 同样，答案[0][2] = 16，答案[1][0] = 27，答案[1][1] = 45，答案[1][2] = 33，答案[2][0] = 24，答案[2][1] = 39，答案[2][2] = 28
> 
> **输入:** mat = {{1，2，3}，{4，5，6}，{7，8，9}}，K = 2
> ***输出:** {{45，45，45}，{45，45，45}，{45，45，45}}*

**天真方法:**最简单的方法是使用两个[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)迭代矩阵元素，并计算所有元素的和**mat[r](I–K≤r≤I+K，j–K≤c≤j+K)**，对于每一个可能的**答案[i][j]** 。最后，遍历矩阵后打印矩阵。

***时间复杂度:**O(N<sup>4</sup>)* *****辅助空间:** O(1)***

**[**基于前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **的方法:**为了优化上述方法，想法是初始化一个辅助矩阵 **aux[M][N]** 来存储矩阵 **mat[][]** 的所有行的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。一旦构造了 **aux[][]** ，**答案【I】【j】**可以通过遍历**【I–K≤r≤I+K】**范围内的所有行并添加**aux[r][max _ col]–aux[r][min _ col]+aux[r][min _ col]**来计算。该增加值表示**行【r】**对**答案【I】【j】**的贡献之和。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required matrix
void matrixBlockSum(vector<vector<int>> mat,int K)
{

    // Stores number of rows and columns
    int n = mat.size();
    int m = mat[0].size();
    vector<vector<int>> mat1(n, vector<int>(m));

    // Traverse the matrix mat[][]
    // row-wise to calculate prefix row sum
    int cnt = 1;
    for (int i = 0; i < n; i++)
    {
        int k = 0;
        for (int j = 0; j < m; j++)
        {

            // Calculate Prefix Sum
            k += mat[i][j];
            mat1[i][j] = k;
            mat[i][j] = cnt;
            cnt += 1;
          }
      }

    // Declare the final matrix
    vector<vector<int>> ans;

    // Traverse the matrix row-wise
    // and fill valid indices ans[i][j]
    for (int i = 0; i < n; i++)
    {

        // Stores required sum of block
        // for each cell in current row
        vector<int> temp;
        for (int j = 0; j < m; j++)
        {

            // Fix the bounds
            // i-k >=0 and i+k < n
            // j-k > =0 and j+k < m
            int mnr = max(0, i - K);
            int mnc = max(0, j - K);
            int mxr = min(n - 1, i + K);
            int mxc = min(m - 1, j + K);
            int ans1 = 0;

            // Iterate in range [minimum row(mnr),
            // maximum row(mxr)] and store the sum of row k
            for (int k = mnr; k <= mxr; k++)
                ans1 += (mat1[k][mxc] - mat1[k][mnc]) + mat[k][mnc];

            // Append it to temp
            temp.push_back(ans1);
          }

        // Append temp to final matrix
        ans.push_back(temp);
      }

    // Print the matrix
    int xx = ans.size(), y = 0;
    cout << "[";
    for(auto i:ans)
    {
      cout << "[";
      y++;
      int x = i.size();
      for(int j = 0; j < x - 1; j++)
        cout << i[j] << ", ";
      cout << i[x - 1] << "]";
      if(y < xx) cout << ", ";
    }
    cout << "] ";
}

// Driver Code
int main()
{
  vector<vector<int>> mat = { {1, 2, 3},
                             {4, 5, 6},
                             {7, 8, 9}};
  int K = 1;
  matrixBlockSum(mat, K);
  return 0;
}

// This code is contributed by mohit kumar 29.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to find the required matrix
  static void matrixBlockSum(int mat[][], int K)
  {

    // Stores number of rows and columns
    int n = mat.length;
    int m = mat[0].length;
    int mat1[][] = new int[n][m];

    // Traverse the matrix mat[][]
    // row-wise to calculate prefix row sum
    int cnt = 1;
    for (int i = 0; i < n; i++)
    {
      int k = 0;
      for (int j = 0; j < m; j++)
      {

        // Calculate Prefix Sum
        k += mat[i][j];
        mat1[i][j] = k;
        mat[i][j] = cnt;
        cnt += 1;
      }
    }

    // Declare the final matrix
    int ans[][] = new int[n][m];

    // Traverse the matrix row-wise
    // and fill valid indices ans[i][j]
    for (int i = 0; i < n; i++)
    {

      // Stores required sum of block
      // for each cell in current row
      // int temp = new int[m];
      for (int j = 0; j < m; j++)
      {

        // Fix the bounds
        // i-k >=0 and i+k < n
        // j-k > =0 and j+k < m
        int mnr = Math.max(0, i - K);
        int mnc = Math.max(0, j - K);
        int mxr = Math.min(n - 1, i + K);
        int mxc = Math.min(m - 1, j + K);
        int ans1 = 0;

        // Iterate in range [minimum row(mnr),
        // maximum row(mxr)] and store the sum of
        // row k
        for (int k = mnr; k <= mxr; k++)
          ans1 += (mat1[k][mxc] - mat1[k][mnc])
          + mat[k][mnc];

        // Append temp to final matrix
        ans[i][j] = (ans1);
      }
    }

    // Print the matrix
    int xx = ans.length, y = 0;
    System.out.print("[");
    for (int i = 0; i < n; i++)
    {
      System.out.print("[");
      y++;
      for (int j = 0; j < m - 1; j++)
        System.out.print(ans[i][j] + ", ");
      System.out.print(ans[i][m - 1] + "]");
      if (y < xx)
        System.out.print(", ");
    }
    System.out.print("] ");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int mat[][]
      = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    int K = 1;
    matrixBlockSum(mat, K);
  }
}

// This code is contributed by Dharanendra L V.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the required matrix

def matrixBlockSum(mat, K):

    # Stores number of rows and columns
    n = len(mat)
    m = len(mat[0])

    # Traverse the matrix mat[][]
    # row-wise to calculate prefix row sum
    for i in range(n):
        k = 0
        for j in range(m):

            # Calculate Prefix Sum
            k += mat[i][j]
            mat[i][j] = (mat[i][j], k)

    # Declare the final matrix
    ans = []

    # Traverse the matrix row-wise
    # and fill valid indices ans[i][j]
    for i in range(n):

        # Stores required sum of block
        # for each cell in current row
        temp = []
        for j in range(m):

            # Fix the bounds
            # i-k >=0 and i+k < n
            # j-k > =0 and j+k < m
            mnr = max(0, i - K)
            mnc = max(0, j - K)
            mxr = min(n - 1, i + K)
            mxc = min(m - 1, j + K)
            ans1 = 0

            # Iterate in range [minimum row(mnr),
            # maximum row(mxr)] and store the sum of row k
            #print(mnr,mxr+1)
            for k in range(mnr, mxr+1):
                ans1 += (mat[k][mxc][1]-mat[k][mnc][1])+mat[k][mnc][0]

            # Append it to temp
            temp.append(ans1)

        # Append temp to final matrix
        ans.append(temp)

    # Print the matrix
    print(ans)

# Driver Code
if __name__ == "__main__":

    mat = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    K = 1
    matrixBlockSum(mat, K)
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the required matrix
  static void matrixBlockSum(int [,]mat, int K)
  {

    // Stores number of rows and columns
    int n = mat.GetLength(0);
    int m = mat.GetLength(1);
    int [,]mat1 = new int[n,m];

    // Traverse the matrix [,]mat
    // row-wise to calculate prefix row sum
    int cnt = 1;
    for (int i = 0; i < n; i++)
    {
      int k = 0;
      for (int j = 0; j < m; j++)
      {

        // Calculate Prefix Sum
        k += mat[i,j];
        mat1[i,j] = k;
        mat[i,j] = cnt;
        cnt += 1;
      }
    }

    // Declare the readonly matrix
    int [,]ans = new int[n,m];

    // Traverse the matrix row-wise
    // and fill valid indices ans[i,j]
    for (int i = 0; i < n; i++)
    {

      // Stores required sum of block
      // for each cell in current row
      // int temp = new int[m];
      for (int j = 0; j < m; j++)
      {

        // Fix the bounds
        // i-k >=0 and i+k < n
        // j-k > =0 and j+k < m
        int mnr = Math.Max(0, i - K);
        int mnc = Math.Max(0, j - K);
        int mxr = Math.Min(n - 1, i + K);
        int mxc = Math.Min(m - 1, j + K);
        int ans1 = 0;

        // Iterate in range [minimum row(mnr),
        // maximum row(mxr)] and store the sum of
        // row k
        for (int k = mnr; k <= mxr; k++)
          ans1 += (mat1[k, mxc] - mat1[k, mnc])
          + mat[k, mnc];

        // Append temp to readonly matrix
        ans[i, j] = (ans1);
      }
    }

    // Print the matrix
    int xx = ans.Length, y = 0;
    Console.Write("[");
    for (int i = 0; i < n; i++)
    {
      Console.Write("[");
      y++;
      for (int j = 0; j < m - 1; j++)
        Console.Write(ans[i, j] + ", ");
      Console.Write(ans[i, m - 1] + "]");
      if (y < xx)
        Console.Write(", ");
    }
    Console.Write("] ");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int [,]mat
      = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    int K = 1;
    matrixBlockSum(mat, K);
  }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to find the required matrix
function matrixBlockSum(mat, k)
{

    // Stores number of rows and columns
    let n = mat.length;
    let m = mat[0].length;
    let mat1 = new Array(n);
    for(let i = 0; i < n; i++)
    {
        mat1[i] = new Array(m);
    }

    // Traverse the matrix mat[][]
    // row-wise to calculate prefix row sum
    let cnt = 1;
    for(let i = 0; i < n; i++)
    {
        let k = 0;
        for(let j = 0; j < m; j++)
        {

            // Calculate Prefix Sum
            k += mat[i][j];
            mat1[i][j] = k;
            mat[i][j] = cnt;
            cnt += 1;
        }
    }

    // Declare the final matrix
    let ans = new Array(n);
    for(let i = 0; i < n; i++)
    {
        ans[i] = new Array(m);
    }

    // Traverse the matrix row-wise
    // and fill valid indices ans[i][j]
    for(let i = 0; i < n; i++)
    {

        // Stores required sum of block
        // for each cell in current row
        // int temp = new int[m];
        for(let j = 0; j < m; j++)
        {

            // Fix the bounds
            // i-k >=0 and i+k < n
            // j-k > =0 and j+k < m
            let mnr = Math.max(0, i - K);
            let mnc = Math.max(0, j - K);
            let mxr = Math.min(n - 1, i + K);
            let mxc = Math.min(m - 1, j + K);
            let ans1 = 0;

            // Iterate in range [minimum row(mnr),
            // maximum row(mxr)] and store the sum of
            // row k
            for (let k = mnr; k <= mxr; k++)
            ans1 += (mat1[k][mxc] - mat1[k][mnc]) +
                      mat[k][mnc];

            // Append temp to final matrix
            ans[i][j] = (ans1);
        }
    }

    // Print the matrix
    let xx = ans.length, y = 0;
    document.write("[");
    for(let i = 0; i < n; i++)
    {
        document.write("[");
        y++;
        for (let j = 0; j < m - 1; j++)
            document.write(ans[i][j] + ", ");

        document.write(ans[i][m - 1] + "]");

        if (y < xx)
            document.write(", ");
    }
    document.write("] ");
}

// Driver Code
let mat = [ [ 1, 2, 3 ],
            [ 4, 5, 6 ],
            [ 7, 8, 9 ] ];
let K = 1;

matrixBlockSum(mat, K);

// This code is contributed by unknown2108

</script>
```

****Output:** 

```
[[12, 21, 16], [27, 45, 33], [24, 39, 28]]
```** 

*****时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )***

****高效方法:**为了优化上述方法，想法是初始化辅助矩阵 **aux[M][N]** ，使得 **aux[i][j]** 使用以下表达式将子矩阵 **mat[0][0]** 至 **mat[i][j]** 中的元素之和存储起来:**

> **指数 **(mnr，mnc)** 和 **(mxr，mxc)** 之间的子矩阵之和由下式给出:
> **aux[mxr][mxc]–aux[mnr–1][mxc]–aux[mxr][MNC–1]+aux[mnr–1][MNC–1]**
> 注:子矩阵**aux[mnr-1][MNC-1]****

****按照以下步骤构建**辅助**矩阵:****

*   ****将第一行 **mat[][]** 复制到 **aux[][]** 。****
*   ****求矩阵的列式和并存储。****
*   ****求更新矩阵 **aux[][]** 的行总和。****
*   ****完成上述步骤后，打印生成的矩阵 **aux[][]** 。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <iostream>
using namespace std;

const int M = 3;
const int N = 3;

// Function to generate the required matrix
void matrixBlockSum(int mat[][M], int K)
{

    // Stores count of rows and columns
    int n = N;
    int m = M;

    // Traverse the matrix to
    // to compute prefix sum
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            if (i - 1 >= 0)
            {
                mat[i][j] += mat[i - 1][j];
            }
            if (j - 1 >= 0)
            {
                mat[i][j] += mat[i][j - 1];
            }
            if (i - 1 >= 0 && j - 1 >= 0)
            {
                mat[i][j] -= mat[i - 1][j - 1];
            }
        }
    }

    int ans[n][m];

    // Traverse the matrix row-wise
    // to fill the required matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Fix the boundaries
            // i-k >=0 and i+k < n
            // j-k > =0 and j+k < m
            int mnr = max(0, i - K);
            int mxr = min(i + K, n - 1);
            int mnc = max(0, j - K);
            int mxc = min(j + K, m - 1);

            // Add sum of elements between
            // (0, 0) and (mxr, mxc)
            ans[i][j] = mat[mxr][mxc];

            // Remove elements between
            // (0, 0) and (mnr-1, mxc)
            if (mnr - 1 >= 0)
            {
                ans[i][j] -= mat[mnr - 1][mxc];
            }

            // Remove elements between
            // (0, 0) and (mxr, mnc-1)
            if (mnc - 1 >= 0)
            {
                ans[i][j] -= mat[mxr][mnc - 1];
            }

            // Add aux[mnr-1][mnc-1] as
            // elements between (0, 0)
            // and (mnr-1, mnc-1) are
            // subtracted twice
            if (mnr - 1 >= 0 && mnc - 1 >= 0)
            {
                ans[i][j] += mat[mnr - 1][mnc - 1];
            }
        }
    }

    // Print the matrix 
    for(int i = 0; i < n; i++)
    {       
        for(int j = 0; j < m; j++)
        {
            cout << ans[i][j] << " ";
        }
    }
}

// Driver code
int main()
{
    int mat[][M] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };
    int K = 1;

    matrixBlockSum(mat, K);
}

// This code is contributed by rag2127**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to generate the required matrix
  static void matrixBlockSum(int[][] mat, int K)
  {

    // Stores count of rows and columns
    int n = mat.length;
    int m = mat[0].length;

    // Traverse the matrix to
    // to compute prefix sum
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < m; j++)
      {
        if (i - 1 >= 0)
        {
          mat[i][j] += mat[i - 1][j];
        }
        if (j - 1 >= 0)
        {
          mat[i][j] += mat[i][j - 1];
        }
        if (i - 1 >= 0 && j - 1 >= 0)
        {
          mat[i][j] -= mat[i - 1][j - 1];
        }
      }
    }

    int[][] ans = new int[n][m];

    // Traverse the matrix row-wise
    // to fill the required matrix
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < m; j++)
      {

        // Fix the boundaries
        // i-k >=0 and i+k < n
        // j-k > =0 and j+k < m
        int mnr = Math.max(0, i - K);
        int mxr = Math.min(i + K, n - 1);
        int mnc = Math.max(0, j - K);
        int mxc = Math.min(j + K, m - 1);

        // Add sum of elements between
        // (0, 0) and (mxr, mxc)
        ans[i][j] = mat[mxr][mxc];

        // Remove elements between
        // (0, 0) and (mnr-1, mxc)
        if (mnr - 1 >= 0)
        {
          ans[i][j] -= mat[mnr - 1][mxc];
        }

        // Remove elements between
        // (0, 0) and (mxr, mnc-1)
        if (mnc - 1 >= 0)
        {
          ans[i][j] -= mat[mxr][mnc - 1];
        }

        // Add aux[mnr-1][mnc-1] as
        // elements between (0, 0)
        // and (mnr-1, mnc-1) are
        // subtracted twice
        if (mnr - 1 >= 0 && mnc - 1 >= 0)
        {
          ans[i][j] += mat[mnr - 1][mnc - 1];
        }
      }
    }

    // Print the matrix 
    for (int i = 0; i < n; i++)
    {       
      for (int j = 0; j < m; j++)
      {
        System.out.print(ans[i][j] + " ");
      }
    }
  }

  // Driver code
  public static void main (String[] args)
  {
    int[][] mat = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    int K = 1;
    matrixBlockSum(mat, K);
  }
}

// This code is contributed by avanitrachhadiya2155.**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to generate the required matrix

def matrixBlockSum(mat, K):

        # Stores count of rows and columns
    n = len(mat)
    m = len(mat[0])

    # Traverse the matrix to
    # to compute prefix sum
    for i in range(n):

        for j in range(m):

            if i-1 >= 0:
                mat[i][j] += mat[i-1][j]
            if j-1 >= 0:
                mat[i][j] += mat[i][j-1]
            if i-1 >= 0 and j-1 >= 0:
                mat[i][j] -= mat[i-1][j-1]

    ans = [[0 for i in range(m)]for i in range(n)]

    # Traverse the matrix row-wise
    # to fill the required matrix
    for i in range(n):
        for j in range(m):

            # Fix the boundaries
            # i-k >=0 and i+k < n
            # j-k > =0 and j+k < m
            mnr = max(0, i - K)
            mxr = min(i + K, n-1)
            mnc = max(0, j - K)
            mxc = min(j + K, m-1)

            # Add sum of elements between
            # (0, 0) and (mxr, mxc)
            ans[i][j] = mat[mxr][mxc]

            # Remove elements between
            # (0, 0) and (mnr-1, mxc)
            if mnr - 1 >= 0:
                ans[i][j] -= mat[mnr-1][mxc]

            # Remove elements between
            # (0, 0) and (mxr, mnc-1)
            if mnc - 1 >= 0:
                ans[i][j] -= mat[mxr][mnc-1]

            # Add aux[mnr-1][mnc-1] as
            # elements between (0, 0)
                # and (mnr-1, mnc-1) are
            # subtracted twice
            if mnr - 1 >= 0 and mnc - 1 >= 0:
                ans[i][j] += mat[mnr - 1][mnc - 1]

    # Print the matrix
    print(ans)

# Driver Code
if __name__ == "__main__":

    mat = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

    K = 1

    matrixBlockSum(mat, K)**
```

## ****C#****

```
**// C# program for the above approach
using System;
class GFG
{

  // Function to generate the required matrix
  static void matrixBlockSum(int[, ] mat, int K)
  {

    // Stores count of rows and columns
    int n = mat.GetLength(0);
    int m = mat.GetLength(1);

    // Traverse the matrix to
    // to compute prefix sum
    for (int i = 0; i < n; i++)
    {

      for (int j = 0; j < m; j++)
      {

        if (i - 1 >= 0)
          mat[i, j] += mat[i - 1, j];
        if (j - 1 >= 0)
          mat[i, j] += mat[i, j - 1];
        if (i - 1 >= 0 && j - 1 >= 0)
          mat[i, j] -= mat[i - 1, j - 1];
      }
    }

    int[, ] ans = new int[n, m];

    // Traverse the matrix row-wise
    // to fill the required matrix
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {

        // Fix the boundaries
        // i-k >=0 and i+k < n
        // j-k > =0 and j+k < m
        int mnr = Math.Max(0, i - K);
        int mxr = Math.Min(i + K, n - 1);
        int mnc = Math.Max(0, j - K);
        int mxc = Math.Min(j + K, m - 1);

        // Add sum of elements between
        // (0, 0) and (mxr, mxc)
        ans[i, j] = mat[mxr, mxc];

        // Remove elements between
        // (0, 0) and (mnr-1, mxc)
        if (mnr - 1 >= 0)
          ans[i, j] -= mat[mnr - 1, mxc];

        // Remove elements between
        // (0, 0) and (mxr, mnc-1)
        if (mnc - 1 >= 0)
          ans[i, j] -= mat[mxr, mnc - 1];

        // Add aux[mnr-1][mnc-1] as
        // elements between (0, 0)
        // and (mnr-1, mnc-1) are
        // subtracted twice
        if (mnr - 1 >= 0 && mnc - 1 >= 0)
          ans[i, j] += mat[mnr - 1, mnc - 1];
      }
    }

    // Print the matrix
    for (int i = 0; i < n; i++)
      for (int j = 0; j < m; j++)
        Console.Write(ans[i, j] + " ");
  }

  // Driver Code
  public static void Main()
  {

    int[, ] mat
      = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    int K = 1;
    matrixBlockSum(mat, K);
  }
}

// This code is contributed by chitranayal.**
```

## ****java 描述语言****

```
**<script>

// JavaScript program for the above approach

// Function to generate the required matrix
function matrixBlockSum(mat,K)
{
    // Stores count of rows and columns
    let n = mat.length;
    let m = mat[0].length;

    // Traverse the matrix to
    // to compute prefix sum
    for (let i = 0; i < n; i++)
    {
      for (let j = 0; j < m; j++)
      {
        if (i - 1 >= 0)
        {
          mat[i][j] += mat[i - 1][j];
        }
        if (j - 1 >= 0)
        {
          mat[i][j] += mat[i][j - 1];
        }
        if (i - 1 >= 0 && j - 1 >= 0)
        {
          mat[i][j] -= mat[i - 1][j - 1];
        }
      }
    }

    let ans = new Array(n);
    for(let i=0;i<n;i++)
    {
        ans[i]=new Array(m);
        for(let j=0;j<m;j++)
            ans[i][j]=0;
    }

    // Traverse the matrix row-wise
    // to fill the required matrix
    for (let i = 0; i < n; i++)
    {
      for (let j = 0; j < m; j++)
      {

        // Fix the boundaries
        // i-k >=0 and i+k < n
        // j-k > =0 and j+k < m
        let mnr = Math.max(0, i - K);
        let mxr = Math.min(i + K, n - 1);
        let mnc = Math.max(0, j - K);
        let mxc = Math.min(j + K, m - 1);

        // Add sum of elements between
        // (0, 0) and (mxr, mxc)
        ans[i][j] = mat[mxr][mxc];

        // Remove elements between
        // (0, 0) and (mnr-1, mxc)
        if (mnr - 1 >= 0)
        {
          ans[i][j] -= mat[mnr - 1][mxc];
        }

        // Remove elements between
        // (0, 0) and (mxr, mnc-1)
        if (mnc - 1 >= 0)
        {
          ans[i][j] -= mat[mxr][mnc - 1];
        }

        // Add aux[mnr-1][mnc-1] as
        // elements between (0, 0)
        // and (mnr-1, mnc-1) are
        // subtracted twice
        if (mnr - 1 >= 0 && mnc - 1 >= 0)
        {
          ans[i][j] += mat[mnr - 1][mnc - 1];
        }
      }
    }

    // Print the matrix
    for (let i = 0; i < n; i++)
    {      
      for (let j = 0; j < m; j++)
      {
        document.write(ans[i][j] + " ");
      }
    }
}

 // Driver code
let mat=[[ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ]];
let K = 1;
matrixBlockSum(mat, K);

// This code is contributed by patel2127

</script>**
```

******Output:** 

```
[[12, 21, 16], [27, 45, 33], [24, 39, 28]]
```**** 

*******时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*****