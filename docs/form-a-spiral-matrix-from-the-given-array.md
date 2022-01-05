# 从给定阵列形成螺旋矩阵

> 原文:[https://www . geeksforgeeks . org/form-a-spiral-matrix-from-the-then-array/](https://www.geeksforgeeks.org/form-a-spiral-matrix-from-the-given-array/)

给定一个数组，任务是形成一个螺旋矩阵

**示例:**

```
Input:
arr[] = { 1, 2, 3, 4, 5,
          6, 7, 8, 9, 10,
          11, 12, 13, 14, 15, 16 };
Output:
 1  2  3  4
 12 13 14  5
 11 16 15  6
 10  9  8  7

Input:
arr[] = { 1, 2, 3, 4, 5, 6,
          7, 8, 9, 10, 11, 12,
          13, 14, 15, 16, 17, 18 };
Output:
1   2  3  4  5 6 
14 15 16 17 18 7 
13 12 11 10  9 8
```

**做法:**这个问题正好和这个问题相反”[以螺旋形式](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)打印给定矩阵。这样做的方法是:

*   遍历给定的数组，逐个选择每个元素。
*   按照螺旋矩阵的顺序填充每个元素。
*   螺旋矩阵的顺序在 4 个循环的帮助下得以维持——左、右、上、下。
*   每个循环打印螺旋矩阵中相应的行/列。

下面是上述方法的实现:

## C++

```
// C++ program to form a Spiral Matrix
// from the given Array

#include <bits/stdc++.h>
using namespace std;

#define R 3
#define C 6

// Function to form the spiral matrix
void formSpiralMatrix(int arr[], int mat[R][C])
{
    int top = 0,
        bottom = R - 1,
        left = 0,
        right = C - 1;

    int index = 0;

    while (1) {

        if (left > right)
            break;

        // print top row
        for (int i = left; i <= right; i++)
            mat[top][i] = arr[index++];
        top++;

        if (top > bottom)
            break;

        // print right column
        for (int i = top; i <= bottom; i++)
            mat[i][right] = arr[index++];
        right--;

        if (left > right)
            break;

        // print bottom row
        for (int i = right; i >= left; i--)
            mat[bottom][i] = arr[index++];
        bottom--;

        if (top > bottom)
            break;

        // print left column
        for (int i = bottom; i >= top; i--)
            mat[i][left] = arr[index++];
        left++;
    }
}

// Function to print the spiral matrix
void printSpiralMatrix(int mat[R][C])
{

    for (int i = 0; i < R; i++) {
        for (int j = 0; j < C; j++)
            cout << mat[i][j] << " ";
        cout << '\n';
    }
}

// Driver code
int main()
{
    int arr[]
        = { 1, 2, 3, 4, 5, 6,
            7, 8, 9, 10, 11, 12,
            13, 14, 15, 16, 17, 18 };
    int mat[R][C];

    formSpiralMatrix(arr, mat);
    printSpiralMatrix(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to form a Spiral Matrix
// from the given Array
class GFG
{
    static final int R = 3 ;
    static final int C = 6;

    // Function to form the spiral matrix
    static void formSpiralMatrix(int arr[], int mat[][])
    {
        int top = 0,
            bottom = R - 1,
            left = 0,
            right = C - 1;

        int index = 0;

        while (true)
        {
            if (left > right)
                break;

            // print top row
            for (int i = left; i <= right; i++)
                mat[top][i] = arr[index++];
            top++;

            if (top > bottom)
                break;

            // print right column
            for (int i = top; i <= bottom; i++)
                mat[i][right] = arr[index++];
            right--;

            if (left > right)
                break;

            // print bottom row
            for (int i = right; i >= left; i--)
                mat[bottom][i] = arr[index++];
            bottom--;

            if (top > bottom)
                break;

            // print left column
            for (int i = bottom; i >= top; i--)
                mat[i][left] = arr[index++];
            left++;
        }
    }

    // Function to print the spiral matrix
    static void printSpiralMatrix(int mat[][])
    {
        for (int i = 0; i < R; i++)
        {
            for (int j = 0; j < C; j++)
                System.out.print(mat[i][j] + " ");
            System.out.println();
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6,
                      7, 8, 9, 10, 11, 12,
                      13, 14, 15, 16, 17, 18 };

        int mat[][] = new int[R][C];

        formSpiralMatrix(arr, mat);
        printSpiralMatrix(mat);
    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python program to form a Spiral Matrix
# from the given Array

R = 3 ;
C = 6;

# Function to form the spiral matrix
def formSpiralMatrix(arr, mat):
    top = 0;
    bottom = R - 1;
    left = 0;
    right = C - 1;

    index = 0;

    while (True):

        if(left > right):
            break;

        # print top row
        for i in range(left, right + 1):
            mat[top][i] = arr[index];
            index += 1;
        top += 1;

        if (top > bottom):
            break;

        # print right column
        for i in range(top, bottom+1):
            mat[i][right] = arr[index];
            index += 1;
        right -= 1;

        if (left > right):
            break;

        # print bottom row
        for i in range(right, left-1, -1):
            mat[bottom][i] = arr[index];
            index += 1;
        bottom -= 1;

        if (top > bottom):
            break;

        # print left column
        for i in range(bottom, top-1, -1):
            mat[i][left] = arr[index];
            index += 1;
        left += 1;
# Function to print the spiral matrix
def printSpiralMatrix(mat):
    for i in range(R):
        for j in range(C):
            print(mat[i][j],end= " ");
        print();

# Driver code
if __name__ == '__main__':
    arr = [ 1, 2, 3, 4, 5, 6,
                7, 8, 9, 10, 11, 12,
                13, 14, 15, 16, 17, 18 ];

    mat= [[0 for i in range(C)] for j in range(R)];
    formSpiralMatrix(arr, mat);
    printSpiralMatrix(mat);

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to form a Spiral Matrix
// from the given Array
using System;

class GFG
{
    static readonly int R = 3;
    static readonly int C = 6;

    // Function to form the spiral matrix
    static void formSpiralMatrix(int []arr,
                                 int [,]mat)
    {
        int top = 0,
            bottom = R - 1,
            left = 0,
            right = C - 1;

        int index = 0;

        while (true)
        {
            if (left > right)
                break;

            // print top row
            for (int i = left; i <= right; i++)
                mat[top, i] = arr[index++];
            top++;

            if (top > bottom)
                break;

            // print right column
            for (int i = top; i <= bottom; i++)
                mat[i, right] = arr[index++];
            right--;

            if (left > right)
                break;

            // print bottom row
            for (int i = right; i >= left; i--)
                mat[bottom, i] = arr[index++];
            bottom--;

            if (top > bottom)
                break;

            // print left column
            for (int i = bottom; i >= top; i--)
                mat[i, left] = arr[index++];
            left++;
        }
    }

    // Function to print the spiral matrix
    static void printSpiralMatrix(int [,]mat)
    {
        for (int i = 0; i < R; i++)
        {
            for (int j = 0; j < C; j++)
                Console.Write(mat[i, j] + " ");
            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 1, 2, 3, 4, 5, 6,
                      7, 8, 9, 10, 11, 12,
                     13, 14, 15, 16, 17, 18 };

        int [,]mat = new int[R, C];

        formSpiralMatrix(arr, mat);
        printSpiralMatrix(mat);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to form a Spiral Matrix
// from the given Array
const R = 3;
const C = 6;

// Function to form the spiral matrix
function formSpiralMatrix(arr, mat)
{
    let top = 0,
    bottom = R - 1,
    left = 0,
    right = C - 1;

    let index = 0;

    while (1)
    {

        if (left > right)
            break;

        // Print top row
        for(let i = left; i <= right; i++)
            mat[top][i] = arr[index++];

        top++;

        if (top > bottom)
            break;

        // Print right column
        for (let i = top; i <= bottom; i++)
            mat[i][right] = arr[index++];
        right--;

        if (left > right)
            break;

        // print bottom row
        for (let i = right; i >= left; i--)
            mat[bottom][i] = arr[index++];

        bottom--;

        if (top > bottom)
            break;

        // Print left column
        for(let i = bottom; i >= top; i--)
            mat[i][left] = arr[index++];

        left++;
    }
}

// Function to print the spiral matrix
function printSpiralMatrix(mat)
{
    for(let i = 0; i < R; i++)
    {
        for(let j = 0; j < C; j++)
            document.write(mat[i][j] + " ");

        document.write("<br>");
    }
}

// Driver code
let arr = [ 1, 2, 3, 4, 5, 6,
            7, 8, 9, 10, 11, 12,
            13, 14, 15, 16, 17, 18 ];

let mat = new Array(R);
for(let i = 0; i < R; i++)
    mat[i] = new Array(C);

formSpiralMatrix(arr, mat);
printSpiralMatrix(mat);

// This code is contributed by subham348

</script>
```

**Output:** 

```
1   2  3  4  5 6 
14 15 16 17 18 7 
13 12 11 10  9 8
```