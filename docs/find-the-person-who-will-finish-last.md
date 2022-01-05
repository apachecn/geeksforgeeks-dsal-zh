# 找到最后完成的人

> 原文:[https://www . geesforgeks . org/find-最后完成的人/](https://www.geeksforgeeks.org/find-the-person-who-will-finish-last/)

给定尺寸为 **M x N** 的[**mat【】【】**二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)[和两人组**P2 P1**，任务是从矩阵中选择一个 **0** 的最后完成者，只有当由 **0** 组成的单元格的行或列在矩阵中有一个或多个 **1** 时，该矩阵才会变为 **1** 。](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)

***注:** P1 先开始挑 **0s** ，两人都想最后完成。给定的矩阵将总是至少有一个 **0** 可供选择。*

**示例:**

> **输入** : mat[][] = {{1，0，0}，{0，0，0}，{0，0，1}}
> **输出** : P1
> **解释** :
> P1 选择 mat[1][1]，则矩阵变为{{1，0，0}，{0，1，0}，{0，0，1}}。
> P2 已经没有 **0** 可以选择了。所以，P1 是最后一名。
> 
> **输入** : mat[][] = {{0，0}，{0，0}}
> **输出** : P2
> **解释** :
> 无论 P1 选择哪一个 **0** P2 总会有一个 **0** 可供选择，
> 在 P2 挑了一个 **0** 之后就不会再有其他的 **0** 可供选择了。

**方法:**这个想法是基于这样的观察:如果一个 **0** 的行或列都有 **1，那么它就不能被采用。**按照以下步骤解决此问题:

*   初始化两个[集合](https://www.geeksforgeeks.org/python-sets/)、**行** & **列**来统计不包含任何 **1** 的行数和列数。
*   遍历矩阵，在集合中添加有 **1** 的行和列。
*   取最小行数或列数，就好像它们中的任何一个变为零，这样就不能再取 **0** s。
*   找到可用的最小行数和列数后，如果选择的数量是奇数，则 **P1** 最后完成，否则 **P2** 最后完成。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the person
// who will finish last
void findLast(int mat[][3])
{

    int m = 3;
    int n = 3;

    // To keep track of rows
    // and columns having 1
    set<int> rows;
    set<int> cols;

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (mat[i][j]) {
                rows.insert(i);
                cols.insert(j);
            }
        }
    }

    // Available rows and columns
    int avRows = m - rows.size();
    int avCols = n - cols.size();

    // Minimum number of choices we have
    int choices = min(avRows, avCols);

    // If number of choices are odd
    if (choices & 1)

        // P1 will finish last
        cout << "P1";

    // Otherwise, P2 will finish last
    else
        cout << "P2";
}

// Given matrix
int main()
{
    int mat[][3]
        = { { 1, 0, 0 }, { 0, 0, 0 }, { 0, 0, 1 } };

    findLast(mat);
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the person
// who will finish last
static void findLast(int mat[][])
{
    int m = 3;
    int n = 3;

    // To keep track of rows
    // and columns having 1
    Set<Integer> rows = new HashSet<Integer>();
    Set<Integer> cols = new HashSet<Integer>();

    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {
            if ((mat[i][j] > 0))
            {
                rows.add(i);
                cols.add(j);
            }
        }
    }

    // Available rows and columns
    int avRows = m - rows.size();
    int avCols = n - cols.size();

    // Minimum number of choices we have
    int choices = Math.min(avRows, avCols);

    // If number of choices are odd
    if ((choices & 1) != 0)

        // P1 will finish last
        System.out.println("P1");

    // Otherwise, P2 will finish last
    else
        System.out.println("P2");
}

// Driver code
public static void main (String[] args)
{
    int mat[][] = { { 1, 0, 0 },
                    { 0, 0, 0 },
                    { 0, 0, 1 } };

    findLast(mat);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the person
# who will finish last
def findLast(mat):

    m = len(mat)
    n = len(mat[0])

    # To keep track of rows
    # and columns having 1
    rows = set()
    cols = set()

    for i in range(m):
        for j in range(n):
            if mat[i][j]:
                rows.add(i)
                cols.add(j)

    # Available rows and columns
    avRows = m-len(list(rows))
    avCols = n-len(list(cols))

    # Minimum number of choices we have
    choices = min(avRows, avCols)

    # If number of choices are odd
    if choices & 1:

        # P1 will finish last
        print('P1')

    # Otherwise, P2 will finish last
    else:
        print('P2')

# Given matrix
mat = [[1, 0, 0], [0, 0, 0], [0, 0, 1]]

findLast(mat)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the person
// who will finish last
static void findLast(int[,] mat)
{
    int m = 3;
    int n = 3;

    // To keep track of rows
    // and columns having 1
    HashSet<int> rows = new HashSet<int>();
    HashSet<int> cols = new HashSet<int>();

    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {
            if ((mat[i,j] > 0))
            {
                rows.Add(i);
                cols.Add(j);
            }
        }
    }

    // Available rows and columns
    int avRows = m - rows.Count;
    int avCols = n - cols.Count;

    // Minimum number of choices we have
    int choices = Math.Min(avRows, avCols);

    // If number of choices are odd
    if ((choices & 1) != 0)

        // P1 will finish last
        Console.WriteLine("P1");

    // Otherwise, P2 will finish last
    else
        Console.WriteLine("P2");
}

// Driver code
static public void Main()
{

    int[,] mat = { { 1, 0, 0 },
                   { 0, 0, 0 },
                   { 0, 0, 1 } };

    findLast(mat);
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

        // Javascript program for the above approach

        // Function to find the person
        // who will finish last
        function findLast( mat)
        {

            let m = mat.length;
            let n = mat[0].length;

            // To keep track of rows
            // and columns having 1
            let rows = new Set();
            let cols = new Set();

            for (let i = 0; i < m; i++) {
                for (let j = 0; j < n; j++) {
                    if (mat[i][j]) {
                        rows.add(i);
                        cols.add(j);
                    }
                }
            }

            // Available rows and columns
            let avRows = m - rows.size;
            let avCols = n - cols.size;

            // Minimum number of choices we have
            let choices = Math.min(avRows, avCols);

            // If number of choices are odd
            if (choices & 1)

                // P1 will finish last
                document.write("P1")

            // Otherwise, P2 will finish last
            else
                document.write("P2")
        }

        // Given matrix

        let mat
            = [ [ 1, 0, 0], [ 0, 0, 0 ], [ 0, 0, 1 ]]

        findLast(mat);

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
P1
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(M*N)*