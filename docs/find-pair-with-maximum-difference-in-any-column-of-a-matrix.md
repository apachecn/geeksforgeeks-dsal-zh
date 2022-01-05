# 在矩阵的任意一列中寻找差异最大的对

> 原文:[https://www . geeksforgeeks . org/find-matrix 任意列差异最大的配对/](https://www.geeksforgeeks.org/find-pair-with-maximum-difference-in-any-column-of-a-matrix/)

给定一个正整数的 N*N 矩阵。任务是找出矩阵任意一列中任意一对元素之间的最大差异。

**示例**:

```
Input : mat[N][N] = {
        { 1, 2, 3, 4, 5 },
        { 5, 3, 5, 4, 0 },
        { 5, 6, 7, 8, 9 },
        { 0, 6, 3, 4, 12 },
        { 9, 7, 12, 4, 3 },
    };
Output : Max difference : 12
5th column has the pair with max difference
(0, 12)

Input : mat[N][N] = {
        { 1, 2, 3 },
        { 5, 3, 5 },
        { 9, 6, 7 }
    };
Output : Max difference : 8 
```

其思想是观察任何列中具有最大差异的对是该列的最大和最小元素之间的差异。现在按列遍历矩阵。找出每列的最大和最小元素之间的差异，并返回最大差异。

下面是上述方法的实现:

## C++

```
// C++ program to find column with
// max difference of any pair of elements
#include <bits/stdc++.h>
using namespace std;

#define N 5 // No of rows and column

// Function to find the column with max difference
int colMaxDiff(int mat[N][N])
{
    int max_diff = INT_MIN;

    // Traverse matrix column wise
    for (int i = 0; i < N; i++) {

        // Insert elements of column to vector
        int max_val = mat[0][i], min_val = mat[0][i];
        for (int j = 1; j < N; j++) {
            max_val = max(max_val, mat[j][i]);
            min_val = min(min_val, mat[j][i]);
        }

        // calculating difference between maximum and
        // minimum
        max_diff = max(max_diff, max_val - min_val);
    }

    return max_diff;
}

// driver code
int main()
{
    int mat[N][N] = {
        { 1, 2, 3, 4, 5 },
        { 5, 3, 5, 4, 0 },
        { 5, 6, 7, 8, 9 },
        { 0, 6, 3, 4, 12 },
        { 9, 7, 12, 4, 3 },
    };

    cout << "Max difference : " << colMaxDiff(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find column with
// max difference of any pair of elements

public class GOC1 {

    static int N = 5; // No of rows and column

    // Function to find the column with max difference
    static int colMaxDiff(int mat[][]) {
        int max_diff = Integer.MIN_VALUE;

        // Traverse matrix column wise
        for (int i = 0; i < N; i++) {

            // Insert elements of column to vector
            int max_val = mat[0][i], min_val = mat[0][i];
            for (int j = 1; j < N; j++) {
                max_val = Math.max(max_val, mat[j][i]);
                min_val = Math.min(min_val, mat[j][i]);
            }

            // calculating difference between maximum and
            // minimum
            max_diff = Math.max(max_diff, max_val - min_val);
        }

        return max_diff;
    }

    // Driver Code
    public static void main(String args[]) {
        int mat[][] = {
                { 1, 2, 3, 4, 5 },
                { 5, 3, 5, 4, 0 },
                { 5, 6, 7, 8, 9 },
                { 0, 6, 3, 4, 12 },
                { 9, 7, 12, 4, 3 },
            };

        System.out.println("Max difference : "+colMaxDiff(mat));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find column with
# max difference of any pair of elements

N = 5 # No of rows and column

# Function to find the column
# with max difference
def colMaxDiff(mat):

    max_diff = 0

    # Traverse matrix column wise
    for i in range (N):

        # Insert elements of column
        # to vector
        max_val = mat[0][i]
        min_val = mat[0][i]
        for j in range (1, N) :
            max_val = max(max_val, mat[j][i])
            min_val = min(min_val, mat[j][i])

        # calculating difference between
        # maximum and minimum
        max_diff = max(max_diff, max_val -
                                 min_val)

    return max_diff

# Driver Code
if __name__ == "__main__":
    mat = [[ 1, 2, 3, 4, 5 ],
           [5, 3, 5, 4, 0 ],
           [ 5, 6, 7, 8, 9 ],
           [ 0, 6, 3, 4, 12 ],
           [ 9, 7, 12, 4, 3 ]]

    print ("Max difference :", colMaxDiff(mat))

# This code is contributed by ita_c
```

## C#

```
// C# program to find column 
// with max difference of
// any pair of elements
using System;

class GFG
{

static int N = 5; // No of rows and column

// Function to find the column
// with max difference
static int colMaxDiff(int [,]mat)
{
    int max_diff = int.MinValue;

    // Traverse matrix column wise
    for (int i = 0; i < N; i++)
    {

        // Insert elements of column
        // to vector
        int max_val = mat[0, i],
            min_val = mat[0, i];
        for (int j = 1; j < N; j++)
        {
            max_val = Math.Max(max_val,
                               mat[j, i]);
            min_val = Math.Min(min_val,
                               mat[j, i]);
        }

        // calculating difference between
        // maximum and minimum
        max_diff = Math.Max(max_diff,
                            max_val - min_val);
    }

    return max_diff;
}

// Driver Code
public static void Main()
{
    int [,]mat = { { 1, 2, 3, 4, 5 },
                   { 5, 3, 5, 4, 0 },
                   { 5, 6, 7, 8, 9 },
                   { 0, 6, 3, 4, 12 },
                   { 9, 7, 12, 4, 3 }};

    Console.WriteLine("Max difference : " +
                          colMaxDiff(mat));
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find column with
// max difference of any pair of elements

// Function to find the column with max difference
function colMaxDiff($mat)
{
    $N = 5;
    $max_diff = PHP_INT_MIN;

    // Traverse matrix column wise
    for ($i = 0; $i < $N; $i++)
    {

        // Insert elements of column to vector
        $max_val = $mat[0][$i]; $min_val = $mat[0][$i];
        for ($j = 1; $j < $N; $j++)
        {
            $max_val = max($max_val, $mat[$j][$i]);
            $min_val = min($min_val, $mat[$j][$i]);
        }

        // calculating difference between maximum and
        // minimum
        $max_diff = max($max_diff, $max_val - $min_val);
    }

    return $max_diff;
}

// driver code
$mat = array(array( 1, 2, 3, 4, 5 ),
             array(5, 3, 5, 4, 0 ),
             array(5, 6, 7, 8, 9 ),
             array(0, 6, 3, 4, 12 ),
             array(9, 7, 12, 4, 3 ));

echo "Max difference : " .
      colMaxDiff($mat) . "\n";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// Javascript program to find column with
// max difference of any pair of elements

    let N = 5; // No of rows and column

    // Function to find the column with max difference
    function colMaxDiff(mat)
    {
        let max_diff = Number.MIN_VALUE;

        // Traverse matrix column wise
        for (let i = 0; i < N; i++) {

            // Insert elements of column to vector
            let max_val = mat[0][i], min_val = mat[0][i];
            for (let j = 1; j < N; j++) {
                max_val = Math.max(max_val, mat[j][i]);
                min_val = Math.min(min_val, mat[j][i]);
            }

            // calculating difference between maximum and
            // minimum
            max_diff = Math.max(max_diff, max_val - min_val);
        }

        return max_diff;
    }

     // Driver Code
    let mat = [[ 1, 2, 3, 4, 5 ],
           [5, 3, 5, 4, 0 ],
           [ 5, 6, 7, 8, 9 ],
           [ 0, 6, 3, 4, 12 ],
           [ 9, 7, 12, 4, 3 ]];

    document.write("Max difference :"+ colMaxDiff(mat))

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Max difference : 12
```

**时间复杂度:** O(n^2)