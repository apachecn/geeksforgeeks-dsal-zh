# 一个矩阵概率题

> 原文:[https://www . geesforgeks . org/a-matrix-probability-question/](https://www.geeksforgeeks.org/a-matrix-probability-question/)

给定一个矩形矩阵，我们可以以相等的概率从当前单元格向 4 个方向移动。4 个方向是右、左、上或下。计算 N 从矩阵中给定位置(I，j)移动后，我们在任何一点都不会越过矩阵边界的概率。
**我们强烈建议你尽量减少浏览器，先自己试试这个。**
想法是执行类似 DFS 的东西。我们递归地在 4 个允许的方向上遍历，对于遇到的每个单元，我们少移动一次就计算出所需的概率。由于每个方向具有相等的概率，每个方向将贡献该小区总概率的 1/4，即 0.25。如果我们走出矩阵，则返回 0，如果完成了 N 个步骤而没有跨越矩阵边界，则返回 1。
以下是以上想法的实现:

## C++

```
/// C++ program to find the probability
// that we do not cross boundary of a
// matrix after N moves.
#include <bits/stdc++.h>
using namespace std;

// check if (x, y) is valid matrix coordinate
bool isSafe(int x, int y, int m, int n)
{
    return (x >= 0 && x < m &&
            y >= 0 && y < n);
}

// Function to calculate probability
// that after N moves from a given
// position (x, y) in m x n matrix,
// boundaries of the matrix will not be crossed.
double findProbability(int m, int n, int x,
                       int y, int N)
{
    // boundary crossed
    if (!isSafe(x, y, m, n))
        return 0.0;

    // N steps taken
    if (N == 0)
        return 1.0;

    // Initialize result
    double prob = 0.0;

    // move up
    prob += findProbability(m, n, x - 1,
                            y, N - 1) * 0.25;

    // move right
    prob += findProbability(m, n, x,
                            y + 1, N - 1) * 0.25;

    // move down
    prob += findProbability(m, n, x + 1,
                            y, N - 1) * 0.25;

    // move left
    prob += findProbability(m, n, x,
                            y - 1, N - 1) * 0.25;

    return prob;
}

// Driver code
int main()
{
    // matrix size
    int m = 5, n = 5;

    // coordinates of starting point
    int i = 1, j = 1;

    // Number of steps
    int N = 2;

    cout << "Probability is "
        << findProbability(m, n, i, j, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the probability
// that we do not cross boundary
// of a matrix after N moves.
import java.io.*;

class GFG {

// check if (x, y) is valid
// matrix coordinate
static boolean isSafe(int x, int y,
                      int m, int n)
{
    return (x >= 0 && x < m &&
            y >= 0 && y < n);
}

// Function to calculate probability
// that after N moves from a given
// position (x, y) in m x n matrix,
// boundaries of the matrix will
// not be crossed.
static double findProbability(int m, int n,
                              int x, int y,
                              int N)
{

    // boundary crossed
    if (! isSafe(x, y, m, n))
        return 0.0;

    // N steps taken
    if (N == 0)
        return 1.0;

    // Initialize result
    double prob = 0.0;

    // move up
    prob += findProbability(m, n, x - 1,
                            y, N - 1) * 0.25;

    // move right
    prob += findProbability(m, n, x, y + 1,
                            N - 1) * 0.25;

    // move down
    prob += findProbability(m, n, x + 1,
                            y, N - 1) * 0.25;

    // move left
    prob += findProbability(m, n, x, y - 1,
                            N - 1) * 0.25;

    return prob;
}

// Driver code
public static void main (String[] args)
{
    // matrix size
    int m = 5, n = 5;

    // coordinates of starting point
    int i = 1, j = 1;

    // Number of steps
    int N = 2;

    System.out.println("Probability is " +
                       findProbability(m, n, i,
                       j, N));

}

}

// This code is contributed by KRV.
```

## 蟒蛇 3

```
# Python3 program to find the probability
# that we do not cross boundary of a
# matrix after N moves.

# check if (x, y) is valid matrix coordinate
def isSafe(x, y, m, n):
    return (x >= 0 and x < m and
            y >= 0 and y < n)

# Function to calculate probability
# that after N moves from a given
# position (x, y) in m x n matrix,
# boundaries of the matrix will
# not be crossed.
def findProbability(m, n, x, y, N):

    # boundary crossed
    if (not isSafe(x, y, m, n)):
        return 0.0

    # N steps taken
    if (N == 0):
        return 1.0

    # Initialize result
    prob = 0.0

    # move up
    prob += findProbability(m, n, x - 1,
                            y, N - 1) * 0.25

    # move right
    prob += findProbability(m, n, x,
                            y + 1, N - 1) * 0.25

    # move down
    prob += findProbability(m, n, x + 1,
                            y, N - 1) * 0.25

    # move left
    prob += findProbability(m, n, x,
                            y - 1, N - 1) * 0.25

    return prob

# Driver code
if __name__ == '__main__':

    # matrix size
    m = 5
    n = 5

    # coordinates of starting po
    i = 1
    j = 1

    # Number of steps
    N = 2

    print("Probability is",
           findProbability(m, n, i, j, N))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the probability
// that we do not cross boundary
// of a matrix after N moves.
using System;

class GFG
{

// check if (x, y) is valid
// matrix coordinate
static bool isSafe(int x, int y,
                   int m, int n)
{
    return (x >= 0 && x < m &&
            y >= 0 && y < n);
}

// Function to calculate probability
// that after N moves from a given
// position (x, y) in m x n matrix,
// boundaries of the matrix will
// not be crossed.
static double findProbability(int m, int n,
                              int x, int y,
                              int N)
{

    // boundary crossed
    if (! isSafe(x, y, m, n))
        return 0.0;

    // N steps taken
    if (N == 0)
        return 1.0;

    // Initialize result
    double prob = 0.0;

    // move up
    prob += findProbability(m, n, x - 1,
                            y, N - 1) * 0.25;

    // move right
    prob += findProbability(m, n, x, y + 1,
                            N - 1) * 0.25;

    // move down
    prob += findProbability(m, n, x + 1,
                            y, N - 1) * 0.25;

    // move left
    prob += findProbability(m, n, x, y - 1,
                            N - 1) * 0.25;

    return prob;
}

// Driver code
public static void Main ()
{
    // matrix size
    int m = 5, n = 5;

    // coordinates of starting point
    int i = 1, j = 1;

    // Number of steps
    int N = 2;

    Console.Write("Probability is " +
                   findProbability(m, n, i,
                   j, N));

}

}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the probability
// that we do not cross boundary of a
// matrix after N moves.

// check if (x, y) is valid
// matrix coordinate
function isSafe($x, $y, $m, $n)
{
    return ($x >= 0 && $x < $m &&
            $y >= 0 && $y < $n);
}

// Function to calculate probability
// that after N moves from a given
// position (x, y) in m x n matrix,
// boundaries of the matrix will
// not be crossed.
function findProbability($m, $n, $x,
                         $y, $N)
{
    // boundary crossed
    if (!isSafe($x, $y, $m, $n))
        return 0.0;

    // N steps taken
    if ($N == 0)
        return 1.0;

    // Initialize result
    $prob = 0.0;

    // move up
    $prob += findProbability($m, $n, $x - 1,
                             $y, $N - 1) * 0.25;

    // move right
    $prob += findProbability($m, $n, $x,
                             $y + 1, $N - 1) * 0.25;

    // move down
    $prob += findProbability($m, $n, $x + 1,
                             $y, $N - 1) * 0.25;

    // move left
    $prob += findProbability($m, $n, $x,
                             $y - 1, $N - 1) * 0.25;

    return $prob;
}

// Driver code

// matrix size
$m = 5; $n = 5;

// coordinates of starting point
$i = 1; $j = 1;

// Number of steps
$N = 2;

echo "Probability is ",
      findProbability($m, $n, $i, $j, $N);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find the probability
// that we do not cross boundary of a
// matrix after N moves.

// check if (x, y) is valid matrix coordinate
function isSafe(x, y, m, n){
    return (x >= 0 && x < m &&
            y >= 0 && y < n);
}

// Function to calculate probability
// that after N moves from a given
// position (x, y) in m x n matrix,
// boundaries of the matrix will not be crossed.
function findProbability( m, n, x,
                       y, N){
    // boundary crossed
    if (!isSafe(x, y, m, n))
        return 0.0;

    // N steps taken
    if (N == 0)
        return 1.0;

    // Initialize result
    let prob = 0.0;

    // move up
    prob += findProbability(m, n, x - 1,
                            y, N - 1) * 0.25;

    // move right
    prob += findProbability(m, n, x,
                            y + 1, N - 1) * 0.25;

    // move down
    prob += findProbability(m, n, x + 1,
                            y, N - 1) * 0.25;

    // move left
    prob += findProbability(m, n, x,
                            y - 1, N - 1) * 0.25;

    return prob;
}

// Driver code
// matrix size
let m = 5, n = 5;
// coordinates of starting point
let i = 1, j = 1;
// Number of steps
let N = 2;
document.write( "Probability is "
        +findProbability(m, n, i, j, N));

</script>
```

**输出:**

```
Probability is 0.875
```

本文由**阿迪蒂亚·戈尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息