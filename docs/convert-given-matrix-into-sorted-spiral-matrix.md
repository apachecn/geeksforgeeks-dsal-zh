# 将给定矩阵转换为有序螺旋矩阵

> 原文:[https://www . geeksforgeeks . org/convert-given-matrix-in-sorted-spiral-matrix/](https://www.geeksforgeeks.org/convert-given-matrix-into-sorted-spiral-matrix/)

给定一个矩阵，任务是将给定的矩阵转换成排序的[螺旋矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)。
**例:**

```
Input: y[][] = {
          { 2, 5, 12 },
          { 22, 54, 55 },
          { 1, 6, 8 }
        };
Output:
       1 2 5 
       45 55 6
       22 12 8

Input: y[][] = {
          { 2, 5, 12 },
          { 22, 45, 55 },
          { 1, 6, 8 },
          { 13, 56, 10 }
        };
Output:
       1 2 5 
       45 55 6 
       22 56 8 
       13 12 10
```

**进场:**

*   将给定的 2D 数组转换为 1D 数组。
*   对 1D 数组进行排序
*   将 1D 转换为螺旋矩阵
*   对于存储所有元素的循环，这个问题可以用 4 来解决。每个 for 循环定义了一个与矩阵一起的单向移动。第一个 for 循环表示从左到右的移动，而第二个爬网表示从上到下的移动，第三个表示从右到左的移动，第四个表示从下到上的移动。

以下是上述方法的实现:

## C++

```
// C++ program to Convert given Matrix
// into sorted Spiral Matrix
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

// Function to convert the array to Spiral
void ToSpiral(int m, int n,
            int Sorted[], int a[MAX][MAX])
{
    // For Array pointer
    int index = 0;

    // k - starting row index
    // m - ending row index
    // l - starting column index
    // n - ending column index
    int k = 0, l = 0;

    while (k < m && l < n)
    {

        // Print the first row
        // from the remaining rows
        for (int i = l; i < n; ++i)
        {
            a[k][i] = Sorted[index];
            index++;
        }

        k++;

        // Print the last column
        // from the remaining columns
        for (int i = k; i < m; ++i)
        {
            a[i][n - 1] = Sorted[index];
            index++;
        }
        n--;

        // Print the last row
        // from the remaining rows
        if (k < m)
        {
            for (int i = n - 1; i >= l; --i)
            {
                a[m - 1][i] = Sorted[index];
                index++;
            }
            m--;
        }

        // Print the first column
        // from the remaining columns
        if (l < n)
        {
            for (int i = m - 1; i >= k; --i)
            {
                a[i][l] = Sorted[index];
                index++;
            }
            l++;
        }
    }
}

// Function to convert 2D array to 1D array
void convert2Dto1D(int y[MAX][MAX],
                   int m, int n,int x[])
{

    int index = 0;

    // Store value 2D Matrix To 1D array
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            x[index] = y[i][j];
            index++;
        }
    }
}

// Function to print the Matrix
void PrintMatrix(int a[MAX][MAX],
                int m, int n)
{

    // Print Spiral Matrix
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cout << a[i][j] << " ";
        }
        cout << endl;
    }
}

// Function to Convert given Matrix
// into sorted Spiral Matrix
void convertMatrixToSortedSpiral(
    int y[MAX][MAX], int m, int n)
{
    int a[MAX][MAX] = {0};
    int x[m * n];

    convert2Dto1D(y, m, n,x);
    sort(x, x + n * m);
    ToSpiral(m, n, x, a);
    PrintMatrix(a, m, n);
}

// Driver code
int main()
{
    int m = 4, n = 3;
    int y[MAX][MAX] = {
        { 2, 5, 12 },
        { 22, 45, 55 },
        { 1, 6, 8 },
        { 13, 56, 10 }};

    convertMatrixToSortedSpiral(y, m, n);

    return 0;
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Convert given Matrix
// into sorted Spiral Matrix

import java.util.*;

public class TwistedMatrix {

    static int MAX = 1000;

    // Function to convert the array to Spiral
    static void ToSpiral(int m, int n,
                         int Sorted[], int a[][])
    {
        // For Array pointer
        int index = 0;

        // k - starting row index
        // m - ending row index
        // l - starting column index
        // n - ending column index
        int k = 0, l = 0;

        while (k < m && l < n) {

            // Print the first row
            // from the remaining rows
            for (int i = l; i < n; ++i) {
                a[k][i] = Sorted[index];
                index++;
            }

            k++;

            // Print the last column
            // from the remaining columns
            for (int i = k; i < m; ++i) {
                a[i][n - 1] = Sorted[index];
                index++;
            }
            n--;

            // Print the last row
            // from the remaining rows
            if (k < m) {
                for (int i = n - 1; i >= l; --i) {
                    a[m - 1][i] = Sorted[index];
                    index++;
                }
                m--;
            }

            // Print the first column
            // from the remaining columns
            if (l < n) {
                for (int i = m - 1; i >= k; --i) {
                    a[i][l] = Sorted[index];
                    index++;
                }
                l++;
            }
        }
    }

    // Function to convert 2D array to 1D array
    public static int[] convert2Dto1D(
        int y[][], int m, int n)
    {

        int index = 0;
        int x[] = new int[m * n];

        // Store value 2D Matrix To 1D array
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                x[index] = y[i][j];
                index++;
            }
        }
        return x;
    }

    // Function to print the Matrix
    public static void PrintMatrix(
        int a[][], int m, int n)
    {

        // Print Spiral Matrix
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(a[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Function to sort the array
    public static int[] SortArray(int x[])
    {

        // Sort array Using InBuilt Function
        Arrays.sort(x);

        return x;
    }

    // Function to Convert given Matrix
    // into sorted Spiral Matrix
    public static void convertMatrixToSortedSpiral(
        int y[][], int m, int n)
    {

        int a[][] = new int[MAX][MAX];
        int x[] = new int[m * n];

        x = convert2Dto1D(y, m, n);
        x = SortArray(x);
        ToSpiral(m, n, x, a);
        PrintMatrix(a, m, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int m = 4, n = 3;
        int y[][] = {
            { 2, 5, 12 },
            { 22, 45, 55 },
            { 1, 6, 8 },
            { 13, 56, 10 }
        };

        convertMatrixToSortedSpiral(y, m, n);
    }
}

// This article is contributed by VRUND R PATEL
```

## 蟒蛇 3

```
# Python3 program to Convert given Matrix
# into sorted Spiral Matrix
MAX = 1000

# Function to convert the array to Spiral
def ToSpiral(m, n, Sorted, a):

    # For Array pointer
    index = 0

    # k - starting row index
    # m - ending row index
    # l - starting column index
    # n - ending column index
    k = 0
    l = 0

    while (k < m and l < n):

        # Print the first row
        # from the remaining rows
        for i in range(l, n, 1):
            a[k][i] = Sorted[index]
            index += 1

        k += 1

        # Print the last column
        # from the remaining columns
        for i in range(k, m, 1):
            a[i][n - 1] = Sorted[index]
            index += 1

        n -= 1

        # Print the last row
        # from the remaining rows
        if (k < m):
            i = n - 1
            while(i >= l):
                a[m - 1][i] = Sorted[index]
                index += 1
                i -= 1

            m -= 1

        # Print the first column
        # from the remaining columns
        if (l < n):
            i = m - 1
            while(i >= k):
                a[i][l] = Sorted[index]
                index += 1
                i -= 1

            l += 1

# Function to convert 2D array to 1D array
def convert2Dto1D(y, m, n):
    index = 0
    x = [0 for i in range(m * n)]

    # Store value 2D Matrix To 1D array
    for i in range(m):
        for j in range(n):
            x[index] = y[i][j]
            index += 1

    return x

# Function to print the Matrix
def PrintMatrix(a, m, n):

    # Print Spiral Matrix
    for i in range(m):
        for j in range(n):
            print(a[i][j], end =" ")

        print('\n', end = "")

# Function to sort the array
def SortArray(x):

    # Sort array Using InBuilt Function
    x.sort(reverse = False)

    return x

# Function to Convert given Matrix
# into sorted Spiral Matrix
def convertMatrixToSortedSpiral(y, m, n):
    a = [[0 for i in range(MAX)]
            for j in range(MAX)]
    x = [0 for i in range(15)]

    x = convert2Dto1D(y, m, n)
    x = SortArray(x)
    ToSpiral(m, n, x, a)
    PrintMatrix(a, m, n)

# Driver code
if __name__ == '__main__':
    m = 4
    n = 3
    y = [[2, 5, 12], [22, 45, 55],
         [1, 6, 8], [13, 56, 10]]

    convertMatrixToSortedSpiral(y, m, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to Convert given Matrix
// into sorted Spiral Matrix
using System;

class GFG
{
    static int MAX = 1000;

    // Function to convert the array to Spiral
    static void ToSpiral(int m, int n,
                         int []Sorted, int [,]a)
    {
        // For Array pointer
        int index = 0;

        // k - starting row index
        // m - ending row index
        // l - starting column index
        // n - ending column index
        int k = 0, l = 0;

        while (k < m && l < n)
        {

            // Print the first row
            // from the remaining rows
            for (int i = l; i < n; ++i)
            {
                a[k, i] = Sorted[index];
                index++;
            }

            k++;

            // Print the last column
            // from the remaining columns
            for (int i = k; i < m; ++i)
            {
                a[i, n - 1] = Sorted[index];
                index++;
            }
            n--;

            // Print the last row
            // from the remaining rows
            if (k < m)
            {
                for (int i = n - 1; i >= l; --i)
                {
                    a[m - 1, i] = Sorted[index];
                    index++;
                }
                m--;
            }

            // Print the first column
            // from the remaining columns
            if (l < n)
            {
                for (int i = m - 1; i >= k; --i)
                {
                    a[i, l] = Sorted[index];
                    index++;
                }
                l++;
            }
        }
    }

    // Function to convert 2D array to 1D array
    public static int[] convert2Dto1D(int [,]y,
                                      int m, int n)
    {
        int index = 0;
        int []x = new int[m * n];

        // Store value 2D Matrix To 1D array
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                x[index] = y[i, j];
                index++;
            }
        }
        return x;
    }

    // Function to print the Matrix
    public static void PrintMatrix(int [,]a,
                                   int m, int n)
    {

        // Print Spiral Matrix
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                Console.Write(a[i, j] + " ");
            }
            Console.WriteLine();
        }
    }

    // Function to sort the array
    public static int[] SortArray(int []x)
    {

        // Sort array Using InBuilt Function
        Array.Sort(x);

        return x;
    }

    // Function to Convert given Matrix
    // into sorted Spiral Matrix
    public static void convertMatrixToSortedSpiral(int [,]y,
                                                   int m, int n)
    {
        int [,]a = new int[MAX, MAX];
        int []x = new int[m * n];

        x = convert2Dto1D(y, m, n);
        x = SortArray(x);
        ToSpiral(m, n, x, a);
        PrintMatrix(a, m, n);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int m = 4, n = 3;
        int [,]y = {{ 2, 5, 12 },
                    { 22, 45, 55 },
                    { 1, 6, 8 },
                    { 13, 56, 10 }};

        convertMatrixToSortedSpiral(y, m, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to Convert given Matrix
// into sorted Spiral Matrix

let MAX = 1000;

// Function to convert the array to Spiral
function ToSpiral(m,n,Sorted,a)
{

    // For Array pointer
        let index = 0;

        // k - starting row index
        // m - ending row index
        // l - starting column index
        // n - ending column index
        let k = 0, l = 0;

        while (k < m && l < n) {

            // Print the first row
            // from the remaining rows
            for (let i = l; i < n; ++i) {
                a[k][i] = Sorted[index];
                index++;
            }

            k++;

            // Print the last column
            // from the remaining columns
            for (let i = k; i < m; ++i) {
                a[i][n - 1] = Sorted[index];
                index++;
            }
            n--;

            // Print the last row
            // from the remaining rows
            if (k < m) {
                for (let i = n - 1; i >= l; --i) {
                    a[m - 1][i] = Sorted[index];
                    index++;
                }
                m--;
            }

            // Print the first column
            // from the remaining columns
            if (l < n) {
                for (let i = m - 1; i >= k; --i) {
                    a[i][l] = Sorted[index];
                    index++;
                }
                l++;
            }
        }
}

// Function to convert 2D array to 1D array
function convert2Dto1D(y,m,n)
{
    let index = 0;
        let x = new Array(m * n);

        // Store value 2D Matrix To 1D array
        for (let i = 0; i < m; i++) {
            for (let j = 0; j < n; j++) {
                x[index] = y[i][j];
                index++;
            }
        }
        return x;
}

// Function to print the Matrix
function PrintMatrix(a,m,n)
{
    // Print Spiral Matrix
        for (let i = 0; i < m; i++) {
            for (let j = 0; j < n; j++) {
                document.write(a[i][j] + " ");
            }
            document.write("<br>");
        }
}

// Function to sort the array
function SortArray(x)
{
    // Sort array Using InBuilt Function
        x.sort(function(a,b){return a-b;});

        return x;
}

 // Function to Convert given Matrix
    // into sorted Spiral Matrix
function convertMatrixToSortedSpiral(y,m,n)
{
    let a = new Array(MAX);
    for(let i=0;i<MAX;i++)
        a[i]=new Array(MAX);
        let x = new Array(m * n);

        x = convert2Dto1D(y, m, n);
        x = SortArray(x);
        ToSpiral(m, n, x, a);
        PrintMatrix(a, m, n);
}

 // Driver code
let m = 4, n = 3;
let y = [
[ 2, 5, 12 ],
[ 22, 45, 55 ],
[ 1, 6, 8 ],
[ 13, 56, 10 ]
];

convertMatrixToSortedSpiral(y, m, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1 2 5 
45 55 6 
22 56 8 
13 12 10
```

**时间复杂度:** O(m*n)

**辅助空间:** O(m*n)