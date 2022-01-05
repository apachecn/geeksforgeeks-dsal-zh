# 检查矩阵是否为拉丁方

> 原文:[https://www . geesforgeks . org/check-a-matrix-is-a-Latin-square-or-not/](https://www.geeksforgeeks.org/check-whether-a-matrix-is-a-latin-square-or-not/)

给定一个大小为 **N x N** 的**正方形矩阵**，任务是检查它是否是[拉丁正方形](https://www.geeksforgeeks.org/latin-square/)。

> 如果矩阵的每个单元格包含 N 个不同值中的一个(在[1，N]范围内)，并且一行或一列中没有重复的值，则正方形矩阵是拉丁正方形。

**示例:**

```
Input: 1 2 3 4
       2 1 4 3
       3 4 1 2
       4 3 2 1
Output: YES

Input: 2 2 2 2
       2 3 2 3
       2 2 2 3
       2 2 2 2
Output: NO
```

**天真方法:**

1.  对于每个元素，我们首先通过迭代给定行和给定列的所有元素来检查给定元素是否已经存在于给定行和给定列中。
2.  如果不是，则检查该值是否小于或等于 N，如果是，则移动到下一个元素。
3.  如果上面的任何一点都是假的，那么这个矩阵就不是拉丁方。

**高效方法:**下面是使用 C++中的[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)的更高效方法:

1.  为每行和每列定义集合，并创建两个集合数组，一个用于所有行，另一个用于列。
2.  迭代所有元素，并将给定元素的值插入相应的行集和列集中。
3.  另外，检查给定值是否小于 N。如果没有，打印“否”并返回。
4.  现在，迭代所有的行集和列集，检查集合的大小是否小于 N。
5.  如果是，打印“是”。否则，打印“否”。

下面是上述方法的实现。

## C++

```
// C++ program to check if given matrix
// is natural latin square or not

#include <bits/stdc++.h>
using namespace std;

void CheckLatinSquare(int mat[4][4])
{
    // Size of square matrix is NxN
    int N = sizeof(mat[0]) / sizeof(mat[0][0]);

    // Vector of N sets corresponding
    // to each row.
    vector<set<int> > rows(N);

    // Vector of N sets corresponding
    // to each column.
    vector<set<int> > cols(N);

    // Number of invalid elements
    int invalid = 0;

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            rows[i].insert(mat[i][j]);
            cols[j].insert(mat[i][j]);

            if (mat[i][j] > N || mat[i][j] <= 0) {
                invalid++;
            }
        }
    }
    // Number of rows with
    // repetitive elements.
    int numrows = 0;

    // Number of columns with
    // repetitive elements.
    int numcols = 0;

    // Checking size of every row
    // and column
    for (int i = 0; i < N; i++) {
        if (rows[i].size() != N) {
            numrows++;
        }
        if (cols[i].size() != N) {
            numcols++;
        }
    }

    if (numcols == 0 && numrows == 0
        && invalid == 0)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    return;
}

// Driver code
int main()
{

    int Matrix[4][4] = { { 1, 2, 3, 4 },
                         { 2, 1, 4, 3 },
                         { 3, 4, 1, 2 },
                         { 4, 3, 2, 1 } };

    // Function call
    CheckLatinSquare(Matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given matrix
// is natural latin square or not
import java.util.*;

class GFG{

@SuppressWarnings("unchecked")
static void CheckLatinSquare(int mat[][])
{

    // Size of square matrix is NxN
    int N = mat.length;

    // Vector of N sets corresponding
    // to each row.
    HashSet<Integer>[] rows = new HashSet[N];

    // Vector of N sets corresponding
    // to each column.
    HashSet<Integer>[] cols = new HashSet[N];

    for(int i = 0; i < N; i++)
    {
        rows[i] = new HashSet<Integer>();
        cols[i] = new HashSet<Integer>();
    }

    // Number of invalid elements
    int invalid = 0;

    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {
            rows[i].add(mat[i][j]);
            cols[j].add(mat[i][j]);

            if (mat[i][j] > N || mat[i][j] <= 0)
            {
                invalid++;
            }
        }
    }

    // Number of rows with
    // repetitive elements.
    int numrows = 0;

    // Number of columns with
    // repetitive elements.
    int numcols = 0;

    // Checking size of every row
    // and column
    for(int i = 0; i < N; i++)
    {
        if (rows[i].size() != N)
        {
            numrows++;
        }
        if (cols[i].size() != N)
        {
            numcols++;
        }
    }

    if (numcols == 0 &&
        numrows == 0 && invalid == 0)
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");

    return;
}

// Driver code
public static void main(String[] args)
{

    int Matrix[][] = { { 1, 2, 3, 4 },
                       { 2, 1, 4, 3 },
                       { 3, 4, 1, 2 },
                       { 4, 3, 2, 1 } };

    // Function call
    CheckLatinSquare(Matrix);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if given matrix
# is natural latin square or not
def CheckLatinSquare(mat):

    # Size of square matrix is NxN
    N = len(mat)

    # Vector of N sets corresponding
    # to each row.
    rows = []
    for i in range(N):
        rows.append(set([]))

    # Vector of N sets corresponding
    # to each column.
    cols = []
    for i in range(N):
        cols.append(set([]))

    # Number of invalid elements
    invalid = 0

    for i in range(N):
        for j in range(N):
            rows[i].add(mat[i][j])
            cols[j].add(mat[i][j])

            if (mat[i][j] > N or mat[i][j] <= 0) :
                invalid += 1

    # Number of rows with
    # repetitive elements.
    numrows = 0

    # Number of columns with
    # repetitive elements.
    numcols = 0

    # Checking size of every row
    # and column
    for i in range(N):
        if (len(rows[i]) != N) :
            numrows+=1

        if (len(cols[i]) != N) :
            numcols+=1

    if (numcols == 0 or numrows == 0 and invalid == 0) :
        print("YES")
    else:
        print("NO")

    return

Matrix = [  [ 1, 2, 3, 4 ],
             [ 2, 1, 4, 3 ],
             [ 3, 4, 1, 2 ],
             [ 4, 3, 2, 1 ] ]

# Function call
CheckLatinSquare(Matrix)

# This code is contributed by decode2207.
```

## C#

```
// C# program to check if given matrix
// is natural latin square or not
using System;
using System.Collections.Generic;
class GFG{
    static void CheckLatinSquare(int[, ] mat)
    {

        // Size of square matrix is NxN
        int N = mat.GetLength(0);

        // List of N sets corresponding
        // to each row.
        HashSet<int>[] rows = new HashSet<int>[ N ];

        // List of N sets corresponding
        // to each column.
        HashSet<int>[] cols = new HashSet<int>[ N ];

        for (int i = 0; i < N; i++)
        {
            rows[i] = new HashSet<int>();
            cols[i] = new HashSet<int>();
        }

        // Number of invalid elements
        int invalid = 0;

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                rows[i].Add(mat[i, j]);
                cols[j].Add(mat[i, j]);

                if (mat[i, j] > N || mat[i, j] <= 0)
                {
                    invalid++;
                }
            }
        }

        // Number of rows with
        // repetitive elements.
        int numrows = 0;

        // Number of columns with
        // repetitive elements.
        int numcols = 0;

        // Checking size of every row
        // and column
        for (int i = 0; i < N; i++)
        {
            if (rows[i].Count != N)
            {
                numrows++;
            }
            if (cols[i].Count != N)
            {
                numcols++;
            }
        }

        if (numcols == 0 && numrows == 0 && invalid == 0)
            Console.Write("YES" + "\n");
        else
            Console.Write("NO" + "\n");
        return;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[, ] Matrix = {{1, 2, 3, 4},
                          {2, 1, 4, 3},
                          {3, 4, 1, 2},
                          {4, 3, 2, 1}};

        // Function call
        CheckLatinSquare(Matrix);
    }
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
YES
```