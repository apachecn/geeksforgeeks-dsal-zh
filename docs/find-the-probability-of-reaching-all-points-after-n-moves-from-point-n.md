# 求 N 从 N 点移动后到达所有点的概率

> 原文:[https://www . geeksforgeeks . org/find-n 次移动后到达所有点的概率-n 点/](https://www.geeksforgeeks.org/find-the-probability-of-reaching-all-points-after-n-moves-from-point-n/)

给定 N，表示人在数字线上的初始位置。也给定 L，这是人向左的概率。求从 N 点开始 N 次移动后到达数字线上所有点的概率，每次移动可以是向左，也可以是向右。

**示例:**

> **输入:** n = 2，l = 0.5
> **输出:**0.2500 0.0000 0.5000 0.0000 0.2500
> 人在 2 次传球中无法到达 n-1 <sup>第</sup>位和 n+1 <sup>第</sup>位，因此概率为 0。此人只需从索引 2 向左移动 2 步就可以到达第 0 个位置，因此到达第 0 个索引的概率为 05*0.5=0.25。同样对于 2n 指数，概率为 0.25。
> 
> **输入:** n = 3，l = 0.1
> **输出:**0.0010 0.0000 0.0270 0.0000 0.2430 0.0000 0.7290
> 人可以通过三种方式到达 n-1 <sup>th</sup> ，即(llr，lrl，rll)，其中 l 表示左，r 表示右。因此 n-1 <sup>第</sup>指数的概率为 0.027。类似地，所有其他点的概率也被计算。

**方法:**构建一个数组 **arr[n+1][2n+1]** ，其中每行代表一个通道，列代表线上的点。一个人可以从指数 N 移动到左边第 0 个<sup>指数或右边第 2n 个<sup>指数的最大值。最初，一次通过后的概率将留给 arr[1][n-1]，右侧留给 arr[1][n+1]。向左的 n-1 步将被完成，因此两个可能的移动要么是向右 n 步，要么是向左 n 步。所以所有人的左右移动的循环关系是:</sup></sup>

> arr[I][j]+=(arr[I–1][j–1]*右)
> arr[I][j]+=(arr[I–1][j+1]*左)

任何指数所有可能移动的概率总和将存储在 arr[n][i]中。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the
// probability of reaching all points
// after N moves from point N
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the probabilities
void printProbabilities(int n, double left)
{
    double right = 1 - left;

    // Array where row represent the pass and the
    // column represents the points on the line
    double arr[n + 1][2 * n + 1] = {{0}};

    // Initially the person can reach left
    // or right with one move
    arr[1][n + 1] = right;
    arr[1][n - 1] = left;

    // Calculate probabilities for N-1 moves
    for (int i = 2; i <= n; i++)
    {
        // when the person moves from ith index in
        // right direction when i moves has been done
        for (int j = 1; j <= 2 * n; j++)
            arr[i][j] += (arr[i - 1][j - 1] * right);

        // when the person moves from ith index in
        // left direction when i moves has been done
        for (int j = 2 * n - 1; j >= 0; j--)
            arr[i][j] += (arr[i - 1][j + 1] * left);
    }

    // Print the arr
    for (int i = 0; i < 2*n+1; i++)
        printf("%5.4f ", arr[n][i]);
}

// Driver Code
int main()
{
    int n = 2;
    double left = 0.5;
    printProbabilities(n, left);
    return 0;
}

/* This code is contributed by SujanDutta */
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the
// probability of reaching all points
// after N moves from point N
import java.util.*;
class GFG {

    // Function to calculate the probabilities
    static void printProbabilities(int n, double left)
    {
        double right = 1 - left;

        // Array where row represent the pass and the
        // column represents the points on the line
        double[][] arr = new double[n + 1][2 * n + 1];

        // Initially the person can reach left
        // or right with one move
        arr[1][n + 1] = right;
        arr[1][n - 1] = left;

        // Calculate probabilities for N-1 moves
        for (int i = 2; i <= n; i++) {

            // when the person moves from ith index in
            // right direction when i moves has been done
            for (int j = 1; j <= 2 * n; j++) {
                arr[i][j] += (arr[i - 1][j - 1] * right);
            }

            // when the person moves from ith index in
            // left direction when i moves has been done
            for (int j = 2 * n - 1; j >= 0; j--) {
                arr[i][j] += (arr[i - 1][j + 1] * left);
            }
        }
        // Calling function to print the array with probabilities
        printArray(arr, n);
    }

    // Function that prints the array
    static void printArray(double[][] arr, int n)
    {
        for (int i = 0; i < arr[0].length; i++) {
            System.out.printf("%5.4f ", arr[n][i]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 2;
        double left = 0.5;
        printProbabilities(n, left);
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate the
# probability of reaching all points
# after N moves from point N

# Function to calculate the probabilities
def printProbabilities(n, left):

    right = 1 - left;

    # Array where row represent the pass
    # and the column represents the
    # points on the line
    arr = [[0 for j in range(2 * n + 1)]
              for i in range(n + 1)]

    # Initially the person can reach
    # left or right with one move
    arr[1][n + 1] = right;
    arr[1][n - 1] = left;

    # Calculate probabilities
    # for N-1 moves
    for i in range(2, n + 1):

        # When the person moves from ith
        # index in right direction when i
        # moves has been done
        for j in range(1, 2 * n + 1):
            arr[i][j] += (arr[i - 1][j - 1] * right);

        # When the person moves from ith
        # index in left direction when i
        # moves has been done
        for j in range(2 * n - 1, -1, -1):
            arr[i][j] += (arr[i - 1][j + 1] * left);

    # Print the arr
    for i in range(2 * n + 1):
        print("{:5.4f} ".format(arr[n][i]), end = ' ');

# Driver code   
if __name__=="__main__":

    n = 2;
    left = 0.5;

    printProbabilities(n, left);

# This code is contributed by rutvik_56
```

## C#

```
// C# program to calculate the
// probability of reaching all points
// after N moves from point N
using System;

class GFG
{

    // Function to calculate the probabilities
    static void printProbabilities(int n, double left)
    {
        double right = 1 - left;

        // Array where row represent the pass and the
        // column represents the points on the line
        double[,] arr = new double[n + 1,2 * n + 1];

        // Initially the person can reach left
        // or right with one move
        arr[1,n + 1] = right;
        arr[1,n - 1] = left;

        // Calculate probabilities for N-1 moves
        for (int i = 2; i <= n; i++)
        {

            // when the person moves from ith index in
            // right direction when i moves has been done
            for (int j = 1; j <= 2 * n; j++)
            {
                arr[i, j] += (arr[i - 1, j - 1] * right);
            }

            // when the person moves from ith index in
            // left direction when i moves has been done
            for (int j = 2 * n - 1; j >= 0; j--)
            {
                arr[i, j] += (arr[i - 1, j + 1] * left);
            }
        }
        // Calling function to print the array with probabilities
        printArray(arr, n);
    }

    // Function that prints the array
    static void printArray(double[,] arr, int n)
    {
        for (int i = 0; i < GetRow(arr,0).GetLength(0); i++)
        {
            Console.Write("{0:F4} ", arr[n,i]);
        }
    }

    public static double[] GetRow(double[,] matrix, int row)
    {
        var rowLength = matrix.GetLength(1);
        var rowVector = new double[rowLength];

        for (var i = 0; i < rowLength; i++)
            rowVector[i] = matrix[row, i];

        return rowVector;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 2;
        double left = 0.5;
        printProbabilities(n, left);
    }
}

/* This code contributed by PrinciRaj1992 */
```

**Output:** 

```
0.2500 0.0000 0.5000 0.0000 0.2500
```

**时间复杂度**:O(N<sup>2</sup>)
T5】辅助空间 : O(N <sup>2</sup> )