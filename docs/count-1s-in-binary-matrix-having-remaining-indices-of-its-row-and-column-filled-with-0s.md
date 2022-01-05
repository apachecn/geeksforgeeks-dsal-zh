# 计数二进制矩阵中的 1，其行和列的剩余索引用 0 填充

> 原文:[https://www . geeksforgeeks . org/count-1-in-binary-matrix-with-s-0 填充行和列的剩余索引/](https://www.geeksforgeeks.org/count-1s-in-binary-matrix-having-remaining-indices-of-its-row-and-column-filled-with-0s/)

给定一个二进制矩阵，大小为 **M * N** 的 **mat[][]** ，任务是从给定的二进制矩阵中计算 **1** s 的数量，该二进制矩阵的对应行和列仅在剩余的索引中由 **0** s 组成。

**示例:**

> **输入:** mat[][] = {{1，0，0}，{0，0，1}，{0，0，0}}
> **输出:** 2
> **说明:**
> 满足条件的只有(0，0)和(1，2)两个单元格。
> 因此，计数为 2。
> 
> **输入:** mat[][] = {{1，0}，{1，1 } }
> T3】输出: 0

**简单方法:**最简单的方法是[迭代矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，并通过遍历给定矩阵的相应行和列来检查给定矩阵中存在的所有 **1** 的给定条件。增加满足条件的所有 **1** 的**计数**。最后打印**把**算作所需答案。

***时间复杂度:**O(M * N<sup>2</sup>)*
***辅助空间:** O(M + N)*

**高效方法:**上述方法可以基于这样的思想进行优化，即这样的行和列的总和将仅为 **1** 。按照以下步骤解决问题:

1.  初始化两个数组，**行【】**和**列【】**，分别存储矩阵每行和每列的和。
2.  初始化一个变量，比如 **cnt** ，来存储满足给定条件的 **1** 的计数。
3.  遍历矩阵每**个 mat【I】【j】= 1**，检查**行【I】**和**列【j】**是否为 **1** 。如果发现为真，则增加 **cnt** 。
4.  完成以上步骤后，打印**计数**的最终值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count required 1s
// from the given matrix
int numSpecial(vector<vector<int> >& mat)
{

    // Stores the dimensions of the mat[][]
    int m = mat.size(), n = mat[0].size();

    int rows[m];
    int cols[n];

    int i, j;

    // Calculate sum of rows
    for (i = 0; i < m; i++) {
        rows[i] = 0;
        for (j = 0; j < n; j++)
            rows[i] += mat[i][j];
    }

    // Calculate sum of columns
    for (i = 0; i < n; i++) {

        cols[i] = 0;
        for (j = 0; j < m; j++)
            cols[i] += mat[j][i];
    }

    // Stores required count of 1s
    int cnt = 0;
    for (i = 0; i < m; i++) {
        for (j = 0; j < n; j++) {

            // If current cell is 1
            // and sum of row and column is 1
            if (mat[i][j] == 1 && rows[i] == 1
                && cols[j] == 1)

                // Increment count of 1s
                cnt++;
        }
    }

    // Return the final count
    return cnt;
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > mat
        = { { 1, 0, 0 }, { 0, 0, 1 }, { 0, 0, 0 } };

    // Function Call
    cout << numSpecial(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count required 1s
// from the given matrix
static int numSpecial(int [][]mat)
{

    // Stores the dimensions of the mat[][]
    int m = mat.length;
    int n = mat[0].length;

    int []rows = new int[m];
    int []cols = new int[n];

    int i, j;

    // Calculate sum of rows
    for(i = 0; i < m; i++)
    {
        rows[i] = 0;

        for(j = 0; j < n; j++)
            rows[i] += mat[i][j];
    }

    // Calculate sum of columns
    for(i = 0; i < n; i++)
    {
        cols[i] = 0;

        for(j = 0; j < m; j++)
            cols[i] += mat[j][i];
    }

    // Stores required count of 1s
    int cnt = 0;

    for(i = 0; i < m; i++)
    {
        for(j = 0; j < n; j++)
        {

            // If current cell is 1
            // and sum of row and column is 1
            if (mat[i][j] == 1 &&
                  rows[i] == 1 &&
                  cols[j] == 1)

                // Increment count of 1s
                cnt++;
        }
    }

    // Return the final count
    return cnt;
}

// Driver Code
public static void main(String[] args)
{

    // Given matrix
    int [][]mat = { { 1, 0, 0 },
                    { 0, 0, 1 },
                    { 0, 0, 0 } };

    // Function call
    System.out.print(numSpecial(mat) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count required 1s
# from the given matrix
def numSpecial(mat):

    # Stores the dimensions
    # of the mat
    m = len(mat)
    n = len(mat[0])

    rows = [0] * m
    cols = [0] * n

    i, j = 0, 0

    # Calculate sum of rows
    for i in range(m):
        rows[i] = 0

        for j in range(n):
            rows[i] += mat[i][j]

    # Calculate sum of columns
    for i in range(n):
        cols[i] = 0

        for j in range(m):
            cols[i] += mat[j][i]

    # Stores required count of 1s
    cnt = 0

    for i in range(m):
        for j in range(n):

            # If current cell is 1
            # and sum of row and column is 1
            if (mat[i][j] == 1 and
                  rows[i] == 1 and
                  cols[j] == 1):

                # Increment count of 1s
                cnt += 1

    # Return the final count
    return cnt

# Driver Code
if __name__ == '__main__':

    # Given matrix
    mat = [ [ 1, 0, 0 ],
            [ 0, 0, 1 ],
            [ 0, 0, 0 ] ]

    # Function call
    print(numSpecial(mat))

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count required 1s
// from the given matrix
static int numSpecial(int [,]mat)
{

    // Stores the dimensions of the [,]mat
    int m = mat.GetLength(0);
    int n = mat.GetLength(1);

    int []rows = new int[m];
    int []cols = new int[n];

    int i, j;

    // Calculate sum of rows
    for(i = 0; i < m; i++)
    {
        rows[i] = 0;

        for(j = 0; j < n; j++)
            rows[i] += mat[i, j];
    }

    // Calculate sum of columns
    for(i = 0; i < n; i++)
    {
        cols[i] = 0;

        for(j = 0; j < m; j++)
            cols[i] += mat[j, i];
    }

    // Stores required count of 1s
    int cnt = 0;

    for(i = 0; i < m; i++)
    {
        for(j = 0; j < n; j++)
        {

            // If current cell is 1 and
            // sum of row and column is 1
            if (mat[i, j] == 1 &&
                  rows[i] == 1 &&
                  cols[j] == 1)

                // Increment count of 1s
                cnt++;
        }
    }

    // Return the readonly count
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{

    // Given matrix
    int [,]mat = { { 1, 0, 0 },
                   { 0, 0, 1 },
                   { 0, 0, 0 } };

    // Function call
    Console.Write(numSpecial(mat) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to count required 1s
// from the given matrix
function numSpecial(mat)
{

    // Stores the dimensions of the mat
    var m = mat.length;
    var n = mat[0].length;

    var rows = Array.from({length: m}, (_, i) => 0);
    var cols = Array.from({length: n}, (_, i) => 0);
    var i, j;

    // Calculate sum of rows
    for(i = 0; i < m; i++)
    {
        rows[i] = 0;

        for(j = 0; j < n; j++)
            rows[i] += mat[i][j];
    }

    // Calculate sum of columns
    for(i = 0; i < n; i++)
    {
        cols[i] = 0;

        for(j = 0; j < m; j++)
            cols[i] += mat[j][i];
    }

    // Stores required count of 1s
    var cnt = 0; 
    for(i = 0; i < m; i++)
    {
        for(j = 0; j < n; j++)
        {

            // If current cell is 1
            // and sum of row and column is 1
            if (mat[i][j] == 1 &&
                  rows[i] == 1 &&
                  cols[j] == 1)

                // Increment count of 1s
                cnt++;
        }
    }

    // Return the final count
    return cnt;
}

// Driver Code

// Given matrix
    var mat = [ [ 1, 0, 0 ],
                    [ 0, 0, 1 ],
                    [ 0, 0, 0 ] ];

// Function call
document.write(numSpecial(mat) + "\n");

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(M + N)*