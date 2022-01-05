# 在矩阵中找到安全的细胞

> 原文:[https://www.geeksforgeeks.org/find-safe-cells-in-a-matrix/](https://www.geeksforgeeks.org/find-safe-cells-in-a-matrix/)

给定一个矩阵**mat【】【】**包含 **Z** 、 **P** 和 ***** 其中 **Z** 为僵尸， **P** 为植物， ***** 为裸地。假设一个僵尸可以攻击一个植物，如果这个植物和僵尸相邻的话(总共 8 个相邻的细胞是可能的)。任务是打印出可以安全躲避僵尸的植物数量。

**示例:**

```
Input: 
mat[] = { "**P*",
          "*Z**", 
          "*Z**", 
          "***P" }
Output: 1

Input: 
mat[] = { "**P*P", 
          "*Z**", 
          "*P**", 
          "***P" }
Output: 2
```

**方法:**逐元素遍历矩阵元素，如果当前元素是植物，即 **mat[i][j] = 'P'** 然后检查植物是否被任何僵尸包围(在所有 8 个相邻的细胞中)。如果工厂是安全的，那么更新**计数=计数+ 1** 。最后打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if mat[i][j] is a zombie
bool isZombie(int i, int j, int r, int c, string mat[])
{
    if (i < 0 || j < 0 || i >= r || j >= c
        || mat[i][j] != 'Z')
        return false;

    return true;
}

// Function to return the count of plants
// that survived from the zombies attack
int Plant_Vs_Zombies(string mat[], int row, int col)
{
    int i, j, count = 0;

    for (i = 0; i < row; i++) {
        for (j = 0; j < col; j++) {

            // If current cell is a plant
            if (mat[i][j] == 'P') {

                // If current plant is safe from zombies
                if (!isZombie(i - 1, j - 1, row, col, mat)
                    && !isZombie(i - 1, j, row, col, mat)
                    && !isZombie(i - 1, j + 1, row, col, mat)
                    && !isZombie(i, j - 1, row, col, mat)
                    && !isZombie(i, j, row, col, mat)
                    && !isZombie(i, j + 1, row, col, mat)
                    && !isZombie(i + 1, j - 1, row, col, mat)
                    && !isZombie(i + 1, j, row, col, mat)
                    && !isZombie(i + 1, j + 1, row, col, mat)) {
                    count++;
                }
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    // Input matrix
    string mat[] = { "**P*", "*Z**", "*Z**", "***P" };

    // Rows and columns of the matrix
    int row = sizeof(mat) / sizeof(mat[0]);
    int col = mat[0].length();

    // Total plants survived
    cout << Plant_Vs_Zombies(mat, row, col);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach.

class GfG
{

    // Function that returns true if
    // mat[i][j] is a zombie
    static boolean isZombie(int i, int j, int r,
                            int c, String mat[])
    {
        if (i < 0 || j < 0 || i >= r || j >= c
            || mat[i].charAt(j) != 'Z')
            return false;

        return true;
    }

    // Function to return the count of plants
    // that survived from the zombies attack
    static int Plant_Vs_Zombies(String mat[],
                            int row, int col)
    {
        int i, j, count = 0;

        for (i = 0; i < row; i++)
        {
            for (j = 0; j < col; j++)
            {

                // If current cell is a plant
                if (mat[i].charAt(j) == 'P')
                {

                    // If current plant is safe from zombies
                    if (!isZombie(i - 1, j - 1, row, col, mat)
                        && !isZombie(i - 1, j, row, col, mat)
                        && !isZombie(i - 1, j + 1, row, col, mat)
                        && !isZombie(i, j - 1, row, col, mat)
                        && !isZombie(i, j, row, col, mat)
                        && !isZombie(i, j + 1, row, col, mat)
                        && !isZombie(i + 1, j - 1, row, col, mat)
                        && !isZombie(i + 1, j, row, col, mat)
                        && !isZombie(i + 1, j + 1, row, col, mat)) {
                        count++;
                    }
                }
            }
        }
        return count;
    }

    // Driver code
    public static void main(String []args)
    {

        // Input matrix
        String[] mat = { "**P*", "*Z**", "*Z**", "***P" };

        // Rows and columns of the matrix
        int row = mat.length;
        int col = mat[0].length();

        // Total plants survived
        System.out.println(Plant_Vs_Zombies(mat, row, col));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach.

# Function that returns true if
# mat[i][j] is a zombie
def isZombie(i, j, r, c, mat):

    if (i < 0 or j < 0 or i >= r or
        j >= c or mat[i][j] != 'Z'):
        return True;

    return False;

# Function to return the count of plants
# that survived from the zombies attack
def Plant_Vs_Zombies(mat, row, col):

    count = 0;

    for i in range(row):
        for j in range(col):

            # If current cell is a plant
            if (mat[i][j] == 'P'):

                # If current plant is safe from zombies
                if (isZombie(i - 1, j - 1, row, col, mat) and
                    isZombie(i - 1, j, row, col, mat) and
                    isZombie(i - 1, j + 1, row, col, mat) and
                    isZombie(i, j - 1, row, col, mat) and
                    isZombie(i, j, row, col, mat) and
                    isZombie(i, j + 1, row, col, mat) and
                    isZombie(i + 1, j - 1, row, col, mat) and
                    isZombie(i + 1, j, row, col, mat) and
                    isZombie(i + 1, j + 1, row, col, mat)):
                    count += 1;
    return count;

# Driver code

# Input matrix
mat = ["**P*", "*Z**", "*Z**", "***P"];

# Rows and columns of the matrix
row = len(mat);
col = len(mat[0]);

# Total plants survived
print(Plant_Vs_Zombies(mat, row, col));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach.
using System;

class GfG
{

    // Function that returns true if
    // mat[i][j] is a zombie
    static bool isZombie(int i, int j, int r,
                            int c, String []mat)
    {
        if (i < 0 || j < 0 || i >= r || j >= c
            || mat[i][j] != 'Z')
            return false;

        return true;
    }

    // Function to return the count of plants
    // that survived from the zombies attack
    static int Plant_Vs_Zombies(String []mat,
                            int row, int col)
    {
        int i, j, count = 0;

        for (i = 0; i < row; i++)
        {
            for (j = 0; j < col; j++)
            {

                // If current cell is a plant
                if (mat[i][j] == 'P')
                {

                    // If current plant is safe from zombies
                    if (!isZombie(i - 1, j - 1, row, col, mat)
                        && !isZombie(i - 1, j, row, col, mat)
                        && !isZombie(i - 1, j + 1, row, col, mat)
                        && !isZombie(i, j - 1, row, col, mat)
                        && !isZombie(i, j, row, col, mat)
                        && !isZombie(i, j + 1, row, col, mat)
                        && !isZombie(i + 1, j - 1, row, col, mat)
                        && !isZombie(i + 1, j, row, col, mat)
                        && !isZombie(i + 1, j + 1, row, col, mat))
                    {
                        count++;
                    }
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String []args)
    {

        // Input matrix
        String[] mat = { "**P*", "*Z**", "*Z**", "***P" };

        // Rows and columns of the matrix
        int row = mat.Length;
        int col = mat[0].Length;

        // Total plants survived
        Console.WriteLine(Plant_Vs_Zombies(mat, row, col));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach.

// Function that returns true if
// mat[i][j] is a zombie
function isZombie($i, $j, $r, $c, $mat)
{
    if ($i < 0 || $j < 0 || $i >= $r ||
        $j >= $c || $mat[$i][$j] != 'Z')
        return false;

    return true;
}

// Function to return the count of plants
// that survived from the zombies attack
function Plant_Vs_Zombies($mat, $row, $col)
{
    $i; $j; $count = 0;

    for ($i = 0; $i < $row; $i++)
    {
        for ($j = 0; $j < $col; $j++)
        {

            // If current cell is a plant
            if ($mat[$i][$j] == 'P')
            {

                // If current plant is safe from zombies
                if (!isZombie($i - 1, $j - 1, $row, $col, $mat) &&
                    !isZombie($i - 1, $j, $row, $col, $mat) &&
                    !isZombie($i - 1, $j + 1, $row, $col, $mat) &&
                    !isZombie($i, $j - 1, $row, $col, $mat) &&
                    !isZombie($i, $j, $row, $col, $mat) &&
                    !isZombie($i, $j + 1, $row, $col, $mat) &&
                    !isZombie($i + 1, $j - 1, $row, $col, $mat) &&
                    !isZombie($i + 1, $j, $row, $col, $mat) &&
                    !isZombie($i + 1, $j + 1, $row, $col, $mat))
                {
                    $count++;
                }
            }
        }
    }
    return $count;
}

// Driver code

// Input matrix
$mat = array( "**P*", "*Z**", "*Z**", "***P" );

// Rows and columns of the matrix
$row = sizeof($mat);
$col = strlen($mat[0]);

// Total plants survived
echo(Plant_Vs_Zombies($mat, $row, $col));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach.

// Function that returns true if
// mat[i][j] is a zombie
function isZombie(i, j, r, c, mat)
{
    if (i < 0 || j < 0 || i >= r ||
       j >= c || mat[i][j] != 'Z')
        return false;

    return true;
}

// Function to return the count of plants
// that survived from the zombies attack
function Plant_Vs_Zombies(mat, row, col)
{
    let i, j, count = 0;

    for(i = 0; i < row; i++)
    {
        for(j = 0; j < col; j++)
        {

            // If current cell is a plant
            if (mat[i][j] == 'P')
            {

                // If current plant is safe from zombies
                if (!isZombie(i - 1, j - 1, row, col, mat) &&
                    !isZombie(i - 1, j, row, col, mat) &&
                    !isZombie(i - 1, j + 1, row, col, mat) &&
                    !isZombie(i, j - 1, row, col, mat) &&
                    !isZombie(i, j, row, col, mat) &&
                    !isZombie(i, j + 1, row, col, mat) &&
                    !isZombie(i + 1, j - 1, row, col, mat) &&
                    !isZombie(i + 1, j, row, col, mat) &&
                    !isZombie(i + 1, j + 1, row, col, mat))
                {
                    count++;
                }
            }
        }
    }
    return count;
}

// Driver code

// Input matrix
let mat = [ "**P*", "*Z**", "*Z**", "***P" ];

// Rows and columns of the matrix
let row = mat.length;
let col = mat[0].length;

// Total plants survived
document.write(Plant_Vs_Zombies(mat, row, col));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
1
```