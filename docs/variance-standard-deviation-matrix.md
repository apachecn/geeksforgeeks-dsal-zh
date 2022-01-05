# 矩阵的方差和标准差

> 原文:[https://www . geesforgeks . org/方差-标准差-矩阵/](https://www.geeksforgeeks.org/variance-standard-deviation-matrix/)

前提–[给定大小为 **n*n** 的矩阵，数组的平均值、方差和标准差](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)、[方差和标准差](https://www.geeksforgeeks.org/program-for-variance-and-standard-deviation-of-an-array/)、
。我们必须计算给定矩阵的方差和标准差。
**示例:**

```
Input : 1 2 3
        4 5 6
        6 6 6 
Output : variance: 3
         deviation: 1

Input : 1 2 3
        4 5 6
        7 8 9 
Output : variance: 6
         deviation: 2  
```

**说明:**
第一个**的意思是**应该是矩阵各个元素的和相加计算出来的。计算平均值后，应从矩阵的每个元素中减去它。然后对每一项进行平方，用总元素除和求出**方差**。
**偏差:**是方差的平方根。
**例:**

```
      1 2 3
      4 5 6
      7 8 9
```

此处均值为 **5** ，方差约为**6.66**T4

下面是代码实现:

## C++

```
// CPP program to find mean and
// variance of a matrix.
#include <bits/stdc++.h>
using namespace std;

// variance function declaration
int variance(int, int, int);

// Function for calculating mean
int mean(int a[][3], int n)
{
    // Calculating sum
    int sum = 0;
    for (int  i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += a[i][j];

    // Returning mean
    return sum / (n * n);
}

// Function for calculating variance
int variance(int a[][3], int n, int m)
{
    int sum = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // subtracting mean from elements
            a[i][j] -= m;

            // a[i][j] = fabs(a[i][j]);
            // squaring each terms
            a[i][j] *= a[i][j];
        }
    }

    // taking sum
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += a[i][j];   

    return sum / (n * n);
}

// driver program
int main()
{
    // declaring and initializing matrix
    int mat[3][3] = { { 1, 2, 3 },
                      { 4, 5, 6 },
                      { 7, 8, 9 } };

    // for mean
    int m = mean(mat, 3);

    // for variance
    int var = variance(mat, 3, m);

    // for standard deviation
    int dev = sqrt(var);

    // displaying variance and deviation
     cout << "Mean: " << m << "\n"
          << "Variance: " << var << "\n"
          << "Deviation: " << dev << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find mean
// and variance of a matrix.
import java.io.*;

class GFG
{
// Function for
// calculating mean
static int mean(int a[][],
                int n)
{
    // Calculating sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += a[i][j];

    // Returning mean
    return sum / (n * n);
}

// Function for
// calculating variance
static int variance(int a[][],
                    int n, int m)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // subtracting mean
            // from elements
            a[i][j] -= m;

            // a[i][j] = fabs(a[i][j]);
            // squaring each terms
            a[i][j] *= a[i][j];
        }
    }

    // taking sum
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += a[i][j];

    return sum / (n * n);
}

// Driver Code
public static void main (String[] args)
{

// declaring and
// initializing matrix
int mat[][] = {{1, 2, 3},
               {4, 5, 6},
               {7, 8, 9}};

// for mean
int m = mean(mat, 3);

// for variance
int var = variance(mat, 3, m);

// for standard
// deviation
double dev = (int)Math.sqrt(var);

// displaying variance
// and deviation
System.out.println("Mean: " + m);
System.out.println("Variance: " +
                            var);
System.out.println("Deviation: " +
                        (int)dev);
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to find mean
# and variance of a matrix.
import math;

# variance function declaration
# Function for calculating mean
def mean(a, n):

    # Calculating sum
    sum = 0;
    for i in range(n):
        for j in range(n):
            sum += a[i][j];

    # Returning mean
    return math.floor(int(sum / (n * n)));

# Function for calculating variance
def variance(a, n, m):
    sum = 0;
    for i in range(n):
        for j in range(n):

            # subtracting mean
            # from elements
            a[i][j] -= m;

            # a[i][j] = fabs(a[i][j]);
            # squaring each terms
            a[i][j] *= a[i][j];

    # taking sum
    for i in range(n):
        for j in range(n):
            sum += a[i][j];

    return math.floor(int(sum / (n * n)));

# Driver Code

# declaring and
# initializing matrix
mat = [[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]];

# for mean
m = mean(mat, 3);

# for variance
var = variance(mat, 3, m);

# for standard deviation
dev = math.sqrt(var);

# displaying variance
# and deviation
print("Mean:", m);
print("Variance:", var);
print("Deviation:", math.floor(dev));

# This code is contributed by mits
```

## C#

```
// C# program to find mean
// and variance of a matrix.
using System;

class GFG
{

// Function for
// calculating mean
static int mean(int [,]a,
                int n)
{
    // Calculating sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += a[i, j];

    // Returning mean
    return sum / (n * n);
}

// Function for
// calculating variance
static int variance(int [,]a,
                    int n, int m)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // subtracting mean
            // from elements
            a[i, j] -= m;

            // a[i][j] = fabs(a[i][j]);
            // squaring each terms
            a[i, j] *= a[i, j];
        }
    }

    // taking sum
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum += a[i,j];

    return sum / (n * n);
}

// Driver Code
static public void Main ()
{

// declaring and
// initializing matrix
int [,]mat = {{1, 2, 3},
              {4, 5, 6},
              {7, 8, 9}};

// for mean
int m = mean(mat, 3);

// for variance
int var = variance(mat, 3, m);

// for standard deviation
double dev = (int)Math.Sqrt(var);

// displaying variance and deviation
Console.WriteLine("Mean: " + m );
    Console.WriteLine("Variance: " + var);
    Console.WriteLine("Deviation: " + dev);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find mean
// and variance of a matrix.

// variance function declaration
// Function for calculating mean
function mean($a, $n)
{
    // Calculating sum
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        for ( $j = 0; $j < $n; $j++)
            $sum += $a[$i][$j];

    // Returning mean
    return floor((int)$sum / ($n * $n));
}

// Function for calculating variance
function variance($a, $n, $m)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {

            // subtracting mean
            // from elements
            $a[$i][$j] -= $m;

            // a[i][j] = fabs(a[i][j]);
            // squaring each terms
            $a[$i][$j] *= $a[$i][$j];
        }
    }

    // taking sum
    for ($i = 0; $i < $n; $i++)
        for ( $j = 0; $j < $n; $j++)
            $sum += $a[$i][$j];

    return floor((int)$sum / ($n * $n));
}

// Driver Code

// declaring and
// initializing matrix
$mat = array(array(1, 2, 3),
             array(4, 5, 6),
             array(7, 8, 9));

// for mean
$m = mean($mat, 3);

// for variance
$var = variance($mat, 3, $m);

// for standard deviation
$dev = sqrt($var);

// displaying variance
// and deviation
echo "Mean: " , $m , "\n",
     "Variance: " , $var ,
      "\n", "Deviation: " ,
        floor($dev) , "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find mean
// and variance of a matrix

// Function for
// calculating mean
function mean(a, n)
{
    // Calculating sum
    let sum = 0;
    for (let i = 0; i < n; i++)
        for (let j = 0; j < n; j++)
            sum += a[i][j];

    // Returning mean
    return sum / (n * n);
}

// Function for
// calculating variance
function variance(a, n, m)
{
    let sum = 0;
    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < n; j++)
        {

            // subtracting mean
            // from elements
            a[i][j] -= m;

            // a[i][j] = fabs(a[i][j]);
            // squaring each terms
            a[i][j] *= a[i][j];
        }
    }

    // taking sum
    for (let i = 0; i < n; i++)
        for (let j = 0; j < n; j++)
            sum += a[i][j];

    return sum / (n * n);
}

// Driver code

// declaring and
// initializing matrix
let mat = [[1, 2, 3],
               [4, 5, 6],
               [7, 8, 9]];

// for mean
let m = mean(mat, 3);

// for variance
let varr = variance(mat, 3, m);

// for standard
// deviation
let dev = Math.sqrt(varr);

// displaying variance
// and deviation
document.write("Mean: " + Math.floor(m) + "<br/>");
document.write("Variance: " +
                            Math.floor(varr) + "<br/>");
document.write("Deviation: " +
                        Math.floor(dev) + "<br/>");

// This code is contributed by code_hunt.                           
</script>
```

**Output :** 

```
Mean: 5
Variance: 6
Deviation: 2
```

本文由**喜马拉雅冉冉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。