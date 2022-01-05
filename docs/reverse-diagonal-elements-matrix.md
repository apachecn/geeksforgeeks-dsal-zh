# 矩阵的反向对角元素

> 原文:[https://www . geesforgeks . org/reverse-对角线-元素-矩阵/](https://www.geeksforgeeks.org/reverse-diagonal-elements-matrix/)

给定一个 n*n 阶的方阵，我们必须把两条对角线的元素都反过来。
**例:**

```
Input : {1, 2, 3,
         4, 5, 6,
         7, 8, 9}
Output :{9, 2, 7,
         4, 5, 6,
         3, 8, 1}
Explanation: 
             Major Diagonal Elements before:  1 5 9
                             After reverse:   9 5 1
             Minor Diagonal Elements before:  3 5 7
                             After reverse:   7 5 3 
Input :{1,  2,  3,  4,
        5,  6,  7,  8,
        9,  10, 11, 12,
        13, 14, 15, 16}

Output :{16, 2, 3, 13,
         5, 11, 10, 8,
         9, 7,  6,  12,
         4, 14, 15, 1}

```

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define N 4

// Function to swap diagonals elements
void reverseDiagonal(int array[][N])
{
    int i = 0, j = N;   
    while (i < j) {

        // For reversing elements of major
        // diagonal.
        swap(array[i][i], array[j - 1][j - 1]);

        // For reversing elements of minor
        // diagonal.
        swap(array[i][j - 1], array[j - 1][i]);

        i++;
        j--;
    }

    // Print matrix after reversals.
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j)
            printf("%d  ", array[i][j]);
        printf("\n");
    }
}

// Driver function
int main()
{
    int matrix[N][N] = { 1, 2,  3,  4,
                         5, 6,  7,  8,
                         9, 10, 11, 12,
                        13, 14, 15, 16 };
    reverseDiagonal(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Reverse
// Diagonal elements of matrix
import java.io.*;

class GFG
{
static int N = 4;

// Function to swap
// diagonals elements
static void reverseDiagonal(int array[][])
{
    int i = 0, j = N;
    int temp = 0;
    while (i < j)
    {

        // For reversing elements
        // of major diagonal.

        temp = array[i][i];
        array[i][i] = array[j - 1][j - 1];
        array[j - 1][j - 1] = temp;

        // For reversing elements
        // of minor diagonal.

        temp = array[i][j - 1];
        array[i][j - 1] = array[j - 1][i];
        array[j - 1][i] = temp;

        i++;
        j--;
    }

    // Print matrix after
    // reversals.
    for (i = 0; i < N; ++i)
    {
        for (j = 0; j < N; ++j)
            System.out.print(array[i][j] + " ");
            System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{
    int matrix[][] = {{1, 2, 3, 4},
                      {5, 6, 7, 8},
                      {9, 10, 11, 12},
                      {13, 14, 15, 16}};
    reverseDiagonal(matrix);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to Reverse
# Diagonal elements of matrix

N = 4

# Function to swap diagonals elements
def reverseDiagonal(array):

    i = 0
    j = N
    while (i < j) :

        # For reversing elements of major
        # diagonal.
        array[i][i], array[j - 1][j - 1] = array[j-1][j-1], array[i][i]

        # For reversing elements of minor
        # diagonal.
        array[i][j - 1], array[j - 1][i] = array[j-1][i], array[i][j-1]

        i += 1
        j -= 1

    # Print matrix after reversals.
    for i in range(N):
        for j in range( N):
            print( array[i][j],end="  ")
        print()

# Driver function
if __name__ == "__main__":

    matrix = [[ 1, 2,  3,  4],
                        [5, 6,  7,  8],
                        [9, 10, 11, 12],
                        [13, 14, 15, 16 ]]
    reverseDiagonal(matrix)
```

## C#

```
// C# Program to Reverse
// Diagonal elements of matrix
using System;

class GFG
{
static int N = 4;

// Function to swap
// diagonals elements
static void reverseDiagonal(int [,]array)
{
    int i = 0, j = N;
    int temp = 0;
    while (i < j)
    {

        // For reversing elements
        // of major diagonal.

        temp = array[i, i];
        array[i, i] = array[j - 1, j - 1];
        array[j - 1, j - 1] = temp;

        // For reversing elements
        // of minor diagonal.

        temp = array[i, j - 1];
        array[i, j - 1] = array[j - 1, i];
        array[j - 1, i] = temp;

        i++;
        j--;
    }

    // Print matrix after
    // reversals.
    for (i = 0; i < N; ++i)
    {
        for (j = 0; j < N; ++j)
            Console.Write(array[i, j] + " ");
            Console.WriteLine();
    }
}

// Driver Code
public static void Main ()
{
    int [,]matrix = {{1, 2, 3, 4},
                     {5, 6, 7, 8},
                     {9, 10, 11, 12},
                     {13, 14, 15, 16}};
    reverseDiagonal(matrix);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to Reverse
// Diagonal elements of matrix

// Function to swap
// diagonals elements
function reverseDiagonal($array)
{
    $N = 4;
    $i = 0; $j = $N;
    $temp = 0;
    while ($i < $j)
    {

        // For reversing elements
        // of major diagonal.

        $temp = $array[$i][$i];
        $array[$i][$i] = $array[$j - 1][$j - 1];
        $array[$j - 1][$j - 1] = $temp;

        // For reversing elements
        // of minor diagonal.

        $temp = $array[$i][$j - 1];
        $array[$i][$j - 1] = $array[$j - 1][$i];
        $array[$j - 1][$i] = $temp;

        $i++;
        $j--;
    }

    // Print matrix after
    // reversals.
    for ($i = 0; $i < $N; ++$i)
    {
        for ($j = 0; $j < $N; ++$j)
            echo $array[$i][$j] . " ";
            echo "\n";
    }
}

// Driver Code
$matrix = array(array(1, 2, 3, 4),
                array(5, 6, 7, 8),
                array(9, 10, 11, 12),
                array(13, 14, 15, 16));

reverseDiagonal($matrix);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript Program to Reverse
// Diagonal elements of matrix
let N = 4;

// Function to swap
// diagonals elements
function reverseDiagonal(array)
{
    let i = 0, j = N;
    let temp = 0;
    while (i < j)
    {

        // For reversing elements
        // of major diagonal.

        temp = array[i][i];
        array[i][i] = array[j - 1][j - 1];
        array[j - 1][j - 1] = temp;

        // For reversing elements
        // of minor diagonal.

        temp = array[i][j - 1];
        array[i][j - 1] = array[j - 1][i];
        array[j - 1][i] = temp;

        i++;
        j--;
    }

    // Print matrix after
    // reversals.
    for (i = 0; i < N; ++i)
    {
        for (j = 0; j < N; ++j)
            document.write(array[i][j] + " ");
            document.write("<br>");
    }
}

// Driver Code

    let matrix = [[1, 2, 3, 4],
                    [5, 6, 7, 8],
                    [9, 10, 11, 12],
                    [13, 14, 15, 16]];
    reverseDiagonal(matrix);

// This code is contributed
// by sravan kumar Gottumukkala

</script>
```

**Output:** 

```
16  2  3  13  
5  11  10  8  
9  7  6  12  
4  14  15  1
```