# 从方阵对角线中找出最小和最大的元素

> 原文:[https://www . geeksforgeeks . org/find-最小和最大元素-从正方形-矩阵-对角线/](https://www.geeksforgeeks.org/find-smallest-and-largest-element-from-square-matrix-diagonals/)

给定一个 n*n 阶的方阵，从给定矩阵的两条对角线上找出最小和最大的元素。

**示例:**

```
Input : matrix = {
            {1, 2, 3, 4, -10},
            {5, 6, 7, 8, 6},
            {1, 2, 11, 3, 4},
            {5, 6, 70, 5, 8},
            {4, 9, 7, 1, 5}};
Output :
Principal Diagonal Smallest Element:  1
Principal Diagonal Greatest Element :11
Secondary Diagonal Smallest Element: -10
Secondary Diagonal Greatest Element: 11
```

解决这个问题背后的思想是，首先检查遍历矩阵，并达到所有对角线元素(对于主对角线 i == j 和次对角线 i+j = size_of_matrix-1)，并将对角线元素与最小值和最大值变量进行比较，并获取新的最小值和最大值。二次对角线也是如此。

**以下是上述方法的实现:**

**例 1:与 O(n^2)复杂性:**

## C++

```
// CPP program to find smallest and
// largest elements of both diagonals
#include<bits/stdc++.h>
using namespace std;

// Function to find smallest and largest element
// from principal and secondary diagonal
void diagonalsMinMax(int mat[5][5])
{
    // take length of matrix
    int n = sizeof(*mat) / 4;
    if (n == 0)
        return;

    // declare and initialize variables
    // with appropriate value
    int principalMin = mat[0][0],
        principalMax = mat[0][0];
    int secondaryMin = mat[n - 1][0],
        secondaryMax = mat[n - 1][0];

    for (int i = 1; i < n; i++)
    {
        for (int j = 1; j < n; j++)
        {

            // Condition for principal
            // diagonal
            if (i == j)
            {

                // take new smallest value
                if (mat[i][j] < principalMin)
                {
                    principalMin = mat[i][j];
                }

                // take new largest value
                if (mat[i][j] > principalMax)
                {
                    principalMax = mat[i][j];
                }
            }

            // Condition for secondary
            // diagonal
            if ((i + j) == (n - 1))
            {

                // take new smallest value
                if (mat[i][j] < secondaryMin)
                {
                    secondaryMin = mat[i][j];
                }

                // take new largest value
                if (mat[i][j] > secondaryMax)
                {
                    secondaryMax = mat[i][j];
                }
            }
        }
    }

    cout << ("Principal Diagonal Smallest Element: ")
        << principalMin << endl;
    cout << ("Principal Diagonal Greatest Element : ")
        << principalMax << endl;

    cout << ("Secondary Diagonal Smallest Element: ")
        << secondaryMin << endl;
    cout << ("Secondary Diagonal Greatest Element: ")
        << secondaryMax << endl;
}

// Driver code
int main()
{
    // Declare and initialize 5X5 matrix
    int matrix[5][5] = {{ 1, 2, 3, 4, -10 },
                        { 5, 6, 7, 8, 6 },
                        { 1, 2, 11, 3, 4 },
                        { 5, 6, 70, 5, 8 },
                        { 4, 9, 7, 1, -5 }};
    diagonalsMinMax(matrix);
}

// This code is contributed by
// Shashank_Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// smallest and largest elements of both diagonals

public class GFG {
    // Function to find smallest and largest element from
    // principal and secondary diagonal
    static void diagonalsMinMax(int[][] mat)
    {
        // take length of matrix
        int n = mat.length;
        if (n == 0)
           return;

        // declare and initialize variables with appropriate value
        int principalMin = mat[0][0], principalMax = mat[0][0];
        int secondaryMin = mat[n-1][0], secondaryMax = mat[n-1][0];

        for (int i = 1; i < n; i++) {
            for (int j = 1; j < n; j++) {

                // Condition for principal
                // diagonal
                if (i == j) {

                    // take new smallest value
                    if (mat[i][j] < principalMin) {
                        principalMin = mat[i][j];
                    }

                    // take new largest value
                    if (mat[i][j] > principalMax) {
                        principalMax = mat[i][j];
                    }
                }

                // Condition for secondary
                // diagonal
                if ((i + j) == (n - 1)) {

                    // take new smallest value
                    if (mat[i][j] < secondaryMin) {
                        secondaryMin = mat[i][j];
                    }

                    // take new largest value
                    if (mat[i][j] > secondaryMax) {
                        secondaryMax = mat[i][j];
                    }
                }
            }
        }

        System.out.println("Principal Diagonal Smallest Element:  "
                           + principalMin);
        System.out.println("Principal Diagonal Greatest Element : "
                           + principalMax);

        System.out.println("Secondary Diagonal Smallest Element: "
                           + secondaryMin);
        System.out.println("Secondary Diagonal Greatest Element: "
                           + secondaryMax);
    }

    // Driver code
    static public void main(String[] args)
    {

        // Declare and initialize 5X5 matrix
        int[][] matrix = {
            { 1, 2, 3, 4, -10 },
            { 5, 6, 7, 8, 6 },
            { 1, 2, 11, 3, 4 },
            { 5, 6, 70, 5, 8 },
            { 4, 9, 7, 1, -5 }
        };

        diagonalsMinMax(matrix);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find smallest and
# largest elements of both diagonals

# Function to find smallest and largest element
# from principal and secondary diagonal
def diagonalsMinMax(mat):

    # take length of matrix
    n = len(mat)
    if (n == 0):
        return

    # declare and initialize variables
    # with appropriate value
    principalMin = mat[0][0]
    principalMax = mat[0][0]
    secondaryMin = mat[0][n-1]
    secondaryMax = mat[0][n-1]

    for i in range(1, n):

        for j in range(1, n):

            # Condition for principal
            # diagonal
            if (i == j):

                # take new smallest value
                if (mat[i][j] < principalMin):

                    principalMin = mat[i][j]

                # take new largest value
                if (mat[i][j] > principalMax):

                    principalMax = mat[i][j]

            # Condition for secondary
            # diagonal
            if ((i + j) == (n - 1)):

                # take new smallest value
                if (mat[i][j] < secondaryMin):

                    secondaryMin = mat[i][j]

                # take new largest value
                if (mat[i][j] > secondaryMax):

                    secondaryMax = mat[i][j]

    print("Principal Diagonal Smallest Element: ",
                                     principalMin)
    print("Principal Diagonal Greatest Element : ",
                                      principalMax)

    print("Secondary Diagonal Smallest Element: ",
                                     secondaryMin)
    print("Secondary Diagonal Greatest Element: ",
                                     secondaryMax)

# Driver code

# Declare and initialize 5X5 matrix
matrix = [[ 1, 2, 3, 4, -10 ],
          [ 5, 6, 7, 8, 6 ],
          [ 1, 2, 11, 3, 4 ],
          [ 5, 6, 70, 5, 8 ],
          [ 4, 9, 7, 1, -5 ]]
diagonalsMinMax(matrix)

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to find smallest and largest
//  elements of both diagonals
using System;

public class GFG {
    // Function to find smallest and largest element from
    // principal and secondary diagonal
    static void diagonalsMinMax(int[,] mat)
    {
        // take length of square matrix
        int n = mat.GetLength(0);
        if (n == 0)
        return;

        // declare and initialize variables with appropriate value
        int principalMin = mat[0,0], principalMax = mat[0,0];
        int secondaryMin = mat[n-1,0], secondaryMax = mat[n-1,0];

        for (int i = 1; i < n; i++) {
            for (int j = 1; j < n; j++) {

                // Condition for principal
                // diagonal
                if (i == j) {

                    // take new smallest value
                    if (mat[i,j] < principalMin) {
                        principalMin = mat[i,j];
                    }

                    // take new largest value
                    if (mat[i,j] > principalMax) {
                        principalMax = mat[i,j];
                    }
                }

                // Condition for secondary
                // diagonal
                if ((i + j) == (n - 1)) {

                    // take new smallest value
                    if (mat[i,j] < secondaryMin) {
                        secondaryMin = mat[i,j];
                    }

                    // take new largest value
                    if (mat[i,j] > secondaryMax) {
                        secondaryMax = mat[i,j];
                    }
                }
            }
        }

        Console.WriteLine("Principal Diagonal Smallest Element: "
                        + principalMin);
        Console.WriteLine("Principal Diagonal Greatest Element : "
                        + principalMax);

        Console.WriteLine("Secondary Diagonal Smallest Element: "
                        + secondaryMin);
        Console.WriteLine("Secondary Diagonal Greatest Element: "
                        + secondaryMax);
    }

    // Driver code
    static void Main()
    {

        // Declare and initialize 5X5 matrix
        int[,] matrix = {
            { 1, 2, 3, 4, -10 },
            { 5, 6, 7, 8, 6 },
            { 1, 2, 11, 3, 4 },
            { 5, 6, 70, 5, 8 },
            { 4, 9, 7, 1, -5 }
        };

        diagonalsMinMax(matrix);
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest and
// largest elements of both diagonals

// Function to find smallest and largest element
// from principal and secondary diagonal
function diagonalsMinMax($mat)
{
    // take length of $matrix
    $n = count($mat);
    if ($n == 0)
        return;

    // declare and initialize variables
    // with appropriate value
    $principalMin = $mat[0][0];
    $principalMax = $mat[0][0];
    $secondaryMin = $mat[$n - 1][0];
    $secondaryMax = $mat[$n - 1][0];

    for ($i = 1; $i < $n; $i++)
    {
        for ($j = 1; $j < $n; $j++)
        {

            // Condition for principal
            // diagonal
            if ($i == $j)
            {

                // take new smallest value
                if ($mat[$i][$j] < $principalMin)
                {
                    $principalMin = $mat[$i][$j];
                }

                // take new largest value
                if ($mat[$i][$j] > $principalMax)
                {
                    $principalMax = $mat[$i][$j];
                }
            }

            // Condition for secondary
            // diagonal
            if (($i + $j) == ($n - 1))
            {

                // take new smallest value
                if ($mat[$i][$j] < $secondaryMin)
                {
                    $secondaryMin = $mat[$i][$j];
                }

                // take new largest value
                if ($mat[$i][$j] > $secondaryMax)
                {
                    $secondaryMax = $mat[$i][$j];
                }
            }
        }
    }

    echo "Principal Diagonal Smallest Element: ",
                             $principalMin, "\n";
    echo "Principal Diagonal Greatest Element : ",
                              $principalMax, "\n";

    echo "Secondary Diagonal Smallest Element: ",
                             $secondaryMin, "\n";
    echo "Secondary Diagonal Greatest Element: ",
                             $secondaryMax, "\n";
}

// Driver code

// Declare and initialize 5X5 matrix
$matrix = array(array ( 1, 2, 3, 4, -10 ),
                array ( 5, 6, 7, 8, 6 ),
                array ( 1, 2, 11, 3, 4 ),
                array ( 5, 6, 70, 5, 8 ),
                array ( 4, 9, 7, 1, -5 ));
diagonalsMinMax($matrix);

// This code is contributed by
// ihritik
?>
```

## java 描述语言

```
<script>
// Javascript program to find smallest and
// largest elements of both diagonals

// Function to find smallest and largest element
// from principal and secondary diagonal
function diagonalsMinMax(mat)
{
    // take length of matrix
    let n = mat.length;
    if (n == 0)
        return;

    // declare and initialize variables
    // with appropriate value
    let principalMin = mat[0][0],
        principalMax = mat[0][0];
    let secondaryMin = mat[n - 1][0],
        secondaryMax = mat[n - 1][0];

    for (let i = 1; i < n; i++)
    {
        for (let j = 1; j < n; j++)
        {

            // Condition for principal
            // diagonal
            if (i == j)
            {

                // take new smallest value
                if (mat[i][j] < principalMin)
                {
                    principalMin = mat[i][j];
                }

                // take new largest value
                if (mat[i][j] > principalMax)
                {
                    principalMax = mat[i][j];
                }
            }

            // Condition for secondary
            // diagonal
            if ((i + j) == (n - 1))
            {

                // take new smallest value
                if (mat[i][j] < secondaryMin)
                {
                    secondaryMin = mat[i][j];
                }

                // take new largest value
                if (mat[i][j] > secondaryMax)
                {
                    secondaryMax = mat[i][j];
                }
            }
        }
    }

    document.write("Principal Diagonal Smallest Element: "
        + principalMin + "<br>");
    document.write("Principal Diagonal Greatest Element : "
        + principalMax + "<br>");

    document.write("Secondary Diagonal Smallest Element: "
        + secondaryMin + "<br>");
    document.write("Secondary Diagonal Greatest Element: "
        + secondaryMax + "<br>");
}

// Driver code
    // Declare and initialize 5X5 matrix
    let matrix = [[ 1, 2, 3, 4, -10 ],
                        [ 5, 6, 7, 8, 6 ],
                        [ 1, 2, 11, 3, 4 ],
                        [ 5, 6, 70, 5, 8 ],
                        [ 4, 9, 7, 1, -5 ]];
    diagonalsMinMax(matrix);

// This code is contributed by subham348.
</script>
```

**Output:** 

```
Principal Diagonal Smallest Element:  -5
Principal Diagonal Greatest Element : 11
Secondary Diagonal Smallest Element: 4
Secondary Diagonal Greatest Element: 11
```

**示例 2:具有 O(n)复杂度:**

## C++

```
// C++ program to find
// smallest and largest elements of both diagonals
#include<bits/stdc++.h>
using namespace std;

const int n = 5;

// Function to find smallest and largest element
// from principal and secondary diagonal
void diagonalsMinMax(int mat [n][n])
{
    // take length of matrix
    if (n == 0)
        return;

    // declare and initialize variables
    // with appropriate value
    int principalMin = mat[0][0],
        principalMax = mat[0][0];
    int secondaryMin = mat[n - 1][0],
        secondaryMax = mat[n - 1][0];

    for (int i = 0; i < n; i++)
    {

        // Condition for principal
        // diagonal mat[i][i]

        // take new smallest value
        if (mat[i][i] < principalMin)
        {
            principalMin = mat[i][i];
        }

        // take new largest value
        if (mat[i][i] > principalMax)
        {
            principalMax = mat[i][i];
        }

        // Condition for secondary
        // diagonal is mat[n-1-i][i]
        // take new smallest value
        if (mat[n - 1 - i][i] < secondaryMin)
        {
            secondaryMin = mat[n - 1 - i][i];
        }

        // take new largest value
        if (mat[n - 1 - i][i] > secondaryMax)
        {
            secondaryMax = mat[n - 1 - i][i];
        }
    }
    cout << "Principal Diagonal Smallest Element: "
         << principalMin << "\n";
    cout << "Principal Diagonal Greatest Element : "
         << principalMax << "\n";

    cout << "Secondary Diagonal Smallest Element: "
         << secondaryMin << "\n";
    cout << "Secondary Diagonal Greatest Element: "
         << secondaryMax;
}

// Driver code
int main()
{

    // Declare and initialize 5X5 matrix
    int matrix [n][n] = {{ 1, 2, 3, 4, -10 },
                         { 5, 6, 7, 8, 6 },
                         { 1, 2, 11, 3, 4 },
                         { 5, 6, 70, 5, 8 },
                         { 4, 9, 7, 1, -5 }};

    diagonalsMinMax(matrix);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// smallest and largest elements of both diagonals

public class GFG {

    // Function to find smallest and largest element from
    // principal and secondary diagonal
    static void diagonalsMinMax(int[][] mat)
    {
        // take length of matrix
        int n = mat.length;
        if (n == 0)
           return;

        // declare and initialism variables with appropriate value
        int principalMin = mat[0][0], principalMax = mat[0][0];
        int secondaryMin = mat[n-1][0], secondaryMax = mat[n-1][0];

        for (int i = 0; i < n; i++) {

            // Condition for principal
            // diagonal mat[i][i]

            // take new smallest value
            if (mat[i][i] < principalMin) {
                principalMin = mat[i][i];
            }
            // take new largest value
            if (mat[i][i] > principalMax) {
                principalMax = mat[i][i];
            }

            // Condition for secondary
            // diagonal is mat[n-1-i][i]
            // take new smallest value
            if (mat[n - 1 - i][i] < secondaryMin) {
                secondaryMin = mat[n - 1 - i][i];
            }
            // take new largest value
            if (mat[n - 1 - i][i] > secondaryMax) {
                secondaryMax = mat[n - 1 - i][i];
            }
        }
        System.out.println("Principal Diagonal Smallest Element:  "
                           + principalMin);
        System.out.println("Principal Diagonal Greatest Element : "
                           + principalMax);

        System.out.println("Secondary Diagonal Smallest Element: "
                           + secondaryMin);
        System.out.println("Secondary Diagonal Greatest Element: "
                           + secondaryMax);
    }

    // Driver code
    static public void main(String[] args)
    {

        // Declare and initialize 5X5 matrix
        int[][] matrix = {
            { 1, 2, 3, 4, -10 },
            { 5, 6, 7, 8, 6 },
            { 1, 2, 11, 3, 4 },
            { 5, 6, 70, 5, 8 },
            { 4, 9, 7, 1, -5 }
        };

        diagonalsMinMax(matrix);
    }
}
```

## 计算机编程语言

```
# Python3 program to find smallest and
# largest elements of both diagonals

n = 5

# Function to find smallest and largest element
# from principal and secondary diagonal
def diagonalsMinMax(mat):

    # take length of matrix
    if (n == 0):
        return

    # declare and initialize variables
    # with appropriate value
    principalMin = mat[0][0]
    principalMax = mat[0][0]
    secondaryMin = mat[n - 1][0]
    secondaryMax = mat[n - 1][0]

    for i in range(n):

        # Condition for principal
        # diagonal mat[i][i]

        # take new smallest value
        if (mat[i][i] < principalMin):
            principalMin = mat[i][i]

        # take new largest value
        if (mat[i][i] > principalMax):
            principalMax = mat[i][i]

        # Condition for secondary
        # diagonal is mat[n-1-i][i]
        # take new smallest value
        if (mat[n - 1 - i][i] < secondaryMin):
            secondaryMin = mat[n - 1 - i][i]

        # take new largest value
        if (mat[n - 1 - i][i] > secondaryMax):
            secondaryMax = mat[n - 1 - i][i]

    print("Principal Diagonal Smallest Element: ",principalMin)
    print("Principal Diagonal Greatest Element : ",principalMax)

    print("Secondary Diagonal Smallest Element: ",secondaryMin)
    print("Secondary Diagonal Greatest Element: ",secondaryMax)

# Driver code

# Declare and initialize 5X5 matrix
matrix= [[ 1, 2, 3, 4, -10 ],
        [ 5, 6, 7, 8, 6 ],
        [ 1, 2, 11, 3, 4 ],
        [ 5, 6, 70, 5, 8 ],
        [ 4, 9, 7, 1, -5 ]]

diagonalsMinMax(matrix)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find smallest and largest
// elements of both diagonals
using System;

public class GFG {
    // Function to find smallest and largest element from
    // principal and secondary diagonal
    static void diagonalsMinMax(int[,] mat)
    {
        // take length of square matrix
        int n = mat.GetLength(0);
        if (n == 0)
        return;

        // declare and initialize variables with appropriate value
        int principalMin = mat[0,0], principalMax = mat[0,0];
        int secondaryMin = mat[n-1,0], secondaryMax = mat[n-1,0];

        for (int i = 0; i < n; i++) {

            // Condition for principal
            // diagonal mat[i][i]

            // take new smallest value
            if (mat[i,i] < principalMin) {
                principalMin = mat[i,i];
            }
            // take new largest value
            if (mat[i,i] > principalMax) {
                principalMax = mat[i,i];
            }

            // Condition for secondary
            // diagonal is mat[n-1-i][i]
            // take new smallest value
            if (mat[n - 1 - i,i] < secondaryMin) {
                secondaryMin = mat[n - 1 - i,i];
            }
            // take new largest value
            if (mat[n - 1 - i,i] > secondaryMax) {
                secondaryMax = mat[n - 1 - i,i];
            }

        }

        Console.WriteLine("Principal Diagonal Smallest Element: "
                        + principalMin);
        Console.WriteLine("Principal Diagonal Greatest Element : "
                        + principalMax);

        Console.WriteLine("Secondary Diagonal Smallest Element: "
                        + secondaryMin);
        Console.WriteLine("Secondary Diagonal Greatest Element: "
                        + secondaryMax);
    }

    // Driver code
    public static void Main()
    {

        // Declare and initialize 5X5 matrix
        int[,] matrix = {
            { 1, 2, 3, 4, -10 },
            { 5, 6, 7, 8, 6 },
            { 1, 2, 11, 3, 4 },
            { 5, 6, 70, 5, 8 },
            { 4, 9, 7, 1, -5 }
        };

        diagonalsMinMax(matrix);
    }
}

/*This code is contributed by 29AjayKumar*/
```

## java 描述语言

```
<script>

// JavaScript program to find
// smallest and largest elements
// of both diagonals

    // Function to find smallest
    // and largest element from
    // principal and secondary diagonal
    function diagonalsMinMax(mat)
    {
        // take length of matrix
        let n = mat.length;
        if (n == 0)
        return;

        // declare and initialism variables
        // with appropriate value
        let principalMin = mat[0][0],
            principalMax = mat[0][0];
        let secondaryMin = mat[n-1][0],
            secondaryMax = mat[n-1][0];

        for (let i = 0; i < n; i++) {

            // Condition for principal
            // diagonal mat[i][i]

            // take new smallest value
            if (mat[i][i] < principalMin) {
                principalMin = mat[i][i];
            }
            // take new largest value
            if (mat[i][i] > principalMax) {
                principalMax = mat[i][i];
            }

            // Condition for secondary
            // diagonal is mat[n-1-i][i]
            // take new smallest value
            if (mat[n - 1 - i][i] < secondaryMin) {
                secondaryMin = mat[n - 1 - i][i];
            }
            // take new largest value
            if (mat[n - 1 - i][i] > secondaryMax) {
                secondaryMax = mat[n - 1 - i][i];
            }
        }
        document.write("Principal Diagonal Smallest Element: "
                        + principalMin+"<br>");
        document.write("Principal Diagonal Greatest Element : "
                        + principalMax+"<br>");

        document.write("Secondary Diagonal Smallest Element: "
                        + secondaryMin+"<br>");
        document.write("Secondary Diagonal Greatest Element: "
                        + secondaryMax+"<br>");
    }

    // Driver code

        // Declare and initialize 5X5 matrix
        let matrix = [
            [ 1, 2, 3, 4, -10 ],
            [ 5, 6, 7, 8, 6 ],
            [ 1, 2, 11, 3, 4 ],
            [ 5, 6, 70, 5, 8 ],
            [ 4, 9, 7, 1, -5 ]
        ];

        diagonalsMinMax(matrix);

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
Principal Diagonal Smallest Element:  -5
Principal Diagonal Greatest Element : 11
Secondary Diagonal Smallest Element: -10
Secondary Diagonal Greatest Element: 11
```