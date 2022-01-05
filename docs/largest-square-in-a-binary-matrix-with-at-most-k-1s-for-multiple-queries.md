# 二进制矩阵中最多 K ^ 1 个查询的最大正方形

> 原文:[https://www . geeksforgeeks . org/最多 k-1s 个二进制矩阵中的最大平方用于多查询/](https://www.geeksforgeeks.org/largest-square-in-a-binary-matrix-with-at-most-k-1s-for-multiple-queries/)

给定一个二进制矩阵 **M** ，其中矩阵的每个元素都是 0 或 1，任务是找到中心为 **(i，j)** 且包含 atmat**K**1 的最大正方形

> **输入:** M[][] = {
> {1，0，1，0，0}
> {1，0，1，1，1}
> {1，1，1，1，1}
> {1，0，0，1，0，0}，{ 0 } }，
> i = 1，j = 2，K = 9
> **输出:** 3
> **解释:**
> 中心在(1，2)的最大长度方块
> 
> **输入:** M[][] = {
> { 1，1，1 }，
> { 1，1，1 }，
> { 1，1，1 }}，
> i = 1，j = 1，K = 9
> **输出:** 3

[Recommended: Please try your approach on {IDE} first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/largest-square-in-a-binary-matrix-with-at-most-k-1s-for-multiple-queries/1/)

**朴素方法:**
对于每个查询，考虑所有具有中心(I，j)的正方形，并将正方形的长度从 1 增加到其最大可能值，直到正方形中 1 的计数小于 k。正方形长度的最大可能值将是 2*MIN_DIST + 1，其中 MIN_DIST 是中心到矩阵边缘的最小距离。所以对于中心为(I，j)的 R*C 矩阵，

```
MIN_DIST = min( i, j, R-i-1, C-j-1 ) 
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's

#include <bits/stdc++.h>
using namespace std;
const int MAX = 100;

// Function to calculate the
// largest square with atmost K
// 1s for Q queries
void largestSquare(int matrix[][MAX],
             int R, int C, int q_i[],
            int q_j[], int K, int Q){

    // Loop to solve for each query
    for (int q = 0; q < Q; q++) {
        int i = q_i[q];
        int j = q_j[q];
        int min_dist = min(min(i, j),
          min(R - i - 1, C - j - 1));
        int ans = -1;
        for (int k = 0; k <= min_dist;
                                 k++) {
            int count = 0;
            // Traversing the each sub
            // square and counting total
            for (int row = i - k; 
              row <= i + k; row++)
                for (int col = j - k;
                  col <= j + k; col++)
                    count += matrix[row][col];

            // Breaks when exceeds
            // the maximum count
            if (count > K)
                break;

            ans = 2 * k + 1;
        }
        cout << ans << "\n";
    }
}

// Driver Code
int main()
{
    int matrix[][MAX] = { { 1, 0, 1, 0, 0 },
                        { 1, 0, 1, 1, 1 },
                        { 1, 1, 1, 1, 1 },
                        { 1, 0, 0, 1, 0 } };
    int K = 9, Q = 1;
    int q_i[] = { 1 };
    int q_j[] = { 2 };
    largestSquare(matrix, 4, 5, q_i,
                          q_j, K, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's
class GFG{

static int MAX = 100;

// Function to calculate the
// largest square with atmost K
// 1s for Q queries
static void largestSquare(int matrix[][], 
                          int R, int C, 
                          int q_i[], int q_j[], 
                          int K, int Q)
{

    // Loop to solve for each query
    for(int q = 0; q < Q; q++) 
    {
       int i = q_i[q];
       int j = q_j[q];
       int min_dist = Math.min(Math.min(i, j),
                      Math.min(R - i - 1, 
                               C - j - 1));
       int ans = -1;
       for(int k = 0; k <= min_dist; k++)
       {
          int count = 0;

          // Traversing the each sub
          // square and counting total
          for(int row = i - k; row <= i + k; row++)
             for(int col = j - k; col <= j + k; col++)
                count += matrix[row][col];

            // Breaks when exceeds
            // the maximum count
            if (count > K)
                break;

            ans = 2 * k + 1;
        }

        System.out.print(ans + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int matrix[][] = { { 1, 0, 1, 0, 0 },
                       { 1, 0, 1, 1, 1 },
                       { 1, 1, 1, 1, 1 },
                       { 1, 0, 0, 1, 0 } };
    int K = 9, Q = 1;
    int q_i[] = { 1 };
    int q_j[] = { 2 };
    largestSquare(matrix, 4, 5, q_i, q_j, K, Q);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find the 
# largest square in the matrix such 
# that it contains at most K 1's 

MAX = 100

# Function to calculate the 
# largest square with atmost K 
# 1s for Q queries 
def largestSquare(matrix, R, C, q_i, q_j, K, Q): 

    # Loop to solve for each query 
    for q in range(Q): 
        i = q_i[q] 
        j = q_j[q] 
        min_dist = min(min(i, j), 
                   min(R - i - 1, C - j - 1)) 
        ans = -1
        for k in range(min_dist + 1):

            count = 0

            # Traversing the each sub 
            # square and counting total 
            for row in range(i - k, i + k + 1): 
                for col in range(j - k, j + k + 1): 
                    count += matrix[row][col] 

            # Breaks when exceeds 
            # the maximum count 
            if count > K: 
                break

            ans = 2 * k + 1
        print(ans) 

# Driver Code 
matrix = [ [ 1, 0, 1, 0, 0 ], 
           [ 1, 0, 1, 1, 1 ], 
           [ 1, 1, 1, 1, 1 ], 
           [ 1, 0, 0, 1, 0 ] ] 
K = 9
Q = 1
q_i = [ 1 ] 
q_j = [ 2 ] 
largestSquare(matrix, 4, 5, q_i, q_j, K, Q)

# This code is contributed by divyamohan123                     

```

## C#

```
// C# implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's
using System;

class GFG{

//static int MAX = 100;

// Function to calculate the
// largest square with atmost K
// 1s for Q queries
static void largestSquare(int [,]matrix, 
                          int R, int C, 
                          int []q_i, int []q_j, 
                          int K, int Q)
{

    // Loop to solve for each query
    for(int q = 0; q < Q; q++) 
    {
       int i = q_i[q];
       int j = q_j[q];
       int min_dist = Math.Min(Math.Min(i, j), 
                               Math.Min(R - i - 1,
                                        C - j - 1));
       int ans = -1;
       for(int k = 0; k <= min_dist; k++)
       {
          int count = 0;

          // Traversing the each sub
          // square and counting total
          for(int row = i - k; row <= i + k; row++)
             for(int col = j - k; col <= j + k; col++)
                count += matrix[row, col];

          // Breaks when exceeds
          // the maximum count
          if (count > K)
              break;

          ans = 2 * k + 1;
       }
       Console.Write(ans + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int [,]matrix = { { 1, 0, 1, 0, 0 },
                      { 1, 0, 1, 1, 1 },
                      { 1, 1, 1, 1, 1 },
                      { 1, 0, 0, 1, 0 } };
    int K = 9, Q = 1;
    int []q_i = {1};
    int []q_j = {2};

    largestSquare(matrix, 4, 5, q_i, q_j, K, Q);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's

var MAX = 100;

// Function to calculate the
// largest square with atmost K
// 1s for Q queries
function largestSquare( matrix,
             R, C, q_i, q_j, K, Q){

    // Loop to solve for each query
    for (var q = 0; q < Q; q++) {
        var i = q_i[q];
        var j = q_j[q];
        var min_dist = Math.min(Math.min(i, j),
          Math.min(R - i - 1, C - j - 1));
        var ans = -1;
        for (var k = 0; k <= min_dist;
                                 k++) {
            var count = 0;
            // Traversing the each sub
            // square and counting total
            for (var row = i - k; 
              row <= i + k; row++)
                for (var col = j - k;
                  col <= j + k; col++)
                    count += matrix[row][col];

            // Breaks when exceeds
            // the maximum count
            if (count > K)
                break;

            ans = 2 * k + 1;
        }
        document.write( ans + "<br>");
    }
}

// Driver Code
var matrix = [ [ 1, 0, 1, 0, 0 ],
                    [ 1, 0, 1, 1, 1 ],
                    [ 1, 1, 1, 1, 1 ],
                    [ 1, 0, 0, 1, 0 ] ];
var K = 9, Q = 1;
var q_i = [1 ];
var q_j = [2 ];
largestSquare(matrix, 4, 5, q_i,
                      q_j, K, Q);

// This code is contributed by famously.
</script>
```

**输出:**

```
3
```

给定解的最坏情况时间复杂度是 **O(Q*N*N*MIN_DIST)** ，其中 N 是正方形的长度(最大值为 2*MIN_DIST + 1)。

**利用动态规划的高效方法:**
思路是利用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)对每个方块中的 1 进行计数，然后将长度增加 1，直到达到极限，最后检查 1 的计数是否小于 K。如果是，则更新答案。
使用以下公式计算从(x1，y1)到(x2，y2)的子矩阵中的 1 的数量:

```
Number of 1's = sumDP[x2][y2] - sumDP[x2][y1-1] -
                sumDP[x1-1][y2] + sumDP[x1-1][y1-1]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's

#include <bits/stdc++.h>
using namespace std;
const int MAX = 100;

// Function to find the 
// largest square in the matrix such
// that it contains atmost K 1's
void largestSquare(int matrix[][MAX],
            int R, int C, int q_i[],
            int q_j[], int K, int Q){

    int countDP[R][C];
    memset(countDP, 0, sizeof(countDP));

    // Precomputing the countDP 
    // prefix sum of the matrix
    countDP[0][0] = matrix[0][0];
    for (int i = 1; i < R; i++)
        countDP[i][0] = countDP[i - 1][0] + 
                             matrix[i][0];
    for (int j = 1; j < C; j++)
        countDP[0][j] = countDP[0][j - 1] +
                             matrix[0][j];
    for (int i = 1; i < R; i++)
        for (int j = 1; j < C; j++)
            countDP[i][j] = matrix[i][j] +
                       countDP[i - 1][j] +
                       countDP[i][j - 1] -
                       countDP[i - 1][j - 1];

    // Loop to solve Queries
    for (int q = 0; q < Q; q++) {
        int i = q_i[q];
        int j = q_j[q];
        // Calculating the maximum
        // possible distance of the
        // centre from edge
        int min_dist = min(min(i, j), 
          min(R - i - 1, C - j - 1));
        int ans = -1;
        for (int k = 0; k <= min_dist;
                                  k++) {
            int x1 = i - k, x2 = i + k;
            int y1 = j - k, y2 = j + k;

            // Calculating the number
            // of 1s in the submatrix
            int count = countDP[x2][y2];
            if (x1 > 0)
                count -= countDP[x1 - 1][y2];
            if (y1 > 0)
                count -= countDP[x2][y1 - 1];
            if (x1 > 0 && y1 > 0)
                count += countDP[x1 - 1][y1 - 1];

            if (count > K)
                break;
            ans = 2 * k + 1;
        }
        cout << ans << "\n";
    }
}

// Driver Code
int main()
{
    int matrix[][MAX] = { { 1, 0, 1, 0, 0 },
                        { 1, 0, 1, 1, 1 },
                        { 1, 1, 1, 1, 1 },
                        { 1, 0, 0, 1, 0 } };

    int K = 9, Q = 1;
    int q_i[] = { 1 };
    int q_j[] = { 2 };
    largestSquare(matrix, 4, 5, q_i,
                          q_j, K, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's
import java.util.*;

class GFG{

static int MAX = 100;

// Function to find the 
// largest square in the matrix such
// that it contains atmost K 1's
static void largestSquare(int matrix[][], int R,
                          int C, int q_i[], 
                          int q_j[], int K,
                          int Q)
{
    int [][]countDP = new int[R][C];

    // Precomputing the countDP 
    // prefix sum of the matrix
    countDP[0][0] = matrix[0][0];
    for(int i = 1; i < R; i++)
        countDP[i][0] = countDP[i - 1][0] + 
                             matrix[i][0];
    for(int j = 1; j < C; j++)
        countDP[0][j] = countDP[0][j - 1] +
                         matrix[0][j];
    for(int i = 1; i < R; i++)
        for(int j = 1; j < C; j++)
            countDP[i][j] = matrix[i][j] +
                           countDP[i - 1][j] +
                           countDP[i][j - 1] -
                           countDP[i - 1][j - 1];

    // Loop to solve Queries
    for(int q = 0; q < Q; q++)
    {
        int i = q_i[q];
        int j = q_j[q];

        // Calculating the maximum
        // possible distance of the
        // centre from edge
        int min_dist = Math.min(Math.min(i, j), 
                       Math.min(R - i - 1, 
                                C - j - 1));

        int ans = -1;
        for(int k = 0; k <= min_dist; k++)
        {
            int x1 = i - k, x2 = i + k;
            int y1 = j - k, y2 = j + k;

            // Calculating the number
            // of 1s in the submatrix
            int count = countDP[x2][y2];
            if (x1 > 0)
                count -= countDP[x1 - 1][y2];
            if (y1 > 0)
                count -= countDP[x2][y1 - 1];
            if (x1 > 0 && y1 > 0)
                count += countDP[x1 - 1][y1 - 1];
            if (count > K)
                break;
            ans = 2 * k + 1;
        }
        System.out.print(ans + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int matrix[][] = { { 1, 0, 1, 0, 0 },
                       { 1, 0, 1, 1, 1 },
                       { 1, 1, 1, 1, 1 },
                       { 1, 0, 0, 1, 0 } };

    int K = 9, Q = 1;
    int q_i[] = { 1 };
    int q_j[] = { 2 };

    largestSquare(matrix, 4, 5, q_i,
                        q_j, K, Q);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to find the 
# largest square in the matrix such 
# that it contains atmost K 1's 

# Function to find the largest 
# square in the matrix such 
# that it contains atmost K 1's 
def largestSquare(matrix, R, C, q_i, 
                     q_j, K, Q):

    countDP = [[0 for x in range(C)]
                  for x in range(R)] 

    # Precomputing the countDP 
    # prefix sum of the matrix 
    countDP[0][0] = matrix[0][0] 

    for i in range(1, R):
        countDP[i][0] = (countDP[i - 1][0] + 
                          matrix[i][0])

    for j in range(1, C):
        countDP[0][j] = (countDP[0][j - 1] + 
                          matrix[0][j])

    for i in range(1, R):
        for j in range(1, C):
            countDP[i][j] = (matrix[i][j] + 
                            countDP[i - 1][j] + 
                            countDP[i][j - 1] - 
                            countDP[i - 1][j - 1])

    # Loop to solve Queries 
    for q in range(0, Q):
        i = q_i[q]
        j = q_j[q]

        # Calculating the maximum 
        # possible distance of the 
        # centre from edge 
        min_dist = min(i, j, R - i - 1,
                             C - j - 1)
        ans = -1
        for k in range(0, min_dist + 1): 
            x1 = i - k
            x2 = i + k
            y1 = j - k
            y2 = j + k 

            # Calculating the number 
            # of 1s in the submatrix 
            count = countDP[x2][y2]; 

            if (x1 > 0): 
                    count -= countDP[x1 - 1][y2]
            if (y1 > 0):
                    count -= countDP[x2][y1 - 1]
            if (x1 > 0 and y1 > 0):
                    count += countDP[x1 - 1][y1 - 1]

            if (count > K):
                    break

            ans = 2 * k + 1

        print(ans)

# Driver Code 
matrix = [ [ 1, 0, 1, 0, 0 ], 
           [ 1, 0, 1, 1, 1 ], 
           [ 1, 1, 1, 1, 1 ], 
           [ 1, 0, 0, 1, 0 ] ] 
K = 9
Q = 1
q_i = [1] 
q_j = [2] 

largestSquare(matrix, 4, 5, q_i, q_j, K, Q) 

# This code is contributed by Stream_Cipher
```

## C#

```
// C# implementation to find the 
// largest square in the matrix such 
// that it contains atmost K 1's 
using System;

class GFG{ 

//static int MAX = 100; 

// Function to find the 
// largest square in the matrix such 
// that it contains atmost K 1's 
static void largestSquare(int [,]matrix, int R, 
                          int C, int []q_i, 
                          int []q_j, int K, 
                          int Q) 
{ 
    int [,]countDP = new int[R, C]; 

    // Precomputing the countDP 
    // prefix sum of the matrix 
    countDP[0, 0] = matrix[0, 0]; 
    for(int i = 1; i < R; i++) 
        countDP[i, 0] = countDP[i - 1, 0] + 
                             matrix[i, 0];

    for(int j = 1; j < C; j++) 
        countDP[0, j] = countDP[0, j - 1] + 
                         matrix[0, j]; 

    for(int i = 1; i < R; i++) 
        for(int j = 1; j < C; j++) 
            countDP[i, j] = matrix[i, j] + 
                           countDP[i - 1, j] + 
                           countDP[i, j - 1] - 
                           countDP[i - 1, j - 1]; 

    // Loop to solve Queries 
    for(int q = 0; q < Q; q++) 
    { 
        int i = q_i[q]; 
        int j = q_j[q]; 

        // Calculating the maximum 
        // possible distance of the 
        // centre from edge 
        int min_dist = Math.Min(Math.Min(i, j), 
                       Math.Min(R - i - 1, 
                                C - j - 1)); 

        int ans = -1; 
        for(int k = 0; k <= min_dist; k++) 
        { 
            int x1 = i - k, x2 = i + k; 
            int y1 = j - k, y2 = j + k; 

            // Calculating the number 
            // of 1s in the submatrix 
            int count = countDP[x2, y2]; 
            if (x1 > 0) 
                count -= countDP[x1 - 1, y2]; 
            if (y1 > 0) 
                count -= countDP[x2, y1 - 1]; 
            if (x1 > 0 && y1 > 0) 
                count += countDP[x1 - 1, y1 - 1]; 
            if (count > K) 
                break; 

            ans = 2 * k + 1; 
        } 
        Console.Write(ans + "\n"); 
    } 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int [,]matrix = { { 1, 0, 1, 0, 0 }, 
                      { 1, 0, 1, 1, 1 }, 
                      { 1, 1, 1, 1, 1 }, 
                      { 1, 0, 0, 1, 0 } }; 

    int K = 9, Q = 1; 
    int []q_i = { 1 }; 
    int []q_j = { 2 }; 

    largestSquare(matrix, 4, 5, q_i, 
                  q_j, K, Q); 
} 
}

// This code is contributed by princi singh
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// largest square in the matrix such
// that it contains atmost K 1's
let MAX = 100;

// Function to find the
// largest square in the matrix such
// that it contains atmost K 1's
function largestSquare(matrix, R, C, q_i, q_j, K, Q)
{
    let countDP = new Array(R);
    for(let i = 0; i < R; i++)
    {
        countDP[i] = new Array(C);
        for(let j = 0; j < C; j++)
            countDP[i][j] = 0;
    }

    // Precomputing the countDP
    // prefix sum of the matrix
    countDP[0][0] = matrix[0][0];
    for(let i = 1; i < R; i++)
        countDP[i][0] = countDP[i - 1][0] +
                             matrix[i][0];
    for(let j = 1; j < C; j++)
        countDP[0][j] = countDP[0][j - 1] +
                         matrix[0][j];
    for(let i = 1; i < R; i++)
        for(let j = 1; j < C; j++)
            countDP[i][j] = matrix[i][j] +
                           countDP[i - 1][j] +
                           countDP[i][j - 1] -
                           countDP[i - 1][j - 1];

    // Loop to solve Queries
    for(let q = 0; q < Q; q++)
    {
        let i = q_i[q];
        let j = q_j[q];

        // Calculating the maximum
        // possible distance of the
        // centre from edge
        let min_dist = Math.min(Math.min(i, j),
                       Math.min(R - i - 1,
                                C - j - 1));

        let ans = -1;
        for(let k = 0; k <= min_dist; k++)
        {
            let x1 = i - k, x2 = i + k;
            let y1 = j - k, y2 = j + k;

            // Calculating the number
            // of 1s in the submatrix
            let count = countDP[x2][y2];
            if (x1 > 0)
                count -= countDP[x1 - 1][y2];
            if (y1 > 0)
                count -= countDP[x2][y1 - 1];
            if (x1 > 0 && y1 > 0)
                count += countDP[x1 - 1][y1 - 1];
            if (count > K)
                break;
            ans = 2 * k + 1;
        }
        document.write(ans + "<br>");
    }
}

// Driver Code
let matrix = [ [ 1, 0, 1, 0, 0 ],
               [ 1, 0, 1, 1, 1 ],
               [ 1, 1, 1, 1, 1 ],
               [ 1, 0, 0, 1, 0 ] ];
let  K = 9, Q = 1;
let q_i = [1];
let q_j = [2];

largestSquare(matrix, 4, 5, q_i,
              q_j, K, Q);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
3
```

给定解的最坏情况时间复杂度是 **O(R*C + Q*MIN_DIST)** ，其中 R，C 是初始矩阵的维数。

**使用动态规划和二分搜索法的有效方法:**
想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来寻找最大的正方形，而不是迭代地增加边的长度，并向最多给出 K 1 的边收敛。
二分搜索法的搜索空间将是-

```
// Minimum possible answer will be
// the square with side 0
l = 0

// Maximum possible will be to include
// the whole square possible from (i, j)
r = min(min(i, j), 
        min(R - i - 1, C - i - 1))
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the 
// largest square in the matrix such
// that it contains atmost K 1's

#include <bits/stdc++.h>
using namespace std;
const int MAX = 100;

// Function to find the 
// largest square in the matrix such
// that it contains atmost K 1's
void largestSquare(int matrix[][MAX], 
            int R, int C, int q_i[],
            int q_j[], int K, int Q){

    int countDP[R][C];
    memset(countDP, 0, sizeof(countDP));

    // Precomputation of the countDP
    // prefix sum of the matrix
    countDP[0][0] = matrix[0][0];
    for (int i = 1; i < R; i++)
        countDP[i][0] = countDP[i - 1][0] +
                             matrix[i][0];
    for (int j = 1; j < C; j++)
        countDP[0][j] = countDP[0][j - 1] +
                             matrix[0][j];
    for (int i = 1; i < R; i++)
        for (int j = 1; j < C; j++)
            countDP[i][j] = matrix[i][j] +
                       countDP[i - 1][j] +
                       countDP[i][j - 1] -
                   countDP[i - 1][j - 1];

    // Loop to solve each query
    for (int q = 0; q < Q; q++) {
        int i = q_i[q];
        int j = q_j[q];
        int min_dist = min(min(i, j),
          min(R - i - 1, C - j - 1));
        int ans = -1, l = 0, u = min_dist;

        // Binary Search to the side which
        // have atmost in K 1's in square
        while (l <= u) {
            int mid = (l + u) / 2;
            int x1 = i - mid, x2 = i + mid;
            int y1 = j - mid, y2 = j + mid;
            // Count total number of 1s in
            // the sub square considered
            int count = countDP[x2][y2];
            if (x1 > 0)
                count -= countDP[x1 - 1][y2];
            if (y1 > 0)
                count -= countDP[x2][y1 - 1];
            if (x1 > 0 && y1 > 0)
                count += countDP[x1 - 1][y1 - 1];

            // If the count is less than or
            // equals to the maximum move
            // to right half
            if (count <= K) {
                ans = 2 * mid + 1;
                l = mid + 1;
            }
            else
                u = mid - 1;
        }
        cout << ans << "\n";
    }
}

int main()
{
    int matrix[][MAX] = { { 1, 0, 1, 0, 0 },
                        { 1, 0, 1, 1, 1 },
                        { 1, 1, 1, 1, 1 },
                        { 1, 0, 0, 1, 0 } };

    int K = 9, Q = 1;
    int q_i[] = { 1 };
    int q_j[] = { 2 };
    largestSquare(matrix, 4, 5,
                q_i, q_j, K, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the 
// largest square in the matrix such 
// that it contains atmost K 1's 
import java.util.*; 

class GFG{

// Function to find the 
// largest square in the matrix such 
// that it contains atmost K 1's 
static void largestSquare(int matrix[][], int R,
                          int C, int q_i[], 
                          int q_j[], int K, int Q)
{ 
    int countDP[][] = new int[R][C]; 
    for(int i = 0; i < R; i++)
        for(int j = 0; j < C; j++)
            countDP[i][j] = 0; 

    // Precomputation of the countDP 
    // prefix sum of the matrix 
    countDP[0][0] = matrix[0][0]; 

    for(int i = 1; i < R; i++) 
        countDP[i][0] = countDP[i - 1][0] + 
                             matrix[i][0]; 

    for(int j = 1; j < C; j++) 
        countDP[0][j] = countDP[0][j - 1] + 
                         matrix[0][j]; 

    for(int i = 1; i < R; i++) 
        for(int j = 1; j < C; j++) 
            countDP[i][j] = matrix[i][j] + 
                           countDP[i - 1][j] + 
                           countDP[i][j - 1] - 
                           countDP[i - 1][j - 1]; 

    // Loop to solve each query 
    for(int q = 0; q < Q; q++)
    { 
        int i = q_i[q]; 
        int j = q_j[q]; 

        int min_dist = Math.min(Math.min(i, j), 
                                Math.min(R - i - 1,
                                         C - j - 1)); 

        int ans = -1, l = 0, u = min_dist; 

        // Binary Search to the side which 
        // have atmost in K 1's in square 
        while (l <= u)
        { 
            int mid = (l + u) / 2; 
            int x1 = i - mid, x2 = i + mid; 
            int y1 = j - mid, y2 = j + mid; 

            // Count total number of 1s in 
            // the sub square considered 
            int count = countDP[x2][y2]; 

            if (x1 > 0) 
                count -= countDP[x1 - 1][y2]; 
            if (y1 > 0) 
                count -= countDP[x2][y1 - 1]; 
            if (x1 > 0 && y1 > 0) 
                count += countDP[x1 - 1][y1 - 1]; 

            // If the count is less than or 
            // equals to the maximum move 
            // to right half 
            if (count <= K) 
            { 
                ans = 2 * mid + 1; 
                l = mid + 1; 
            } 
            else
                u = mid - 1; 
        } 
        System.out.println(ans); 
    } 
} 

// Driver code
public static void main(String args[]) 
{ 
    int matrix[][] = { { 1, 0, 1, 0, 0 }, 
                       { 1, 0, 1, 1, 1 }, 
                       { 1, 1, 1, 1, 1 }, 
                       { 1, 0, 0, 1, 0 } }; 

    int K = 9, Q = 1; 
    int q_i[] = {1}; 
    int q_j[] = {2}; 

    largestSquare(matrix, 4, 5, q_i, q_j, K, Q); 
} 
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 implementation to find the 
# largest square in the matrix such 
# that it contains atmost K 1's 

# Function to find the 
# largest square in the matrix such 
# that it contains atmost K 1's 
def largestSquare(matrix, R, C, q_i, 
                     q_j, K, Q):

    countDP = [[0 for x in range(C)]
                  for x in range(R)] 

    # Precomputing the countDP 
    # prefix sum of the matrix 
    countDP[0][0] = matrix[0][0] 

    for i in range(1, R):
        countDP[i][0] = (countDP[i - 1][0] +
                              matrix[i][0])
    for j in range(1, C):
        countDP[0][j] = (countDP[0][j - 1] +
                          matrix[0][j])
    for i in range(1, R):
        for j in range(1, C):
            countDP[i][j] = (matrix[i][j] + 
                            countDP[i - 1][j] + 
                            countDP[i][j - 1] - 
                            countDP[i - 1][j - 1])

    # Loop to solve Queries 
    for q in range(0,Q):
        i = q_i[q]
        j = q_j[q]

        # Calculating the maximum 
        # possible distance of the 
        # centre from edge 
        min_dist = min(i, j, R - i - 1, 
                             C - j - 1)
        ans = -1
        l = 0
        u = min_dist

        while (l <= u):
            mid = int((l + u) / 2) 
            x1 = i - mid
            x2 = i + mid 
            y1 = j - mid
            y2 = j + mid 

        # Count total number of 1s in 
        # the sub square considered 
            count = countDP[x2][y2]

            if (x1 > 0):
                    count -= countDP[x1 - 1][y2] 
            if (y1 > 0):
                    count -= countDP[x2][y1 - 1]
            if (x1 > 0 and y1 > 0): 
                    count += countDP[x1 - 1][y1 - 1]

        # If the count is less than or 
        # equals to the maximum move 
        # to right half 
            if (count <= K): 
                    ans = 2 * mid + 1
                    l = mid + 1
            else:
                u = mid - 1

        print(ans)

# Driver Code 
matrix = [ [ 1, 0, 1, 0, 0 ], 
           [ 1, 0, 1, 1, 1 ], 
           [ 1, 1, 1, 1, 1 ], 
           [ 1, 0, 0, 1, 0 ] ] 
K = 9
Q = 1
q_i = [1] 
q_j = [2] 

largestSquare(matrix, 4, 5, q_i, q_j, K, Q) 

# This code is contributed by Stream_Cipher
```

## C#

```
// C# implementation to find the 
// largest square in the matrix such 
// that it contains atmost K 1's 
using System.Collections.Generic; 
using System;

class GFG{

// Function to find the largest 
// square in the matrix such 
// that it contains atmost K 1's 
static void largestSquare(int [,]matrix, int R,
                          int C, int []q_i, 
                          int []q_j, int K, int Q)
{ 
    int [,]countDP = new int[R, C]; 
    for(int i = 0; i < R; i++)
        for(int j = 0; j < C; j++)
            countDP[i, j]=0; 

    // Precomputation of the countDP 
    // prefix sum of the matrix 
    countDP[0, 0] = matrix[0, 0]; 
    for(int i = 1; i < R; i++) 
        countDP[i, 0] = countDP[i - 1, 0] + 
                         matrix[i, 0]; 

    for(int j = 1; j < C; j++) 
        countDP[0, j] = countDP[0, j - 1] + 
                         matrix[0, j]; 

    for(int i = 1; i < R; i++) 
        for(int j = 1; j < C; j++) 
            countDP[i, j] = matrix[i, j] + 
                           countDP[i - 1, j] + 
                           countDP[i, j - 1] - 
                           countDP[i - 1, j - 1]; 

    // Loop to solve each query 
    for(int q = 0; q < Q; q++)
    { 
        int i = q_i[q]; 
        int j = q_j[q]; 

        int min_dist = Math.Min(Math.Min(i, j), 
                                Math.Min(R - i - 1,
                                         C - j - 1));

        int ans = -1, l = 0, u = min_dist; 

        // Binary Search to the side which 
        // have atmost in K 1's in square 
        while (l <= u) 
        { 
            int mid = (l + u) / 2; 
            int x1 = i - mid, x2 = i + mid; 
            int y1 = j - mid, y2 = j + mid; 

            // Count total number of 1s in 
            // the sub square considered 
            int count = countDP[x2, y2];

            if (x1 > 0) 
                count -= countDP[x1 - 1, y2]; 
            if (y1 > 0) 
                count -= countDP[x2, y1 - 1]; 
            if (x1 > 0 && y1 > 0) 
                count += countDP[x1 - 1, y1 - 1]; 

            // If the count is less than or 
            // equals to the maximum move 
            // to right half 
            if (count <= K) 
            { 
                ans = 2 * mid + 1; 
                l = mid + 1; 
            } 
            else
                u = mid - 1; 
        } 
        Console.WriteLine(ans); 
    } 
} 

// Driver code
public static void Main() 
{ 
    int [,]matrix = { { 1, 0, 1, 0, 0 }, 
                      { 1, 0, 1, 1, 1 }, 
                      { 1, 1, 1, 1, 1 }, 
                      { 1, 0, 0, 1, 0 } }; 

    int K = 9, Q = 1; 
    int []q_i = { 1 }; 
    int []q_j = { 2 }; 

    largestSquare(matrix, 4, 5, 
                     q_i, q_j, K, Q); 
} 
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// largest square in the matrix such
// that it contains atmost K 1's

// Function to find the
// largest square in the matrix such
// that it contains atmost K 1's
function largestSquare(matrix,R,C,q_i,q_j,K,Q)
{
    let countDP = new Array(R);
    for(let i = 0; i < R; i++)
    {
        countDP[i]=new Array(C);
        for(let j = 0; j < C; j++)
            countDP[i][j] = 0;
     }
    // Precomputation of the countDP
    // prefix sum of the matrix
    countDP[0][0] = matrix[0][0];

    for(let i = 1; i < R; i++)
        countDP[i][0] = countDP[i - 1][0] +
                             matrix[i][0];

    for(let j = 1; j < C; j++)
        countDP[0][j] = countDP[0][j - 1] +
                         matrix[0][j];

    for(let i = 1; i < R; i++)
        for(let j = 1; j < C; j++)
            countDP[i][j] = matrix[i][j] +
                           countDP[i - 1][j] +
                           countDP[i][j - 1] -
                           countDP[i - 1][j - 1];

    // Loop to solve each query
    for(let q = 0; q < Q; q++)
    {
        let i = q_i[q];
        let j = q_j[q];

        let min_dist = Math.min(Math.min(i, j),
                                Math.min(R - i - 1,
                                         C - j - 1));

        let ans = -1, l = 0, u = min_dist;

        // Binary Search to the side which
        // have atmost in K 1's in square
        while (l <= u)
        {
            let mid = Math.floor((l + u) / 2);
            let x1 = i - mid, x2 = i + mid;
            let y1 = j - mid, y2 = j + mid;

            // Count total number of 1s in
            // the sub square considered
            let count = countDP[x2][y2];

            if (x1 > 0)
                count -= countDP[x1 - 1][y2];
            if (y1 > 0)
                count -= countDP[x2][y1 - 1];
            if (x1 > 0 && y1 > 0)
                count += countDP[x1 - 1][y1 - 1];

            // If the count is less than or
            // equals to the maximum move
            // to right half
            if (count <= K)
            {
                ans = 2 * mid + 1;
                l = mid + 1;
            }
            else
                u = mid - 1;
        }
        document.write(ans+"<br>");
    }
}

// Driver code
let matrix=[[ 1, 0, 1, 0, 0 ],
                       [ 1, 0, 1, 1, 1 ],
                       [ 1, 1, 1, 1, 1 ],
                       [ 1, 0, 0, 1, 0 ]];

let K = 9, Q = 1;
let q_i = [1];
let q_j = [2];

largestSquare(matrix, 4, 5, q_i, q_j, K, Q);

// This code is contributed by patel2127
</script>
```

**输出:**

```
3
```

**时间复杂度:** O( R*C + Q*log(MIN_DIST))