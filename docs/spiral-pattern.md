# 螺旋图案

> 原文:[https://www.geeksforgeeks.org/spiral-pattern/](https://www.geeksforgeeks.org/spiral-pattern/)

给定数字 N，任务是打印以下图案:-

**示例:**

```
Input : N = 4
Output : 4 4 4 4 4 4 4
         4 3 3 3 3 3 4
         4 3 2 2 2 3 4
         4 3 2 1 2 3 4
         4 3 2 2 2 3 4
         4 3 3 3 3 3 4
         4 4 4 4 4 4 4

Input : N = 2
Output : 2 2 2
         2 1 2
         2 2 2
```

**方法 1:** 常见的观察是这样形成的正方形将具有(2*N-1)x(2*N-1)的大小。用 N 填充第一行和第一列，最后一行和第一列，然后逐渐减少 N，类似地填充剩余的行和列。填充 2 行 2 列后，每次减少 N。

下面是上述方法的实现:

## C++

```
// C++ program to print the
// spiral pattern
#include <bits/stdc++.h>
using namespace std;

// Function to print the pattern
void pattern(int value)
{
    // Declare a square matrix
    int row = 2 * value - 1;
    int column = 2 * value - 1;
    int arr[row][column];

    int i, j, k;

    for (k = 0; k < value; k++) {

        // store the first row
        // from 1st column to last column
        j = k;
        while (j < column - k) {
            arr[k][j] = value - k;
            j++;
        }

        // store the last column
        // from top to bottom
        i = k + 1;
        while (i < row - k) {
            arr[i][row - 1 - k] = value - k;
            i++;
        }

        // store the last row
        // from last column to 1st column
        j = column - k - 2;
        while (j >= k) {
            arr[column - k - 1][j] = value - k;
            j--;
        }

        // store the first column
        // from bottom to top
        i = row - k - 2;
        while (i > k) {
            arr[i][k] = value - k;
            i--;
        }
    }

    // print the pattern
    for (i = 0; i < row; i++) {
        for (j = 0; j < column; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int n = 5;
    pattern(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// the spiral pattern
class GFG {

    // Function to print the pattern
    static void pattern(int value)
    {
        // Declare a square matrix
        int row = 2 * value - 1;
        int column = 2 * value - 1;
        int[][] arr = new int[row][column];

        int i, j, k;

        for (k = 0; k < value; k++) {

            // store the first row
            // from 1st column to last column
            j = k;
            while (j < column - k) {
                arr[k][j] = value - k;
                j++;
            }

            // store the last column
            // from top to bottom
            i = k + 1;
            while (i < row - k) {
                arr[i][row - 1 - k] = value - k;
                i++;
            }

            // store the last row
            // from last column
            // to 1st column
            j = column - k - 2;
            while (j >= k) {
                arr[column - k - 1][j] = value - k;
                j--;
            }

            // store the first column
            // from bottom to top
            i = row - k - 2;
            while (i > k) {
                arr[i][k] = value - k;
                i--;
            }
        }

        // print the pattern
        for (i = 0; i < row; i++) {
            for (j = 0; j < column; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        pattern(n);
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to print
# the spiral pattern

# Function to print the pattern
def pattern(value):

    # Declare a square matrix
    row = 2 * value - 1
    column = 2 * value - 1
    arr = [[0 for i in range(row)]
              for j in range (column)]

    for k in range( value):

        # store the first row
        # from 1st column to
        # last column
        j = k
        while (j < column - k):
            arr[k][j] = value - k
            j += 1

        # store the last column
        # from top to bottom
        i = k + 1
        while (i < row - k):
            arr[i][row - 1 - k] = value - k
            i += 1

        # store the last row
        # from last column
        # to 1st column
        j = column - k - 2
        while j >= k :
            arr[column - k - 1][j] = value - k
            j -= 1

        # store the first column
        # from bottom to top
        i = row - k - 2
        while i > k :
            arr[i][k] = value - k
            i -= 1

    # print the pattern
    for i in range(row):
        for j in range(column):
            print(arr[i][j], end = " ")
        print()

# Driver code
if __name__ == "__main__":
    n = 5
    pattern(n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print
// the spiral pattern
using System;

class GFG {

    // Function to print the pattern
    static void pattern(int value)
    {

        // Declare a square matrix
        int row = 2 * value - 1;
        int column = 2 * value - 1;
        int[, ] arr = new int[row, column];

        int i, j, k;

        for (k = 0; k < value; k++) {

            // store the first row
            // from 1st column to
            // last column
            j = k;
            while (j < column - k) {
                arr[k, j] = value - k;
                j++;
            }

            // store the last column
            // from top to bottom
            i = k + 1;
            while (i < row - k) {
                arr[i, row - 1 - k] = value - k;
                i++;
            }

            // store the last row
            // from last column
            // to 1st column
            j = column - k - 2;
            while (j >= k) {
                arr[column - k - 1, j] = value - k;
                j--;
            }

            // store the first column
            // from bottom to top
            i = row - k - 2;
            while (i > k) {
                arr[i, k] = value - k;
                i--;
            }
        }

        // print the pattern
        for (i = 0; i < row; i++) {
            for (j = 0; j < column; j++) {
                Console.Write(arr[i, j] + " ");
            }
            Console.Write("\n");
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        pattern(n);
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the spiral pattern

// Function to print the pattern
function pattern($value)
{
    // Declare a square matrix
    $row = 2 * $value - 1;
    $column = 2 * $value - 1;
    $arr = array(array());

    for ($k = 0; $k < $value; $k++)
    {

        // store the first row
        // from 1st column to
        // last column
        $j = $k;
        while ($j < $column - $k)
        {
            $arr[$k][$j] = $value - $k;
            $j++;
        }

        // store the last column
        // from top to bottom
        $i = $k + 1;
        while ($i < $row - $k)
        {
            $arr[$i][$row - 1 - $k] = $value - $k;
            $i++;
        }

        // store the last row
        // from last column
        // to 1st column
        $j = $column - $k - 2;
        while ($j >= $k)
        {
            $arr[$column - $k - 1][$j] = $value - $k;
            $j--;
        }

        // store the first column
        // from bottom to top
        $i = $row - $k - 2;
        while ($i > $k)
        {
            $arr[$i][$k] = $value - $k;
            $i--;
        }
    }

    // print the pattern
    for ($i = 0; $i < $row; $i++)
    {
        for ($j = 0; $j < $column; $j++)
        {
            echo $arr[$i][$j] . " ";
        }
        echo "\n";
    }
}

// Driver code
$n = 5;
pattern($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to print the
// spiral pattern

// Function to print the pattern
function pattern(value)
{

    // Declare a square matrix
    let row = 2 * value - 1;
    let column = 2 * value - 1;
    let arr = new Array(row);

    for(let i = 0; i < row; i++)
    {
        arr[i] = new Array(column);
       }

    let i, j, k;

    for(k = 0; k < value; k++)
    {

        // Store the first row
        // from 1st column to last column
        j = k;

        while (j < column - k)
        {
            arr[k][j] = value - k;
            j++;
        }

        // Store the last column
        // from top to bottom
        i = k + 1;
        while (i < row - k)
        {
            arr[i][row - 1 - k] = value - k;
            i++;
        }

        // Store the last row
        // from last column to 1st column
        j = column - k - 2;
        while (j >= k)
        {
            arr[column - k - 1][j] = value - k;
            j--;
        }

        // Store the first column
        // from bottom to top
        i = row - k - 2;
        while (i > k)
        {
            arr[i][k] = value - k;
            i--;
        }
    }

    // Print the pattern
    for(i = 0; i < row; i++)
    {
        for(j = 0; j < column; j++)
        {
            document.write(arr[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver code
let n = 5;

pattern(n);

// This code is contributed by subham348

</script>
```

**Output:** 

```
5 5 5 5 5 5 5 5 5 
5 4 4 4 4 4 4 4 5 
5 4 3 3 3 3 3 4 5 
5 4 3 2 2 2 3 4 5 
5 4 3 2 1 2 3 4 5 
5 4 3 2 2 2 3 4 5 
5 4 3 3 3 3 3 4 5 
5 4 4 4 4 4 4 4 5 
5 5 5 5 5 5 5 5 5
```

**方法 2:** 从 **i = 1** 和 **j = 1** 开始索引，可以观察到所需矩阵的每个值都将是**max(ABS(I–n)，ABS(j–n)+1**。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <algorithm>
#include <iostream>
using namespace std;

// Function to print the required pattern
void pattern(int n)
{

    // Calculating boundary size
    int p = 2 * n - 1;

    for (int i = 1; i <= p; i++) {
        for (int j = 1; j <= p; j++) {

            // Printing the values
            cout << max(abs(i - n), abs(j - n)) + 1 << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int n = 5;

    pattern(n);

    return 0;
}
// This code is contributed by : Vivek kothari
```

## C

```
// C implementation of the approach
#include <stdio.h>
#include <stdlib.h>

// Function Declaration
int max(int, int);

// Function to print the required pattern
void pattern(int n)
{

    // Calculating boundary size
    int size = 2 * n - 1;

    for(int i = 1; i <= size; i++)
    {
        for(int j = 1; j <= size; j++)
        {

            // Printing the values
            printf("%d ", max(abs(i - n),
                              abs(j - n)) + 1);
        }
        printf("\n");
    }
}

// Function to return maximum value
int max(int val1, int val2)
{
    if (val1 > val2)
        return val1;

    return val2;
}

// Driver code
int main()
{
    int n = 5;

    pattern(n);

    return 0;
}

// This code is contributed by Yuvaraj R
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function to print the required pattern
public static void pattern(int n)
{

    // Calculating boundary size
    int size = 2 * n - 1;

    for(int i = 1; i <= size; i++)
    {
        for(int j = 1; j <= size; j++)
        {

            // Printing the values
            System.out.print(Math.max(
                Math.abs(i - n),
                Math.abs(j - n)) + 1 + " ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    pattern(n);
}
}

// This code is contributed by Yuvaraj R
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the required pattern
def pattern(n):

    # Calculating boundary size
    p = 2 * n - 1
    for i in range(1, p + 1):
        for j in range(1, p + 1):

            # Printing the values
            print(max(abs(i - n), abs(j - n)) + 1, " ", end="")
        print()

# Driver code
n = 5
pattern(n)

# This code is contributed by subhammahato348
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to print the required pattern
static void pattern(int n)
{

    // Calculating boundary size
    int size = 2 * n - 1;

    for(int i = 1; i <= size; i++)
    {
        for(int j = 1; j <= size; j++)
        {

            // Printing the values
            Console.Write(Math.Max(Math.Abs(i - n),
                                   Math.Abs(j - n)) +
                                   1 + " ");
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main()
{
    int n = 5;

    pattern(n);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the required pattern
function pattern(n)
{

    // Calculating boundary size
    let p = 2 * n - 1;

    for (let i = 1; i <= p; i++) {
        for (let j = 1; j <= p; j++) {

            // Printing the values
            document.write((Math.max(Math.abs(i - n),
                        Math.abs(j - n)) + 1) + " ");
        }
        document.write("<br>");
    }
}

// Driver code
let n = 5;

pattern(n);

</script>
```

**Output**

```
5 5 5 5 5 5 5 5 5 
5 4 4 4 4 4 4 4 5 
5 4 3 3 3 3 3 4 5 
5 4 3 2 2 2 3 4 5 
5 4 3 2 1 2 3 4 5 
5 4 3 2 2 2 3 4 5 
5 4 3 3 3 3 3 4 5 
5 4 4 4 4 4 4 4 5 
5 5 5 5 5 5 5 5 5 
```