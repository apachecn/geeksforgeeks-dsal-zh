# 子矩阵的异或运算查询

> 原文:[https://www.geeksforgeeks.org/xor-of-a-submatrix-queries/](https://www.geeksforgeeks.org/xor-of-a-submatrix-queries/)

给定一个 **N * N** 矩阵和 **q** 查询，每个查询都包含一个矩形子矩阵的左上角和右下角的位置，任务是从这个子矩阵中找到所有元素的异或。
**例:**

> **输入:** arr[][] = {{1，2，3}，{4，5，6}，{7，8，9}}，q[] = {{1，1，2，2，2}，{1，2，2，2 } }
> T3】输出:t5】2
> 15
> 查询 1: 5 ^ 6 ^ 8 ^ 9 = 2
> 查询 2: 6 ^ 9 = 15
> **输入:**arr[][]= { }

一个**简单的解决方案**是为每个查询找到整个子矩阵的异或。因此，每个查询的最坏情况时间复杂度将是 0(n<sup>2</sup>)。
**高效方法:**我们都很熟悉线性阵列上前缀异或的思想，即

> 如果 arr[] = {1，2，3，4}并且我们计算 prefixXOR[] = {1，3，0，4}，其中 prefixXOR[i]存储从 arr[0]到 arr[i]【t0]的值的 XOR，那么子阵列 arr[I]到 arr[j]的 XOR 可以被发现为 prefixXOR[j]^ prefixXOR[I–1]
> 例如，子阵列{2，3}的 xor 将是 XOR(0，1) = 1
> 这是因为在 prefixxor 中

我们将尝试将同样的方法扩展到二维矩阵。我们将计算前缀异或矩阵，这将有助于我们解决 O(1)中的每个查询。
在这种情况下，我们在位置(R，C)的前缀-XOR 矩阵将存储左上角在(0，0)和右下角在(R，C)的矩形子矩阵的 XOR。
我们分两步计算前缀异或。

1.  从左到右计算原始矩阵每行的前缀异或。
2.  在上面的矩阵中，从上到下计算每一列的前缀异或。

一旦我们有了所需的前缀异或矩阵，我们就可以简单地回答查询。从(R1，C1)到(R2，C2)的子矩阵的 XOR 可以计算为**前缀 _xor[R2][C2] ^前缀 _ xor[R1–1][C2]^前缀 _ xor[R2][C1–1]^前缀 _ xor[R1–1][C1–1]**。
**注:**如果 R1 或 C1 等于 0，那么 R1-1 或 C1-1 也应该是 0。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
#define n 3
using namespace std;

// Function to pre-compute the xor
void preComputeXor(int arr[][n], int prefix_xor[][n])
{
    // Left to right prefix xor
    // for each row
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            if (j == 0)
                prefix_xor[i][j] = arr[i][j];
            else
                prefix_xor[i][j]
                    = (prefix_xor[i][j - 1] ^ arr[i][j]);
        }

    // Top to bottom prefix xor
    // for each column
    for (int i = 0; i < n; i++)
        for (int j = 1; j < n; j++)
            prefix_xor[j][i]
                = (prefix_xor[j - 1][i] ^ prefix_xor[j][i]);
}

// Function to process the queries
// x1, x2, y1, y2 represent the
// positions of the top-left
// and bottom right corners
int ansQuerie(int prefix_xor[][n], int x1, int y1, int x2, int y2)
{

    // To store the xor values
    int xor_1 = 0, xor_2 = 0, xor_3 = 0;

    // Finding the values we need to xor
    // with value at (x2, y2) in prefix-xor
    // matrix
    if (x1 != 0)
        xor_1 = prefix_xor[x1 - 1][y2];
    if (y1 != 0)
        xor_2 = prefix_xor[x2][y1 - 1];
    if (x1 != 0 and y1 != 0)
        xor_3 = prefix_xor[x1 - 1][y1 - 1];

    // Return the required prefix xor
    return ((prefix_xor[x2][y2] ^ xor_1) ^ (xor_2 ^ xor_3));
}

// Driver code
int main()
{
    int arr[][n] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };

    // To store pre-computed xor
    int prefix_xor[n][n];

    // Pre-computing xor
    preComputeXor(arr, prefix_xor);

    // Queries
    cout << ansQuerie(prefix_xor, 1, 1, 2, 2) << endl;
    cout << ansQuerie(prefix_xor, 1, 2, 2, 2) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

static int n = 3;

// Function to pre-compute the xor
static void preComputeXor(int arr[][],
                            int prefix_xor[][])
{
    // Left to right prefix xor
    // for each row
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
        {
            if (j == 0)
                prefix_xor[i][j] = arr[i][j];
            else
                prefix_xor[i][j] =
                    (prefix_xor[i][j - 1] ^ arr[i][j]);
        }

    // Top to bottom prefix xor
    // for each column
    for (int i = 0; i < n; i++)
        for (int j = 1; j < n; j++)
            prefix_xor[j][i] =
                (prefix_xor[j - 1][i] ^ prefix_xor[j][i]);
}

// Function to process the queries
// x1, x2, y1, y2 represent the
// positions of the top-left
// and bottom right corners
static int ansQuerie(int prefix_xor[][], int x1,
                    int y1, int x2, int y2)
{

    // To store the xor values
    int xor_1 = 0, xor_2 = 0, xor_3 = 0;

    // Finding the values we need to xor
    // with value at (x2, y2) in prefix-xor
    // matrix
    if (x1 != 0)
        xor_1 = prefix_xor[x1 - 1][y2];
    if (y1 != 0)
        xor_2 = prefix_xor[x2][y1 - 1];
    if (x1 != 0 && y1 != 0)
        xor_3 = prefix_xor[x1 - 1][y1 - 1];

    // Return the required prefix xor
    return ((prefix_xor[x2][y2] ^ xor_1) ^ (xor_2 ^ xor_3));
}

// Driver code
public static void main(String[] args)
{
    int arr[][] = new int[][]{{ 1, 2, 3 },
                            { 4, 5, 6 },
                            { 7, 8, 9 }};

    // To store pre-computed xor
    int prefix_xor[][] = new int[n][n];

    // Pre-computing xor
    preComputeXor(arr, prefix_xor);

    // Queries
    System.out.println(ansQuerie(prefix_xor, 1, 1, 2, 2));
    System.out.println(ansQuerie(prefix_xor, 1, 2, 2, 2));
}
}

// This code is contributed by
// Prerna Saini.
```

## 蟒蛇 3

```
n = 3

# Function to pre-compute the xor
def preComputeXor(arr, prefix_xor):

    # Left to right prefix xor
    # for each row
    for i in range(n):
        for j in range(n):
            if (j == 0):
                prefix_xor[i][j] = arr[i][j]
            else:
                prefix_xor[i][j] = (prefix_xor[i][j - 1] ^
                                               arr[i][j])

    # Top to bottom prefix xor
    # for each column
    for i in range(n):
        for j in range(1, n):
            prefix_xor[j][i] = (prefix_xor[j - 1][i] ^
                                    prefix_xor[j][i])

# Function to process the queries
# x1, x2, y1, y2 represent the
# positions of the top-left
# and bottom right corners
def ansQuerie(prefix_xor, x1, y1, x2, y2):

    # To store the xor values
    xor_1, xor_2, xor_3 = 0, 0, 0

    # Finding the values we need to xor
    # with value at (x2, y2) in prefix-xor
    # matrix
    if (x1 != 0):
        xor_1 = prefix_xor[x1 - 1][y2]
    if (y1 != 0):
        xor_2 = prefix_xor[x2][y1 - 1]
    if (x1 != 0 and y1 != 0):
        xor_3 = prefix_xor[x1 - 1][y1 - 1]

    # Return the required prefix xor
    return ((prefix_xor[x2][y2] ^ xor_1) ^
                         (xor_2 ^ xor_3))

# Driver code
arr = [[ 1, 2, 3 ],
       [ 4, 5, 6 ],
       [ 7, 8, 9 ]]

# To store pre-computed xor
prefix_xor = [[0 for i in range(n)]
                 for i in range(n)]

# Pre-computing xor
preComputeXor(arr, prefix_xor)

# Queries
print(ansQuerie(prefix_xor, 1, 1, 2, 2))
print(ansQuerie(prefix_xor, 1, 2, 2, 2))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{
    static int n = 3;

    // Function to pre-compute the xor
    static void preComputeXor(int [,]arr,
                                int [,]prefix_xor)
    {
        // Left to right prefix xor
        // for each row
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
            {
                if (j == 0)
                    prefix_xor[i, j] = arr[i, j];
                else
                    prefix_xor[i, j] =
                   (prefix_xor[i, j - 1] ^ arr[i, j]);
            }

        // Top to bottom prefix xor
        // for each column
        for (int i = 0; i < n; i++)
            for (int j = 1; j < n; j++)
                prefix_xor[j, i] =
                    (prefix_xor[j - 1, i] ^
                     prefix_xor[j, i]);
    }

    // Function to process the queries
    // x1, x2, y1, y2 represent the
    // positions of the top-left
    // and bottom right corners
    static int ansQuerie(int [,]prefix_xor, int x1,
                         int y1, int x2, int y2)
    {

        // To store the xor values
        int xor_1 = 0, xor_2 = 0, xor_3 = 0;

        // Finding the values we need to xor
        // with value at (x2, y2) in prefix-xor
        // matrix
        if (x1 != 0)
            xor_1 = prefix_xor[x1 - 1, y2];
        if (y1 != 0)
            xor_2 = prefix_xor[x2, y1 - 1];
        if (x1 != 0 && y1 != 0)
            xor_3 = prefix_xor[x1 - 1, y1 - 1];

        // Return the required prefix xor
        return ((prefix_xor[x2,y2] ^ xor_1) ^
                            (xor_2 ^ xor_3));
    }

    // Driver code
    public static void Main()
    {
        int [,]arr = {{ 1, 2, 3 },
                      { 4, 5, 6 },
                      { 7, 8, 9 }};

        // To store pre-computed xor
        int [,]prefix_xor = new int[n, n];

        // Pre-computing xor
        preComputeXor(arr, prefix_xor);

        // Queries
        Console.WriteLine(ansQuerie(prefix_xor, 1, 1, 2, 2));
        Console.WriteLine(ansQuerie(prefix_xor, 1, 2, 2, 2));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$n = 3;

// Function to pre-compute the xor
function preComputeXor($arr, &$prefix_xor)
{
    global $n;

    // Left to right prefix xor
    // for each row
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)
        {
            if ($j == 0)
                $prefix_xor[$i][$j] = $arr[$i][$j];
            else
                $prefix_xor[$i][$j] = ($prefix_xor[$i][$j - 1] ^
                                              $arr[$i][$j]);
        }

    // Top to bottom prefix xor
    // for each column
    for ($i = 0; $i < $n; $i++)
        for ($j = 1; $j < $n; $j++)
            $prefix_xor[$j][$i] = ($prefix_xor[$j - 1][$i] ^
                                   $prefix_xor[$j][$i]);
}

// Function to process the queries
// x1, x2, y1, y2 represent the
// positions of the top-left
// and bottom right corners
function ansQuerie($prefix_xor, $x1,
                   $y1, $x2, $y2)
{

    // To store the xor values
    $xor_1 = $xor_2 = $xor_3 = 0;

    // Finding the values we need to xor
    // with value at (x2, y2) in prefix-xor
    // matrix
    if ($x1 != 0)
        $xor_1 = $prefix_xor[$x1 - 1][$y2];
    if ($y1 != 0)
        $xor_2 = $prefix_xor[$x2][$y1 - 1];
    if ($x1 != 0 and $y1 != 0)
        $xor_3 = $prefix_xor[$x1 - 1][$y1 - 1];

    // Return the required prefix xor
    return (($prefix_xor[$x2][$y2] ^ $xor_1) ^
                           ($xor_2 ^ $xor_3));
}

// Driver code
$arr = array(array( 1, 2, 3 ),
             array( 4, 5, 6 ),
             array( 7, 8, 9 ));

// To store pre-computed xor
$prefix_xor = array_fill(0, $n,
              array_fill(0, $n, 0));

// Pre-computing xor
preComputeXor($arr, $prefix_xor);

// Queries
echo ansQuerie($prefix_xor, 1, 1, 2, 2) . "\n";
echo ansQuerie($prefix_xor, 1, 2, 2, 2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var n = 3;

    // Function to pre-compute the xor
    function preComputeXor(arr , prefix_xor)
    {
        // Left to right prefix xor
        // for each row
        for (i = 0; i < n; i++)
            for (j = 0; j < n; j++) {
                if (j == 0)
                    prefix_xor[i][j] = arr[i][j];
                else
                    prefix_xor[i][j] =
                    (prefix_xor[i][j - 1] ^ arr[i][j]);
            }

        // Top to bottom prefix xor
        // for each column
        for (i = 0; i < n; i++)
            for (j = 1; j < n; j++)
                prefix_xor[j][i] =
                (prefix_xor[j - 1][i] ^ prefix_xor[j][i]);
    }

    // Function to process the queries
    // x1, x2, y1, y2 represent the
    // positions of the top-left
    // and bottom right corners
    function ansQuerie(prefix_xor , x1 , y1 , x2 , y2) {

        // To store the xor values
        var xor_1 = 0, xor_2 = 0, xor_3 = 0;

        // Finding the values we need to xor
        // with value at (x2, y2) in prefix-xor
        // matrix
        if (x1 != 0)
            xor_1 = prefix_xor[x1 - 1][y2];
        if (y1 != 0)
            xor_2 = prefix_xor[x2][y1 - 1];
        if (x1 != 0 && y1 != 0)
            xor_3 = prefix_xor[x1 - 1][y1 - 1];

        // Return the required prefix xor
        return ((prefix_xor[x2][y2] ^ xor_1) ^
                               (xor_2 ^ xor_3));
    }

    // Driver code

        var arr = [[ 1, 2, 3 ], [ 4, 5, 6 ],
                                [ 7, 8, 9 ] ];

        // To store pre-computed xor
        var prefix_xor = Array(n);
        for(var i = 0;i<n;i++)
        prefix_xor[i] = Array(n).fill(0);

        // Pre-computing xor
        preComputeXor(arr, prefix_xor);

        // Queries
        document.write(ansQuerie(prefix_xor, 1, 1, 2, 2)+
        "<br/>");
        document.write(ansQuerie(prefix_xor, 1, 2, 2, 2));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
2
15
```