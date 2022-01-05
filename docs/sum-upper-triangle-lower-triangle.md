# 上三角和下三角之和

> 原文:[https://www . geesforgeks . org/sum-上三角-下三角/](https://www.geeksforgeeks.org/sum-upper-triangle-lower-triangle/)

给定一个矩阵，打印上下三角形元素的总和(即对角线上的元素和上下元素)。
**例:**

```
Input : {6, 5, 4}
        {1, 2, 5}
        {7, 9, 7}
Output :
Upper sum is 29
Lower sum is 32
```

解决方案非常简单，我们只需要遍历矩阵，并相应地计算上下三角形的和。

## C++

```
// C++ program to calculate the sum
// of upper and lower triangle
#include <bits/stdc++.h>
using namespace std;

/*function to calculate sum*/
void sum(int mat[3][3], int r, int c)
{
    int i, j;
    int upper_sum = 0;
    int lower_sum = 0;

    /*to calculate sum of upper triangle*/
    for (i = 0; i < r; i++)
        for (j = 0; j < c; j++) {
            if (i <= j) {
                upper_sum += mat[i][j];
            }
        }

    printf("Upper sum is %d\n", upper_sum);

    /*to calculate sum of lower*/
    for (i = 0; i < r; i++)
        for (j = 0; j < c; j++) {
            if (j <= i) {
                lower_sum += mat[i][j];
            }
        }

    printf("Lower sum is %d", lower_sum);
}

/*driver function*/
int main()
{
    int r = 3;
    int c = 3;

    /*giving the matrix*/
    int mat[3][3] = {{ 6, 5, 4 },
                     { 1, 2, 5 },
                     { 7, 9, 7 }};

    /*calling the function*/
    sum(mat, r, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the sum
// of upper and lower triangle

class GFG
{
    /*function to calculate sum*/
    static void sum(int mat[][], int r, int c)
    {
        int i, j;
        int upper_sum = 0;
        int lower_sum = 0;

        /*calculate sum of upper triangle*/
        for (i = 0; i < r; i++)
            for (j = 0; j < c; j++)
            {
                if (i <= j)
                {
                    upper_sum += mat[i][j];
                }
            }

        System.out.println("Upper sum is " + upper_sum);

        /*calculate sum of lower*/
        for (i = 0; i < r; i++)
            for (j = 0; j < c; j++)
            {
                if (j <= i)
                {
                    lower_sum += mat[i][j];
                }
            }

        System.out.print("Lower sum is " + lower_sum);
    }

    // Driver code
    public static void main (String[] args)
    {
        int r = 3;
        int c = 3;

        /*giving the matrix*/
        int mat[][] = {{ 6, 5, 4 },
                        { 1, 2, 5 },
                        { 7, 9, 7 }};

        /*calling the function*/
        sum(mat, r, c);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to calculate the sum
# of upper and lower triangle

# function to calculate sum
def Sum(mat, r, c):

    i, j = 0, 0;
    upper_sum = 0;
    lower_sum = 0;

    # to calculate sum of upper triangle
    for i in range(r):
        for j in range(c):
            if (i <= j):
                upper_sum += mat[i][j];

    print("Upper sum is ", upper_sum);

    # to calculate sum of lower
    for i in range(r):
        for j in range(c):
            if (j <= i):
                lower_sum += mat[i][j];

    print("Lower sum is ", lower_sum);

# Driver Code
r = 3;
c = 3;

# giving the matrix
mat = [[ 6, 5, 4 ],
       [ 1, 2, 5 ],
       [ 7, 9, 7 ]];

# calling the function
Sum(mat, r, c);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to calculate the sum
// of upper and lower triangle
using System;

class GFG
{
    /*function to calculate sum*/
    static void sum(int [,]mat, int r, int c)
    {
        int i, j;
        int upper_sum = 0;
        int lower_sum = 0;

        /*calculate sum of upper triangle*/
        for (i = 0; i < r; i++)
            for (j = 0; j < c; j++)
            {
                if (i <= j)
                {
                   upper_sum += mat[i,j];
                }
            }

        Console.WriteLine("Upper sum is " +
                                upper_sum);

        /*calculate sum of lower*/
        for (i = 0; i < r; i++)
            for (j = 0; j < c; j++)
            {
                if (j <= i)
                {
                   lower_sum += mat[i,j];
                }
            }

        Console.Write("Lower sum is " +
                            lower_sum);
    }

    // Driver code
    public static void Main ()
    {
        int r = 3;
        int c = 3;

        /*giving the matrix*/
        int [,]mat = {{6, 5, 4},
                      {1, 2, 5},
                      {7, 9, 7}};

        /*calling the function*/
        sum(mat, r, c);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate the sum
// of upper and lower triangle

// function to calculate sum
function sum($mat, $r, $c)
{

    $upper_sum = 0;
    $lower_sum = 0;

    /* to calculate sum of
       upper triangle */
    for ($i = 0; $i < $r; $i++)
        for ($j = 0; $j < $c; $j++)
        {
            if ($i <= $j)
            {
                $upper_sum += $mat[$i][$j];
            }
        }

    echo "Upper sum is ". $upper_sum."\n";

    /* to calculate sum of lower */
    for ($i = 0; $i < $r; $i++)
        for ($j = 0; $j < $c; $j++)
        {
            if ($j <= $i)
            {
                $lower_sum += $mat[$i][$j];
            }
        }

    echo "Lower sum is ". $lower_sum;
}

    // Driver Code
    $r = 3;
    $c = 3;

    /*giving the matrix*/
    $mat = array(array(6, 5, 4),
                 array(1, 2, 5),
                 array(7, 9, 7));

    /*calling the function*/
    sum($mat, $r, $c);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate the sum
// of upper and lower triangle

/*function to calculate sum*/
function sum(mat,r,c)
{
    let i, j;
    let upper_sum = 0;
    let lower_sum = 0;

    /*to calculate sum of upper triangle*/
    for (i = 0; i < r; i++)
        for (j = 0; j < c; j++) {
            if (i <= j) {
                upper_sum += mat[i][j];
            }
        }

    document.write("Upper sum is "+ upper_sum+"<br/>");

    /*to calculate sum of lower*/
    for (i = 0; i < r; i++)
        for (j = 0; j < c; j++) {
            if (j <= i) {
                lower_sum += mat[i][j];
            }
        }

    document.write("Lower sum is "+lower_sum);
}

/*driver function*/

    let r = 3;
    let c = 3;

    /*giving the matrix*/
    let mat = [[ 6, 5, 4 ],
                     [ 1, 2, 5 ],
                     [ 7, 9, 7 ]];

    /*calling the function*/
    sum(mat, r, c);

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
Upper sum is 29
Lower sum is 32
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。