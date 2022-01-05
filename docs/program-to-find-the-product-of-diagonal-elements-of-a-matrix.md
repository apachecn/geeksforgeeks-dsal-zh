# 求矩阵对角元素乘积的程序

> 原文:[https://www . geesforgeks . org/program-to-find-矩阵对角元素的乘积/](https://www.geeksforgeeks.org/program-to-find-the-product-of-diagonal-elements-of-a-matrix/)

给定一个 N * N 矩阵，任务是求左右对角线元素的乘积。
**例:**

```
Input: arr[] = 1 2 3 4
               5 6 7 8 
               9 7 4 2
               2 2 2 1
Output: 9408
Explanation:
Product of left diagonal = 1 * 4 * 6 * 1 = 24
Product of right diagonal = 4 * 7 * 7 * 2 = 392
Total product = 24 * 392 = 9408

Input: arr[] = 2 1 2 1 2
               1 2 1 2 1
               2 1 2 1 2
               1 2 1 2 1
               2 1 2 1 2  
Output : 512
Explanation:
Product of left diagonal = 2 * 2 * 2 * 2 * 2 = 32
Product of right diagonal = 2 * 2 * 2 * 2 * 2 = 32
But we have a common element in this case so
Total product = (32 * 32)/2  = 512
```

**进场:**

*   我们需要找出矩阵的主对角线和次对角线元素。请参考本文中的【[程序打印矩阵对角线](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix/)】

*   在这种方法中，我们使用一个循环，即一个循环来计算主对角线和次对角线的乘积
*   奇数矩阵用中间元素除答案

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ Program to find the Product
// of diagonal elements of a matrix

#include <bits/stdc++.h>
using namespace std;

// Function to find the product of diagonals
int productDiagonals(int arr[][100], int n)
{

    int product = 1;
    // loop for calculating product of both
    // the principal and secondary diagonals
    for (int i = 0; i < n; i++) {

        // For principal diagonal index of row
        // is equal to index of column
        product = product * arr[i][i];

        // For secondary diagonal index
        // of column is n-(index of row)-1
        product = product * arr[i][n - i - 1];
    }

    // Divide the answer by middle element for
    // matrix of odd size
    if (n % 2 == 1) {
        product = product / arr[n / 2][n / 2];
    }

    return product;
}

// Driver code
int main()
{
    int arr1[100][100] = { { 1, 2, 3, 4 },
                           { 5, 6, 7, 8 },
                           { 9, 7, 4, 2 },
                           { 2, 2, 2, 1 } };
    // Function calling
    cout << productDiagonals(arr1, 4) << endl;

    int arr2[100][100] = { { 2, 1, 2, 1, 2 },
                           { 1, 2, 1, 2, 1 },
                           { 2, 1, 2, 1, 2 },
                           { 1, 2, 1, 2, 1 },
                           { 2, 1, 2, 1, 2 } };
    // Function calling
    cout << productDiagonals(arr2, 5) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the Product
// of diagonal elements of a matrix
import java.util.*;

class GFG
{

// Function to find the product of diagonals
static int productDiagonals(int arr[][], int n)
{

    int product = 1;
    // loop for calculating product of both
    // the principal and secondary diagonals
    for (int i = 0; i < n; i++)
    {

        // For principal diagonal index of row
        // is equal to index of column
        product = product * arr[i][i];

        // For secondary diagonal index
        // of column is n-(index of row)-1
        product = product * arr[i][n - i - 1];
    }

    // Divide the answer by middle element for
    // matrix of odd size
    if (n % 2 == 1)
    {
        product = product / arr[n / 2][n / 2];
    }

    return product;
}

// Driver code
public static void main(String[] args)
{
    int arr1[][] = { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 9, 7, 4, 2 },
                        { 2, 2, 2, 1 } };
    // Function calling
    System.out.print(productDiagonals(arr1, 4) + "\n");

    int arr2[][] = { { 2, 1, 2, 1, 2 },
                        { 1, 2, 1, 2, 1 },
                        { 2, 1, 2, 1, 2 },
                        { 1, 2, 1, 2, 1 },
                        { 2, 1, 2, 1, 2 } };
    // Function calling
    System.out.print(productDiagonals(arr2, 5) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Program to find the Product
# of diagonal elements of a matrix

# Function to find the product of diagonals
def productDiagonals(arr, n):

    product = 1;

    # loop for calculating product of both
    # the principal and secondary diagonals
    for i in range(n):

        # For principal diagonal index of row
        # is equal to index of column
        product = product * arr[i][i];

        # For secondary diagonal index
        # of column is n-(index of row)-1
        product = product * arr[i][n - i - 1];

    # Divide the answer by middle element for
    # matrix of odd size
    if (n % 2 == 1):
        product = product // arr[n // 2][n // 2];

    return product;

# Driver code
if __name__ == '__main__':
    arr1 = [[ 1, 2, 3, 4 ],[ 5, 6, 7, 8 ],
            [ 9, 7, 4, 2 ],[ 2, 2, 2, 1 ]];

    # Function calling
    print(productDiagonals(arr1, 4));

    arr2 = [[ 2, 1, 2, 1, 2 ],[ 1, 2, 1, 2, 1 ],
            [ 2, 1, 2, 1, 2 ],[ 1, 2, 1, 2, 1 ],
            [ 2, 1, 2, 1, 2 ]];

    # Function calling
    print(productDiagonals(arr2, 5));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# Program to find the Product
// of diagonal elements of a matrix
using System;

class GFG
{

// Function to find the product of diagonals
static int productDiagonals(int [,]arr, int n)
{

    int product = 1;

    // loop for calculating product of both
    // the principal and secondary diagonals
    for (int i = 0; i < n; i++)
    {

        // For principal diagonal index of row
        // is equal to index of column
        product = product * arr[i,i];

        // For secondary diagonal index
        // of column is n-(index of row)-1
        product = product * arr[i,n - i - 1];
    }

    // Divide the answer by middle element for
    // matrix of odd size
    if (n % 2 == 1)
    {
        product = product / arr[n / 2,n / 2];
    }

    return product;
}

// Driver code
public static void Main(String[] args)
{
    int [,]arr1 = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 7, 4, 2 },
                    { 2, 2, 2, 1 } };

    // Function calling
    Console.Write(productDiagonals(arr1, 4) + "\n");

    int [,]arr2 = { { 2, 1, 2, 1, 2 },
                    { 1, 2, 1, 2, 1 },
                    { 2, 1, 2, 1, 2 },
                    { 1, 2, 1, 2, 1 },
                    { 2, 1, 2, 1, 2 } };

    // Function calling
    Console.Write(productDiagonals(arr2, 5) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program to find the Product
// of diagonal elements of a matrix

// Function to find the product of diagonals
function productDiagonals(arr, n)
{

    var product = 1;
    // loop for calculating product of both
    // the principal and secondary diagonals
    for (var i = 0; i < n; i++) {

        // For principal diagonal index of row
        // is equal to index of column
        product = product * arr[i][i];

        // For secondary diagonal index
        // of column is n-(index of row)-1
        product = product * arr[i][n - i - 1];
    }

    // Divide the answer by middle element for
    // matrix of odd size
    if (n % 2 == 1) {
        product =
        product / arr[parseInt(n / 2)][parseInt(n / 2)];
    }

    return product;
}

// Driver code
var arr1 = [ [ 1, 2, 3, 4 ],
                       [ 5, 6, 7, 8 ],
                       [ 9, 7, 4, 2 ],
                       [ 2, 2, 2, 1 ] ];
// Function calling
document.write( productDiagonals(arr1, 4) + "<br>");
var arr2 = [ [ 2, 1, 2, 1, 2 ],
                       [ 1, 2, 1, 2, 1 ],
                       [ 2, 1, 2, 1, 2 ],
                       [ 1, 2, 1, 2, 1 ],
                       [ 2, 1, 2, 1, 2 ] ];
// Function calling
document.write( productDiagonals(arr2, 5));

</script>
```

**Output:** 

```
9408
512
```

**时间复杂度:** O(N)