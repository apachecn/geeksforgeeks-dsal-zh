# 查找位置元素的数量

> 原文:[https://www . geeksforgeeks . org/find-位置元素数/](https://www.geeksforgeeks.org/find-number-of-positional-elements/)

给定一个整数矩阵，任务是找出位置元素的个数。位置元素是行或列中最小或最大的元素。

示例:

> 输入:a = {{1，3，4}，{5，2，9}，{8，7，6}}
> 输出:7
> 共有 7 个元素最小元素为 1，2，6 和 4。最大元素是 9，8 和 7。
> 
> 输入:a = {{1，1}，{1，1}，{1，1}}
> 输出:6

**来源** : [高盛面试集](https://www.geeksforgeeks.org/goldman-sachs-interview-experience-for-experienced/)
思路是存储每一行每一列的最大值和最小值，然后检查所需条件。

下面是上述方法的实现。

## C++

```
// CPP program to find positional elements in
// a matrix.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

int countPositional(int a[][MAX], int m, int n)
{
    // rwomax[i] is going to store maximum of
    // i-th row and other arrays have similar
    // meaning
    int rowmax[m], rowmin[m];
    int colmax[n], colmin[n];

    // Find rminn and rmaxx for every row
    for (int i = 0; i < m; i++) {
        int rminn = INT_MAX;
        int rmaxx = INT_MIN;
        for (int j = 0; j < n; j++) {
            if (a[i][j] > rmaxx)
                rmaxx = a[i][j];
            if (a[i][j] < rminn)
                rminn = a[i][j];
        }
        rowmax[i] = rmaxx;
        rowmin[i] = rminn;
    }

    // Find cminn and cmaxx for every column
    for (int j = 0; j < n; j++) {
        int cminn = INT_MAX;
        int cmaxx = INT_MIN;
        for (int i = 0; i < m; i++) {
            if (a[i][j] > cmaxx)
                cmaxx = a[i][j];
            if (a[i][j] < cminn)
                cminn = a[i][j];
        }

        colmax[j] = cmaxx;
        colmin[j] = cminn;
    }

    // Check for optimal element
    int count = 0;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if ((a[i][j] == rowmax[i])
                || (a[i][j] == rowmin[i])
                || (a[i][j] == colmax[j])
                || (a[i][j] == colmin[j])) {
                count++;
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    int a[][MAX] = { { 1, 3, 4 },
                     { 5, 2, 9 },
                     { 8, 7, 6 } };
    int m = 3, n = 3;
    cout << countPositional(a, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find positional elements in
// a matrix.
class GfG {

    static int MAX = 100;

    static int countPositional(int a[][], int m, int n)
    {
        // rwomax[i] is going to store maximum of
        // i-th row and other arrays have similar
        // meaning
        int rowmax[] = new int[m];
        int rowmin[] = new int[m];
        int colmax[] = new int[n];
        int colmin[] = new int[n];

        // Find rminn and rmaxx for every row
        for (int i = 0; i < m; i++) {
            int rminn = Integer.MAX_VALUE;
            int rmaxx = Integer.MIN_VALUE;
            for (int j = 0; j < n; j++) {
                if (a[i][j] > rmaxx)
                    rmaxx = a[i][j];
                if (a[i][j] < rminn)
                    rminn = a[i][j];
            }
            rowmax[i] = rmaxx;
            rowmin[i] = rminn;
        }

        // Find cminn and cmaxx for every column
        for (int j = 0; j < n; j++) {
            int cminn = Integer.MAX_VALUE;
            int cmaxx = Integer.MIN_VALUE;
            for (int i = 0; i < m; i++) {
                if (a[i][j] > cmaxx)
                    cmaxx = a[i][j];
                if (a[i][j] < cminn)
                    cminn = a[i][j];
            }

            colmax[j] = cmaxx;
            colmin[j] = cminn;
        }

        // Check for optimal element
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if ((a[i][j] == rowmax[i])
                    || (a[i][j] == rowmin[i])
                    || (a[i][j] == colmax[j])
                    || (a[i][j] == colmin[j])) {
                    count++;
                }
            }
        }

        return count;
    }

    public static void main(String[] args)
    {
        int a[][] = new int[][] { { 1, 3, 4 }, { 5, 2, 9 }, { 8, 7, 6 } };
        int m = 3, n = 3;
        System.out.println(countPositional(a, m, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find positional elements in a matrix.
import sys

MAX = 100

def countPositional(a, m, n):

    # rwomax[i] is going to store maximum of
    # i-th row and other arrays have similar
    # meaning
    rowmax = [0] * m
    rowmin = [0] * m
    colmax = [0] * n
    colmin = [0] * n

    # Find rminn and rmaxx for every row
    for i in range(m) :
        rminn = sys.maxsize
        rmaxx = -sys.maxsize
        for j in range(n) :
            if (a[i][j] > rmaxx) :
                rmaxx = a[i][j]
            if (a[i][j] < rminn) :
                rminn = a[i][j]

        rowmax[i] = rmaxx
        rowmin[i] = rminn

    # Find cminn and cmaxx for every column
    for j in range(n) :
        cminn = sys.maxsize
        cmaxx = -sys.maxsize
        for i in range(m) :
            if (a[i][j] > cmaxx) :
                cmaxx = a[i][j]
            if (a[i][j] < cminn) :
                cminn = a[i][j]

        colmax[j] = cmaxx
        colmin[j] = cminn

    # Check for optimal element
    count = 0
    for i in range(m) :
        for j in range(n) :
            if ((a[i][j] == rowmax[i]) or (a[i][j] == rowmin[i])
                or (a[i][j] == colmax[j])
                or (a[i][j] == colmin[j])) :
                count += 1

    return count

# Driver code
a = [ [ 1, 3, 4 ], [ 5, 2, 9 ], [ 8, 7, 6 ] ]
m, n = 3, 3
print(countPositional(a, m, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find positional elements in
using System;

class GFG {

    static int countPositional(int[, ] a, int m, int n)
    {
        // rwomax[i] is going to store maximum of
        // i-th row and other arrays have similar
        // meaning
        int[] rowmax = new int[m];
        int[] rowmin = new int[m];
        int[] colmax = new int[n];
        int[] colmin = new int[n];

        // Find rminn and rmaxx for every row
        for (int i = 0; i < m; i++) {
            int rminn = int.MaxValue;
            int rmaxx = int.MinValue;
            for (int j = 0; j < n; j++) {
                if (a[i, j] > rmaxx)
                    rmaxx = a[i, j];
                if (a[i, j] < rminn)
                    rminn = a[i, j];
            }
            rowmax[i] = rmaxx;
            rowmin[i] = rminn;
        }

        // Find cminn and cmaxx for every column
        for (int j = 0; j < n; j++) {
            int cminn = int.MaxValue;
            int cmaxx = int.MinValue;
            for (int i = 0; i < m; i++) {
                if (a[i, j] > cmaxx)
                    cmaxx = a[i, j];
                if (a[i, j] < cminn)
                    cminn = a[i, j];
            }

            colmax[j] = cmaxx;
            colmin[j] = cminn;
        }

        // Check for optimal element
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if ((a[i, j] == rowmax[i])
                    || (a[i, j] == rowmin[i])
                    || (a[i, j] == colmax[j])
                    || (a[i, j] == colmin[j])) {
                    count++;
                }
            }
        }

        return count;
    }

    // Driver Code
    static public void Main()
    {
        int[, ] a = new int[, ] { { 1, 3, 4 }, { 5, 2, 9 }, { 8, 7, 6 } };
        int m = 3, n = 3;
        Console.WriteLine(countPositional(a, m, n));
    }
}

// This code is contributed by Tushil.
```

## java 描述语言

```
<script>

// Javascript program to find positional
// elements in a matrix.
let MAX = 100;

function countPositional(a, m, n)
{

    // rwomax[i] is going to store maximum of
    // i-th row and other arrays have similar
    // meaning
    let rowmax = new Array(m);
    let rowmin = new Array(m);
    let colmax = new Array(n);
    let colmin = new Array(n);

    // Find rminn and rmaxx for every row
    for(let i = 0; i < m; i++)
    {
        let rminn = Number.MAX_VALUE;
        let rmaxx = Number.MIN_VALUE;
        for(let j = 0; j < n; j++)
        {
            if (a[i][j] > rmaxx)
                rmaxx = a[i][j];
            if (a[i][j] < rminn)
                rminn = a[i][j];
        }
        rowmax[i] = rmaxx;
        rowmin[i] = rminn;
    }

    // Find cminn and cmaxx for every column
    for(let j = 0; j < n; j++)
    {
        let cminn = Number.MAX_VALUE;
        let cmaxx = Number.MIN_VALUE;
        for(let i = 0; i < m; i++)
        {
            if (a[i][j] > cmaxx)
                cmaxx = a[i][j];
            if (a[i][j] < cminn)
                cminn = a[i][j];
        }

        colmax[j] = cmaxx;
        colmin[j] = cminn;
    }

    // Check for optimal element
    let count = 0;
    for(let i = 0; i < m; i++)
    {
        for(let j = 0; j < n; j++)
        {
            if ((a[i][j] == rowmax[i]) ||
                (a[i][j] == rowmin[i]) ||
                (a[i][j] == colmax[j]) ||
                (a[i][j] == colmin[j]))
            {
                count++;
            }
        }
    }

    return count;
}

// Driver code
let a = [ [ 1, 3, 4 ],
          [ 5, 2, 9 ],
          [ 8, 7, 6 ] ];
let m = 3, n = 3;
document.write(countPositional(a, m, n));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
7
```