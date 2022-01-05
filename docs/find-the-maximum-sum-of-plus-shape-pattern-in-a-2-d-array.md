# 求二维数组中加号形状模式的最大和

> 原文:[https://www . geeksforgeeks . org/find-a-2-d-数组中形状加图案的最大和/](https://www.geeksforgeeks.org/find-the-maximum-sum-of-plus-shape-pattern-in-a-2-d-array/)

给定一个 **2-D** 阵的大小 **N*M** 哪里，![3\leq N, M \leq 1000  ](img/4080e4eacccb313877243e1f6afe249e.png "Rendered by QuickLaTeX.com")。任务是找到 **+** 形状图案可达到的最大值。数组的元素可以是负数。
以坐标(x，y)为中心的任意元素，然后在所有四个方向**(如果可能的话)**展开，形成**加号(+)** 形状图案。
A **加(+)** 形状至少有五个元素为 **{ (x-1，y)，(x，y-1)，(x，y)，(x+1，y)，(x，y+1) }** 即手臂应该有**长度> 1** 但不一定要有相同的长度。
**例:**

```
Input: N = 3, M = 4
       1 1 1 1
      -6 1 1 -4
       1 1 1 1
Output: 0
Here, (x, y)=(2, 3) center of pattern(+).
Other four arms are, left arm = (2, 2), right arm = (2, 4), 
up arm = (1, 3), down arm = (2, 3).
Hence sum of all elements are ( 1 + 1 + (-4) + 1 + 1 ) = 0.

Input: N = 5, M = 3
       1 2 3
      -6 1 -4
       1 1 1
       7 8 9
       6 3 2
Output: 31
```

**方法:**这个问题是标准[最大和邻接子阵](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)的一个应用。
我们快速预先计算每一行和每一列的最大连续子序列(子阵列)和，在 4 个方向，即**上、下、左、右**。这可以使用一维数组的标准最大连续子序列和来完成。
我们为每个方向制作四个二维数组 1。

1.  **向上[I][j]**–从第 1、2、3、…、I 行向上的连续元素子序列的最大和。更正式地说，它表示从 arr[1][j]、arr[2][j]、…、arr[i][j]列表中添加连续元素子序列所获得的最大和
2.  **向下[I][j]**-从行 I、i+1、i+2、…、N 向下方向的元素的连续子序列的最大和更正式地说，它表示从 arr[i][j]、arr[i+1][j]、…、arr[N][j]的列表中添加元素的连续子序列所获得的最大和
3.  **左[I][j]**–从列 1、2、3、…、j 向左方向的元素的连续子序列的最大和更正式地说，它表示从 arr[i][1]、arr[i][2]、…、arr[i][j]的列表中添加元素的连续子序列所获得的最大和
4.  **右[I][j]**–从列 j、j+1、j+2、…、M 向右的元素的连续子序列的最大和更正式地说，它表示从 arr[i][j]、arr[i][j+1]、…、arr[i][M]的列表中添加元素的连续子序列所获得的最大和

剩下的就是，将每个单元格作为 **+** 的可能中心进行检查，并使用预先计算的数据来找到由 O(1)中的 **+** 形状实现的值。
![Ans_{i, j} = up[i-1][j] + down[i+1][j] + left[i][j-1]+right[i][j+1]+arr[i][j]_{adding\;the\;value\;at \;center\; of\; +}  ](img/45f4803fed561e9cc42bf13f8a3a71fa.png "Rendered by QuickLaTeX.com")
以下是上述方法的实施:

## C++

```
// C++ program to find the maximum value
// of a + shaped pattern in 2-D array
#include <bits/stdc++.h>
using namespace std;
#define N 100

const int n = 3, m = 4;

// Function to return maximum Plus value
int maxPlus(int (&arr)[n][m])
{

    // Initializing answer with the minimum value
    int ans = INT_MIN;

    // Initializing all four arrays
    int left[N][N], right[N][N], up[N][N], down[N][N];

    // Initializing left and up array.
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            left[i][j] = max(0LL, (j ? left[i][j - 1] : 0LL)) 
                                             + arr[i][j];
            up[i][j] = max(0LL, (i ? up[i - 1][j] : 0LL))
                                              + arr[i][j];
        }
    }

    // Initializing right and down array.
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            right[i][j] = max(0LL, (j + 1 == m ? 0LL: right[i][j + 1]))
                                                            + arr[i][j];
            down[i][j] = max(0LL, (i + 1 == n ? 0LL: down[i + 1][j]))
                                                            + arr[i][j];
        }
    }

    // calculating value of maximum Plus (+) sign
    for (int i = 1; i < n - 1; ++i)
        for (int j = 1; j < m - 1; ++j)
            ans = max(ans, up[i - 1][j] + down[i + 1][j]
                        + left[i][j - 1] + right[i][j + 1] + arr[i][j]);

    return ans;
}

// Driver code
int main()
{

    int arr[n][m] = { { 1, 1, 1, 1 },
                      { -6, 1, 1, -4 },
                      { 1, 1, 1, 1 } };

    // Function call to find maximum value
    cout << maxPlus(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum value
// of a + shaped pattern in 2-D array

class GFG
{
    public static int N = 100;

    public static int n = 3, m = 4;

    // Function to return maximum Plus value
    public static int maxPlus(int[][] arr)
    {

        // Initializing answer with the minimum value
        int ans = Integer.MIN_VALUE;

        // Initializing all four arrays
        int[][] left = new int[N][N];
        int[][] right = new int[N][N];
        int[][] up = new int[N][N];
        int[][] down = new int[N][N];

        // Initializing left and up array.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                left[i][j] = Math.max(0, ((j != 0) ? left[i][j - 1] : 0))
                                                + arr[i][j];
                up[i][j] = Math.max(0, ((i != 0)? up[i - 1][j] : 0))
                                                + arr[i][j];
            }
        }

        // Initializing right and down array.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                right[i][j] = Math.max(0, (j + 1 == m ? 0: right[i][j + 1]))
                                                                + arr[i][j];
                down[i][j] = Math.max(0, (i + 1 == n ? 0: down[i + 1][j]))
                                                                + arr[i][j];
            }
        }

        // calculating value of maximum Plus (+) sign
        for (int i = 1; i < n - 1; ++i)
            for (int j = 1; j < m - 1; ++j)
                ans = Math.max(ans, up[i - 1][j] + down[i + 1][j]
                            + left[i][j - 1] + right[i][j + 1] + arr[i][j]);

        return ans;
    }

    // Driver code
    public static void main(String[] args) {
        int[][] arr = new int[][]{ { 1, 1, 1, 1 },
                                   { -6, 1, 1, -4 },
                                   { 1, 1, 1, 1 } };
        // Function call to find maximum value
        System.out.println( maxPlus(arr) );
    }
}

// This code is contributed by PrinciRaj1992.
```

## 蟒蛇 3

```
# Python 3 program to find the maximum value
# of a + shaped pattern in 2-D array

N = 100

n = 3
m = 4

# Function to return maximum
# Plus value
def maxPlus(arr):

    # Initializing answer with
    # the minimum value
    ans = 0

    # Initializing all four arrays
    left = [[0 for x in range(N)]
               for y in range(N)]
    right = [[0 for x in range(N)]
                for y in range(N)]
    up = [[0 for x in range(N)]
             for y in range(N)]
    down = [[0 for x in range(N)]
               for y in range(N)]

    # Initializing left and up array.
    for i in range(n) :
        for j in range(m) :
            left[i][j] = (max(0, (left[i][j - 1] if j else 0)) +
                                  arr[i][j])
            up[i][j] = (max(0, (up[i - 1][j] if i else 0)) +
                                arr[i][j])

    # Initializing right and down array.
    for i in range(n) :
        for j in range(m) :
            right[i][j] = max(0, (0 if (j + 1 == m ) else
                                  right[i][j + 1])) + arr[i][j]
            down[i][j] = max(0, (0 if (i + 1 == n ) else
                                 down[i + 1][j])) + arr[i][j]

    # calculating value of maximum
    # Plus (+) sign
    for i in range(1, n - 1):
        for j in range(1, m - 1):
            ans = max(ans, up[i - 1][j] + down[i + 1][j] +
                         left[i][j - 1] + right[i][j + 1] +
                         arr[i][j])

    return ans

# Driver code
if __name__ == "__main__":
    arr = [[ 1, 1, 1, 1 ],
        [ -6, 1, 1, -4 ],
        [ 1, 1, 1, 1 ]]

    # Function call to find maximum value
    print(maxPlus(arr))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the maximum value
// of a + shaped pattern in 2-D array
using System;

class GFG
{
    public static int N = 100;

    public static int n = 3, m = 4;

    // Function to return maximum Plus value
    public static int maxPlus(int[,] arr)
    {

        // Initializing answer with the minimum value
        int ans = int.MinValue;

        // Initializing all four arrays
        int[,] left = new int[N,N];
        int[,] right = new int[N,N];
        int[,] up = new int[N,N];
        int[,] down = new int[N,N];

        // Initializing left and up array.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                left[i,j] = Math.Max(0, ((j != 0) ? left[i,j - 1] : 0))  
                                                 + arr[i,j];
                up[i,j] = Math.Max(0, ((i != 0)? up[i - 1,j] : 0))
                                                  + arr[i,j];
            }
        }

        // Initializing right and down array.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                right[i,j] = Math.Max(0, (j + 1 == m ? 0: right[i,j + 1]))
                                                                + arr[i,j];
                down[i,j] = Math.Max(0, (i + 1 == n ? 0: down[i + 1,j]))
                                                                + arr[i,j];
            }
        }

        // calculating value of maximum Plus (+) sign
        for (int i = 1; i < n - 1; ++i)
            for (int j = 1; j < m - 1; ++j)
                ans = Math.Max(ans, up[i - 1,j] + down[i + 1,j] 
                            + left[i,j - 1] + right[i,j + 1] + arr[i,j]);

        return ans;
    }

    // Driver code
    static void Main()
    {
        int[,] arr = new int[,]{ { 1, 1, 1, 1 },
                      { -6, 1, 1, -4 },
                      { 1, 1, 1, 1 } };

        // Function call to find maximum value
        Console.Write( maxPlus(arr) );
    }
}

// This code is contributed by DrRoot_
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum value
// of a + shaped pattern in 2-D array

    let N = 100;
    let n = 3, m = 4;

    //Function to return maximum Plus value 

    function maxPlus(arr)
    {
        // Initializing answer with the minimum value
        let ans = 0;

        // Initializing all four arrays
        let left = new Array(N);
        let right = new Array(N);
        let up = new Array(N);
        let down = new Array(N);
        for(let i=0;i<N;i++)
        {
            left[i]=new Array(N);
            right[i]=new Array(N);
            up[i]=new Array(N);
            down[i]=new Array(N);
            for(let j=0;j<N;j++)
            {
                left[i][j]=0;
                right[i][j]=0;
                up[i][j]=0;
                down[i][j]=0;
            }

        }

        // Initializing left and up array.
        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < m; j++)
            {
                left[i][j] = Math.max(0, ((j != 0) ?
                                left[i][j - 1] : 0))
                                          + arr[i][j];
                up[i][j] = Math.max(0, ((i != 0)?
                            up[i - 1][j] : 0))
                                + arr[i][j];
            }
        }

        // Initializing right and down array.
        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < m; j++)
            {
                right[i][j] = Math.max(0, (j + 1 == m ?
                0: right[i][j + 1])) + arr[i][j];
                down[i][j] = Math.max(0, (i + 1 == n ? 0:
                down[i + 1][j])) + arr[i][j];
            }
        }

        // calculating value of maximum Plus (+) sign
        for (let i = 1; i < n - 1; ++i)
            for (let j = 1; j < m - 1; ++j)
            {   
                ans = Math.max(ans, up[i - 1][j] +
                down[i + 1][j] + left[i][j - 1] +
                right[i][j + 1] + arr[i][j]);
              }
        return ans;
    }

    // Driver code
    let arr = [[ 1, 1, 1, 1 ],
        [ -6, 1, 1, -4 ],
        [ 1, 1, 1, 1 ]];
    document.write(maxPlus(arr));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(N <sup>2</sup> )