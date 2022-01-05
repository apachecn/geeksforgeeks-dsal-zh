# 按行排序的二进制矩阵中最左边至少有一个 1 的列|集合 2

> 原文:[https://www . geesforgeks . org/最左边一列至少有一行 1 的排序二进制矩阵集-2/](https://www.geeksforgeeks.org/leftmost-column-with-atleast-one-1-in-a-row-wise-sorted-binary-matrix-set-2/)

给定一个包含 0 和 1 的二进制矩阵 **mat[][]** ，矩阵的每一行按非递减顺序排序，任务是找到矩阵最左边的列，其中至少有一个 1。
**注:**如无此列返回-1。
**例:**

```
Input: 
mat[][] = {{0, 0, 0, 1}
           {0, 1, 1, 1}
           {0, 0, 1, 1}}
Output: 2
Explanation:
The 2nd column of the
matrix contains atleast a 1.

Input: 
mat[][] = {{0, 0, 0}
           {0, 1, 1}  
           {1, 1, 1}}
Output: 1
Explanation:
The 1st column of the
matrix contains atleast a 1.

Input: 
mat[][] = {{0, 0}
           {0, 0}}
Output: -1
Explanation:
There is no such column which 
contains atleast one 1.
```

**进场:**

*   这里我们从第一行的最后一个元素开始遍历。这包括两个步骤。
    1.  如果当前迭代元素是 1，我们就减少列索引。因为我们找到了值为 1 的最左边的列索引，所以我们不必检查具有更大列索引的元素。
    2.  如果当前迭代元素是 0，我们增加行索引。由于该元素为 0，我们不需要检查该行的先前元素。
*   我们继续，直到其中一个行或列索引变得无效。

下面是上述方法的实现。

## C++

```
// C++ program to calculate leftmost
// column having at least a 1
#include <bits/stdc++.h>
using namespace std;

#define N 3
#define M 4

// Function return leftmost
// column having at least a 1
int FindColumn(int mat[N][M])
{
    int row = 0, col = M - 1;
    int flag = 0;

    while (row < N && col >= 0)
    {
        // If current element is
        // 1 decrement column by 1
        if (mat[row][col] == 1)
        {
            col--;
            flag = 1;
        }
        // If current element is
        // 0 increment row by 1
        else
        {
            row++;
        }
    }

    col++;

    if (flag)
        return col + 1;
    else
        return -1;
}

// Driver code
int main()
{
    int mat[N][M] = { { 0, 0, 0, 1 },
                      { 0, 1, 1, 1 },
                      { 0, 0, 1, 1 } };

    cout << FindColumn(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate leftmost
// column having at least a 1
import java.util.*;

class GFG{

static final int N = 3;
static final int M = 4;

// Function return leftmost
// column having at least a 1
static int FindColumn(int mat[][])
{
    int row = 0, col = M - 1;
    int flag = 0;

    while(row < N && col >= 0)
    {
        // If current element is
        // 1 decrement column by 1
        if(mat[row][col] == 1)
        {
           col--;
           flag = 1;
        }
        // If current element is
        // 0 increment row by 1
        else
        {
            row++;
        }
    }
    col++;

    if (flag!=0)
        return col + 1;
    else
        return -1;
}

// Driver code
public static void main(String[] args)
{
    int[][] mat = { { 0, 0, 0, 1 },
                    { 0, 1, 1, 1 },
                    { 0, 0, 1, 1 } };

    System.out.print(FindColumn(mat));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to calculate leftmost
# column having at least a 1
N = 3
M = 4

# Function return leftmost
# column having at least a 1
def findColumn(mat: list) -> int:
    row = 0
    col = M - 1

    while row < N and col >= 0:

        # If current element is
        # 1 decrement column by 1
        if mat[row][col] == 1:
            col -= 1
            flag = 1

        # If current element is
        # 0 increment row by 1
        else:
            row += 1

    col += 1

    if flag:
        return col + 1
    else:
        return -1

# Driver Code
if __name__ == "__main__":

    mat = [ [0, 0, 0, 1],
            [0, 1, 1, 1],
            [0, 0, 1, 1] ]

    print(findColumn(mat))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to calculate leftmost
// column having at least 1
using System;

class GFG{

static readonly int N = 3;
static readonly int M = 4;

// Function return leftmost
// column having at least a 1
static int FindColumn(int [,]mat)
{
    int row = 0, col = M - 1;
    int flag = 0;

    while(row < N && col >= 0)
    {

        // If current element is
        // 1 decrement column by 1
        if (mat[row, col] == 1)
        {
            col--;
            flag = 1;
        }

        // If current element is
        // 0 increment row by 1
        else
        {
            row++;
        }
    }
    col++;

    if (flag != 0)
        return col + 1;
    else
        return -1;
}

// Driver code
public static void Main(String[] args)
{
    int[,] mat = { { 0, 0, 0, 1 },
                   { 0, 1, 1, 1 },
                   { 0, 0, 1, 1 } };

    Console.Write(FindColumn(mat));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript program to calculate leftmost
    // column having at least 1

    let N = 3;
    let M = 4;

    // Function return leftmost
    // column having at least a 1
    function FindColumn(mat)
    {
        let row = 0, col = M - 1;
        let flag = 0;

        while(row < N && col >= 0)
        {

            // If current element is
            // 1 decrement column by 1
            if (mat[row][col] == 1)
            {
                col--;
                flag = 1;
            }

            // If current element is
            // 0 increment row by 1
            else
            {
                row++;
            }
        }
        col++;

        if (flag != 0)
            return col + 1;
        else
            return -1;
    }

    let mat = [ [ 0, 0, 0, 1 ],
                 [ 0, 1, 1, 1 ],
                 [ 0, 0, 1, 1 ] ];

    document.write(FindColumn(mat));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N + M)。其中 N 是行数，M 是列数。
**空间复杂度:** O(1)