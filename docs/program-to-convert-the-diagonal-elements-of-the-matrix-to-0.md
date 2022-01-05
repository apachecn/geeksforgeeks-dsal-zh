# 将矩阵对角线元素转换为 0 的程序

> 原文:[https://www . geeksforgeeks . org/program-to-convert-the-对角元素矩阵-0/](https://www.geeksforgeeks.org/program-to-convert-the-diagonal-elements-of-the-matrix-to-0/)

给定一个 N*N 矩阵。任务是将矩阵的对角线元素转换为 0。
**例** :

```
Input: mat[][] = 
{{ 2, 1, 7 },
 { 3, 7, 2 },
 { 5, 4, 9 }}
Output: 
{ {0, 1, 0},
  {3, 0, 2},
  {0, 4, 0}}

Input:  mat[][] = 
{{1, 3, 5, 6, 7},
 {3, 5, 3, 2, 1},
 {1, 2, 3, 4, 5},
 {7, 9, 2, 1, 6},
 {9, 1, 5, 3, 2}}
Output: 
{{0, 3, 5, 6, 0},
 {3, 0, 3, 0, 1},
 {1, 2, 0, 4, 5},
 {7, 0, 2, 0, 6},
 {0, 1, 5, 3, 0}}
```

**方法:**运行两个循环，即外部循环代表行数，内部循环代表列数。检查以下情况:

> 如果**((I = = j)| |(I+j+1)= = n)**
> mat[I][j]= 0

以下是上述方法的实现:

## C++

```
// C++ program to change value of
// diagonal elements of a matrix to 0.
#include <iostream>
using namespace std;
const int MAX = 100;

// to print the resultant matrix
void print(int mat[][MAX], int n, int m)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++)
            cout << mat[i][j] << " ";

        cout << endl;
    }
}

// function to change the values
// of diagonal elements to 0
void makediagonalzero(int mat[][MAX], int n, int m)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // right and left diagonal condition
            if (i == j || (i + j + 1) == n)
                mat[i][j] = 0;
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver code
int main()
{

    int n = 3, m = 3;
    int mat[][MAX] = { { 2, 1, 7 },
                       { 3, 7, 2 },
                       { 5, 4, 9 } };

    makediagonalzero(mat, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change value of
// diagonal elements of a matrix to 0.
class GFG
{

static final int MAX = 100;

// to print the resultant matrix
static void print(int mat[][], int n, int m)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            System.out.print(mat[i][j] + " ");
        }

        System.out.println();
    }
}

// function to change the values
// of diagonal elements to 0
static void makediagonalzero(int mat[][],
                             int n, int m)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // right and left diagonal condition
            if (i == j || (i + j + 1) == n)
            {
                mat[i][j] = 0;
            }
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver code
public static void main(String args[])
{
    int n = 3, m = 3;
    int mat[][] = {{2, 1, 7},
                   {3, 7, 2},
                   {5, 4, 9}};

    makediagonalzero(mat, n, m);
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to change value of
# diagonal elements of a matrix to 0.
MAX = 100

# to print the resultant matrix
def print_1(mat, n, m):

    for i in range(n):
        for j in range(m):
            print( mat[i][j], end = " ")

        print()

# function to change the values
# of diagonal elements to 0
def makediagonalzero(mat, n, m):

    for i in range(n):
        for j in range(m):

            # right and left diagonal condition
            if (i == j or (i + j + 1) == n):
                mat[i][j] = 0

    # print resultant matrix
    print_1(mat, n, m)

# Driver code
if __name__ == "__main__":

    n = 3
    m = 3
    mat = [[ 2, 1, 7 ],
           [ 3, 7, 2 ],
           [ 5, 4, 9 ]]

    makediagonalzero(mat, n, m)

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to change value of
// diagonal elements of a matrix to 0.
using System;

class GFG
{

static int MAX = 100;

// to print the resultant matrix
static void print(int[,] mat, int n, int m)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            Console.Write(mat[i, j] + " ");
        }

        Console.WriteLine();
    }
}

// function to change the values
// of diagonal elements to 0
static void makediagonalzero(int[,] mat,
                            int n, int m)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // right and left diagonal condition
            if (i == j || (i + j + 1) == n)
            {
                mat[i, j] = 0;
            }
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver code
public static void Main()
{
    int n = 3, m = 3;
    int[,] mat = {{2, 1, 7},
                  {3, 7, 2},
                  {5, 4, 9}};

    makediagonalzero(mat, n, m);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to change value of
// diagonal elements of a matrix to 0.

// to print the resultant matrix
function printsd(&$mat, $n, $m)
{
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        {
            echo ($mat[$i][$j]);
            echo (" ");
        }
        echo ("\n");
    }
}

// function to change the values
// of diagonal elements to 0
function makediagonalzero(&$mat, $n, $m)
{
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        {

            // right and left diagonal condition
            if ($i == $j || ($i + $j + 1) == $n)
                $mat[$i][$j] = 0;
        }
    }

    // print resultant matrix
    printsd($mat, $n, $m);
}

// Driver code
$n = 3; $m = 3;
$mat = array(array(2, 1, 7),
             array(3, 7, 2),
             array(5, 4, 9));

makediagonalzero($mat, $n, $m);

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to change value of
// diagonal elements of a matrix to 0.

const MAX = 100;

// to print the resultant matrix
function print(mat, n, m)
{
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < m; j++)
            document.write(mat[i][j] + " ");

        document.write("<br>");
    }
}

// function to change the values
// of diagonal elements to 0
function makediagonalzero(mat, n, m)
{
    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < m; j++)
        {

            // right and left diagonal condition
            if (i == j || (i + j + 1) == n)
                mat[i][j] = 0;
        }
    }

    // print resultant matrix
    print(mat, n, m);
}

// Driver code
    let n = 3, m = 3;
    let mat = [ [ 2, 1, 7 ],
                       [ 3, 7, 2 ],
                       [ 5, 4, 9 ] ];

    makediagonalzero(mat, n, m);

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
0 1 0 
3 0 2 
0 4 0
```

**Another approach :**  

## C++

```
// C++ program to change value of
// diagonal elements of a matrix to 0.
#include <bits/stdc++.h>
#define COL 100
using namespace std;

// Method to replace the diagonal matrix with zeros
void diagonalMat( int m[][COL] ,int row, int col)
{

    // l is the left iterator which is
    // iterationg from 0 to col-1[4] here
    //k is the right iterator which is
    // iterating from col-1 to 0
    int i = 0, l = 0, k = col - 1;

    // i used to iterate over rows of the matrix
    while (i < row)
    {
        int j = 0;

        // condition to check if it is
        // the centre of the matrix
        if (l == k)
        {
            m[l][k] = 0;
            l++;
            k--;
        }         //otherwize the diagonal will be equivalaent to l or k
            //increment l because l is traversing from left
            //to right and decrement k for vice-cersa
        else
        {
            m[i][l] = 0;
            l++;
            m[i][k] = 0;
            k--;
        }

        // print every element after replacing from the column
        while (j < col)
        {
            cout << " "<< m[i][j];
            j++;
        }
        i++;
        cout << "\n";
    }

}

// Driver code
int main()
{
    int m[][COL] ={{ 2, 1, 7},
                    { 3, 7, 2},
                    { 5, 4, 9}};
    int row = 3, col = 3;
    diagonalMat( m, row, col);
    return 0;
}

// This code has been contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change value of
// diagonal elements of a matrix to 0.
import java.io.*;

class GFG {
    public static void main (String[] args) {
        int m[][] = {{ 2, 1, 7 },
                    { 3, 7, 2 },
                    { 5, 4, 9 }};
        int row = 3, col = 3;
        GFG.diagonalMat(row,col,m);
    }
    // method to replace the diagonal matrix with zeros
    public static void diagonalMat(int row, int col, int m[][]){

        // l is the left iterator which is
        // iterationg from 0 to col-1[4] here
        //k is the right iterator which is
        // iterating from col-1 to 0
        int i =0,l=0,k=col-1;

        // i used to iterate over rows of the matrix
        while(i<row){
            int j=0;
            // condition to check if it is
            // the centre of the matrix
            if(l==k){
                m[l][k] = 0;
                l++;
                k--;
            }
            //otherwize the diagonal will be equivalaent to l or k
            //increment l because l is traversing from left
            //to right and decrement k for vice-cersa
            else{
                m[i][l] = 0;
                l++;
                m[i][k]=0;
                k--;
            }
            // print every element after replacing from the column
            while(j<col){
                System.out.print(" "+ m[i][j]);
                j++;
            }
            i++;
            System.out.println();
        }

    }

}
```

## 蟒蛇 3

```
# Python3 program to change value of
# diagonal elements of a matrix to 0.

# method to replace the diagonal
# matrix with zeros
def diagonalMat(row, col, m):

    # l is the left iterator which is
    # iterationg from 0 to col-1[4] here
    # k is the right iterator which is
    # iterating from col-1 to 0
    i, l, k = 0, 0, col - 1;

    # i used to iterate over rows of the matrix
    while(i < row):
        j = 0;

        # condition to check if it is
        # the centre of the matrix
        if(l == k):
            m[l][k] = 0;
            l += 1;
            k -= 1;

        # otherwize the diagonal will be equivalaent to l or k
        # increment l because l is traversing from left
        # to right and decrement k for vice-cersa
        else:
            m[i][l] = 0;
            l += 1;
            m[i][k] = 0;
            k -= 1;

        # print every element
        # after replacing from the column
        while(j < col):
            print(" ", m[i][j], end = "");
            j += 1;
        i += 1;
        print("");

# Driver Code
if __name__ == '__main__':
    m = [[2, 1, 7 ],
        [ 3, 7, 2 ],
        [ 5, 4, 9 ]];
    row, col = 3, 3;
    diagonalMat(row, col, m);

# This code contributed by Rajput-Ji
```

## C#

```
// C# program to change value of
// diagonal elements of a matrix to 0.
using System;

class GFG {
    public static void Main () {
        int[,]  m = {{ 2, 1, 7 },
                    { 3, 7, 2 },
                    { 5, 4, 9 }};
        int row = 3, col = 3;
        GFG.diagonalMat(row,col,m);
    }
    // method to replace the diagonal matrix with zeros
    public static void diagonalMat(int row, int col, int[,] m){

        // l is the left iterator which is
        // iterationg from 0 to col-1[4] here
        //k is the right iterator which is
        // iterating from col-1 to 0
        int i =0,l=0,k=col-1;

        // i used to iterate over rows of the matrix
        while(i < row){
            int j=0;
            // condition to check if it is
            // the centre of the matrix
            if(l==k){
                m[l,k] = 0;
                l++;
                k--;
            }
            //otherwize the diagonal will be equivalaent to l or k
            //increment l because l is traversing from left
            //to right and decrement k for vice-cersa
            else{
                m[i,l] = 0;
                l++;
                m[i,k]=0;
                k--;
            }
            // print every element after replacing from the column
            while(j < col){
                Console.Write(" " + m[i,j]);
                j++;
            }
            i++;
            Console.WriteLine();
        }

    }

}
      //This code is contributed by Mukul singh
```

## java 描述语言

```
<script>
// Javascript program to change value of
// diagonal elements of a matrix to 0.

const COL = 100;

// Method to replace the diagonal matrix with zeros
function diagonalMat(m, row, col)
{

    // l is the left iterator which is
    // iterationg from 0 to col-1[4] here
    //k is the right iterator which is
    // iterating from col-1 to 0
    let i = 0, l = 0, k = col - 1;

    // i used to iterate over rows of the matrix
    while (i < row)
    {
        let j = 0;

        // condition to check if it is
        // the centre of the matrix
        if (l == k)
        {
            m[l][k] = 0;
            l++;
            k--;
        }         //otherwize the diagonal will be equivalaent to l or k
            //increment l because l is traversing from left
            //to right and decrement k for vice-cersa
        else
        {
            m[i][l] = 0;
            l++;
            m[i][k] = 0;
            k--;
        }

        // print every element after replacing from the column
        while (j < col)
        {
            document.write(" " + m[i][j]);
            j++;
        }
        i++;
        document.write("<br>");
    }

}

// Driver code
    let m =[[ 2, 1, 7],
                    [ 3, 7, 2],
                    [ 5, 4, 9]];
    let row = 3, col = 3;
    diagonalMat( m, row, col);

</script>
```

**Output:** 

```
 0 1 0
 3 0 2
 0 4 0
```

**时间复杂度:** O(n*m)