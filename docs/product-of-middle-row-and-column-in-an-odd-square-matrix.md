# 奇数方阵中中间行和中间列的乘积

> 原文:[https://www . geesforgeks . org/奇数方阵中行列积/](https://www.geeksforgeeks.org/product-of-middle-row-and-column-in-an-odd-square-matrix/)

给定奇数维(3 * 3，5 * 5)的整数方阵。任务是找到中间行和中间列元素的乘积。

**示例:**

```
Input: mat[][] = 
{{2, 1, 7},
 {3, 7, 2},
 {5, 4, 9}}
Output: Product of middle row = 42
        Product of middle column = 28
Explanation: Product of Middle row elements (3*7*2)
Product of Middle Column elements (1*7*4)

Input: mat[][] =
{ {1, 3, 5, 6, 7},
  {3, 5, 3, 2, 1},
  {1, 2, 3, 4, 5},
  {7, 9, 2, 1, 6},
  {9, 1, 5, 3, 2}}
Output: Product of middle row = 120
        Product of middle column = 450 
```

**方法:**由于给定的矩阵是奇数维的，所以中间的行和列总是在 n/2。因此，运行一个从 i = 0 到 N 的循环，生成中间行的所有元素，即 **row_prod *= mat[n / 2][i]** 。同样，中间一列元素的乘积将是 **col_prod *= mat[i][n / 2]** 。

下面是上述方法的实现:

## C++

```
// C++ program to find product of
// middle row and middle column in matrix
#include <iostream>
using namespace std;
const int MAX = 100;

void middleProduct(int mat[][MAX], int n)
{

    // loop for product of row and column
    int row_prod = 1, col_prod = 1;
    for (int i = 0; i < n; i++) {
        row_prod *= mat[n / 2][i];
        col_prod *= mat[i][n / 2];
    }

    // Print result
    cout << "Product of middle row = "
         << row_prod << endl;

    cout << "Product of middle column = "
         << col_prod;
}

// Driver code
int main()
{
    int mat[][MAX] = { { 2, 1, 7 },
                       { 3, 7, 2 },
                       { 5, 4, 9 } };

    middleProduct(mat, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of
// middle row and middle column in matrix
import java.io.*;

class GFG {

static int MAX = 100;

static void middleProduct(int mat[][], int n)
{

    // loop for product of row and column
    int row_prod = 1, col_prod = 1;
    for (int i = 0; i < n; i++) {
        row_prod *= mat[n / 2][i];
        col_prod *= mat[i][n / 2];
    }

    // Print result
    System.out.print("Product of middle row = "
        + row_prod);

    System.out.print( "Product of middle column = "
        + col_prod);
}

    // Driver code
    public static void main (String[] args) {
            int mat[][] = { { 2, 1, 7 },
                    { 3, 7, 2 },
                    { 5, 4, 9 } };

    middleProduct(mat, 3);
    }
}
// This code is contributed by shs
```

## 蟒蛇 3

```
# Python3 program to find product of
# middle row and middle column in matrix

MAX = 100

def middleProduct(mat, n):

    # loop for product of row and column
    row_prod = 1
    col_prod = 1
    for i in range(n) :
        row_prod *= mat[n // 2][i]
        col_prod *= mat[i][n // 2]

    # Print result
    print ("Product of middle row = ",
                             row_prod)

    print ("Product of middle column = ",
                                col_prod)

# Driver code
if __name__ == "__main__":

    mat = [[ 2, 1, 7 ],
           [ 3, 7, 2 ],
           [ 5, 4, 9 ]]

    middleProduct(mat, 3)

# This code is contributed by ita_c   
```

## C#

```
// C# program to find product of
// middle row and middle column in matrix
using System;

class GFG {

//static int MAX = 100;

static void middleProduct(int [,]mat, int n)
{

    // loop for product of row and column
    int row_prod = 1, col_prod = 1;
    for (int i = 0; i < n; i++) {
        row_prod *= mat[n / 2,i];
        col_prod *= mat[i,n / 2];
    }

    // Print result
    Console.WriteLine("Product of middle row = "
        + row_prod);

    Console.WriteLine( "Product of middle column = "
        + col_prod);
}

    // Driver code
    public static void Main () {
            int [,]mat = { { 2, 1, 7 },
                    { 3, 7, 2 },
                    { 5, 4, 9 } };

    middleProduct(mat, 3);
    }
}
// This code is contributed by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product of
// middle row and middle column in matrix

$MAX = 100;

function middleProduct($mat, $n)
{

    // loop for product of row and column
    $row_prod = 1; $col_prod = 1;
    for ($i = 0; $i < $n; $i++)
    {
        $row_prod *= $mat[$n / 2][$i];
        $col_prod *= $mat[$i][$n / 2];
    }

    // Print result
    echo "Product of middle row = " .
                    $row_prod . "\n";

    echo "Product of middle column = " .
                              $col_prod;
}

// Driver code
$mat= array(array( 2, 1, 7 ),
            array( 3, 7, 2 ),
            array( 5, 4, 9 ));

middleProduct($mat, 3);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to find product of
// middle row and middle column in matrix

    let MAX = 100;
    function middleProduct(mat,n)
    {
        // loop for product of row and column
        let row_prod = 1, col_prod = 1;
        for (let i = 0; i < n; i++) {
            row_prod *= mat[Math.floor(n / 2)][i];
            col_prod *= mat[i][Math.floor(n / 2)];
        }

        // Print result
        document.write("Product of middle row = "
            + row_prod+"<br>");

            document.write( "Product of middle column = "
            + col_prod+"<br>");
    }

    // Driver code
    let mat = [[ 2, 1, 7 ],
                  [ 3, 7, 2 ],
               [ 5, 4, 9 ]];

    middleProduct(mat, 3);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Product of middle row = 42
Product of middle column = 28
```

**时间复杂度:** O(n)