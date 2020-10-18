# 矩阵对角元素的正方形

> 原文： [https://www.geeksforgeeks.org/squares-of-matrix-diagonal-elements/](https://www.geeksforgeeks.org/squares-of-matrix-diagonal-elements/)

您给定了一个具有奇数维的整数矩阵。 在两侧找到对角线元素的平方。

**示例**：

```
Input  :  1 2 3
          4 5 6
          7 8 9
Output :  Diagonal one: 1 25 81
          Diagonal two: 9 25 49

Input  :  2 5 7  
          3 7 2
          5 6 9
Output :  Diagonal one : 4 49 81
          Diagonal two : 49 49 25

```



**方法 1**：首先，找到矩阵的对角元素，然后打印该元素的平方。

## C++ 

```cpp

// Simple CPP program to print squares of 
// diagonal elements. 
#include <iostream> 
using namespace std; 

#define MAX 100 

// function of diagonal square 
void diagonalsquare(int mat[][MAX], int row,  
                                  int column) 
{ 
    // This loop is for finding square of first  
    // diagonal elements 
    cout << "Diagonal one : "; 
    for (int i = 0; i < row; i++) 
    { 
        for (int j = 0; j < column; j++) 

            // if this condition will become true  
            // then we will get diagonal element 
            if (i == j) 

                // printing square of diagonal element 
                cout << mat[i][j] * mat[i][j] << " "; 
    } 

    // This loop is for finding square of second  
    // side of diagonal elements 
    cout << " \n\nDiagonal two : "; 
    for (int i = 0; i < row; i++) 
    { 
        for (int j = 0; j < column; j++) 

            // if this condition will become true 
            // then we will get second side diagonal  
            // element 
            if (i + j == column - 1) 

                // printing square of diagonal element 
                cout << mat[i][j] * mat[i][j] << "  "; 
    } 
} 

// Driver code 
int main() 
{ 
    int mat[][MAX] = { { 2, 5, 7 }, 
                       { 3, 7, 2 },  
                       { 5, 6, 9 } }; 
    diagonalsquare(mat, 3, 3); 
    return 0; 
} 

```

## Java

```java

// Simple JAva program to print squares of 
// diagonal elements. 
import java.io.*; 

class GFG 
{ 
    static int MAX =100; 

    // function of diagonal square 
    static void diagonalsquare(int mat[][], int row,  
                                         int column) 
    { 
        // This loop is for finding square of first  
        // diagonal elements 
        System.out.print( "Diagonal one : "); 
        for (int i = 0; i < row; i++) 
        { 
            for (int j = 0; j < column; j++) 

                // if this condition will become true  
                // then we will get diagonal element 
                if (i == j) 

                    // printing square of diagonal element 
                    System.out.print ( mat[i][j] * mat[i][j] +" "); 
        } 
        System.out.println(); 

        // This loop is for finding square of second  
        // side of diagonal elements 
        System.out.print("Diagonal two : "); 
        for (int i = 0; i < row; i++) 
        { 
            for (int j = 0; j < column; j++) 

                // if this condition will become true 
                // then we will get second side diagonal  
                // element 
                if (i + j == column - 1) 

                    // printing square of diagonal element 
                    System.out.print(mat[i][j] * mat[i][j] +" "); 
        } 
    } 

    // Driver code 
    public static void main (String[] args)  
    { 
        int mat[][] = { { 2, 5, 7 }, 
                        { 3, 7, 2 },  
                        { 5, 6, 9 } }; 
        diagonalsquare(mat, 3, 3); 

    } 
} 

// This code is contributed by vt_m. 

```

## Python3

```py

# Simple Python program  
# to print squares 
# of diagonal elements. 

# function of diagonal square 
def diagonalsquare(mat, row, column) : 

    # This loop is for finding square 
    # of first diagonal elements 
    print ("Diagonal one : ", end = "") 
    for i in range(0, row) : 
        for j in range(0, column) : 

            # if this condition will  
            # become true then we will 
            # get diagonal element 
            if (i == j) :  
                # printing square of  
                # diagonal element 
                print ("{} ".format(mat[i][j] * 
                                    mat[i][j]), end = "") 

    # This loop is for finding  
    # square of second side  
    # of diagonal elements 
    print (" \n\nDiagonal two : ", end = "") 
    for i in range(0, row) : 
        for j in range(0, column) : 

            # if this condition will become 
            # true then we will get second 
            # side diagonal element 
            if (i + j == column - 1) : 

                # printing square of diagonal 
                # element 
                print ("{} ".format(mat[i][j] * 
                                    mat[i][j]), end = "") 

# Driver code 
mat = [[ 2, 5, 7 ], 
        [ 3, 7, 2 ],  
        [ 5, 6, 9 ]] 
diagonalsquare(mat, 3, 3) 

# This code is contributed by  
# Manish Shaw(manishshaw1) 

```

## C# 

```cs

// Simple C# program to print squares of 
// diagonal elements. 
using System; 

class GFG 
{ 
    //static int MAX =100; 

    // function of diagonal square 
    static void diagonalsquare(int [,]mat, int row,  
                                        int column) 
    { 

        // This loop is for finding 
        // square of first  
        // diagonal elements 
        Console.Write( "Diagonal one : "); 
        for (int i = 0; i < row; i++) 
        { 
            for (int j = 0; j < column; j++) 

                // if this condition will become true  
                // then we will get diagonal element 
                if (i == j) 

                    // printing square of diagonal element 
                    Console.Write ( mat[i,j] * mat[i,j] +" "); 
        } 
        Console.WriteLine(); 

        // This loop is for finding  
        // square of second side of 
        // diagonal elements 
        Console.Write("Diagonal two : "); 
        for (int i = 0; i < row; i++) 
        { 
            for (int j = 0; j < column; j++) 

                // if this condition will become true 
                // then we will get second side diagonal  
                // element 
                if (i + j == column - 1) 

                    // printing square of diagonal element 
                    Console.Write(mat[i,j] * mat[i,j] +" "); 
        } 
    } 

    // Driver code 
    public static void Main ()  
    { 
        int [,]mat = {{ 2, 5, 7 }, 
                      { 3, 7, 2 },  
                      { 5, 6, 9 }}; 
        diagonalsquare(mat, 3, 3); 

    } 
} 

// This code is contributed by anuj_67\. 

```

## PHP

```php

<?php 
// Simple PHP program to print squares 
// of diagonal elements. 

//$MAX = 100; 

// function of diagonal square 
function diagonalsquare($mat, $row,  
                            $column) 
{ 
    // This loop is for finding square 
    // of first diagonal elements 
    echo "Diagonal one : "; 
    for ( $i = 0; $i < $row; $i++) 
    { 
        for ( $j = 0; $j < $column; $j++) 

            // if this condition will become true  
            // then we will get diagonal element 
            if ($i == $j) 

                // printing square of diagonal 
                // element 
                echo $mat[$i][$j] * $mat[$i][$j]  
                                          , " "; 
    } 

    // This loop is for finding square of second  
    // side of diagonal elements 
    echo " \n\nDiagonal two : "; 
    for ( $i = 0; $i < $row; $i++) 
    { 
        for ($j = 0; $j < $column; $j++) 

            // if this condition will become 
            // true then we will get second 
            // side diagonal element 
            if ($i + $j == $column - 1) 

                // printing square of diagonal 
                // element 
                echo $mat[$i][$j] * $mat[$i][$j], 
                                            " "; 
    } 
} 

// Driver code 
    $mat = array(array( 2, 5, 7 ), 
                 array( 3, 7, 2 ),  
                 array( 5, 6, 9 ) ); 
    diagonalsquare($mat, 3, 3); 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
Diagonal one : 4 49 81  

Diagonal two : 49  49  25
```

**时间复杂度** `O(n * n)`。

**方法 2**：

一种有效的解决方案也与朴素的方法相同，但是在这种方法中，我们只用一个循环找到对角线元素，然后打印该元素的平方。

## C++

```

// Efficient CPP program to print squares of 
// diagonal elements. 
#include <iostream> 
using namespace std; 

#define MAX 100 

// function of diagonal square 
void diagonalsquare(int mat[][MAX], int row, 
                                 int column) 
{ 
    // This loop is for finding of square of  
    // the first side of diagonal elements 
    cout << " \nDiagonal one : "; 
    for (int i = 0; i < row; i++) 
    { 

        // printing direct square of diagonal  
        // element there is no need to check  
        // condition 
        cout << mat[i][i] * mat[i][i] << " "; 
    } 

    // This loop is for finding square of the  
    // second side of diagonal elements 
    cout << " \n\nDiagonal two : "; 
    for (int i = 0; i < row; i++) 
    { 
        // printing direct square of diagonal  
        // element in the second side 
        cout << mat[i][row - i - 1] * mat[i][row - i - 1]  
            << " "; 
    } 
} 

// Driver code 
int main() 
{ 
    int mat[][MAX] = { { 2, 5, 7 }, 
                    { 3, 7, 2 },  
                    { 5, 6, 9 } }; 
    diagonalsquare(mat, 3, 3); 
    return 0; 
} 

```