# 矩阵对角线元素的第 k 个最高异或

> 原文:[https://www . geeksforgeeks . org/kth-矩阵对角线元素的最高异或/](https://www.geeksforgeeks.org/kth-highest-xor-of-diagonal-elements-from-a-matrix/)

给定一个大小为 **N * N** 的正方形[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】【】**，任务是计算每一个对角元素的异或值，并求出得到的 **K <sup>th</sup>** 最大异或值。
**注:**矩阵中有**2 * N–1**条对角线。i <sup>第</sup>条对角线的起点为**(最小值(N，I)，(1 +最大值(I–N，0))。**

**示例:**

> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}}，K = 3
> **输出:** 6
> **解释:**
> 第一对角线的异或= 1。
> 第二对角线的异或= 4 ^ 2 = 6。
> 第三对角线的异或= 7 ^ 5 ^ 3 = 1。
> 第四对角线的异或= 8 ^ 6 = 14。
> 第五对角线的异或= 9。
> 
> **输入:** mat[][] = {{1，2}，{4，5}}，K = 2
> **输出:** 6
> **解释:**
> 第一对角线的异或=1。
> 第二对角线的异或= 4 ^ 2 = 6。
> 第三对角线的异或= 5。

**方法:**按照以下步骤解决问题

*   [对角遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)。
*   对于每一条**I<sup>th</sup>T3【对角线】，起点为**(最小值(N，I)，(1 +最大值(I–N，0))。****
*   将每个对角线的**异或**存储在一个向量中。
*   [排序向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)。
*   打印获得的 **K <sup>th</sup>** 最大值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find K-th maximum XOR
// of any diagonal in the matrix
void findXOR(vector<vector<int> > mat, int K)
{
    // Number or rows
    int N = mat.size();

    // Number of columns
    int M = mat[0].size();

    // Store XOR of diagonals
    vector<int> digXOR;

    // Traverse each diagonal
    for (int l = 1; l <= (N + M - 1); l++) {

        // Starting column of diagonal
        int s_col = max(0, l - N);

        // Count total elements in the diagonal
        int count = min({ l, (M - s_col), N });

        // Store XOR of current diagonal
        int currXOR = 0;

        for (int j = 0; j < count; j++) {
            currXOR
                = (currXOR
                   ^ mat[min(N, l) - j - 1][s_col + j]);
        }

        // Push XOR of current diagonal
        digXOR.push_back(currXOR);
    }

    // Sort XOR values of diagonals
    sort(digXOR.begin(), digXOR.end());

    // Print the K-th Maximum XOR
    cout << digXOR[N + M - 1 - K];
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 } };

    int K = 3;

    findXOR(mat, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find K-th maximum XOR
// of any diagonal in the matrix
static void findXOR(int[][] mat, int K)
{

    // Number or rows
    int N = mat.length;

    // Number of columns
    int M = mat[0].length;

    // Store XOR of diagonals
    ArrayList<Integer> digXOR
            = new ArrayList<Integer>();

    // Traverse each diagonal
    for (int l = 1; l <= (N + M - 1); l++) {

        // Starting column of diagonal
        int s_col = Math.max(0, l - N);

        // Count total elements in the diagonal
        int count = Math.min( l, Math.min((M - s_col), N));

        // Store XOR of current diagonal
        int currXOR = 0;

        for (int j = 0; j < count; j++) {
            currXOR
                = (currXOR
                   ^ mat[Math.min(N, l) - j - 1][s_col + j]);
        }

        // Push XOR of current diagonal
        digXOR.add(currXOR);
    }

    // Sort XOR values of diagonals
    Collections.sort(digXOR);

    // Print the K-th Maximum XOR
    System.out.print(digXOR.get(N + M - 1 - K));
}

// Driver Code
public static void main(String[] args)
{
    int[][] mat
        = { { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 } };

    int K = 3;

    findXOR(mat, K);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find K-th maximum XOR
# of any diagonal in the matrix
def findXOR(mat, K):

    # Number or rows
    N = len(mat)

    # Number of columns
    M = len(mat[0])

    # Store XOR of diagonals
    digXOR = []

    # Traverse each diagonal
    for l in range(1, N + M, 1):

        # Starting column of diagonal
        s_col = max(0, l - N)

        # Count total elements in the diagonal
        count = min([l, (M - s_col), N])

        # Store XOR of current diagonal
        currXOR = 0
        for j in range(count):
            currXOR = (currXOR ^ mat[min(N, l) - j - 1][s_col + j])

        # Push XOR of current diagonal
        digXOR.append(currXOR)

    # Sort XOR values of diagonals
    digXOR.sort(reverse=False)

    # Print the K-th Maximum XOR
    print(digXOR[N + M - 1 - K])

# Driver Code
if __name__ == '__main__':
    mat = [[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]]
    K = 3
    findXOR(mat, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find K-th maximum XOR
// of any diagonal in the matrix
static void findXOR(int[,]mat, int K)
{

    // Number or rows
    int N = mat.GetLength(0);

    // Number of columns
    int M = mat.GetLength(1);

    // Store XOR of diagonals
    List<int> digXOR = new List<int>();

    // Traverse each diagonal
    for(int l = 1; l <= (N + M - 1); l++)
    {

        // Starting column of diagonal
        int s_col = Math.Max(0, l - N);

        // Count total elements in the diagonal
        int count = Math.Min(l, Math.Min((M - s_col), N));

        // Store XOR of current diagonal
        int currXOR = 0;

        for(int j = 0; j < count; j++)
        {
            currXOR = (currXOR ^ mat[Math.Min(N, l) - j - 1,
                                              s_col + j]);
        }

        // Push XOR of current diagonal
        digXOR.Add(currXOR);
    }

    // Sort XOR values of diagonals
    digXOR.Sort();

    // Print the K-th Maximum XOR
    Console.Write(digXOR[N + M - 1 - K]);
}

// Driver Code
public static void Main(String[] args)
{
    int[,] mat = { { 1, 2, 3 },
                   { 4, 5, 6 },
                   { 7, 8, 9 } };

    int K = 3;

    findXOR(mat, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to find K-th maximum XOR
// of any diagonal in the matrix
function findXOR(mat, K)
{

    // Number or rows
    let N = mat.length;

    // Number of columns
    let M = mat[0].length;

    // Store XOR of diagonals
    let digXOR = [];

    // Traverse each diagonal
    for (let l = 1; l <= (N + M - 1); l++) {

        // Starting column of diagonal
        let s_col = Math.max(0, l - N);

        // Count total elements in the diagonal
        let count = Math.min(l, (M - s_col), N);

        // Store XOR of current diagonal
        let currXOR = 0;

        for (let j = 0; j < count; j++) {
            currXOR
                = (currXOR
                    ^ mat[Math.min(N, l) - j - 1][s_col + j]);
        }

        // Push XOR of current diagonal
        digXOR.push(currXOR);
    }

    // Sort XOR values of diagonals
    digXOR.sort((a, b) => a - b);

    // Print the K-th Maximum XOR
    document.write(digXOR[N + M - 1 - K]);
}

// Driver Code
let mat
    = [[1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]];

let K = 3;
findXOR(mat, K);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N * M)*
***空间复杂度:** O(N * M)*