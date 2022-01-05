# 检查给定矩阵是否可以增加矩阵

> 原文:[https://www . geesforgeks . org/check-可能-使-给定-矩阵-增加-矩阵-非/](https://www.geeksforgeeks.org/check-possible-make-given-matrix-increasing-matrix-not/)

给定一个 N×M 的正整数矩阵，任务是找出是否有可能使矩阵增加。打印以其他方式构建的矩阵打印-1。矩阵元素应该大于零。
一个矩阵被称为递增矩阵，如果:-

*   对于每一行，元素以递增的顺序排列。
*   对于每一列，元素的顺序是递增的。

**例:**

> 输入:N = 4，M = 4
> 1 2 2 3
> 1-1 7-1
> 6-1-1-1-1
> 1-1-1-1-1
> 输出:
> 1 2 2 3
> 1 2 7
> 6 6 7
> 6 6 7 7
> 可以看出这是递增矩阵。
> 输入:N = 2，M = 3
> 1 4 -1
> 1 -1 3
> 输出:-1
> 这里，在第一行，我们要放一些大于
> 4 的东西，使其递增顺序。但是，在此之后，
> 第三列将永远不会按递增顺序排列。
> 所以，不可能让它增加矩阵。

注意:一个矩阵可以有多个解。

**方法:**让 dp[i][j]表示矩阵 dp 的第 I 行和第 j 列的元素。由于矩阵是非递减的，所以应满足以下两个条件:

*   dp[i][j] >= dp[i][j-1]，在第 I 行中，元素是非递减的。
*   dp[i][j] >= dp[i-1][j]，在 j 列中，元素是非递减的。

这意味着 dp[i][j] >= dp[r]每 1 <= r <= i, 1 <= c <= j (one element is greater than all the elements that are up to the left).
设 I 为包含-1 的 dp 的第一行，在该行中设 j 为最左边-1 的列。用最小可能值替换 dp[i][j]总是方便的，否则，可能无法找到另一个向右下方的-1 的有效值。因此，一个可能的解决方案(也是字典上最小的)是设置 dp[i][j] = max { dp[i][j-1]，dp[i-1][j] }。
在填充 dp 中的一些未知位置后，可能会发现 dp 的一个值小于左边的一些元素。在这种情况下，没有解决办法。

## C++

```
// CPP program to Check if we can make
// the given matrix increasing matrix or not
#include <bits/stdc++.h>
using namespace std;
#define n 4
#define m 4

// Function to find increasing matrix
void findIncreasingMatrix(int dp[n + 1][m + 1])
{
    bool flag = false;
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= m; ++j) {

            // Putting max into b as per the above approach
            int b = max(dp[i - 1][j], dp[i][j - 1]);

            // If b is -1 than putting 1 to it
            b = max(1, b);

            // If dp[i][j] has to be filled with max
            if (dp[i][j] == -1)
                dp[i][j] = b;

            // If dp[i][j] is less than from it's left
            // element or from it's upper element
            else if (dp[i][j] < b)
                flag = true;
        }
    }

    // If it is not possible
    if (flag)
        cout << -1 << '\n';

    else {

        // Printing the increasing matrix
        for (int i = 1; i <= n; ++i) {
            for (int j = 1; j <= m; ++j) {
                cout << dp[i][j] << ' ';
            }
            cout << endl;
        }
    }
}

// Drivers code
int main()
{
    /* Here the matrix is 1 2 3 3
                          1 -1 7 -1
                          6 -1 -1 -1
                          -1 -1 -1 -1
       Putting 0 in first row & column */

    int dp[n + 1][m + 1] = { { 0, 0, 0, 0, 0 },
                             { 0, 1, 2, 2, 3 },
                             { 0, 1, -1, 7, -1 },
                             { 0, 6, -1, -1, -1 },
                             { 0, -1, -1, -1, -1 } };

    findIncreasingMatrix(dp);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if we
// can make the given matrix
// increasing matrix or not
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
static final int n = 4;
static final int m = 4;

// Function to find increasing matrix
static void findIncreasingMatrix(int dp[][])
{
    boolean flag = false;
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= m; ++j)
        {

            // Putting max into b as per
            // the above approach
            int b = Math.max(dp[i - 1][j],
                             dp[i][j - 1]);

            // If b is -1 than putting 1 to it
            b = Math.max(1, b);

            // If dp[i][j] has to be
            // filled with max
            if (dp[i][j] == -1)
                dp[i][j] = b;

            // If dp[i][j] is less than from
            // it's left element or from
            // it's upper element
            else if (dp[i][j] < b)
                flag = true;
        }
    }

    // If it is not possible
    if (flag == true)
        System.out.println("-1");

    else
    {

        // Printing the increasing matrix
        for (int i = 1; i <= n; ++i)
        {
            for (int j = 1; j <= m; ++j)
            {
                System.out.print(dp[i][j] + " ");
            }
            System.out.println();
        }
    }
}

// Driver code
public static void main(String args[])
{
    /* Here the matrix is 1 2 3 3
                        1 -1 7 -1
                        6 -1 -1 -1
                        -1 -1 -1 -1
    Putting 0 in first row & column */

    int dp[][] = {{ 0, 0, 0, 0, 0 },
                  { 0, 1, 2, 2, 3 },
                  { 0, 1, -1, 7, -1 },
                  { 0, 6, -1, -1, -1 },
                  { 0, -1, -1, -1, -1 }};

    findIncreasingMatrix(dp);
}
}

// This code is contributed
// by Subhadeep
```

## 蟒蛇 3

```
# Python3 program to Check if we can make
# the given matrix increasing matrix or not

# Function to find increasing matrix
def findIncreasingMatrix(dp):

    flag = False
    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # Putting max into b as per
            # the above approach
            b = max(dp[i - 1][j], dp[i][j - 1])

            # If b is -1 than putting 1 to it
            b = max(1, b)

            # If dp[i][j] has to be filled with max
            if dp[i][j] == -1:
                dp[i][j] = b

            # If dp[i][j] is less than from it's left
            # element or from it's upper element
            elif dp[i][j] < b:
                flag = True

    # If it is not possible
    if flag:
        print(-1)

    else:
        # Printing the increasing matrix
        for i in range(1, n + 1):
            for j in range(1, m + 1):
                print(dp[i][j], end = ' ')

            print()

# Driver code
if __name__ == "__main__":

    dp = [[0, 0, 0, 0, 0],
          [0, 1, 2, 2, 3],
          [0, 1, -1, 7, -1],
          [0, 6, -1, -1, -1],
          [0, -1, -1, -1, -1]]
    n = m = 4

    findIncreasingMatrix(dp)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to Check if we
// can make the given matrix
// increasing matrix or not
using System;

class GFG
{

static readonly int n = 4;
static readonly int m = 4;

// Function to find increasing matrix
static void findIncreasingMatrix(int [,]dp)
{
    bool flag = false;
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= m; ++j)
        {

            // Putting max into b as per
            // the above approach
            int b = Math.Max(dp[i - 1, j],
                            dp[i, j - 1]);

            // If b is -1 than putting 1 to it
            b = Math.Max(1, b);

            // If dp[i,j] has to be
            // filled with max
            if (dp[i, j] == -1)
                dp[i, j] = b;

            // If dp[i,j] is less than from
            // it's left element or from
            // it's upper element
            else if (dp[i, j] < b)
                flag = true;
        }
    }

    // If it is not possible
    if (flag == true)
        Console.WriteLine("-1");

    else
    {

        // Printing the increasing matrix
        for (int i = 1; i <= n; ++i)
        {
            for (int j = 1; j <= m; ++j)
            {
                Console.Write(dp[i, j] + " ");
            }
            Console.WriteLine();
        }
    }
}

// Driver code
public static void Main()
{
    /* Here the matrix is 1 2 3 3
                        1 -1 7 -1
                        6 -1 -1 -1
                        -1 -1 -1 -1
    Putting 0 in first row & column */

    int [,]dp = {{ 0, 0, 0, 0, 0 },
                { 0, 1, 2, 2, 3 },
                { 0, 1, -1, 7, -1 },
                { 0, 6, -1, -1, -1 },
                { 0, -1, -1, -1, -1 }};

    findIncreasingMatrix(dp);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Check if we can make
// the given matrix increasing matrix or not
$n = 4;
$m = 4;

// Function to find increasing matrix
function findIncreasingMatrix($dp)
{
    global $n;
    global $m;

    $flag = false;
    for ($i = 1; $i <= $n; ++$i)
    {
        for ($j = 1; $j <= $m; ++$j)
        {

            // Putting max into b as per the above approach
            $b = max($dp[$i - 1][$j], $dp[$i][$j - 1]);

            // If b is -1 than putting 1 to it
            $b = max(1, $b);

            // If dp[i][j] has to be filled with max
            if ($dp[$i][$j] == -1)
                $dp[$i][$j] = $b;

            // If dp[i][j] is less than from it's left
            // element or from it's upper element
            else if ($dp[$i][$j] < $b)
                $flag = true;
        }
    }

    // If it is not possible
    if ($flag)
        echo -1,'\n';

    else
    {

        // Printing the increasing matrix
        for ($i = 1; $i <= $n; ++$i)
        {
            for ( $j = 1; $j <= $m; ++$j)
            {
                echo $dp[$i][$j], ' ';
            }
            echo "\n";
        }
    }
}

// Driver Code

/* Here the matrix is 1 2 3 3
                    1 -1 7 -1
                    6 -1 -1 -1
                    -1 -1 -1 -1
Putting 0 in first row & column */
$dp = array(array(0, 0, 0, 0, 0),
            array(0, 1, 2, 2, 3),
            array(0, 1, -1, 7, -1),
            array(0, 6, -1, -1, -1),
            array(0, -1, -1, -1, -1));

findIncreasingMatrix($dp);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
    // Javascript program to Check if we can make
    // the given matrix increasing matrix or not

    let n = 4;
    let m = 4;

    // Function to find increasing matrix
    function findIncreasingMatrix(dp)
    {
        let flag = false;
        for (let i = 1; i <= n; ++i) {
            for (let j = 1; j <= m; ++j) {

                // Putting max into b as per the above approach
                let b = Math.max(dp[i - 1][j], dp[i][j - 1]);

                // If b is -1 than putting 1 to it
                b = Math.max(1, b);

                // If dp[i][j] has to be filled with max
                if (dp[i][j] == -1)
                    dp[i][j] = b;

                // If dp[i][j] is less than from it's left
                // element or from it's upper element
                else if (dp[i][j] < b)
                    flag = true;
            }
        }

        // If it is not possible
        if (flag)
            document.write(-1 + "</br>");

        else {

            // Printing the increasing matrix
            for (let i = 1; i <= n; ++i) {
                for (let j = 1; j <= m; ++j) {
                    document.write(dp[i][j] + " ");
                }
                document.write("</br>");
            }
        }
    }

    /* Here the matrix is 1 2 3 3
                          1 -1 7 -1
                          6 -1 -1 -1
                          -1 -1 -1 -1
       Putting 0 in first row & column */

    let dp = [ [ 0, 0, 0, 0, 0 ],
              [ 0, 1, 2, 2, 3 ],
              [ 0, 1, -1, 7, -1 ],
              [ 0, 6, -1, -1, -1 ],
              [ 0, -1, -1, -1, -1 ] ];

    findIncreasingMatrix(dp);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
1 2 2 3 
1 2 7 7 
6 6 7 7 
6 6 7 7
```