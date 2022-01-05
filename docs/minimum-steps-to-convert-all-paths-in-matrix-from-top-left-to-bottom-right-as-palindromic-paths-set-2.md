# 将矩阵中从左上方到右下方的所有路径转换为回文路径的最小步骤|设置 2

> 原文:[https://www . geeksforgeeks . org/将矩阵中的所有路径从上到下从左到右转换为回文路径的最小步骤集-2/](https://www.geeksforgeeks.org/minimum-steps-to-convert-all-paths-in-matrix-from-top-left-to-bottom-right-as-palindromic-paths-set-2/)

给定一个矩阵**mat【】【】**有 **N** 行和 **M** 列。任务是找到矩阵中所需的最小变化数，使得从左上角到右下角的每条路径都是回文路径。在路径中，从一个单元格到另一个单元格只允许向右和向下移动。

**示例:**

> **输入:** M = 2，N = 2，mat[M][N] = {{0，0}，{0，1}}
> **输出:** 1
> **说明:**
> 将矩阵[0][0]从 0 变为 1。从(0，0)到(1，1)的两条路径变成回文。
> 
> **输入:** M = 3，N = 7，mat[M][N] = {{1，2，3，4，5，6，7}，{2，2，3，3，4，3，2}，{1，2，3，2，5，6，4}}
> **输出:** 10

**天真方法:**天真方法请参考[这篇](https://www.geeksforgeeks.org/minimum-steps-to-convert-all-paths-in-matrix-from-top-left-to-bottom-right-as-palindromic-paths/)文章。

***时间复杂度:** O(N^3)*
***辅助空间:** O(N)*

**有效方法:**
必须进行以下观察:

*   每个值 **(i+j)** 都有唯一的对角线，其中 **i** 是行索引， **j** 是列索引。
*   该任务简化为选择两条对角线，这两条对角线分别与单元(0，0)和单元(M–1，N–1)的距离相同，并使它们的所有元素等于一个单一的数字，这在两个选定的对角线上重复了大多数次。
*   如果单元格(0，0)和(M–1，N–1)之间的元素数量是奇数，则存在与两个单元格等距的公共对角线。对角线的元素不需要修改，因为它们不影响路径的回文排列。
*   如果(0，0)和(M–1，N–1)之间的单元数是偶数，则不存在这样的公共对角线。

按照以下步骤解决问题:

1.  创建一个 2D 数组**频率 _ 对角线**，存储每个选定对角线上所有数字的频率。
2.  每个对角线可以唯一地表示为(I，j)的和。
3.  初始化一个**计数**变量，该变量存储需要替换数值的单元格总数的计数。
4.  迭代**mat【】【】**并增加当前元素在其所属对角线上的频率((i + j)值)。
5.  将变量**元素数量**初始化为 1，该变量存储当前选择的每对对角线中的元素数量。
6.  初始化 **start = 0** 和**end = M+N–2**，重复以下步骤直到 **start < end** :
    *   找出与 **(0，0)** 和 **(M-1，N-1)** 等距的两条所选对角线中出现次数最多的数字的出现频率。
    *   让上一步的频率为 **X** 。将值**(两条对角线上的元素总数–X)**相加，以计算最小变化数。
    *   将**开始的**增加 1，将**结束的**减少 1，如果当前对角线上的元素数量小于矩阵任意对角线上的最大可能元素数量，则将**元素数量**增加 1。
7.  完成上述步骤后，打印总计数的值。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of replacements
int MinReplacements(
    int M, int N, int mat[][30])
{

    // 2D array to store frequency
    // of all the numbers in
    // each diagonal

    int frequency_diagonal[100][10005];

    // Initialise all the elements
    // of 2D array with 0
    memset(frequency_diagonal, 0,
           sizeof(frequency_diagonal));

    // Initialise answer as 0
    int answer = 0;

    // Iterate over the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // Update the frequency of
            // number mat[i][j]
            // for the diagonal
            // identified by (i+j)
            frequency_diagonal[i + j]
                              [mat[i][j]]++;
        }
    }

    // Initialize start as 0
    // which indicates the
    // first diagonal
    int start = 0;

    // Initialize end as
    // M + N - 2 which indicates
    // the last diagonal
    int end = M + N - 2;

    // Number of elements in
    // the current diagonal
    int no_of_elemnts = 1;

    // Maximum possible number
    // of elements in a diagonal
    // can be minimum of (number of
    // rows and number of columns)
    int max_elements = min(M, N);

    while (start < end) {

        // The frequency of number
        // which occurs for the
        // maximum number of times
        // in the two selected
        // diagonals
        int X = INT_MIN;

        for (int i = 0; i <= 10000; i++) {
            X = max(
                X,
                frequency_diagonal[start][i]
                    + frequency_diagonal[end][i]);
        }

        answer = answer + (2 * (no_of_elemnts)) - X;

        // Increment start
        start++;
        // Decrement end
        end--;

        // Increment current number
        // of elements until it reaches
        // the maximum possible value
        if (no_of_elemnts < max_elements)
            no_of_elemnts++;
    }

    // return the final answer
    return answer;
}

// Driver Code
int main()
{
    // Number of rows
    int M = 3;

    // Number of columns
    int N = 7;

    int mat[30][30]
        = { { 1, 2, 3, 4, 5, 6, 7 },
            { 2, 2, 3, 3, 4, 3, 2 },
            { 1, 2, 3, 2, 5, 6, 4 } };

    cout << MinReplacements(M, N, mat)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG{

// Function to calculate the minimum
// number of replacements
static int MinReplacements(int M, int N,
                           int mat[][])
{

    // 2D array to store frequency
    // of all the numbers in
    // each diagonal
    int [][]frequency_diagonal = new int[100][10005];

    // Initialise answer as 0
    int answer = 0;

    // Iterate over the matrix
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Update the frequency of
            // number mat[i][j]
            // for the diagonal
            // identified by (i+j)
            frequency_diagonal[i + j][mat[i][j]]++;
        }
    }

    // Initialize start as 0
    // which indicates the
    // first diagonal
    int start = 0;

    // Initialize end as
    // M + N - 2 which indicates
    // the last diagonal
    int end = M + N - 2;

    // Number of elements in
    // the current diagonal
    int no_of_elemnts = 1;

    // Maximum possible number
    // of elements in a diagonal
    // can be minimum of (number of
    // rows and number of columns)
    int max_elements = Math.min(M, N);

    while (start < end)
    {

        // The frequency of number
        // which occurs for the
        // maximum number of times
        // in the two selected
        // diagonals
        int X = Integer.MIN_VALUE;

        for(int i = 0; i <= 10000; i++)
        {
            X = Math.max(X,
                frequency_diagonal[start][i] +
                frequency_diagonal[end][i]);
        }

        answer = answer + (2 * (no_of_elemnts)) - X;

        // Increment start
        start++;

        // Decrement end
        end--;

        // Increment current number
        // of elements until it reaches
        // the maximum possible value
        if (no_of_elemnts < max_elements)
            no_of_elemnts++;
    }

    // return the final answer
    return answer;
}

// Driver Code
public static void main(String[] args)
{

    // Number of rows
    int M = 3;

    // Number of columns
    int N = 7;

    int mat[][] = { { 1, 2, 3, 4, 5, 6, 7 },
                    { 2, 2, 3, 3, 4, 3, 2 },
                    { 1, 2, 3, 2, 5, 6, 4 } };

    System.out.print(MinReplacements(M, N, mat) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program of the above approach
import sys

# Function to calculate the minimum
# number of replacements
def MinReplacements(M, N, mat):

    # 2D array to store frequency
    # of all the numbers in
    # each diagonal
    frequency_diagonal = [[0 for x in range(10005)]
                             for y in range (100)];

    # Initialise answer as 0
    answer = 0

    # Iterate over the matrix
    for i in range(M):
        for j in range(N):

            # Update the frequency of
            # number mat[i][j]
            # for the diagonal
            # identified by (i+j)
            frequency_diagonal[i + j][mat[i][j]] += 1

    # Initialize start as 0
    # which indicates the
    # first diagonal
    start = 0

    # Initialize end as
    # M + N - 2 which indicates
    # the last diagonal
    end = M + N - 2

    # Number of elements in
    # the current diagonal
    no_of_elemnts = 1

    # Maximum possible number
    # of elements in a diagonal
    # can be minimum of (number of
    # rows and number of columns)
    max_elements = min(M, N)

    while (start < end):

        # The frequency of number
        # which occurs for the
        # maximum number of times
        # in the two selected
        # diagonals
        X = -sys.maxsize - 1

        for i in range(10001):
            X = max(X,
                    frequency_diagonal[start][i] +
                    frequency_diagonal[end][i])

        answer = answer + (2 * (no_of_elemnts)) - X

        # Increment start
        start += 1

        # Decrement end
        end -= 1

        # Increment current number
        # of elements until it reaches
        # the maximum possible value
        if (no_of_elemnts < max_elements):
            no_of_elemnts += 1

    # Return the final answer
    return answer

# Driver Code

# Number of rows
M = 3

# Number of columns
N = 7

mat = [ [ 1, 2, 3, 4, 5, 6, 7 ],
        [ 2, 2, 3, 3, 4, 3, 2 ],
        [ 1, 2, 3, 2, 5, 6, 4 ] ]

print(MinReplacements(M, N, mat))

# This code is contributed by chitranayal
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Function to calculate the minimum
// number of replacements
static int MinReplacements(int M, int N,
                           int [,]mat)
{

    // 2D array to store frequency
    // of all the numbers in
    // each diagonal
    int [,]frequency_diagonal = new int[100, 10005];

    // Initialise answer as 0
    int answer = 0;

    // Iterate over the matrix
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Update the frequency of
            // number mat[i,j]
            // for the diagonal
            // identified by (i+j)
            frequency_diagonal[i + j, mat[i, j]]++;
        }
    }

    // Initialize start as 0
    // which indicates the
    // first diagonal
    int start = 0;

    // Initialize end as
    // M + N - 2 which indicates
    // the last diagonal
    int end = M + N - 2;

    // Number of elements in
    // the current diagonal
    int no_of_elemnts = 1;

    // Maximum possible number
    // of elements in a diagonal
    // can be minimum of (number of
    // rows and number of columns)
    int max_elements = Math.Min(M, N);

    while (start < end)
    {

        // The frequency of number
        // which occurs for the
        // maximum number of times
        // in the two selected
        // diagonals
        int X = int.MinValue;

        for(int i = 0; i <= 10000; i++)
        {
            X = Math.Max(X,
                frequency_diagonal[start, i] +
                frequency_diagonal[end, i]);
        }

        answer = answer + (2 * (no_of_elemnts)) - X;

        // Increment start
        start++;

        // Decrement end
        end--;

        // Increment current number
        // of elements until it reaches
        // the maximum possible value
        if (no_of_elemnts < max_elements)
            no_of_elemnts++;
    }

    // Return the readonly answer
    return answer;
}

// Driver Code
public static void Main(String[] args)
{

    // Number of rows
    int M = 3;

    // Number of columns
    int N = 7;

    int [,]mat = { { 1, 2, 3, 4, 5, 6, 7 },
                   { 2, 2, 3, 3, 4, 3, 2 },
                   { 1, 2, 3, 2, 5, 6, 4 } };

    Console.Write(MinReplacements(M, N, mat) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to calculate the minimum
// number of replacements
function MinReplacements(M,N,mat)
{
    // 2D array to store frequency
    // of all the numbers in
    // each diagonal
    let frequency_diagonal = new Array(100);
      for(let i=0;i<100;i++)
    {
        frequency_diagonal[i]=new Array(10005);
        for(let j=0;j<10005;j++)
        {
            frequency_diagonal[i][j]=0;
        }
    }

    // Initialise answer as 0
    let answer = 0;

    // Iterate over the matrix
    for(let i = 0; i < M; i++)
    {
        for(let j = 0; j < N; j++)
        {

            // Update the frequency of
            // number mat[i][j]
            // for the diagonal
            // identified by (i+j)
            frequency_diagonal[i + j][mat[i][j]]++;
        }
    }

    // Initialize start as 0
    // which indicates the
    // first diagonal
    let start = 0;

    // Initialize end as
    // M + N - 2 which indicates
    // the last diagonal
    let end = M + N - 2;

    // Number of elements in
    // the current diagonal
    let no_of_elemnts = 1;

    // Maximum possible number
    // of elements in a diagonal
    // can be minimum of (number of
    // rows and number of columns)
    let max_elements = Math.min(M, N);

    while (start < end)
    {

        // The frequency of number
        // which occurs for the
        // maximum number of times
        // in the two selected
        // diagonals
        let X = Number.MIN_VALUE;

        for(let i = 0; i <= 10000; i++)
        {
            X = Math.max(X,
                frequency_diagonal[start][i] +
                frequency_diagonal[end][i]);
        }

        answer = answer + (2 * (no_of_elemnts)) - X;

        // Increment start
        start++;

        // Decrement end
        end--;

        // Increment current number
        // of elements until it reaches
        // the maximum possible value
        if (no_of_elemnts < max_elements)
            no_of_elemnts++;
    }

    // return the final answer
    return answer;
}

// Driver Code
// Number of rows
    let M = 3;

    // Number of columns
    let N = 7;

    let mat = [[ 1, 2, 3, 4, 5, 6, 7 ],
                    [ 2, 2, 3, 3, 4, 3, 2 ],
                    [ 1, 2, 3, 2, 5, 6, 4 ]];

    document.write(MinReplacements(M, N, mat) + "<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(M * N)*