# 通过改变任意子矩阵角元素的奇偶性来检查矩阵 A 是否可以转换为 B

> 原文:[https://www . geeksforgeeks . org/check-if-matrix-a-可以通过改变任意子矩阵的角元素奇偶性来转换为 b/](https://www.geeksforgeeks.org/check-if-matrix-a-can-be-converted-to-b-by-changing-parity-of-corner-elements-of-any-submatrix/)

给定两个二元矩阵， **N×M** 的 **A[][]** 和 **B[][]** 。在一次操作中，可以选择一个子矩阵(最小 2 行 2c 列)并改变角元素的奇偶性，即 **1** 可以变为 **0** ，而 **0** 可以变为 **1** 。任务是检查矩阵 A 是否可以用任意数量的运算转换成 B。

**示例:**

> **输入:** A[][] = {{0，1，0}，{0，1，0}，{1，0，0}}，
> B[][] = {{1，0，0}，{1，0，0}，{1，0，0 } }
> T4】输出:是
> 选择左上角为(0，0)
> 右下角为(1，1)的子矩阵。
> 更改此子矩阵的角元素
> 的奇偶性会将 A[][]转换为 B[][]
> **输入:** A[][] = {{0，1，0，1}，{1，0，1，0}，{0，1，0，1，1}}，
> B[][] = {{1，1，1，1，1}，{1，1，1，1}}
> **输出::**

**方法:**首先要注意的是，尽管进行了转换，但两个矩阵的总奇偶性将保持不变。因此，检查 **a[i][j]** 是否与 **b[i][j]** 不相同，然后将左上角为 **(0，0)** 和右下角为 **(i，j)** 的子矩阵的角元素的奇偶性更改为 **1 ≤ i，j** 。对每个不等于 b[i][j]的 a[i][j]执行奇偶校验更改后，检查两个矩阵是否相同。如果它们相同，我们可以将 A 改为 b。
下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;
#define N 3
#define M 3

// Boolean function that returns
// true or false
bool check(int a[N][M], int b[N][M])
{
    // Traverse for all elements
    for (int i = 1; i < N; i++) {
        for (int j = 1; j < M; j++) {

            // If both are not equal
            if (a[i][j] != b[i][j]) {

                // Change the parity of
                // all corner elements
                a[i][j] ^= 1;
                a[0][0] ^= 1;
                a[0][j] ^= 1;
                a[i][0] ^= 1;
            }
        }
    }

    // Check if A is equal to B
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            // Not equal
            if (a[i][j] != b[i][j])
                return false;
        }
    }
    return true;
}

// Driver Code
int main()
{
    // First binary matrix
    int a[N][N] = { { 0, 1, 0 },
                    { 0, 1, 0 },
                    { 1, 0, 0 } };

    // Second binary matrix
    int b[N][N] = { { 1, 0, 0 },
                    { 1, 0, 0 },
                    { 1, 0, 0 } };

    if (check(a, b))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG
{

static final int N = 3,M =3;

// Boolean function that returns
// true or false
static boolean check(int a[][], int b[][])
{
    // Traverse for all elements
    for (int i = 1; i < N; i++)
    {
        for (int j = 1; j < M; j++)
        {

            // If both are not equal
            if (a[i][j] != b[i][j])
            {

                // Change the parity of
                // all corner elements
                a[i][j] ^= 1;
                a[0][0] ^= 1;
                a[0][j] ^= 1;
                a[i][0] ^= 1;
            }
        }
    }

    // Check if A is equal to B
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            // Not equal
            if (a[i][j] != b[i][j])
                return false;
        }
    }
    return true;
}

// Driver Code
public static void main(String args[])
{
    // First binary matrix
    int a[][] = { { 0, 1, 0 },
                    { 0, 1, 0 },
                    { 1, 0, 0 } };

    // Second binary matrix
    int b[][] = { { 1, 0, 0 },
                    { 1, 0, 0 },
                    { 1, 0, 0 } };

    if (check(a, b))
        System.out.print( "Yes");
    else
        System.out.print( "No");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
N = 3
M = 3

# Boolean function that returns
# true or false
def check(a, b):

    # Traverse for all elements
    for i in range(1, N, 1):
        for j in range(1, M, 1):

            # If both are not equal
            if (a[i][j] != b[i][j]):

                # Change the parity of
                # all corner elements
                a[i][j] ^= 1
                a[0][0] ^= 1
                a[0][j] ^= 1
                a[i][0] ^= 1

    # Check if A is equal to B
    for i in range(N):
        for j in range(M):

            # Not equal
            if (a[i][j] != b[i][j]):
                return False

    return True

# Driver Code
if __name__ == '__main__':

    # First binary matrix
    a = [[0, 1, 0],
         [0, 1, 0],
         [1, 0, 0]]

    # Second binary matrix
    b = [[1, 0, 0],
         [1, 0, 0],
         [1, 0, 0]]

    if (check(a, b)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

static readonly int N = 3,M =3;

// Boolean function that returns
// true or false
static bool check(int [,]a, int [,]b)
{
    // Traverse for all elements
    for (int i = 1; i < N; i++)
    {
        for (int j = 1; j < M; j++)
        {

            // If both are not equal
            if (a[i,j] != b[i,j])
            {

                // Change the parity of
                // all corner elements
                a[i,j] ^= 1;
                a[0,0] ^= 1;
                a[0,j] ^= 1;
                a[i,0] ^= 1;
            }
        }
    }

    // Check if A is equal to B
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            // Not equal
            if (a[i,j] != b[i,j])
                return false;
        }
    }
    return true;
}

// Driver Code
public static void Main(String []args)
{
    // First binary matrix
    int [,]a = { { 0, 1, 0 },
                    { 0, 1, 0 },
                    { 1, 0, 0 } };

    // Second binary matrix
    int [,]b = { { 1, 0, 0 },
                    { 1, 0, 0 },
                    { 1, 0, 0 } };

    if (check(a, b))
        Console.Write( "Yes");
    else
        Console.Write( "No");
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

$N = 3;
$M = 3 ;

// Boolean function that returns
// true or false
function check($a, $b)
{
    // Traverse for all elements
    for ($i = 1; $i < $GLOBALS['N']; $i++)
    {
        for ($j = 1; $j < $GLOBALS['M']; $j++)
        {

            // If both are not equal
            if ($a[$i][$j] != $b[$i][$j])
            {

                // Change the parity of
                // all corner elements
                $a[$i][$j] ^= 1;
                $a[0][0] ^= 1;
                $a[0][$j] ^= 1;
                $a[$i][0] ^= 1;
            }
        }
    }

    // Check if A is equal to B
    for ($i = 0; $i < $GLOBALS['N']; $i++)
    {
        for ($j = 0; $j < $GLOBALS['M']; $j++)
        {

            // Not equal
            if ($a[$i][$j] != $b[$i][$j])
                return false;
        }
    }
    return true;
}

    // Driver Code
    // First binary matrix
    $a = array(array( 0, 1, 0 ),
                array( 0, 1, 0 ),
                array( 1, 0, 0 ) );

    // Second binary matrix
    $b = array( array( 1, 0, 0 ),
                array(1, 0, 0 ),
                array( 1, 0, 0 ) );

    if (check($a, $b))
        echo "Yes";
    else
        echo "No";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the
// above approach    
var N = 3, M = 3;

    // Boolean function that returns
    // true or false
    function check(a , b) {
        // Traverse for all elements
        for (i = 1; i < N; i++) {
            for (j = 1; j < M; j++) {

                // If both are not equal
                if (a[i][j] != b[i][j]) {

                    // Change the parity of
                    // all corner elements
                    a[i][j] ^= 1;
                    a[0][0] ^= 1;
                    a[0][j] ^= 1;
                    a[i][0] ^= 1;
                }
            }
        }

        // Check if A is equal to B
        for (i = 0; i < N; i++) {
            for (j = 0; j < M; j++) {

                // Not equal
                if (a[i][j] != b[i][j])
                    return false;
            }
        }
        return true;
    }

    // Driver Code

        // First binary matrix
        var a = [ [ 0, 1, 0 ],
                [ 0, 1, 0 ],
                [ 1, 0, 0 ] ];

        // Second binary matrix
        var b = [ [ 1, 0, 0 ],
                [ 1, 0, 0 ],
                [ 1, 0, 0 ] ];

        if (check(a, b))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by aashish1995
</script>
```

**Output:** 

```
Yes
```

时间复杂度:0(N * M)

辅助空间:0(1)