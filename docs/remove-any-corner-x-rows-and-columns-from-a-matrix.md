# 从矩阵中移除任意角 X 行和列

> 原文:[https://www . geesforgeks . org/remove-any-corner-x-row-and-columns-from-a-matrix/](https://www.geeksforgeeks.org/remove-any-corner-x-rows-and-columns-from-a-matrix/)

给定一个 **NxN** 矩阵和一个整数 **X** 。任务是从 **NxN** 矩阵中移除 **X** 行和 **X** 列。

*   **从矩阵中删除前 X 行和列。**

**示例:**

```
Input: n = 4, 
       arr[][] = {{20, 2, 10, 16},
                  {20, 17, 11, 6},
                  {14, 16, 1, 3},
                  {10, 2, 17, 4}}, 
       x = 2
Output:
1 3
17 4

Explanation:
Here the value of X is 2.
So remove the first 2 rows 
and the first 2 columns from the matrix. 
Hence the output is
1 3 
17 4
```

**简单方法:**

*   跳过前 **x** 行和列，打印矩阵中剩余的元素。
*   从**第 XT**行开始，打印到**第 n-1**行。
*   从**第 XT**列开始，一直打印到**第 n-1**列。

**实施:**

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to remove first x
// rows and columns from an array
void remove_X_Rows_and_Columns(int* a, int n, int x)
{

    cout << "\nRemoving First " << x
         << " rows and columns:\n";

    // Start from the xth row
    // and print till n-1th row
    for (int i = x; i < n; i++) {

        // Start from the xth column
        // and print till the n-1th column
        for (int j = x; j < n; j++) {

            // Accessing the array using pointers
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

// Print the matrix
void printMatrix(int* a, int n)
{

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

int main()
{
    int n = 4;

    // get the array inputs
    int a[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    cout << "Original Matrix:\n";
    printMatrix((int*)a, n);

    int x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns((int*)a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to remove first x
// rows and columns from an array
static void remove_X_Rows_and_Columns(int a[][],
                                      int n, int x)
{
    System.out.print("\nRemoving First " + x +
                     " rows and columns:\n");

    // Start from the xth row
    // and print till n-1th row
    for(int i = x; i < n; i++)
    {

        // Start from the xth column
        // and print till the n-1th column
        for(int j = x; j < n; j++)
        {

            // Accessing the array using pointers
            System.out.print(a[i][j] + " ");
        }
        System.out.println();
    }
}

// Print the matrix
static void printMatrix(int a[][], int n)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            System.out.print(a[ i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String [] args)
{
    int n = 4;

    // Get the array inputs
    int a[][] = new int[n][n];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    System.out.println( "Original Matrix:");
    printMatrix(a, n);

    int x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to remove first x
# rows and columns from an array
def remove_X_Rows_and_Columns(a, n, x):

    print("Removing First ", x,
          " rows and columns:")

    # Start from the xth row
    # and print till n-1th row
    for i in range(x, n):

        # Start from the xth column
        # and print till the n-1th column
        for j in range(x, n):

            # Accessing the array using pointers
            print(a[i][j], end = " ")

        print()

# Print the matrix
def prMatrix(a, n):

    for i in range(n):
        for j in range(n):
            print(a[i][j], end = " ")

        print()

# Driver Code
if __name__ == '__main__':

    n = 4

    # get the array inputs
    a = [[0 for i in range(n)]
            for i in range(n)]
    for i in range(n):
        for j in range(n):
            a[i][j] = (i * 10 + j)

    # Print the matrix
    print("Original Matrix:")
    prMatrix(a, n)

    x = 2

    # passing the two dimensional
    # array using a single pointer
    remove_X_Rows_and_Columns(a, n, x)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to remove first x
// rows and columns from an array
static void remove_X_Rows_and_Columns(int[,] a, 
                                      int n, int x)
{
    Console.WriteLine("\nRemoving First " + x +
                      " rows and columns:\n");

    // Start from the xth row
    // and print till n-1th row
    for(int i = x; i < n; i++)
    {

        // Start from the xth column
        // and print till the n-1th column
        for(int j = x; j < n; j++)
        {

            // Accessing the array using pointers
            Console.Write(a[i, j] + " ");

        }
        Console.WriteLine();
    }
}

// Print the matrix
static void printMatrix(int[,] a, int n)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            Console.Write(a[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
static public void Main()
{
    int n = 4;

    // Get the array inputs
    int[,] a = new int[n, n];

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            a[i,j] = (i * 10 + j);
        }
    }

    // Print the matrix
    Console.WriteLine( "Original Matrix:");
    printMatrix(a, n);
    int x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to remove first x
// rows and columns from an array
function remove_X_Rows_and_Columns($a, $n, $x)
{
    echo "\nRemoving First ", $x,
         " rows and columns:\n";

    // Start from the xth row
    // and print till n-1th row
    for ($i = $x; $i < $n; $i++)
    {

        // Start from the xth column
        // and print till the n-1th column
        for ($j = $x; $j < $n; $j++)
        {

            // Accessing the array using pointers
            echo $a[$i][$j], " ";
        }
        echo "\n";
    }
}

// Print the matrix
function printMatrix($a, $n)
{

    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            echo $a[$i][$j], " ";
        }
        echo "\n";
    }
}

$n = 4;

// get the array inputs
$a = array(array());

for ($i = 0; $i < $n; $i++)
{
    for ($j = 0; $j < $n; $j++)
    {
        $a[$i][$j] = $i * 10 + $j;
    }
}

// Print the matrix
echo "Original Matrix:\n";
printMatrix($a, $n);

$x = 2;

// passing the two dimensional
// array using a single pointer
remove_X_Rows_and_Columns($a, $n, $x);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // javascript implementation of the above approach   
    // Function to remove first x
    // rows and columns from an array
    function remove_X_Rows_and_Columns(a , n , x) {
        document.write("<br/>Removing First " + x + " rows and columns:<br/>");

        // Start from the xth row
        // and print till n-1th row
        for (i = x; i < n; i++) {

            // Start from the xth column
            // and print till the n-1th column
            for (j = x; j < n; j++) {

                // Accessing the array using pointers
                document.write(a[i][j] + " ");
            }
            document.write("<br/>");
        }
    }

    // Print the matrix
    function printMatrix(a , n) {
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                document.write(a[i][j] + " ");
            }
            document.write("<br/>");
        }
    }

    // Driver Code

        var n = 4;

        // Get the array inputs
        var a = Array(n);
        for (i = 0; i < n; i++) {
        a[i] = Array(n).fill(0);
            for (j = 0; j < n; j++) {
                a[i][j] = (i * 10 + j);
            }
        }

        // Print the matrix
        document.write("Original Matrix:");
        printMatrix(a, n);

        var x = 2;

        // Passing the two dimensional
        // array using a single pointer
        remove_X_Rows_and_Columns(a, n, x);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
Original Matrix:
0 1 2 3 
10 11 12 13 
20 21 22 23 
30 31 32 33 

Removing First 2 rows and columns:
22 23 
32 33
```

*   **从矩阵中删除最后 X 行和列。**

**示例:**

```
Input: n = 4, 
       arr[][] = {{20, 2, 10, 16},
                  {20, 17, 11, 6},
                  {14, 16, 1, 3},
                  {10, 2, 17, 4}}, 
       x = 2
Output:
20 2
20 17

Explanation:
Here the value of X is 2.
So remove the last 2 rows and 
the last 2 columns from the matrix. 
Hence the output is
20 2
20 17
```

**简单方法**

*   跳过最后的 **x** 行和列，打印矩阵中剩余的元素。
*   从**第 0 行**开始打印，直到**第 n-XT 行**为止。
*   从**第 0 列**开始，打印至**第 n-XT**列。

**实施:**

## C++

```
#include <iostream>
using namespace std;

// Function to remove last x rows
// and columns from an array
void remove_X_Rows_and_Columns(int* a, int n, int x)
{

    cout << "\nRemoving Last " << x
         << " rows and columns:\n";

    // Start from the 0th row
    // and print till n-xth row
    for (int i = 0; i < n - x; i++) {

        // Start from the 0th column
        // and print till the n-xth column
        for (int j = 0; j < n - x; j++) {

            // Accessing the array using pointers
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

// Print the matrix
void printMatrix(int* a, int n)
{

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

int main()
{
    int n = 4;

    // get the array inputs
    int a[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    cout << "Original Matrix:\n";
    printMatrix((int*)a, n);

    int x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns((int*)a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG{

public static void remove_X_Rows_and_Columns(
    int[][] a,int n, int x)
{
    System.out.println("\nRemoving Last " + x +
                       " rows and columns:\n");

    // Start from the 0th row
    // and print till n-xth row
    for(int i = 0; i < n - x; i++)
    {

        // Start from the 0th column
        // and print till the n-xth column
        for(int j = 0; j < n - x; j++)
        {

            // Accessing the array using pointers
            System.out.print(a[i][j] + " ");
        }
        System.out.println();
    }       
}

// Print the matrix
public static void printMatrix(int[][] a, int n)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            System.out.print(a[i][j] + " ");
        }
        System.out.println();
    }       
}

// Driver code
public static void main(String[] args)
{
    int n = 4;

    // Get the array inputs
    int[][] a = new int[n][n];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    System.out.println("Original Matrix:");

    printMatrix(a, n);

    int x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);
}
}

// This code is contributed by patel2127
```

## 蟒蛇 3

```
# Function to remove last x rows
# and columns from an array
def remove_X_Rows_and_Columns(a, n, x):
    print("\nRemoving Last", x, "rows and columns:")

    # Start from the 0th row
    # and print till n-xth row
    for i in range(n - x):

        # Start from the 0th column
        # and print till the n-xth column
        for j in range(n - x):

            # Accessing the array using pointers
            print(a[i][j], end = " ")
        print()

# Print the matrix
def printMatrix(a, n):
    for i in range(n):
        for j in range(n):
            print(a[i][j], end = " ")
        print()

n = 4

# get the array inputs
a = [[0 for i in range(n)] for j in range(n)]
for i in range(n):
    for j in range(n):
        a[i][j] = (i * 10 + j)

# Print the matrix
print("Original Matrix:")
printMatrix(a, n)
x = 2

# passing the two dimensional
# array using a single pointer
remove_X_Rows_and_Columns(a, n, x)

# This code is contributed by rag2127
```

## C#

```
using System;

public class GFG{

    public static void remove_X_Rows_and_Columns(
    int[,] a,int n, int x)
{
    Console.WriteLine("\nRemoving Last " + x +
                       " rows and columns:\n");

    // Start from the 0th row
    // and print till n-xth row
    for(int i = 0; i < n - x; i++)
    {

        // Start from the 0th column
        // and print till the n-xth column
        for(int j = 0; j < n - x; j++)
        {

            // Accessing the array using pointers
            Console.Write(a[i,j] + " ");
        }
        Console.WriteLine();
    }      
}

// Print the matrix
public static void printMatrix(int[,] a, int n)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            Console.Write(a[i,j] + " ");
        }
        Console.WriteLine();
    }      
}

// Driver code

    static public void Main (){

        int n = 4;

    // Get the array inputs
    int[,] a = new int[n,n];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            a[i,j] = (i * 10 + j);
        }
    }

    // Print the matrix
    Console.WriteLine("Original Matrix:");

    printMatrix(a, n);

    int x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);

    }
}

// This code is contributed by ab2127.
```

## java 描述语言

```
<script>

// Function to remove last x rows
// and columns from an array
function remove_X_Rows_and_Columns(a, n, x)
{
    document.write("<br>Removing Last"+ x+ "rows and columns:<br>");

    // Start from the 0th row
    // and print till n-xth row
    for (let i = 0; i < n - x; i++) {

        // Start from the 0th column
        // and print till the n-xth column
        for (let j = 0; j < n - x; j++) {

            // Accessing the array using pointers
            document.write(a[i][j]+" ");
        }
        document.write("<br>")
    }
}

// Print the matrix
function printMatrix(a,n)
{
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            document.write(a[i][j]+" ");
        }
        document.write("<br>")
    }
}

let n = 4;

    // get the array inputs
    let a = new Array(n);
    for (let i = 0; i < n; i++) {
        a[i]=new Array(n);
        for (let j = 0; j < n; j++) {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    document.write("Original Matrix:<br>");
    printMatrix(a, n);

    let x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Original Matrix:
0 1 2 3 
10 11 12 13 
20 21 22 23 
30 31 32 33 

Removing Last 2 rows and columns:
0 1 
10 11
```

*   **从矩阵中删除前 X 行和后 X 列。**

**示例:**

```
Input: n = 4, 
       arr[][] = {{20, 2, 10, 16},
                  {20, 17, 11, 6},
                  {14, 16, 1, 3},
                  {10, 2, 17, 4}}, 
       x = 2
Output:
14 16
10 2

Explanation:
Here the value of X is 2.
So remove the first 2 rows 
and the last 2 columns from the matrix. 
Hence the output is
14 16
10 2
```

**简单方法**

*   跳过前 **x** 行和后 **x** 列，打印矩阵中剩余的元素。
*   从**第 XT**行开始，打印到**第 n-1**行。
*   从**第 0 列**开始，打印至**第 n-XT**列。

**实施:**

## C++

```
#include <iostream>
using namespace std;

// Function to remove first x rows
// and last x columns from an array
void remove_X_Rows_and_Columns(int* a, int n, int x)
{

    cout << "\nRemoving First " << x
         << " rows and Last " << x
         << " columns:\n";

    // Start from the xth row
    // and print till n-1th row
    for (int i = x; i < n; i++) {

        // Start from the 0th column
        // and print till the n-xth column
        for (int j = 0; j < n - x; j++) {

            // Accessing the array using pointers
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

// Print the matrix
void printMatrix(int* a, int n)
{

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

int main()
{
    int n = 4;

    // get the array inputs
    int a[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    cout << "Original Matrix:\n";
    printMatrix((int*)a, n);

    int x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns((int*)a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

// Function to remove first x rows
// and last x columns from an array
static void remove_X_Rows_and_Columns(int[][] a, int n,
                                      int x)
{

    System.out.print("\nRemoving First " + x +
                     " rows and Last " + x +
                     " columns:\n");

    // Start from the xth row
    // and print till n-1th row
    for(int i = x; i < n; i++)
    {

        // Start from the 0th column
        // and print till the n-xth column
        for(int j = 0; j < n - x; j++)
        {

            // Accessing the array using pointers
            System.out.print(a[i][j]+ " ");
        }
        System.out.println();
    }
}

// Print the matrix
static void printMatrix(int[][] a, int n)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            System.out.print(a[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 4;

    // Get the array inputs
    int [][]a = new int[n][n];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    System.out.print("Original Matrix:\n");
    printMatrix(a, n);

    int x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
using System;

public class GFG{

// Function to remove first x rows
// and last x columns from an array
static void remove_X_Rows_and_Columns(int[,] a, int n,
                                      int x)
{

    Console.Write("\nRemoving First " + x +
                     " rows and Last " + x +
                     " columns:\n");

    // Start from the xth row
    // and print till n-1th row
    for(int i = x; i < n; i++)
    {

        // Start from the 0th column
        // and print till the n-xth column
        for(int j = 0; j < n - x; j++)
        {

            // Accessing the array using pointers
            Console.Write(a[i,j]+ " ");
        }
        Console.WriteLine();
    }
}

// Print the matrix
static void printMatrix(int[,] a, int n)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            Console.Write(a[i,j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 4;

    // Get the array inputs
    int [,]a = new int[n,n];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            a[i,j] = (i * 10 + j);
        }
    }

    // Print the matrix
    Console.Write("Original Matrix:\n");
    printMatrix(a, n);

    int x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Function to remove first x rows
// and last x columns from an array
function remove_X_Rows_and_Columns(a , n,x)
{
    document.write("<br>Removing First " + x +
                     " rows and Last " + x +
                     " columns:<br>");

    // Start from the xth row
    // and print till n-1th row
    for(var i = x; i < n; i++)
    {

        // Start from the 0th column
        // and print till the n-xth column
        for(var j = 0; j < n - x; j++)
        {

            // Accessing the array using pointers
            document.write(a[i][j]+ " ");
        }
        document.write('<br>');
    }
}

// Print the matrix
function printMatrix(a , n)
{
    for(var i = 0; i < n; i++)
    {
        for(var j = 0; j < n; j++)
        {
            document.write(a[i][j] + " ");
        }
        document.write('<br>');
    }
}

// Driver code
    var n = 4;

    // Get the array inputs
    var a = Array(n).fill(0).map(x => Array(n).fill(0));
    for(var i = 0; i < n; i++)
    {
        for(var j = 0; j < n; j++)
        {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    document.write("Original Matrix:<br>");
    printMatrix(a, n);
    var x = 2;

    // Passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
Original Matrix:
0 1 2 3 
10 11 12 13 
20 21 22 23 
30 31 32 33 

Removing First 2 rows and Last 2 columns:
20 21 
30 31
```

*   **从矩阵中删除最后 X 行和前 X 列。**

**示例:**

```
Input: n = 4, 
       arr[][] = {{20, 2, 10, 16},
                  {20, 17, 11, 6},
                  {14, 16, 1, 3},
                  {10, 2, 17, 4}}, 
       x = 2
Output:
10 16
11 6

Explanation:
Here the value of X is 2.
So remove the last 2 rows and
the first 2 columns from the matrix. 
Hence the output is
10 16
11 6
```

**简单方法**

*   跳过最后的 **x** 行和第一个 **x** 列，打印矩阵中剩余的元素。
*   从**第 0 行**开始打印，直到**第 n-XT 行**为止。
*   从**第 XT**列开始，一直打印到**第 n-1**列。

**实施:**

## C++

```
#include <iostream>
using namespace std;

// Function to remove last x rows
// and first x columns from an array
void remove_X_Rows_and_Columns(int* a, int n, int x)
{

    cout << "\nRemoving Last " << x
         << " rows and First " << x
         << " columns:\n";

    // Start from the 0th row
    // and print till n-xth row
    for (int i = 0; i < n - x; i++) {

        // Start from the xth column and
        // print till the n-1th column
        for (int j = x; j < n; j++) {

            // Accessing the array using pointers
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

// Print the matrix
void printMatrix(int* a, int n)
{

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << *((a + i * n) + j) << " ";
        }
        cout << endl;
    }
}

int main()
{
    int n = 4;

    // get the array inputs
    int a[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    cout << "Original Matrix:\n";
    printMatrix((int*)a, n);

    int x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns((int*)a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

  // Function to remove last x rows
  // and first x columns from an array
  static void remove_X_Rows_and_Columns(int[][] a, int n, int x)
  {

    System.out.print("\nRemoving Last " +  x
                     + " rows and First " +  x
                     + " columns:\n");

    // Start from the 0th row
    // and print till n-xth row
    for (int i = 0; i < n - x; i++) {

      // Start from the xth column and
      // print till the n-1th column
      for (int j = x; j < n; j++) {

        // Accessing the array using pointers
        System.out.print(a[i][j]+ " ");
      }
      System.out.println();
    }
  }

  // Print the matrix
  static void printMatrix(int[][] a, int n)
  {

    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        System.out.print(a[i][j]+ " ");
      }
      System.out.println();
    }
  }

  public static void main(String[] args)
  {
    int n = 4;

    // get the array inputs
    int [][]a= new int[n][n];
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        a[i][j] = (i * 10 + j);
      }
    }

    // Print the matrix
    System.out.print("Original Matrix:\n");
    printMatrix(a, n);

    int x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);

  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Function to remove last x rows
# and first x columns from an array
def remove_X_Rows_and_Columns(a, n, x):

    print("\nRemoving Last ", x ,
          " rows and First ", x,
          " columns:")

    # Start from the 0th row
    # and print till n-xth row
    for i in range(n - x):

        # Start from the xth column and
        # print till the n-1th column
        for j in range(x, n):

            # Accessing the array using pointers
            print(a[i][j], end = " ")

        print()

# Print the matrix
def printMatrix(a, n):

    for i in range(n):
        for j in range(n):
            print(a[i][j], end = " ")

        print()

# Driver code
if __name__ == '__main__':

    n = 4

    # Get the array inputs
    a = [[0 for i in range(n)]
            for i in range(n)]

    for i in range(n):
        for j in range(n):
            a[i][j] = (i * 10 + j)

    # Print the matrix
    print("Original Matrix:")
    printMatrix(a, n)

    x = 2

    # Passing the two dimensional
    # array using a single pointer
    remove_X_Rows_and_Columns(a, n, x)

# This code is contributed by mohit kumar 29
```

## C#

```
using System;
using System.Collections.Generic;

public class GFG{

  // Function to remove last x rows
  // and first x columns from an array
  static void remove_X_Rows_and_Columns(int[,] a, int n, int x)
  {

    Console.Write("\nRemoving Last " +  x
                  + " rows and First " +  x
                  + " columns:\n");

    // Start from the 0th row
    // and print till n-xth row
    for (int i = 0; i < n - x; i++) {

      // Start from the xth column and
      // print till the n-1th column
      for (int j = x; j < n; j++) {

        // Accessing the array using pointers
        Console.Write(a[i,j]+ " ");
      }
      Console.WriteLine();
    }
  }

  // Print the matrix
  static void printMatrix(int[,] a, int n)
  {

    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        Console.Write(a[i,j]+ " ");
      }
      Console.WriteLine();
    }
  }

  public static void Main(String[] args)
  {
    int n = 4;

    // get the array inputs
    int [,]a= new int[n,n];
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        a[i,j] = (i * 10 + j);
      }
    }

    // Print the matrix
    Console.Write("Original Matrix:\n");
    printMatrix(a, n);

    int x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript implementation of above approach

    // Function to remove last x rows
    // and first x columns from an array
    function remove_X_Rows_and_Columns(a, n, x)
    {

        document.write("</br>" + "Removing Last " + x
             + " rows and First " + x
             + " columns:" + "</br>");

        // Start from the 0th row
        // and print till n-xth row
        for (let i = 0; i < n - x; i++) {

            // Start from the xth column and
            // print till the n-1th column
            for (let j = x; j < n; j++) {

                // Accessing the array using pointers
                document.write(a[i][j] + " ");
            }
            document.write("</br>");
        }
    }

    // Print the matrix
    function printMatrix(a, n)
    {

        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {
                document.write(a[i][j] + " ");
            }
            document.write("</br>");
        }
    }

    let n = 4;

    // get the array inputs
    let a = new Array(n);
    for (let i = 0; i < n; i++) {
        a[i] = new Array(n);
        for (let j = 0; j < n; j++) {
            a[i][j] = (i * 10 + j);
        }
    }

    // Print the matrix
    document.write("Original Matrix:" + "</br>");
    printMatrix(a, n);

    let x = 2;

    // passing the two dimensional
    // array using a single pointer
    remove_X_Rows_and_Columns(a, n, x);

</script>
```

**Output:** 

```
Original Matrix:
0 1 2 3 
10 11 12 13 
20 21 22 23 
30 31 32 33 

Removing Last 2 rows and First 2 columns:
2 3 
12 13
```