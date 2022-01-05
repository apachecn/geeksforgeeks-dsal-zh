# 矩阵中大于修正平均值的元素数量

> 原文:[https://www . geesforgeks . org/find-number-elements-greater-modified-mean-matrix/](https://www.geeksforgeeks.org/find-number-elements-greater-modified-mean-matrix/)

通常矩阵的平均值是矩阵中所有元素的平均值。将修改后的平均值视为行方向最小值和列方向最大值的平均值的下限。行方向的最小值是给定矩阵每行的最小元素，列方向的最大值是每列的最大元素。给定一个 n*m 阶的矩阵，求大于所得新平均值的元素个数。

```
mean = floor ( (sum(row-wise Min) + sum (col-wise Max )) / 
                                  (row_no. + col_no.) )
```

**示例:**

```
Input : mat[][] = {1, 5, 6,
                   2, 3, 0,
                   5, 2, 8}
Output : 4

Input : mat[][] = {1, 5,
                   5, 2}
Output : 2
```

求所有行方向最小值之和和所有列方向最大值之和。取这个和的平均值，用(n+m)除和值，即行和列的总数。现在，我们有了行方向的最小值和列方向的最大值的平均值，迭代矩阵以找到大于计算平均值的元素数。
以下是上述方法的实现:

## C++

```
// CPP program to count number of
// elements greater than mean
#include <bits/stdc++.h>
using namespace std;

// define constant for row and column
#define n 4
#define m 5

// function to count elements
// greater than mean
int countElements(int mat[][m])
{
    // For each row find minimum
    // element and add to rowSum
    int rowSum = 0;
    for (int i = 0; i < n; i++) {
        int min = mat[i][0];
        for (int j = 1; j < m; j++)
            if (mat[i][j] < min)
                min = mat[i][j];
        rowSum += min;
    }

    // For each column find maximum
    // element and add to colSum
    int colSum = 0;
    for (int i = 0; i < m; i++) {
        int max = mat[0][i];
        for (int j = 1; j < n; j++)
            if (max < mat[j][i])
                max = mat[j][i];
        colSum += max;
    }

    // Calculate mean of row-wise
    // minimum and column wise maximum
    int mean = (rowSum + colSum) / (m + n);

    // For whole matrix count
    // elements greater than mean
    int count = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (mean < mat[i][j])
                count++;
    return count;
}

// driver function
int main()
{
    int mat[n][m] = { 5, 4, 2, 8, 7,
                      1, 5, 8, 3, 4,
                      8, 5, 4, 6, 0,
                      2, 5, 8, 9, 4 };
    cout << countElements(mat);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// number of elements
// greater than mean
class GFG {

    static int n = 4, m = 5;

    // function to count
    // elements greater
    // than mean
    static int countElements(int mat[][])
    {
        // For each row find
        // minimum element
        // and add to rowSum
        int rowSum = 0;
        for (int i = 0; i < n; i++)
        {
            int min = mat[i][0];

            for (int j = 1; j < m; j++)
                if (mat[i][j] < min)
                    min = mat[i][j];

            rowSum += min;
        }

        // For each column
        // find maximum
        // element and add
        // to colSum
        int colSum = 0;
        for (int i = 0; i < m; i++) {
            int max = mat[0][i];

            for (int j = 1; j < n; j++)
                if (max < mat[j][i])
                    max = mat[j][i];

            colSum += max;
        }

        // Calculate mean of
        // row-wise minimum
        // and column wise
        // maximum
        int mean = (rowSum + colSum) / (m + n);

        // For whole matrix
        // count elements
        // greater than mean
        int count = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)

                if (mean < mat[i][j])
                    count++;

        return count;
    }

    // driver function
    public static void main(String[] args)
    {
        int mat[][] = {{ 5, 4, 2, 8, 7},
                        {1, 5, 8, 3, 4},
                        {8, 5, 4, 6, 0},
                        {2, 5, 8, 9, 4}};
        System.out.println(countElements(mat));
    }
}

// This article is contribute by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to count
# number of elements
# greater than mean
n = 4;
m = 5;

# Function to count
# elements greater
# than mean
def countElements(mat):

    # For each row find
    # minimum element
    # and add to rowSum
    rowSum = 0;

    for i in range(n):
        min = mat[i][0];
        for j in range(1, m):
            if (mat[i][j] < min):
                min = mat[i][j];

        rowSum += min;

    # For each column
    # find maximum
    # element and add
    # to colSum
    colSum = 0;

    for i in range(m):
        max = mat[0][i];
        for j in range(1, n):
            if (max < mat[j][i]):
                max = mat[j][i];

        colSum += max;

    # Calculate mean of
    # row-wise minimum
    # and column wise
    # maximum
    mean = ((rowSum + colSum) /
           (m + n));

    # For whole matrix
    # count elements
    # greater than mean
    count = 0;
    for i in range(n):
        for j in range(m):
            if (mean < mat[i][j]):
                count += 1;

    return count;

# Driver code
if __name__ == '__main__':

    mat = [[5, 4, 2, 8, 7],
           [1, 5, 8, 3, 4],
           [8, 5, 4, 6, 0],
           [2, 5, 8, 9, 4]];
    print(countElements(mat));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to count number of
// elements greater than mean
using System;

class GFG {

    static int n = 4, m = 5;

    // function to count elements
    // greater than mean
    static int countElements(int [,]mat)
    {
        // For each row find minimum
        // element and add to rowSum
        int rowSum = 0;
        for (int i = 0; i < n; i++)
        {
            int min = mat[i,0];

            for (int j = 1; j < m; j++)
                if (mat[i,j] < min)
                    min = mat[i,j];

            rowSum += min;
        }

        // For each column find maximum
        // element and add to colSum
        int colSum = 0;
        for (int i = 0; i < m; i++) {
            int max = mat[0,i];

            for (int j = 1; j < n; j++)
                if (max < mat[j,i])
                    max = mat[j,i];

            colSum += max;
        }

        // Calculate mean of row-wise minimum
        // and column wise maximum
        int mean = (rowSum + colSum) / (m + n);

        // For whole matrix count
        // elements greater than mean
        int count = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)

                if (mean < mat[i,j])
                    count++;

        return count;
    }

    // Driver function
    public static void Main()
    {
        int [,]mat = {{5, 4, 2, 8, 7},
                      {1, 5, 8, 3, 4},
                      {8, 5, 4, 6, 0},
                      {2, 5, 8, 9, 4}};
    Console.Write(countElements(mat));
    }
}

// This article is contribute by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// elements greater than mean

// define constant for
// row and column
$n = 4;
$m = 5;

// function to count elements
// greater than mean
function countElements($mat)
{

    // For each row find minimum
    // element and add to rowSum
    $rowSum = 0;
    global $n, $m;
    for ($i = 0; $i < $n; $i++)
    {
        $min = $mat[$i][0];
        for ($j = 1; $j < $m; $j++)
            if ($mat[$i][$j] < $min)
                $min = $mat[$i][$j];
        $rowSum += $min;
    }

    // For each column find maximum
    // element and add to colSum
    $colSum = 0;
    for ($i = 0; $i < $m; $i++)
    {
        $max = $mat[0][$i];
        for ($j = 1; $j < $n; $j++)
            if ($max < $mat[$j][$i])
                $max = $mat[$j][$i];
        $colSum += $max;
    }

    // Calculate mean of row-wise
    // minimum and column wise maximum
    $mean = ($rowSum + $colSum) / ($m + $n);

    // For whole matrix count
    // elements greater than mean
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $m; $j++)
            if ($mean < $mat[$i][$j])
                $count++;
    return $count;
}

// Driver Code
$mat = array(array(5, 4, 2, 8, 7),
             array(1, 5, 8, 3, 4),
             array(8, 5, 4, 6, 0),
             array(2, 5, 8, 9, 4));
echo countElements($mat);
// This code is contribute by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of
// elements greater than mean

// define constant for row and column
var n = 4
var m = 5

// function to count elements
// greater than mean
function countElements(mat)
{
    // For each row find minimum
    // element and add to rowSum
    var rowSum = 0;
    for (var i = 0; i < n; i++) {
        var min = mat[i][0];
        for (var j = 1; j < m; j++)
            if (mat[i][j] < min)
                min = mat[i][j];
        rowSum += min;
    }

    // For each column find maximum
    // element and add to colSum
    var colSum = 0;
    for (var i = 0; i < m; i++) {
        var max = mat[0][i];
        for (var j = 1; j < n; j++)
            if (max < mat[j][i])
                max = mat[j][i];
        colSum += max;
    }

    // Calculate mean of row-wise
    // minimum and column wise maximum
    var mean = (rowSum + colSum) / (m + n);

    // For whole matrix count
    // elements greater than mean
    var count = 0;
    for (var i = 0; i < n; i++)
        for (var j = 0; j < m; j++)
            if (mean < mat[i][j])
                count++;
    return count;
}

// driver function
var mat = [ [5, 4, 2, 8, 7],
                  [1, 5, 8, 3, 4],
                  [8, 5, 4, 6, 0],
                  [2, 5, 8, 9, 4 ]];
document.write( countElements(mat));

</script>
```

**输出:**

```
11
```