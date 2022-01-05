# 以数字形式打印数字的程序

> 原文:[https://www.geeksforgeeks.org/print-numbers-digital-form/](https://www.geeksforgeeks.org/print-numbers-digital-form/)

给定一个数字 **n** ，然后以数字形式打印数字。

**示例:**

```
Input : 5
Output : 
  - - 
|    
 - - 
    |
 - - 

Input :  8 
Output :
 - - 
|   |
 - - 
|   |
 - -
```

**说明:**
取一个 5*5 大小的矩阵，在矩阵中存储 0 和 1。如果矩阵单元为 0，则用于空格，如果矩阵单元为 1，则用于水平线或垂直线。

如果行号为偶数，则打印水平的 **(-)** 行，如果行号为奇数，则打印垂直的 **( | )** 行。

## C++

```
//  C++ program to print
// number in digital form
#include <iostream>
#include <vector>
using namespace std;

// Function to print numbers
void print(int mat[][5])
{

    // If in matrix row number is even then print "-"
    // otherwise print "|"
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (i % 2 == 0) {
                if (mat[i][j] == 1)
                    cout << "-";
                else
                    cout << " ";
            }
            else {
                if (mat[i][j] == 1)
                    cout << "|";
                else
                    cout << " ";
            }
        }
        cout << endl;
    }
}
void digit0()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 0, 0, 0, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}
void digit1()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 0, 0, 0, 0 },
                    { 0, 0, 1, 0, 0 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 1, 0, 0 },
                    { 0, 0, 0, 0, 0 } };
    print(mat);
}
void digit2()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 0 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}
void digit3()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}
void digit4()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 0, 0, 0, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 0, 0, 0, 0 } };
    print(mat);
}
void digit5()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 0 },
                    { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}
void digit6()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 0 },
                    { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}
void digit7()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 0, 0, 0, 0 } };
    print(mat);
}
void digit8()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}
void digit9()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    int mat[5][5] = { { 0, 1, 0, 1, 0 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 0, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 } };
    print(mat);
}

// Function to check number
void checkDigit(int num)
{
    // for digit 0
    if (num == 0)
        digit0();

    // for digit 1
    else if (num == 1)
        digit1();

    // for digit 2
    else if (num == 2)
        digit2();

    // for digit 3
    else if (num == 3)
        digit3();

    // for digit 4
    else if (num == 4)
        digit4();

    // for digit 5
    else if (num == 5)
        digit5();

    // for digit 6
    else if (num == 6)
        digit6();

    // for digit 7
    else if (num == 7)
        digit7();

    // for digit 8
    else if (num == 8)
        digit8();

    // for digit 9
    else if (num == 9)
        digit9();
}

// Driver program
int main()
{
    // Input a number
    int num = 9;

    // function call to check digit
    checkDigit(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// number in digital form
import java.io.*;

class GFG {
    // Function to print numbers
    static void print(int mat[][])
    {

        // If in matrix row number is even then print "-"
        // otherwise print "|"
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                if (i % 2 == 0) {
                    if (mat[i][j] == 1)
                        System.out.print("-");
                    else
                        System.out.print(" ");
                }
                else {
                    if (mat[i][j] == 1)
                        System.out.print("|");
                    else
                        System.out.print(" ");
                }
            }
            System.out.println();
        }
    }
    static void digit0()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }
    static void digit1()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 0, 0, 0, 0 },
                        { 0, 0, 1, 0, 0 },
                        { 0, 0, 0, 0, 0 },
                        { 0, 0, 1, 0, 0 },
                        { 0, 0, 0, 0, 0 } };
        print(mat);
    }
    static void digit2()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }
    static void digit3()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }
    static void digit4()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 0, 0, 0, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 } };
        print(mat);
    }
    static void digit5()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }
    static void digit6()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }
    static void digit7()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 } };
        print(mat);
    }
    static void digit8()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }
    static void digit9()
    {
        // In matrix 0 used for space
        // and 1 for either - or |
        int mat[][] = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    // Function to check number
    static void checkDigit(int num)
    {
        // for digit 0
        if (num == 0)
            digit0();

        // for digit 1
        else if (num == 1)
            digit1();

        // for digit 2
        else if (num == 2)
            digit2();

        // for digit 3
        else if (num == 3)
            digit3();

        // for digit 4
        else if (num == 4)
            digit4();

        // for digit 5
        else if (num == 5)
            digit5();

        // for digit 6
        else if (num == 6)
            digit6();

        // for digit 7
        else if (num == 7)
            digit7();

        // for digit 8
        else if (num == 8)
            digit8();

        // for digit 9
        else if (num == 9)
            digit9();
    }

    // Driver program
    public static void main (String[] args)
    {
        // Input a number
        int num = 9;

        // function call to check digit
        checkDigit(num);

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to prints
# number in digital form

# Function to prints numbers
def prints(mat):

    # If in matrix row number is even then
    # prints "-" otherwise prints "|"
    for i in range(5):
        for j in range(5):

            if (i % 2 == 0):
                if (mat[i][j] == 1):
                    print('', end = '-')
                else:
                    print('', end = ' ')
            else:
                if (mat[i][j] == 1):
                    print('', end = '|')
                else:
                    print('', end = ' ')

        print()

def digit0():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

def digit1():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 1, 0, 0 ],
            [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 1, 0, 0 ],
            [ 0, 0, 0, 0, 0 ] ]

    prints(mat)

def digit2():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

def digit3():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

def digit4():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 0, 0, 0, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ] ]

    prints(mat)

def digit5():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

def digit6():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

def digit7():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ] ]

    prints(mat)

def digit8():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

def digit9():

    # In matrix 0 used for space
    # and 1 for either - or |
    mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ]

    prints(mat)

# Function to check number
def checkDigit(num):

    # For digit 0
    if (num == 0):
        digit0()

    # For digit 1
    elif (num == 1):
        digit1()

    # For digit 2
    elif (num == 2):
        digit2()

    # For digit 3
    elif (num == 3):
        digit3()

    # For digit 4
    elif (num == 4):
        digit4()

    # For digit 5
    elif (num == 5):
        digit5()

    # For digit 6
    elif (num == 6):
        digit6()

    # For digit 7
    elif (num == 7):
        digit7()

    # For digit 8
    elif (num == 8):
        digit8()

    # For digit 9
    elif (num == 9):
        digit9()

# Driver code
if __name__=='__main__':

    # Input a number
    num = 9

    # Function call to check digit
    checkDigit(num)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print
// number in digital form
using System;

class GFG {

    // Function to print numbers
    static void print(int [,]mat)
    {

        // If in matrix row number is even
        // then print "-" otherwise print "|"
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                if (i % 2 == 0) {
                    if (mat[i,j] == 1)
                        Console.Write("-");
                    else
                        Console.Write(" ");
                }
                else {
                    if (mat[i,j] == 1)
                        Console.Write("|");
                    else
                        Console.Write(" ");
                }
            }

            Console.WriteLine();
        }
    }

    static void digit0()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    static void digit1()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 0, 0, 0, 0 },
                        { 0, 0, 1, 0, 0 },
                        { 0, 0, 0, 0, 0 },
                        { 0, 0, 1, 0, 0 },
                        { 0, 0, 0, 0, 0 } };
        print(mat);
    }

    static void digit2()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    static void digit3()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    static void digit4()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 0, 0, 0, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 } };
        print(mat);
    }

    static void digit5()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    static void digit6()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    static void digit7()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 0, 0 } };
        print(mat);
    }

    static void digit8()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    static void digit9()
    {

        // In matrix 0 used for space
        // and 1 for either - or |
        int [ ,]mat = { { 0, 1, 0, 1, 0 },
                        { 1, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 0, 0, 0, 1 },
                        { 0, 1, 0, 1, 0 } };
        print(mat);
    }

    // Function to check number
    static void checkDigit(int num)
    {

        // for digit 0
        if (num == 0)
            digit0();

        // for digit 1
        else if (num == 1)
            digit1();

        // for digit 2
        else if (num == 2)
            digit2();

        // for digit 3
        else if (num == 3)
            digit3();

        // for digit 4
        else if (num == 4)
            digit4();

        // for digit 5
        else if (num == 5)
            digit5();

        // for digit 6
        else if (num == 6)
            digit6();

        // for digit 7
        else if (num == 7)
            digit7();

        // for digit 8
        else if (num == 8)
            digit8();

        // for digit 9
        else if (num == 9)
            digit9();
    }

    // Driver program
    public static void Main ()
    {

        // Input a number
        int num = 9;

        // function call to check digit
        checkDigit(num);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to prints
// number in digital form

// Function to print numbers
function printnum(array $mat)
{
    // If in matrix row number is even
    // then print "-" otherwise print "|"
    for ($i = 0; $i < 5; $i++)
    {
        for ($j = 0; $j < 5; $j++)
        {
            if ($i % 2 == 0)
            {
                if ($mat[$i][$j] == 1)
                    echo "-";
                else
                    echo " ";
            }
            else
            {
                if ($mat[$i][$j] == 1)
                    echo "|";
                else
                    echo " ";
            }
        }
        echo "\n";
    }
}

function digit0()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat= array(array( 0, 1, 0, 1, 0 ),
                array( 1, 0, 0, 0, 1 ),
                array( 0, 0, 0, 0, 0 ),
                array( 1, 0, 0, 0, 1 ),
                array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

function digit1()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat = array(array( 0, 0, 0, 0, 0 ),
                 array( 0, 0, 1, 0, 0 ),
                 array( 0, 0, 0, 0, 0 ),
                 array( 0, 0, 1, 0, 0 ),
                 array( 0, 0, 0, 0, 0 ));
    printnum($mat);
}

function digit2()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat= array(array( 0, 1, 0, 1, 0 ),
                array( 0, 0, 0, 0, 1 ),
                array( 0, 1, 0, 1, 0 ),
                array( 1, 0, 0, 0, 0 ),
                array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

function digit3()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat= array(array( 0, 1, 0, 1, 0 ),
                array( 0, 0, 0, 0, 1 ),
                array( 0, 1, 0, 1, 0 ),
                array( 0, 0, 0, 0, 1 ),
                array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

function digit4()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat= array(array( 0, 0, 0, 0, 0 ),
                array( 1, 0, 0, 0, 1 ),
                array( 0, 1, 0, 1, 0 ),
                array( 0, 0, 0, 0, 1 ),
                array( 0, 0, 0, 0, 0 ));
    printnum($mat);
}

function digit5()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat = array(array( 0, 1, 0, 1, 0 ),
                 array( 1, 0, 0, 0, 0 ),
                 array( 0, 1, 0, 1, 0 ),
                 array( 0, 0, 0, 0, 1 ),
                 array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

function digit6()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat = array(array( 0, 1, 0, 1, 0 ),
                 array( 1, 0, 0, 0, 0 ),
                 array( 0, 1, 0, 1, 0 ),
                 array( 1, 0, 0, 0, 1 ),
                 array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

function digit7()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat = array(array( 0, 1, 0, 1, 0 ),
                 array( 0, 0, 0, 0, 1 ),
                 array( 0, 0, 0, 0, 0 ),
                 array( 0, 0, 0, 0, 1 ),
                 array( 0, 0, 0, 0, 0 ) );
    printnum($mat);
}

function digit8()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat = array(array( 0, 1, 0, 1, 0 ),
                 array( 1, 0, 0, 0, 1 ),
                 array( 0, 1, 0, 1, 0 ),
                 array( 1, 0, 0, 0, 1 ),
                 array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

function digit9()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    $mat = array(array( 0, 1, 0, 1, 0 ),
                 array( 1, 0, 0, 0, 1 ),
                 array( 0, 1, 0, 1, 0 ),
                 array( 0, 0, 0, 0, 1 ),
                 array( 0, 1, 0, 1, 0 ));
    printnum($mat);
}

// Function to check number
function checkDigit($num)
{
    // for digit 0
    if ($num == 0)
        digit0();

    // for digit 1
    else if ($num == 1)
        digit1();

    // for digit 2
    else if ($num == 2)
        digit2();

    // for digit 3
    else if ($num == 3)
        digit3();

    // for digit 4
    else if ($num == 4)
        digit4();

    // for digit 5
    else if ($num == 5)
        digit5();

    // for digit 6
    else if ($num == 6)
        digit6();

    // for digit 7
    else if ($num == 7)
        digit7();

    // for digit 8
    else if ($num == 8)
        digit8();

    // for digit 9
    else if ($num == 9)
        digit9();
}

// Driver code
$num = 9;
checkDigit($num);

// This code is contributed by Mithun Kumar
?>
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to print numbers
function print(mat)
{
    // If in matrix row number is even then print "-"
    // otherwise print "|"
    for (var i = 0; i < 5; i++) {
        for (var j = 0; j < 5; j++) {
            if (i % 2 == 0) {
                if (mat[i][j] == 1)
                    document.write("-");
                else
                    document.write(" ");
            }
            else {
                if (mat[i][j] == 1)
                    document.write(" |");
                else
                    document.write(" ");
            }
        }
        document.write("<br>");
    }
}
function digit0()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}
function digit1()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 1, 0, 0 ],
            [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 1, 0, 0 ],
            [ 0, 0, 0, 0, 0 ] ];
    print(mat);
}
function digit2()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}
function digit3()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}
function digit4()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 0, 0, 0, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ] ];
    print(mat);
}
function digit5()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}
function digit6()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}
function digit7()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 0, 0, 0, 0 ] ];
    print(mat);
}
function digit8()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}
function digit9()
{
    // In matrix 0 used for space
    // and 1 for either - or |
    var mat = [ [ 0, 1, 0, 1, 0 ],
            [ 1, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ],
            [ 0, 0, 0, 0, 1 ],
            [ 0, 1, 0, 1, 0 ] ];
    print(mat);
}

// Function to check number
function checkDigit(num)
{
    // for digit 0
    if (num == 0)
        digit0();

    // for digit 1
    else if (num == 1)
        digit1();

    // for digit 2
    else if (num == 2)
        digit2();

    // for digit 3
    else if (num == 3)
        digit3();

    // for digit 4
    else if (num == 4)
        digit4();

    // for digit 5
    else if (num == 5)
        digit5();

    // for digit 6
    else if (num == 6)
        digit6();

    // for digit 7
    else if (num == 7)
        digit7();

    // for digit 8
    else if (num == 8)
        digit8();

    // for digit 9
    else if (num == 9)
        digit9();
}

// Driver program
// Input a number
var num = 9;

// function call to check digit
checkDigit(num);

// This code is contributed by Shubham Singh
</script>
```

**Output:** 

```
 - - 
|   |
 - - 
    |
 - -
```