# Q 查询后找到零矩阵中偶数单元的个数

> 原文:[https://www . geeksforgeeks . org/find-q 查询后零矩阵中偶数单元的数量/](https://www.geeksforgeeks.org/find-number-of-even-cells-in-a-zero-matrix-after-q-queries/)

给定一个**N×N**大小的零矩阵，任务是在执行 Q 查询后找到包含偶数的单元格的数量。每个查询都采用(X，Y)的形式，因此对于给定的单元格(X，Y)，必须对第 X 行和第 Y 列中的所有单元格执行增量操作。
**注:**开头的 0 也作为偶数计算。
**例:**

```
Input: N = 2, Q = { {1, 1}, {1, 2}, {2, 1} }
Output: 2
Explanation:
In the first query, we add 1  
to all elements of row 1 and column 1.
Our matrix become
2 1
1 0

In the second query, we add 1
to all elements of row 1 and column 2.
Our matrix become
3 3
1 1

In the last query, we add 1
to all elements of row 2 and column 1.
Our matrix finally become
4 3
3 2

In the final updated matrix, there 
are 2 even numbers 4 and 3 
respectively, hence ans is 2

Input: N = 2, Q = { {1, 1} } 
Output: 1
```

**<u>天真方法:</u>** 天真方法是根据查询更新矩阵中的每个单元格。然后遍历矩阵找出偶数单元格。
**时间复杂度:** O(N <sup>2</sup> )
**<u>高效方法:</u>**

*   维护两个数组，一个用于行操作，一个用于列操作。
*   行[i]将存储 i+1 <sup>第</sup>行的操作数，列[i]将存储 i+1 <sup>第</sup>列的操作数。
*   如果将 1 添加到第 i <sup>行第</sup>行，我们将进行行[i-1]++，假设基于 0 的索引。
*   列也一样。
*   现在，我们需要观察奇+奇=偶，偶+偶=偶。
*   因此，如果行[i]和列[j]都是奇数或偶数，那么该单元将具有偶数值。
*   所以我们只需要计算两个数组中的奇数和偶数，然后相乘。

以下是上述方法的实现:

## C++

```
// C++ program find Number of Even cells
// in a Zero Matrix after Q queries

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// even cell in a 2D matrix
int findNumberOfEvenCells(int n, int q[][2], int size)
{

    // Maintain two arrays, one for rows operation
    // and one for column operation
    int row[n] = { 0 };
    int col[n] = { 0 };

    for (int i = 0; i < size; i++) {
        int x = q[i][0];
        int y = q[i][1];

        // Increment operation on row[i]
        row[x - 1]++;

        // Increment operation on col[i]
        col[y - 1]++;
    }

    int r1 = 0, r2 = 0;
    int c1 = 0, c2 = 0;

    // Count odd and even values in
    // both arrays and multiply them
    for (int i = 0; i < n; i++) {

        // Count of rows having even numbers
        if (row[i] % 2 == 0) {
            r1++;
        }
        // Count of rows having odd numbers
        if (row[i] % 2 == 1) {
            r2++;
        }
        // Count of columns having even numbers
        if (col[i] % 2 == 0) {
            c1++;
        }
        // Count of columns having odd numbers
        if (col[i] % 2 == 1) {
            c2++;
        }
    }

    int count = r1 * c1 + r2 * c2;

    return count;
}

// Driver code
int main()
{

    int n = 2;
    int q[][2] = { { 1, 1 },
                   { 1, 2 },
                   { 2, 1 } };

    int size = sizeof(q) / sizeof(q[0]);
    cout << findNumberOfEvenCells(n, q, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find Number of Even cells
// in a Zero Matrix after Q queries
class GFG
{

    // Function to find the number of
    // even cell in a 2D matrix
    static int findNumberOfEvenCells(int n, int q[][], int size)
    {

        // Maintain two arrays, one for rows operation
        // and one for column operation
        int row[] = new int[n] ;
        int col[] = new int[n] ;

        for (int i = 0; i < size; i++)
        {
            int x = q[i][0];
            int y = q[i][1];

            // Increment operation on row[i]
            row[x - 1]++;

            // Increment operation on col[i]
            col[y - 1]++;
        }

        int r1 = 0, r2 = 0;
        int c1 = 0, c2 = 0;

        // Count odd and even values in
        // both arrays and multiply them
        for (int i = 0; i < n; i++)
        {

            // Count of rows having even numbers
            if (row[i] % 2 == 0)
            {
                r1++;
            }

            // Count of rows having odd numbers
            if (row[i] % 2 == 1)
            {
                r2++;
            }

            // Count of columns having even numbers
            if (col[i] % 2 == 0)
            {
                c1++;
            }

            // Count of columns having odd numbers
            if (col[i] % 2 == 1)
            {
                c2++;
            }
        }

        int count = r1 * c1 + r2 * c2;
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {

        int n = 2;
        int q[][] = { { 1, 1 },
                    { 1, 2 },
                    { 2, 1 } };

        int size = q.length;
        System.out.println(findNumberOfEvenCells(n, q, size));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program find Number of Even cells
# in a Zero Matrix after Q queries

# Function to find the number of
# even cell in a 2D matrix
def findNumberOfEvenCells(n, q, size) :

    # Maintain two arrays, one for rows operation
    # and one for column operation
    row = [0]*n ;
    col = [0]*n

    for i in range(size) :
        x = q[i][0];
        y = q[i][1];

        # Increment operation on row[i]
        row[x - 1] += 1;

        # Increment operation on col[i]
        col[y - 1] += 1;

    r1 = 0;
    r2 = 0;
    c1 = 0;
    c2 = 0;

    # Count odd and even values in
    # both arrays and multiply them
    for i in range(n) :
        # Count of rows having even numbers
        if (row[i] % 2 == 0) :
            r1 += 1;

        # Count of rows having odd numbers
        if (row[i] % 2 == 1) :
            r2 += 1;

        # Count of columns having even numbers
        if (col[i] % 2 == 0) :
            c1 +=1;

        # Count of columns having odd numbers
        if (col[i] % 2 == 1) :
            c2 += 1;

    count = r1 * c1 + r2 * c2;

    return count;

# Driver code
if __name__ == "__main__" :

    n = 2;
    q = [ [ 1, 1 ],
            [ 1, 2 ],
            [ 2, 1 ] ];

    size = len(q);

    print(findNumberOfEvenCells(n, q, size));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program find Number of Even cells
// in a Zero Matrix after Q queries
using System;

class GFG
{

    // Function to find the number of
    // even cell in a 2D matrix
    static int findNumberOfEvenCells(int n, int [,]q, int size)
    {

        // Maintain two arrays, one for rows operation
        // and one for column operation
        int []row = new int[n] ;
        int []col = new int[n] ;

        for (int i = 0; i < size; i++)
        {
            int x = q[i, 0];
            int y = q[i, 1];

            // Increment operation on row[i]
            row[x - 1]++;

            // Increment operation on col[i]
            col[y - 1]++;
        }

        int r1 = 0, r2 = 0;
        int c1 = 0, c2 = 0;

        // Count odd and even values in
        // both arrays and multiply them
        for (int i = 0; i < n; i++)
        {

            // Count of rows having even numbers
            if (row[i] % 2 == 0)
            {
                r1++;
            }

            // Count of rows having odd numbers
            if (row[i] % 2 == 1)
            {
                r2++;
            }

            // Count of columns having even numbers
            if (col[i] % 2 == 0)
            {
                c1++;
            }

            // Count of columns having odd numbers
            if (col[i] % 2 == 1)
            {
                c2++;
            }
        }

        int count = r1 * c1 + r2 * c2;
        return count;
    }

    // Driver code
    public static void Main ()
    {

        int n = 2;
        int [,]q = { { 1, 1 },
                    { 1, 2 },
                    { 2, 1 } };

        int size = q.GetLength(0);
        Console.WriteLine(findNumberOfEvenCells(n, q, size));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript program find Number of Even cells
    // in a Zero Matrix after Q queries

    // Function to find the number of
    // even cell in a 2D matrix
    function findNumberOfEvenCells(n, q, size)
    {

        // Maintain two arrays, one for rows operation
        // and one for column operation
        let row = new Array(n);
        row.fill(0);
        let col = new Array(n);
        col.fill(0);

        for (let i = 0; i < size; i++)
        {
            let x = q[i][0];
            let y = q[i][1];

            // Increment operation on row[i]
            row[x - 1]++;

            // Increment operation on col[i]
            col[y - 1]++;
        }

        let r1 = 0, r2 = 0;
        let c1 = 0, c2 = 0;

        // Count odd and even values in
        // both arrays and multiply them
        for (let i = 0; i < n; i++)
        {

            // Count of rows having even numbers
            if (row[i] % 2 == 0)
            {
                r1++;
            }

            // Count of rows having odd numbers
            if (row[i] % 2 == 1)
            {
                r2++;
            }

            // Count of columns having even numbers
            if (col[i] % 2 == 0)
            {
                c1++;
            }

            // Count of columns having odd numbers
            if (col[i] % 2 == 1)
            {
                c2++;
            }
        }

        let count = r1 * c1 + r2 * c2;
        return count;
    }

    let n = 2;
    let q = [ [ 1, 1 ],
              [ 1, 2 ],
              [ 2, 1 ] ];

    let size = q.length;
    document.write(findNumberOfEvenCells(n, q, size));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)