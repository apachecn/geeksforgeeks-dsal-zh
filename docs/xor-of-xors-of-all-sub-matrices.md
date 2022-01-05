# 所有子矩阵的异或

> 原文:[https://www . geeksforgeeks . org/xor-of-xor-of-all-sub-matrix/](https://www.geeksforgeeks.org/xor-of-xors-of-all-sub-matrices/)

给定一个**‘N * N’**矩阵，任务是找出所有可能子矩阵的异或。
**例:**

```
Input :arr =  {{3, 1},
               {1, 3}}
Output : 0
Explanation: All the elements lie in 4 submatrices each. 
4 being even, there total contribution towards 
final answer becomes 0\. Thus, ans = 0.

Input : arr = {{6, 7, 13},
               {8, 3, 4},
               {9, 7, 6}};
Output : 4
```

一个**简单的方法**是生成所有可能的子矩阵，唯一地找到每个子矩阵的异或，然后把它们全部异或起来。这种方法的时间复杂度为 0(n<sup>6</sup>)。
**更好的解决方案:**对于每个索引(R，C)，我们将尝试找到该索引所在的子矩阵的数量。如果子矩阵的数量是奇数，那么最终答案将更新为 **ans = (ans ^ arr[R][C])** 。如果是偶数，我们不需要更新答案。这是可行的，因为一个数异或本身给出零，运算顺序不影响最终的异或值。
假设基于 0 的索引，索引(R，C)所在的子矩阵数等于

```
(R + 1)*(C + 1)*(N - R)*(N - C)
```

下面是上述方法的实现:

## C++

```
// C++ program to find the XOR of XOR's of
// all submatrices

#include <iostream>
using namespace std;

#define n 3

// Function to find to required
// XOR value
int submatrixXor(int arr[][n])
{
    int ans = 0;

    // Nested loop to find the
    // number of sub-matrix each
    // index belongs to
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            // Number of ways to choose
            // from top-left elements
            int top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            int bottom_right = (n - i) * (n - j);

            if ((top_left % 2 == 1) && (bottom_right % 2 == 1))
                ans = (ans ^ arr[i][j]);
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[][n] = { { 6, 7, 13 },
                     { 8, 3, 4 },
                     { 9, 7, 6 } };

    cout << submatrixXor(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find the XOR of XOR's
// of all submatrices
class GFG
{

// Function to find to required
// XOR value
static int submatrixXor(int[][]arr)
{
    int n = 3;
    int ans = 0;

    // Nested loop to find the
    // number of sub-matrix each
    // index belongs to
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            // Number of ways to choose
            // from top-left elements
            int top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            int bottom_right = (n - i) * (n - j);

            if ((top_left % 2 == 1) &&
                (bottom_right % 2 == 1))
                ans = (ans ^ arr[i][j]);
        }
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int[][] arr = {{ 6, 7, 13},
                   { 8, 3, 4 },
                   { 9, 7, 6 }};

    System.out.println(submatrixXor(arr));
}
}

// This code is contributed
// by Code_Mech.
```

## 蟒蛇 3

```
# Python3 program to find the XOR of
# XOR's of all submatrices

# Function to find to required
# XOR value
def submatrixXor(arr, n):

    ans = 0

    # Nested loop to find the
    # number of sub-matrix each
    # index belongs to
    for i in range(0, n):
        for j in range(0, n):

            # Number of ways to choose
            # from top-left elements
            top_left = (i + 1) * (j + 1)

            # Number of ways to choose
            # from bottom-right elements
            bottom_right = (n - i) * (n - j)
            if (top_left % 2 == 1 and
                bottom_right % 2 == 1):
                ans = (ans ^ arr[i][j])
    return ans

# Driver code
n = 3
arr = [[6, 7, 13],
       [8, 3, 4],
       [9, 7, 6]]
print(submatrixXor(arr, n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find the XOR of XOR's
// of all submatrices
using System;

class GFG
{

// Function to find to required
// XOR value
static int submatrixXor(int [,]arr)
{
    int n = 3;
    int ans = 0;

    // Nested loop to find the
    // number of sub-matrix each
    // index belongs to
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            // Number of ways to choose
            // from top-left elements
            int top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            int bottom_right = (n - i) * (n - j);

            if ((top_left % 2 == 1) &&
                (bottom_right % 2 == 1))
                ans = (ans ^ arr[i, j]);
        }
    }

    return ans;
}

// Driver Code
public static void Main()
{
    int [, ]arr = {{ 6, 7, 13},
                   { 8, 3, 4 },
                   { 9, 7, 6 }};

    Console.Write(submatrixXor(arr));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the XOR of
// XOR's of all submatrices

// Function to find to required
// XOR value
function submatrixXor($arr)
{
    $ans = 0;
    $n = 3 ;

    // Nested loop to find the
    // number of sub-matrix each
    // index belongs to
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            // Number of ways to choose
            // from top-left elements
            $top_left = ($i + 1) * ($j + 1);

            // Number of ways to choose
            // from bottom-right elements
            $bottom_right = ($n - $i) * ($n - $j);

            if (($top_left % 2 == 1) &&
                ($bottom_right % 2 == 1))
                $ans = ($ans ^ $arr[$i][$j]);
        }
    }

    return $ans;
}

// Driver Code
$arr = array(array( 6, 7, 13 ),
             array( 8, 3, 4 ),
             array( 9, 7, 6 ));

echo submatrixXor($arr);

# This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// XOR of XOR's of
// all submatrices

const n = 3;

// Function to find to required
// XOR value
function submatrixXor(arr)
{
    let ans = 0;

    // Nested loop to find the
    // number of sub-matrix each
    // index belongs to
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            // Number of ways to choose
            // from top-left elements
            let top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            let bottom_right = (n - i) * (n - j);

            if ((top_left % 2 == 1) &&
            (bottom_right % 2 == 1))

                ans = (ans ^ arr[i][j]);
        }
    }

    return ans;
}

// Driver Code
    let arr = [ [ 6, 7, 13 ],
                [ 8, 3, 4 ],
                [ 9, 7, 6 ] ];

    document.write(submatrixXor(arr));

</script>
```

**Output:** 

```
4
```

**时间复杂度**:O(N<sup>2</sup>)
T5】辅助空间: O(1)