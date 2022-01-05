# 二维数组中乘积最大的路径

> 原文:[https://www . geeksforgeeks . org/2 维阵列中具有最大产品的路径/](https://www.geeksforgeeks.org/path-with-maximum-product-in-2-d-array/)

给定一个大小为 **N*M** 的 2D 矩阵。任务是找到从 **(0，0)** 到 **(N-1，M-1)** 的最大产品路径。只能从 **(i，j)** 向右移动到 **(i，j+1)** ，从 **(i，j)** 向下移动到 **(i+1，j)** 。
**示例:**

> **输入:** arr[][] = { {1，2，3}，{4，5，6}，{7，8，9 } }
> T3】输出: 2016
> 乘积最大的路径是:1- > 4- > 7- > 8- > 9 = 2016

**进场:**
要选择从当前位置往哪个方向走，我们必须检查给出最大乘积的方向。我们将维护两个 2D 阵列:

1.  **maxPath[i][j]:** 将存储最大产品至 **(i，j)**
2.  **minPath[i][j]:** 它会将最小产品存储到 **(i，j)**

**步骤:**

*   将 maxPath[0][0]和 minPath[0][0]初始化为 arr[0][0]。
*   对于 maxPath[i][j]中的所有剩余单元格，检查当前单元格(I，j)和前一单元格(i-1，j)的乘积是否最大，方法是:

> 考虑行:
> **maxvalue 1 = max(arr[I][j]* maxPath[I-1][j]，arr[I][j]* minPath[I-1][j])**
> 考虑列:
> **maxvalue 2 = max(maxPath[I][j–1]* arr[I][j]，minPath[I][j–1]* arr[I][j])**
> as arr[I][j]可以为负，如果 minPath[i][j]为负。那么，
> arr[i][j]*minPath[i][j]为正，可以是最大乘积。

*   对于 minPath[i][j]中的所有剩余单元格，通过:
    检查当前单元格(I，j)和前一单元格(i-1，j)的乘积是否最小

> 考虑行:
> **minvalue 1 = min(maxPath[I–1][j]* arr[I][j]，minPath[I–1][j]* arr[I][j])**
> 考虑列:
> **minvalue 2 = min(maxPath[I][j–1]* arr[I][j]，minPath[I][j–1]* arr[I][j])**

*   更新 **minPath[i][j] = min(minValue1，minvalue 2)**&**maxPath[I][j]= max(maxvalue 1，maxValue2)**
*   返回**最大路径【n-1】【m-1】**求最大乘积。

下面是上述方法的实现:

## C++

```
// C++ Program to find maximum
// product path from (0, 0) to
// (N-1, M-1)
#include <bits/stdc++.h>
using namespace std;
#define N 3
#define M 3

// Function to find maximum product
int maxProductPath(int arr[N][M])
{

    // It will store the maximum
    // product till a given cell.
    vector<vector<int> > maxPath(N, vector<int>(M, INT_MIN));

    // It will store the minimum
    // product till a given cell
    // (for -ve elements)
    vector<vector<int> > minPath(N, vector<int>(M, INT_MAX));

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            int minVal = INT_MAX;
            int maxVal = INT_MIN;

            // If we are at topmost
            // or leftmost, just
            // copy the elements.
            if (i == 0 && j == 0) {
                maxVal = arr[i][j];
                minVal = arr[i][j];
            }

            // If we're not at the
            // above, we can consider
            // the above value.
            if (i > 0) {
                int tempMax = max(maxPath[i - 1][j] * arr[i][j],
                                  minPath[i - 1][j] * arr[i][j]);
                maxVal = max(maxVal, tempMax);

                int tempMin = min(maxPath[i - 1][j] * arr[i][j],
                                  minPath[i - 1][j] * arr[i][j]);
                minVal = min(minVal, tempMin);
            }

            // If we're not on the
            // leftmost, we can consider
            // the left value.
            if (j > 0) {
                int tempMax = max(maxPath[i][j - 1] * arr[i][j],
                                  minPath[i][j - 1] * arr[i][j]);
                maxVal = max(maxVal, tempMax);

                int tempMin = min(maxPath[i][j - 1] * arr[i][j],
                                  minPath[i][j - 1] * arr[i][j]);
                minVal = min(minVal, tempMin);
            }

            // Store max & min product
            // till i, j.
            maxPath[i][j] = maxVal;
            minPath[i][j] = minVal;
        }
    }

    // Return the max product path
    // from 0, 0 -> N-1, M-1.
    return maxPath[N - 1][M - 1];
}

// Driver Code
int main()
{
    int arr[N][M] = { { 1, -2, 3 },
                      { 4, -5, 6 },
                      { -7, -8, 9 } };

    // Print maximum product from
    // (0, 0) to (N-1, M-1)
    cout << maxProductPath(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find maximum
// product path from (0, 0) to
// (N-1, M-1)
class GFG
{

static final int N = 3;
static final int M = 3;

// Function to find maximum product
static int maxProductPath(int arr[][])
{

    // It will store the maximum
    // product till a given cell.
    int [][]maxPath = new int[N][M];

    // It will store the minimum
    // product till a given cell
    // (for -ve elements)
    int [][]minPath = new int[N][M];

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            int minVal = Integer.MAX_VALUE;
            int maxVal = Integer.MIN_VALUE;

            // If we are at topmost
            // or leftmost, just
            // copy the elements.
            if (i == 0 && j == 0)
            {
                maxVal = arr[i][j];
                minVal = arr[i][j];
            }

            // If we're not at the
            // above, we can consider
            // the above value.
            if (i > 0)
            {
                int tempMax = Math.max(maxPath[i - 1][j] * arr[i][j],
                                minPath[i - 1][j] * arr[i][j]);
                maxVal = Math.max(maxVal, tempMax);

                int tempMin = Math.min(maxPath[i - 1][j] * arr[i][j],
                                minPath[i - 1][j] * arr[i][j]);
                minVal = Math.min(minVal, tempMin);
            }

            // If we're not on the
            // leftmost, we can consider
            // the left value.
            if (j > 0) {
                int tempMax = Math.max(maxPath[i][j - 1] * arr[i][j],
                                minPath[i][j - 1] * arr[i][j]);
                maxVal = Math.max(maxVal, tempMax);

                int tempMin = Math.min(maxPath[i][j - 1] * arr[i][j],
                                minPath[i][j - 1] * arr[i][j]);
                minVal = Math.min(minVal, tempMin);
            }

            // Store max & min product
            // till i, j.
            maxPath[i][j] = maxVal;
            minPath[i][j] = minVal;
        }
    }

    // Return the max product path
    // from 0, 0.N-1, M-1.
    return maxPath[N - 1][M - 1];
}

// Driver Code
public static void main(String[] args)
{
    int arr[][] = { { 1, -2, 3 },
                    { 4, -5, 6 },
                    { -7, -8, 9 } };

    // Print maximum product from
    // (0, 0) to (N-1, M-1)
    System.out.print(maxProductPath(arr) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to find maximum
# product path from (0, 0) to
# (N-1, M-1)
import sys
N = 3;
M = 3;

# Function to find maximum product
def maxProductPath(arr):

    # It will store the maximum
    # product till a given cell.
    maxPath = [[0 for i in range(M)] for j in range(N)];

    # It will store the minimum
    # product till a given cell
    # (for -ve elements)
    minPath = [[0 for i in range(M)] for j in range(N)];

    for i in range(N):
        for j in range(M):

            minVal = sys.maxsize;
            maxVal = -sys.maxsize;

            # If we are at topmost
            # or leftmost, just
            # copy the elements.
            if (i == 0 and j == 0):
                maxVal = arr[i][j];
                minVal = arr[i][j];

            # If we're not at the
            # above, we can consider
            # the above value.
            if (i > 0):
                tempMax = max(maxPath[i - 1][j] * arr[i][j],\
                            minPath[i - 1][j] * arr[i][j]);
                maxVal = max(maxVal, tempMax);

                tempMin = min(maxPath[i - 1][j] * arr[i][j],\
                    minPath[i - 1][j] * arr[i][j]);
                minVal = min(minVal, tempMin);

            # If we're not on the
            # leftmost, we can consider
            # the left value.
            if (j > 0):
                tempMax = max(maxPath[i][j - 1] * arr[i][j],\
                    minPath[i][j - 1] * arr[i][j]);
                maxVal = max(maxVal, tempMax);

                tempMin = min(maxPath[i][j - 1] * arr[i][j],\
                    minPath[i][j - 1] * arr[i][j]);
                minVal = min(minVal, tempMin);

            # Store max & min product
            # till i, j.
            maxPath[i][j] = maxVal;
            minPath[i][j] = minVal;

    # Return the max product path
    # from 0, 0.N-1, M-1.
    return maxPath[N - 1][M - 1];

# Driver Code
if __name__ == '__main__':
    arr = [[ 1, -2, 3 ],[ 4, -5, 6 ],[ -7, -8, 9]];

    # Prmaximum product from
    # (0, 0) to (N-1, M-1)
    print(maxProductPath(arr));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# Program to find maximum
// product path from (0, 0) to
// (N-1, M-1)
using System;

class GFG
{

static readonly int N = 3;
static readonly int M = 3;

// Function to find maximum product
static int maxProductPath(int [,]arr)
{

    // It will store the maximum
    // product till a given cell.
    int [,]maxPath = new int[N, M];

    // It will store the minimum
    // product till a given cell
    // (for -ve elements)
    int [,]minPath = new int[N, M];

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            int minVal = int.MaxValue;
            int maxVal = int.MinValue;

            // If we are at topmost
            // or leftmost, just
            // copy the elements.
            if (i == 0 && j == 0)
            {
                maxVal = arr[i, j];
                minVal = arr[i, j];
            }

            // If we're not at the
            // above, we can consider
            // the above value.
            if (i > 0)
            {
                int tempMax = Math.Max(maxPath[i - 1,j] * arr[i,j],
                                minPath[i - 1,j] * arr[i,j]);
                maxVal = Math.Max(maxVal, tempMax);

                int tempMin = Math.Min(maxPath[i - 1,j] * arr[i,j],
                                minPath[i - 1,j] * arr[i,j]);
                minVal = Math.Min(minVal, tempMin);
            }

            // If we're not on the
            // leftmost, we can consider
            // the left value.
            if (j > 0) {
                int tempMax = Math.Max(maxPath[i,j - 1] * arr[i,j],
                                minPath[i,j - 1] * arr[i,j]);
                maxVal = Math.Max(maxVal, tempMax);

                int tempMin = Math.Min(maxPath[i,j - 1] * arr[i,j],
                                minPath[i,j - 1] * arr[i,j]);
                minVal = Math.Min(minVal, tempMin);
            }

            // Store max & min product
            // till i, j.
            maxPath[i, j] = maxVal;
            minPath[i, j] = minVal;
        }
    }

    // Return the max product path
    // from 0, 0.N - 1, M - 1.
    return maxPath[N - 1, M - 1];
}

// Driver Code
public static void Main(String[] args)
{
    int [,]arr = { { 1, -2, 3 },
                    { 4, -5, 6 },
                    { -7, -8, 9 } };

    // Print maximum product from
    // (0, 0) to (N - 1, M - 1)
    Console.Write(maxProductPath(arr) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
2016
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N*M)