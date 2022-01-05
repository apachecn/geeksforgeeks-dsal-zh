# 计算网格中的魔方

> 原文:[https://www . geeksforgeeks . org/count-网格幻方/](https://www.geeksforgeeks.org/count-magic-squares-in-a-grid/)

给定一个整数**网格**。任务是在给定的网格中找到 3×3(连续的)**幻方子网格**的总数。幻方是一个 3×3 的格子，里面填满了从 1 到 9 的所有不同的数字，这样每一行、每一列和两条对角线的和都相等。
**例:**

> 输入:G = { { 4，3，8，4 }，{ 9，5，1，9 }，{ 2，7，6，2 } }
> 输出:1
> 说明:下面的子格是一个 3×3 的幻方:[ 4 3 8，9 5 1，2 7 6 ]
> 输入:G = { { 1，2，3，4，5 }，{ 6，7，8，9，10 }，{ 10，11，12，13，14 }，{ 15，16

**方法:**让我们分别检查每 3×3 个子网格。对于每个网格，所有数字必须是唯一的，并且在 **(1 和 9)** 之间以及每**行**、**列**之间，并且两条**对角线**必须具有相等的总和。
还要注意，如果一个子网格的中间元素是 5，那么这个子网格就是幻方。因为将穿过中心的四条线的 12 个值相加，加起来是 60，但它们也加起来是整个网格(45)，加上中间值的 3 倍。这意味着中间值是 5。因此，我们可以检查这个条件，这有助于我们跳过各种子网格。
你可以在这里[魔方](https://en.wikipedia.org/wiki/Magic_square)或者在这里[这里](https://www.geeksforgeeks.org/magic-square/)了解更多。
检查子网格是否为幻方的步骤如下:

> *   The middle element must be 5.
> *   The sum of the grid must be 45 and contain all different values from 1 to 9.
> *   Each row and column must add up to 15.
> *   The sum of the two diagonals must also be 15.

**以下是上述方法的实施:**

## C++

```
// CPP program to count magic squares
#include <bits/stdc++.h>
using namespace std;

const int R = 3;
const int C = 4;

// function to check is subgrid is Magic Square
int magic(int a, int b, int c, int d, int e,
                int f, int g, int h, int i)
{
    set<int> s1 = { a, b, c, d, e, f, g, h, i },
             s2 = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

    // Elements of grid must contain all numbers from 1 to
    // 9, sum of all rows, columns and diagonals must be
    // same, i.e., 15.
    if (s1 == s2 && (a + b + c) == 15 && (d + e + f) == 15 &&
       (g + h + i) == 15 && (a + d + g) == 15 &&                    
       (b + e + h) == 15 && (c + f + i) == 15 &&
       (a + e + i) == 15 && (c + e + g) == 15)
       return true;
    return false;   
}

// Function to count total Magic square subgrids
int CountMagicSquare(int Grid[R][C])
{
    int ans = 0;

    for (int i = 0; i < R - 2; i++)
        for (int j = 0; j < C - 2; j++) {

            // if condition true skip check
            if (Grid[i + 1][j + 1] != 5)
                continue;

            // check for magic square subgrid
            if (magic(Grid[i][j], Grid[i][j + 1],
                Grid[i][j + 2], Grid[i + 1][j],
                Grid[i + 1][j + 1], Grid[i + 1][j + 2],
                Grid[i + 2][j], Grid[i + 2][j + 1],
                Grid[i + 2][j + 2]))

                ans += 1;
          cout<<"ans = "<<ans<<endl;
        }

    // return total magic square
    return ans;
}

// Driver program
int main()
{
    int G[R][C] = { { 4, 3, 8, 4 },
                    { 9, 5, 1, 9 },
                    { 2, 7, 6, 2 } };

    // function call to print required answer
    cout << CountMagicSquare(G);

    return 0;
}

// This code is written by Sanjit_Prasad
```

## 蟒蛇 3

```
# Python3 program to count magic squares
R = 3
C = 4

# function to check is subgrid is Magic Square
def magic(a, b, c, d, e, f, g, h, i):

    s1 = set([a, b, c, d, e, f, g, h, i])
    s2 = set([1, 2, 3, 4, 5, 6, 7, 8, 9])

    # Elements of grid must contain all numbers
    # from 1 to 9, sum of all rows, columns and
    # diagonals must be same, i.e., 15.
    if (s1 == s2 and (a + b + c) == 15 and
       (d + e + f) == 15 and (g + h + i) == 15 and
       (a + d + g) == 15 and (b + e + h) == 15 and
       (c + f + i) == 15 and (a + e + i) == 15 and
       (c + e + g) == 15):
        return True

    return false    

# Function to count total Magic square subgrids
def CountMagicSquare(Grid):

    ans = 0

    for i in range(0, R - 2):
        for j in range(0, C - 2):

            # if condition true skip check
            if Grid[i + 1][j + 1] != 5:
                continue

            # check for magic square subgrid
            if (magic(Grid[i][j], Grid[i][j + 1],
                  Grid[i][j + 2], Grid[i + 1][j],
                  Grid[i + 1][j + 1], Grid[i + 1][j + 2],
                  Grid[i + 2][j], Grid[i + 2][j + 1],
                  Grid[i + 2][j + 2]) == True):

                ans += 1

    # return total magic square
    return ans

# Driver Code
if __name__ == "__main__":

    G = [[4, 3, 8, 4],
         [9, 5, 1, 9],
         [2, 7, 6, 2]]

    # Function call to print required answer
    print(CountMagicSquare(G))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count magic squares
using System;
using System.Collections.Generic;

class GFg {
    const int R = 3;
    const int C = 4;

    // function to check is subgrid is Magic Square
    static int magic(int a, int b, int c, int d, int e,
                     int f, int g, int h, int i)
    {
        HashSet<int> s1 = new HashSet<int>() {
            a, b, c, d, e, f, g, h, i
        };
        HashSet<int> s2 = new HashSet<int>() {
            1, 2, 3, 4, 5, 6, 7, 8, 9
        };

        // Elements of grid must contain all numbers from 1
        // to 9, sum of all rows, columns and diagonals must
        // be same, i.e., 15.
        if (s1.SetEquals(s2) && (a + b + c) == 15
            && (d + e + f) == 15 && (g + h + i) == 15
            && (a + d + g) == 15 && (b + e + h) == 15
            && (c + f + i) == 15 && (a + e + i) == 15
            && (c + e + g) == 15)
            return 1;
        return 0;
    }

    // Function to count total Magic square subgrids
    static int CountMagicSquare(int[, ] Grid)
    {
        int ans = 0;

        for (int i = 0; i < R - 2; i++)
            for (int j = 0; j < C - 2; j++) {

                // if condition true skip check
                if (Grid[i + 1, j + 1] != 5)
                    continue;

                // check for magic square subgrid
                if (magic(Grid[i, j], Grid[i, j + 1],
                          Grid[i, j + 2], Grid[i + 1, j],
                          Grid[i + 1, j + 1],
                          Grid[i + 1, j + 2],
                          Grid[i + 2, j],
                          Grid[i + 2, j + 1],
                          Grid[i + 2, j + 2])
                    != 0)

                    ans += 1;
            }

        // return total magic square
        return ans;
    }

    // Driver program
    public static void Main()
    {
        int[, ] G = { { 4, 3, 8, 4 },
                      { 9, 5, 1, 9 },
                      { 2, 7, 6, 2 } };

        // function call to print required answer
        Console.WriteLine(CountMagicSquare(G));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to count magic squares
var R = 3;
var C = 4;

function eqSet(as, bs) {
    if (as.size !== bs.size) return false;
    for (var a of as) if (!bs.has(a)) return false;
    return true;
}

// function to check is subgrid is Magic Square
function magic(a, b, c, d, e, f, g, h, i)
{
    var s1 = new Set([a, b, c, d, e, f, g, h, i]);
    var s2 = new Set([ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]);

    // Elements of grid must contain all numbers from 1 to
    // 9, sum of all rows, columns and diagonals must be
    // same, i.e., 15.
    if (eqSet(s1, s2) && (a + b + c) == 15 && (d + e + f) == 15 &&
       (g + h + i) == 15 && (a + d + g) == 15 &&                    
       (b + e + h) == 15 && (c + f + i) == 15 &&
       (a + e + i) == 15 && (c + e + g) == 15)
       return true;
    return false;   
}

// Function to count total Magic square subgrids
function CountMagicSquare(Grid)
{
    var ans = 0;

    for (var i = 0; i < R - 2; i++)
        for (var j = 0; j < C - 2; j++) {

            // if condition true skip check
            if (Grid[i + 1][j + 1] != 5)
                continue;

            // check for magic square subgrid
            if (magic(Grid[i][j], Grid[i][j + 1],
                Grid[i][j + 2], Grid[i + 1][j],
                Grid[i + 1][j + 1], Grid[i + 1][j + 2],
                Grid[i + 2][j], Grid[i + 2][j + 1],
                Grid[i + 2][j + 2]))
                ans += 1;
        }

    // return total magic square
    return ans;
}

// Driver program
var G = [[4, 3, 8, 4 ],
                [ 9, 5, 1, 9 ],
                [ 2, 7, 6, 2 ]];
// function call to print required answer
document.write( CountMagicSquare(G));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(R * C)