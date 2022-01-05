# 第一元素为奇数的二维矩阵的列的和

> 原文:[https://www . geesforgeks . org/a-2-d-矩阵的列总和-其中第一个元素是奇数/](https://www.geeksforgeeks.org/sum-of-columns-of-a-2-d-matrix-where-first-element-is-odd/)

给定一个矩阵 **mat[][]** ，任务是打印列的**和，其中**第一个元素是奇数**。**

**示例:**

> **输入:** mat[][] = {
> {8，2，3，5}，
> {9，8，7，6}，
> {1，2，5，5} }
> **输出:** 31
> 只有**第三**和**第四**列以奇数元素开始。
> 和，和= 3 + 7 + 5 + 5 + 6 + 5 = 31
> 
> **输入:** mat[][] = {
> {10，80，20，12，40}，
> {10，21，23，45，29}，
> {19，18，17，16，15}，
> {10，11，12，13，14} }
> **输出:** -1

**方法:**初始化 **sum = 0** 并开始遍历第一行。如果第一行中的任何元素是奇数，则将该列的所有元素相加。打印最后的**和**。

下面是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the sum of those columns
// of a given matrix that start with an odd element
int sumColumns(int arr[][4], int r, int c)
{

    // Initialize sum to 0
    int sum = 0;

    // Traverse through all the elements of the first row
    for (int j = 0; j < c; j++)
    {
        // If the element is odd
        if (arr[0][j] % 2 != 0)
        {
            // Add all the elements of that column
            for (int i = 0; i < r; i++)
                sum += arr[i][j];
        }

    }

    // Return the sum
    return sum;

}

// Driver code
int main()
{
int arr[3][4] = {{8, 2, 3, 5},{9, 8, 7, 6}, {1, 2, 5, 5}};
int r = sizeof(arr)/sizeof(arr[0]);
int c = sizeof(arr[0])/sizeof(int);
cout<<(sumColumns(arr, 3, 4));
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the sum of those columns
// of a given matrix that start with an odd element
static int sumColumns(int arr[][], int r, int c)
{

    // Initialize sum to 0
    int sum = 0;

    // Traverse through all the
    // elements of the first row
    for (int j = 0; j < c; j++)
    {
        // If the element is odd
        if (arr[0][j] % 2 != 0)
        {
            // Add all the elements of that column
            for (int i = 0; i < r; i++)
                sum += arr[i][j];
        }
    }

    // Return the sum
    return sum;
}

// Driver code
public static void main (String[] args)
{
    int arr[][] = {{8, 2, 3, 5},{9, 8, 7, 6}, {1, 2, 5, 5}};
    System.out.println(sumColumns(arr, 3, 4));
}
}

// This code is contributed by
// shs..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of those columns
# of a given matrix that start with an odd element
def sumColumns(arr, r, c):

    # Initialize sum to 0
    sum = 0

    # Traverse through all the elements of the first row
    for j in range(c):

        # If the element is odd
        if (arr[0][j] % 2 != 0):

            # Add all the elements of that column
            for i in range(r):
                sum += arr[i][j]

    # Return the sum
    return sum

# Driver code
arr = [ [8, 2, 3, 5], [9, 8, 7, 6], [1, 2, 5, 5] ]
r = len(arr)
c = len(arr[0])
print(sumColumns(arr, r, c))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the sum of those columns
    // of a given matrix that start with an odd element
    static int sumColumns(int [,]arr, int r, int c)
    {

        // Initialize sum to 0
        int sum = 0;

        // Traverse through all the
        // elements of the first row
        for (int j = 0; j < c; j++)
        {
            // If the element is odd
            if (arr[0, j] % 2 != 0)
            {
                // Add all the elements of that column
                for (int i = 0; i < r; i++)
                    sum += arr[i, j];
            }
        }

        // Return the sum
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int [,]arr= {{8, 2, 3, 5}, {9, 8, 7, 6}, {1, 2, 5, 5}};
        Console.WriteLine(sumColumns(arr, 3, 4));
    }
}

// This code is contributed by aishwarya.27
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the sum of those
// columns of a given matrix that start
// with an odd element
function sumColumns($arr, $r, $c)
{

    // Initialize sum to 0
    $sum = 0;

    // Traverse through all the elements
    // of the first row
    for ($j = 0; $j < $c; $j++)
    {
        // If the element is odd
        if ($arr[0][$j] % 2 != 0)
        {
            // Add all the elements of that column
            for ($i = 0; $i < $r; $i++)
                $sum += $arr[$i][$j];
        }
    }

    // Return the sum
    return $sum;
}

// Driver code
$arr = array(array(8, 2, 3, 5),
             array(9, 8, 7, 6),
             array(1, 2, 5, 5));

$r = sizeof($arr);
$c = sizeof($arr[0]);

echo (sumColumns($arr, $r, $c));

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of those columns
// of a given matrix that start with an odd element
function sumColumns(arr, r, c)
{

    // Initialize sum to 0
    var sum = 0;

    // Traverse through all the elements of the first row
    for (var j = 0; j < c; j++)
    {
        // If the element is odd
        if (arr[0][j] % 2 != 0)
        {
            // Add all the elements of that column
            for (var i = 0; i < r; i++)
                sum += arr[i][j];
        }

    }

    // Return the sum
    return sum;

}

// Driver code

var arr = [[8, 2, 3, 5],[9, 8, 7, 6], [1, 2, 5, 5]];
var r = arr.length;
var c = arr[0].length;
document.write(sumColumns(arr, 3, 4));

</script>
```

**Output:** 

```
31
```