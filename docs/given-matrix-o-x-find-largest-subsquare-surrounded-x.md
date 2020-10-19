# 给定矩阵`O`和`X`，找到被`X`包围的最大子正方形

> 原文： [https://www.geeksforgeeks.org/given-matrix-o-x-find-largest-subsquare-surrounded-x/](https://www.geeksforgeeks.org/given-matrix-o-x-find-largest-subsquare-surrounded-x/)

给定一个矩阵，其中每个元素均为`O`或`X`，请找到被`X`包围的最大子正方形。

在下面的文章中，假定给定矩阵也是方阵。 下面给出的代码可以很容易地扩展到矩形矩阵。

**示例**：

```
Input: mat[N][N] = { {'X', 'O', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'O', 'X', 'O'},
                     {'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'O'},
                    };
Output: 3
The square submatrix starting at (1, 1) is the largest
submatrix surrounded by 'X'

Input: mat[M][N] = { {'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'O', 'X', 'X', 'O', 'X'},
                     {'X', 'X', 'X', 'O', 'O', 'X'},
                     {'X', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'X', 'O'},
                    };
Output: 4
The square submatrix starting at (0, 2) is the largest
submatrix surrounded by 'X'

```



一种**简单解决方案**是考虑每个正方形子矩阵，并检查是否所有角边都填充有`X`。 该解决方案的时间复杂度为`O(N ^ 4)`。

我们可以在`O(N ^ 3)`时间中使用额外的空间来解决此问题。 这个想法是创建两个辅助数组`hor[N][N]`和`ver[N][N]`。 存储在`hor[i][j]`中的值是直到`mat[][]`中的`mat[i][j]`为止的水平连续`X`字符数。 同样，存储在`ver[i][j]`中的值是直到`mat[][]`中的`mat[i][j]`为止的垂直连续`X`字符数。 以下是一个示例。

```

mat[6][6] =  X  O  X  X  X  X
             X  O  X  X  O  X
             X  X  X  O  O  X
             O  X  X  X  X  X
             X  X  X  O  X  O
             O  O  X  O  O  O

hor[6][6] = 1  0  1  2  3  4
            1  0  1  2  0  1
            1  2  3  0  0  1
            0  1  2  3  4  5
            1  2  3  0  1  0
            0  0  1  0  0  0

ver[6][6] = 1  0  1  1  1  1
            2  0  2  2  0  2
            3  1  3  0  0  3
            0  2  4  1  1  4
            1  3  5  0  2  0
            0  0  6  0  0  0
```

一旦我们在`hor[][]`和`ver[][]`中填充了值，就从矩阵的最右下角开始，并逐行地移到最左上角。 对于每个访问的入口`mat[i][j]`，我们比较`hor[i][j]`和`ver[i][j]`的值，并选择两个中较小的一个作为正方形。 假设其中两个较小的为`small`。 选择两个较小的值后，我们分别检查`ver[][]`和`hor[][]`的左边缘和上边缘。 如果他们有相同的条目，那么我们找到了一个子正方形。 否则，我们尝试使用`small-1`。

以下是上述想法的实现。

## C++ 

```cpp

// A C++ program to find  the largest subsquare 
// surrounded by 'X' in a given matrix of 'O' and 'X' 
#include<iostream> 
using namespace std; 

// Size of given matrix is N X N 
#define N 6 

// A utility function to find minimum of two numbers 
int getMin(int x, int y) { return (x<y)? x: y; } 

// Returns size of maximum size subsquare matrix 
// surrounded by 'X' 
int findSubSquare(int mat[][N]) 
{ 
    int max = 0; // Initialize result 

    // Initialize the left-top value in hor[][] and ver[][] 
    int hor[N][N], ver[N][N]; 
    hor[0][0] = ver[0][0] = (mat[0][0] == 'X'); 

    // Fill values in hor[][] and ver[][] 
    for (int i=0; i<N; i++) 
    { 
        for (int j=0; j<N; j++) 
        { 
            if (mat[i][j] == 'O') 
                ver[i][j] = hor[i][j] = 0; 
            else
            { 
                hor[i][j] = (j==0)? 1: hor[i][j-1] + 1; 
                ver[i][j] = (i==0)? 1: ver[i-1][j] + 1; 
            } 
        } 
    } 

    // Start from the rightmost-bottommost corner element and find 
    // the largest ssubsquare with the help of hor[][] and ver[][] 
    for (int i = N-1; i>=1; i--) 
    { 
        for (int j = N-1; j>=1; j--) 
        { 
            // Find smaller of values in hor[][] and ver[][] 
            // A Square can only be made by taking smaller 
            // value 
            int small = getMin(hor[i][j], ver[i][j]); 

            // At this point, we are sure that there is a right 
            // vertical line and bottom horizontal line of length 
            // at least 'small'. 

            // We found a bigger square if following conditions 
            // are met: 
            // 1)If side of square is greater than max. 
            // 2)There is a left vertical line of length >= 'small' 
            // 3)There is a top horizontal line of length >= 'small' 
            while (small > max) 
            { 
                if (ver[i][j-small+1] >= small && 
                    hor[i-small+1][j] >= small) 
                { 
                    max = small; 
                } 
                small--; 
            } 
        } 
    } 
    return max; 
} 

// Driver program to test above function 
int main() 
{ 
    int mat[][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'}, 
                     {'X', 'O', 'X', 'X', 'O', 'X'}, 
                     {'X', 'X', 'X', 'O', 'O', 'X'}, 
                     {'O', 'X', 'X', 'X', 'X', 'X'}, 
                     {'X', 'X', 'X', 'O', 'X', 'O'}, 
                     {'O', 'O', 'X', 'O', 'O', 'O'}, 
                    }; 
    cout << findSubSquare(mat); 
    return 0; 
} 

```

## Java

```java
// A JAVA program to find the
// largest subsquare surrounded
// by 'X' in a given matrix of
// 'O' and 'X'
import java.util.*;

class GFG 
{
    // Size of given
    // matrix is N X N
    static int N = 6;

    // A utility function to
    // find minimum of two numbers
    static int getMin(int x, int y)
    {
        return (x < y) ? x : y;
    }

    // Returns size of maximum
    // size subsquare matrix
    // surrounded by 'X'
    static int findSubSquare(int mat[][])
    {
        int max = 0; // Initialize result

        // Initialize the left-top
        // value in hor[][] and ver[][]
        int hor[][] = new int[N][N];
        int ver[][] = new int[N][N];
        hor[0][0] = ver[0][0] = 'X';

        // Fill values in
        // hor[][] and ver[][]
        for (int i = 0; i < N; i++) 
        {
            for (int j = 0; j < N; j++)
            {
                if (mat[i][j] == 'O')
                    ver[i][j] = hor[i][j] = 0;
                else 
                {
                    hor[i][j]
                        = (j == 0) ? 1 : hor[i][j - 1] + 1;
                    ver[i][j]
                        = (i == 0) ? 1 : ver[i - 1][j] + 1;
                }
            }
        }

        // Start from the rightmost-
        // bottommost corner element
        // and find the largest
        // subsquare with the help
        // of hor[][] and ver[][]
        for (int i = N - 1; i >= 1; i--) 
        {
            for (int j = N - 1; j >= 1; j--) 
            {
                // Find smaller of values in
                // hor[][] and ver[][] A Square
                // can only be made by taking
                // smaller value
                int small = getMin(hor[i][j], ver[i][j]);

                // At this point, we are sure
                // that there is a right vertical
                // line and bottom horizontal
                // line of length at least 'small'.

                // We found a bigger square
                // if following conditions
                // are met:
                // 1)If side of square
                //   is greater than max.
                // 2)There is a left vertical
                //   line of length >= 'small'
                // 3)There is a top horizontal
                //   line of length >= 'small'
                while (small > max) 
                {
                    if (ver[i][j - small + 1] >= small
                        && hor[i - small + 1][j] >= small) 
                    {
                        max = small;
                    }
                    small--;
                }
            }
        }
        return max;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // TODO Auto-generated method stub

        int mat[][] = { { 'X', 'O', 'X', 'X', 'X', 'X' },
                        { 'X', 'O', 'X', 'X', 'O', 'X' },
                        { 'X', 'X', 'X', 'O', 'O', 'X' },
                        { 'O', 'X', 'X', 'X', 'X', 'X' },
                        { 'X', 'X', 'X', 'O', 'X', 'O' },
                        { 'O', 'O', 'X', 'O', 'O', 'O' } };
      
        // Function call
        System.out.println(findSubSquare(mat));
    }
}

// This code is contributed
// by ChitraNayal
```

## Python3

```py
# A Python3 program to find the largest
# subsquare surrounded by 'X' in a given
# matrix of 'O' and 'X'
import math as mt

# Size of given matrix is N X N
N = 6

# A utility function to find minimum
# of two numbers


def getMin(x, y):
    if x < y:
        return x
    else:
        return y

# Returns size of Maximum size
# subsquare matrix surrounded by 'X'


def findSubSquare(mat):

    Max = 0  # Initialize result

    # Initialize the left-top value
    # in hor[][] and ver[][]
    hor = [[0 for i in range(N)]
           for i in range(N)]
    ver = [[0 for i in range(N)]
           for i in range(N)]

    if mat[0][0] == 'X':
        hor[0][0] = 1
        ver[0][0] = 1

    # Fill values in hor[][] and ver[][]
    for i in range(N):

        for j in range(N):

            if (mat[i][j] == 'O'):
                ver[i][j], hor[i][j] = 0, 0
            else:
                if j == 0:
                    ver[i][j], hor[i][j] = 1, 1
                else:
                    (ver[i][j],
                     hor[i][j]) = (ver[i - 1][j] + 1,
                                   hor[i][j - 1] + 1)

    # Start from the rightmost-bottommost corner
    # element and find the largest ssubsquare
    # with the help of hor[][] and ver[][]
    for i in range(N - 1, 0, -1):

        for j in range(N - 1, 0, -1):

            # Find smaller of values in hor[][] and
            # ver[][]. A Square can only be made by
            # taking smaller value
            small = getMin(hor[i][j], ver[i][j])

            # At this point, we are sure that there
            # is a right vertical line and bottom
            # horizontal line of length at least 'small'.

            # We found a bigger square if following
            # conditions are met:
            # 1)If side of square is greater than Max.
            # 2)There is a left vertical line
            #   of length >= 'small'
            # 3)There is a top horizontal line
            #   of length >= 'small'
            while (small > Max):

                if (ver[i][j - small + 1] >= small and
                        hor[i - small + 1][j] >= small):

                    Max = small

                small -= 1

    return Max


# Driver Code
mat = [['X', 'O', 'X', 'X', 'X', 'X'],
       ['X', 'O', 'X', 'X', 'O', 'X'],
       ['X', 'X', 'X', 'O', 'O', 'X'],
       ['O', 'X', 'X', 'X', 'X', 'X'],
       ['X', 'X', 'X', 'O', 'X', 'O'],
       ['O', 'O', 'X', 'O', 'O', 'O']]

# Function call
print(findSubSquare(mat))

# This code is contributed by
# Mohit kumar 29
```

## C#

```cs
// A C# program to find the
// largest subsquare surrounded
// by 'X' in a given matrix of
// 'O' and 'X'
using System;

class GFG 
{
    // Size of given
    // matrix is N X N
    static int N = 6;

    // A utility function to
    // find minimum of two numbers
    static int getMin(int x, int y)
    {
        return (x < y) ? x : y;
    }

    // Returns size of maximum
    // size subsquare matrix
    // surrounded by 'X'
    static int findSubSquare(int[, ] mat)
    {
        int max = 0; // Initialize result

        // Initialize the left-top
        // value in hor[][] and ver[][]
        int[, ] hor = new int[N, N];
        int[, ] ver = new int[N, N];
        hor[0, 0] = ver[0, 0] = 'X';

        // Fill values in
        // hor[][] and ver[][]
        for (int i = 0; i < N; i++) 
        {
            for (int j = 0; j < N; j++) 
            {
                if (mat[i, j] == 'O')
                    ver[i, j] = hor[i, j] = 0;
                else 
                {
                    hor[i, j]
                        = (j == 0) ? 1 : hor[i, j - 1] + 1;
                    ver[i, j]
                        = (i == 0) ? 1 : ver[i - 1, j] + 1;
                }
            }
        }

        // Start from the rightmost-
        // bottommost corner element
        // and find the largest
        // subsquare with the help
        // of hor[][] and ver[][]
        for (int i = N - 1; i >= 1; i--) 
        {
            for (int j = N - 1; j >= 1; j--) 
            {
                // Find smaller of values in
                // hor[][] and ver[][] A Square
                // can only be made by taking
                // smaller value
                int small = getMin(hor[i, j], ver[i, j]);

                // At this point, we are sure
                // that there is a right vertical
                // line and bottom horizontal
                // line of length at least 'small'.

                // We found a bigger square
                // if following conditions
                // are met:
                // 1)If side of square
                // is greater than max.
                // 2)There is a left vertical
                // line of length >= 'small'
                // 3)There is a top horizontal
                // line of length >= 'small'
                while (small > max)
                {
                    if (ver[i, j - small + 1] >= small
                        && hor[i - small + 1, j] >= small) 
                    {
                        max = small;
                    }
                    small--;
                }
            }
        }
        return max;
    }

    // Driver Code
    public static void Main()
    {
        // TODO Auto-generated method stub

        int[, ] mat = { { 'X', 'O', 'X', 'X', 'X', 'X' },
                        { 'X', 'O', 'X', 'X', 'O', 'X' },
                        { 'X', 'X', 'X', 'O', 'O', 'X' },
                        { 'O', 'X', 'X', 'X', 'X', 'X' },
                        { 'X', 'X', 'X', 'O', 'X', 'O' },
                        { 'O', 'O', 'X', 'O', 'O', 'O' } };
      
        // Function call
        Console.WriteLine(findSubSquare(mat));
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## PHP

```php
<?php 
// A PHP program to find 
// the largest subsquare
// surrounded by 'X' in a 
// given matrix of 'O' and 'X'

// Size of given 
// matrix is N X N
$N = 6;

// A utility function to find 
// minimum of two numbers
function getMin($x, $y) 
{ 
    return ($x < $y) ? $x : $y; 
}

// Returns size of maximum
// size subsquare matrix
// surrounded by 'X'
function findSubSquare($mat)
{
    $max = 0; // Initialize result
    $hor[0][0] = $ver[0][0] = ($mat[0][0] == 'X');

    // Fill values in
    // $hor and $ver
    for ($i = 0; $i < $GLOBALS['N']; $i++)
    {
        for ($j = 0; $j < $GLOBALS['N']; $j++)
        {
            if ($mat[$i][$j] == 'O')
                $ver[$i][$j] = $hor[$i][$j] = 0;
            else
            {
                $hor[$i][$j] = ($j == 0) ? 1 : 
                                $hor[$i][$j - 1] + 1;
                $ver[$i][$j] = ($i == 0) ? 1 : 
                                $ver[$i - 1][$j] + 1;
            }
        }
    }

    // Start from the rightmost-
    // bottommost corner element 
    // and find the largest 
    // subsquare with the help of
    // $hor and $ver
    for ($i = $GLOBALS['N'] - 1; $i >= 1; $i--)
    {
        for ($j = $GLOBALS['N'] - 1; $j >= 1; $j--)
        {
            // Find smaller of values in 
            // $hor and $ver A Square can 
            // only be made by taking 
            // smaller value
            $small = getMin($hor[$i][$j],
                            $ver[$i][$j]);

            // At this point, we are sure 
            // that there is a right vertical 
            // line and bottom horizontal 
            // line of length at least '$small'.

            // We found a bigger square if 
            // following conditions are met:
            // 1)If side of square is 
            //   greater than $max.
            // 2)There is a left vertical 
            //   line of length >= '$small'
            // 3)There is a top horizontal
            //   line of length >= '$small'
            while ($small > $max)
            {
                if ($ver[$i][$j - $small + 1] >= $small &&
                    $hor[$i - $small + 1][$j] >= $small)
                {
                    $max = $small;
                }
                $small--;
            }
        }
    }
    return $max;
}

// Driver Code
$mat = array(array('X', 'O', 'X', 'X', 'X', 'X'),
             array('X', 'O', 'X', 'X', 'O', 'X'),
             array('X', 'X', 'X', 'O', 'O', 'X'),
             array('O', 'X', 'X', 'X', 'X', 'X'),
             array('X', 'X', 'X', 'O', 'X', 'O'),
             array('O', 'O', 'X', 'O', 'O', 'O'));

// Function call
echo findSubSquare($mat);

// This code is contributed
// by ChitraNayal
?>
```

输出：

```
4
```

优化方法：

一种更优化的解决方案是在名为`dp`的对矩阵中水平和垂直地预先计算连续的`X`的数量。现在，对于dp的每个条目，我们都有一个对`(int, int)`，表示该点之前的最大连续`X`，即：

+   `dp[i][j].first`表示水平的连续`X`，直到该点为止。
+   `dp[i][j].second`表示垂直的连续X，直到该点为止。

现在，可以形成一个正方形，以`dp[i][j]`作为右下角，其边的长度最大为`min(dp[i][j].first, dp[i][j].second)`。

因此，我们制作另一个矩阵maxside，它将表示以右下角为`arr[i][j]`形成的最大正方形边。我们将尝试从正方形的属性中获得一些直觉，即正方形的所有边都相等。

让我们存储可获得的最大值，即`val = min(dp[i][j].first, dp[i][j].second)`。从点`(i, j)`开始，我们沿水平方向向后移动距离`Val`，并检查直到该点的最小垂直连续`X`是否等于`Val`。

同样，我们垂直向后移动距离`Val`，并检查直到该点的最小水平连续`X`是否等于`Val`？在这里，我们利用正方形的所有边都相等的事实。

输入矩阵：

```
X  O  X  X  X  X
X  O  X  X  O  X
X  X  X  O  O  X
O  X  X  X  X  X
X  X  X  O  X  O
O  O  X  O  O  O
```

矩阵`dp`的值：

```
(1,1) (0,0) (1,1) (2,7) (3,1) (4,1)  

(1,2) (0,0) (1,2) (2,8) (0,0) (1,2)  

(1,3) (2,1) (3,3) (0,0) (0,0) (1,3)  

(0,0) (1,2) (2,4) (3,1) (4,1) (5,4)  

(1,1) (2,3) (3,5) (0,0) (1,2) (0,0)  

(0,0) (0,0) (1,6) (0,0) (0,0) (0,0) 
```

以下是上述想法的实现：

## C++

```cpp
// A C++ program to find  the largest subsquare
// surrounded by 'X' in a given matrix of 'O' and 'X'
#include <bits/stdc++.h>
using namespace std;

// Size of given matrix is N X N
#define N 6

int maximumSubSquare(int arr[][N])
{
    pair<int, int> dp[51][51];
    int maxside[51][51];

    // Initialize maxside with 0
    memset(maxside, 0, sizeof(maxside));

    int x = 0, y = 0;

    // Fill the dp matrix horizontally.
    // for contiguous 'X' increment the value of x,
    // otherwise make it 0
    for (int i = 0; i < N; i++) 
    {
        x = 0;
        for (int j = 0; j < N; j++) 
        {
            if (arr[i][j] == 'X')
                x += 1;
            else
                x = 0;
            dp[i][j].first = x;
        }
    }

    // Fill the dp matrix vertically.
    // For contiguous 'X' increment the value of y,
    // otherwise make it 0
    for (int i = 0; i < N; i++) 
    {
        for (int j = 0; j < N; j++) 
        {
            if (arr[j][i] == 'X')
                y += 1;
            else
                y = 0;
            dp[j][i].second = y;
        }
    }

    // Now check , for every value of (i, j) if sub-square
    // is possible,
    // traverse back horizontally by value val, and check if
    // vertical contiguous
    // 'X'enfing at (i , j-val+1) is greater than equal to
    // val.
    // Similarly, check if traversing back vertically, the
    // horizontal contiguous
    // 'X'ending at (i-val+1, j) is greater than equal to
    // val.
    int maxval = 0, val = 0;
    for (int i = 0; i < N; i++) 
    {
        for (int j = 0; j < N; j++) 
        {
            val = min(dp[i][j].first, dp[i][j].second);
            if (dp[i][j - val + 1].second >= val
                && dp[i - val + 1][j].first >= val)
                maxside[i][j] = val;
            else
                maxside[i][j] = 0;

            // store the final answer in maxval
            maxval = max(maxval, maxside[i][j]);
        }
    }

    // return the final answe.
    return maxval;
}

// Driver code
int main()
{
    int mat[][N] = {
        { 'X', 'O', 'X', 'X', 'X', 'X' },
        { 'X', 'O', 'X', 'X', 'O', 'X' },
        { 'X', 'X', 'X', 'O', 'O', 'X' },
        { 'O', 'X', 'X', 'X', 'X', 'X' },
        { 'X', 'X', 'X', 'O', 'X', 'O' },
        { 'O', 'O', 'X', 'O', 'O', 'O' },
    };

    // Function call
    cout << maximumSubSquare(mat);
    return 0;
}
```

输出：

```
4
```

时间复杂度：`O(N ^ 2)`。

辅助空间复杂度：`O(N ^ 2)`。