# 按降序排列矩阵的行，然后按升序排列列

> 原文:[https://www . geeksforgeeks . org/sorting-行-矩阵-降序-后跟-列-升序/](https://www.geeksforgeeks.org/sorting-rows-of-matrix-in-descending-order-followed-by-columns-in-ascending-order/)

给定不同元素的矩阵。任务是按降序对矩阵的行进行排序，然后按升序对列进行排序。
**例** :

```
Input: a[3][3] =  {{1, 2, 3},
                              {4, 5, 6}, 
                              {7, 8, 9}};
Output: 
3 2 1
6 5 4
9 8 7

Input: a[3][3] = {{3, 2, 1},
                             {9, 8, 7}, 
                             {6, 5, 4}};
Output: 
3 2 1 
6 5 4 
9 8 7
```

**进场:**

1.  逐个遍历所有行，并使用简单数组排序按降序对行进行排序。
2.  将矩阵转换为转置矩阵。
3.  再次对所有行进行排序，但这次是按升序排序。
4.  再次将矩阵转换为其转置。
5.  打印最终矩阵。

以下是上述方法的实现:

## C++

```
// C++ implementation to sort the rows
// of matrix in descending order followed by
// sorting the columns in ascending order
#include <bits/stdc++.h>
using namespace std;

#define MAX_SIZE 10

// function to sort each row of the matrix
// according to the order specified by
// descending.
void sortByRow(int mat[][MAX_SIZE], int n,
               bool descending)
{
    for (int i = 0; i < n; i++) {
        if (descending == true)
            sort(mat[i], mat[i] + n, greater<int>());
        else
            sort(mat[i], mat[i] + n);
    }
}

// function to find transpose of the matrix
void transpose(int mat[][MAX_SIZE], int n)
{
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // swapping element at index (i, j)
            // by element at index (j, i)
            swap(mat[i][j], mat[j][i]);
}

// function to sort the matrix row-wise
// and column-wise
void sortMatRowAndColWise(int mat[][MAX_SIZE],
                          int n)
{
    // sort rows of mat[][] in descending order
    sortByRow(mat, n, true);

    // get transpose of mat[][]
    transpose(mat, n);

    // again sort rows of mat[][] in ascending
    // order.
    sortByRow(mat, n, false);

    // again get transpose of mat[][]
    transpose(mat, n);
}

// function to print the matrix
void printMat(int mat[][MAX_SIZE], int n)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            cout << mat[i][j] << " ";
        cout << endl;
    }
}

// Driver code
int main()
{
    int n = 3;

    int mat[n][MAX_SIZE] = { { 3, 2, 1 },
                             { 9, 8, 7 },
                             { 6, 5, 4 } };

    cout << "Original Matrix:\n";
    printMat(mat, n);

    sortMatRowAndColWise(mat, n);

    cout << "\nMatrix After Sorting:\n";
    printMat(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the rows
// of matrix in descending order followed
// by sorting the columns in ascending order
import java.util.*;

class GFG
{

static int MAX_SIZE = 10;

// function to sort each row of the matrix
// according to the order specified by
// descending.
static void sortByRow(int[][] mat, int n,
                      boolean descending)
{
    int temp = 0;
    for (int i = 0; i < n; i++)
    {
        if (descending == true)
        {
            int t = i;
            for (int p = 0; p < n; p++)
            {
                for (int j = p + 1; j < n; j++)
                {

                    if (mat[t][p] < mat[t][j])
                    {
                        temp = mat[t][p];

                        mat[t][p] = mat[t][j];

                        mat[t][j] = temp;
                    }
                }
            }
        }

        else
            Arrays.sort(mat[i]);
    }
}

// function to find transpose of the matrix
static void transpose(int mat[][], int n)
{
    int temp = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // swapping element at index (i, j)
            // by element at index (j, i)
            temp = mat[i][j];
            mat[i][j] = mat[j][i];
            mat[j][i] = temp;
        }
    }
}

// function to sort the matrix row-wise
// and column-wise
static void sortMatRowAndColWise(int mat[][],
                                 int n)
{
    // sort rows of mat[][] in
    // descending order
    sortByRow(mat, n, true);

    // get transpose of mat[][]
    transpose(mat, n);

    // again sort rows of mat[][] in
    // ascending order.
    sortByRow(mat, n, false);

    // again get transpose of mat[][]
    transpose(mat, n);
}

// function to print the matrix
static void printMat(int mat[][], int n)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
            System.out.print(mat[i][j] + " ");
        System.out.println();
    }
}

// Driver code
public static void main(String args[])
{
    int n = 3;

    int [][]mat = {{ 3, 2, 1 },
                   { 9, 8, 7 },
                   { 6, 5, 4 }};

    System.out.println("Original Matrix:");
    printMat(mat, n);

    sortMatRowAndColWise(mat, n);

    System.out.println("\n" + "Matrix After Sorting:");
    printMat(mat, n);
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 implementation to sort the rows
# of matrix in descending order followed by
# sorting the columns in ascending order
MAX_SIZE = 10

# function to sort each row of the matrix
# according to the order specified by
# descending.
def sortByRow(mat, n, descending):

    for i in range(n):
        if (descending == True):
            mat[i].sort(reverse = True)
        else:
            mat[i].sort()

# function to find transpose of the matrix
def transpose(mat, n):

    for i in range(n):
        for j in range(i + 1, n):

            # swapping element at index (i, j)
            # by element at index (j, i)
            mat[i][j], mat[j][i] = mat[j][i], mat[i][j]

# function to sort the matrix row-wise
# and column-wise
def sortMatRowAndColWise(mat, n):

    # sort rows of mat[][] in descending order
    sortByRow(mat, n, True)

    # get transpose of mat[][]
    transpose(mat, n)

    # again sort rows of mat[][] in ascending
    # order.
    sortByRow(mat, n, False)

    # again get transpose of mat[][]
    transpose(mat, n);

# function to print the matrix
def printMat(mat, n):

    for i in range(n):
        for j in range( n):
            print(mat[i][j], end = " ")
        print()

# Driver code
if __name__ == "__main__":
    n = 3

    mat = [[3, 2, 1 ],
           [9, 8, 7 ],
           [6, 5, 4 ]]

    print("Original Matrix: ")
    printMat(mat, n)

    sortMatRowAndColWise(mat, n)

    print("Matrix After Sorting:")
    printMat(mat, n)

# This code is contributed by ita_c
```

## C#

```
// C# implementation to sort the rows
// of matrix in descending order followed
// by sorting the columns in ascending order
using System;

class GFG
{
static int MAX_SIZE = 10;

// function to sort each row of the matrix
// according to the order specified by
// descending.
static void sortByRow(int[,] mat, int n,
                      bool descending)
{
    int temp = 0;
    for (int i = 0; i < n; i++)
    {
        if (descending == true)
        {
            int t = i;
            for (int p = 0; p < n; p++)
            {
                for (int j = p + 1; j < n; j++)
                {

                    if (mat[t, p] < mat[t, j])
                    {
                        temp = mat[t, p];

                        mat[t, p] = mat[t, j];

                        mat[t, j] = temp;
                    }
                }
            }
        }
        else
            sortByRow(mat, i, n);
    }
}

// function to sort each
// row of the matrix
static void sortByRow(int [,]mat,
                      int row, int n)
{

    // sorting row number 'i'
    for (int i = row; i < row + 1; i++)
    {
        for(int j = 0; j < n - 1; j++)
        {
            if(mat[i, j] > mat[i, j + 1])
            {

                var temp = mat[i, j];
                mat[i, j] = mat[i, j + 1];
                mat[i, j + 1] = temp;

            }
        }
    }
}

// function to find transpose of the matrix
static void transpose(int [,]mat, int n)
{
    int temp = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // swapping element at index (i, j)
            // by element at index (j, i)
            temp = mat[i, j];
            mat[i, j] = mat[j, i];
            mat[j, i] = temp;
        }
    }
}

// function to sort the matrix
// row-wise and column-wise
static void sortMatRowAndColWise(int [,]mat,
                                 int n)
{
    // sort rows of [,]mat in
    // descending order
    sortByRow(mat, n, true);

    // get transpose of [,]mat
    transpose(mat, n);

    // again sort rows of [,]mat in
    // ascending order.
    sortByRow(mat, n, false);

    // again get transpose of [,]mat
    transpose(mat, n);
}

// function to print the matrix
static void printMat(int [,]mat, int n)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
            Console.Write(mat[i, j] + " ");
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String []args)
{
    int n = 3;

    int [,]mat = {{ 3, 2, 1 },
                  { 9, 8, 7 },
                  { 6, 5, 4 }};

    Console.WriteLine("Original Matrix:");
    printMat(mat, n);

    sortMatRowAndColWise(mat, n);

    Console.WriteLine("\nMatrix After Sorting:");
    printMat(mat, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to sort the rows
// of matrix in descending order followed
// by sorting the columns in ascending order

    let MAX_SIZE = 10;

    // function to sort each row of the matrix
// according to the order specified by
// descending.
    function sortByRow(mat,n,descending)
    {
        let temp = 0;
    for (let i = 0; i < n; i++)
    {
        if (descending == true)
        {
            let t = i;
            for (let p = 0; p < n; p++)
            {
                for (let j = p + 1; j < n; j++)
                {

                    if (mat[t][p] < mat[t][j])
                    {
                        temp = mat[t][p];

                        mat[t][p] = mat[t][j];

                        mat[t][j] = temp;
                    }
                }
            }
        }

        else
            mat[i].sort(function(a,b){return a-b;});
    }
    }

    // function to find transpose of the matrix
    function transpose(mat,n)
    {
        let temp = 0;
    for (let i = 0; i < n; i++)
    {
        for (let j = i + 1; j < n; j++)
        {

            // swapping element at index (i, j)
            // by element at index (j, i)
            temp = mat[i][j];
            mat[i][j] = mat[j][i];
            mat[j][i] = temp;
        }
    }
    }

    // function to sort the matrix row-wise
// and column-wise
    function sortMatRowAndColWise(mat,n)
    {
        // sort rows of mat[][] in
    // descending order
    sortByRow(mat, n, true);

    // get transpose of mat[][]
    transpose(mat, n);

    // again sort rows of mat[][] in
    // ascending order.
    sortByRow(mat, n, false);

    // again get transpose of mat[][]
    transpose(mat, n);
    }

    // function to print the matrix
    function printMat(mat,n)
    {
        for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < n; j++)
            document.write(mat[i][j] + " ");
        document.write("<br>");
    }
    }

    // Driver code
    let n = 3;

    let mat = [[3, 2, 1 ],
           [9, 8, 7 ],
           [6, 5, 4 ]];

    document.write("Original Matrix:<br>");
    printMat(mat, n);

    sortMatRowAndColWise(mat, n);

    document.write("<br>" + "Matrix After Sorting:<br>");
    printMat(mat, n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Original Matrix:
3 2 1 
9 8 7 
6 5 4 

Matrix After Sorting:
3 2 1 
6 5 4 
9 8 7
```