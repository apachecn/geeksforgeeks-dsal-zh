# 检查是否可以选择每一行中的一个数字，使得数字的异或大于零

> 原文:[https://www . geesforgeks . org/check-if-a-numbers-from-row-can-selected-so-xor-of-numbers-大于零/](https://www.geeksforgeeks.org/check-if-a-number-from-every-row-can-be-selected-such-that-xor-of-the-numbers-is-greater-than-zero/)

给定二维数组的顺序 **N X M** 数组元素，任务是检查我们是否可以从每一行中选择一个数字，使得所选数字的**异或**大于 **0** 。
**注**:最少 2 排。
**举例:**

```
Input: a[][] = {{7, 7, 7}, 
                {10, 10, 7}} 
Output: Yes

Input: a[][] = {{1, 1, 1},
                {1, 1, 1}, 
                {1, 1, 1}, 
                {1, 1, 1}} 
Output: No 
```

**逼近**:首先检查每行第一列元素的异或是否为 0。如果它是非零的，那么它是可能的。如果它为零，检查任何一行是否有两个或更多不同的元素，那么也是可能的。如果以上两个条件都不满足，那么就不可能。
以下是上述办法的实施情况:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define N 2
#define M 3

// Function to check if a number from every row
// can be selected such that xor of the numbers
// is greater than zero
bool check(int mat[N][M])
{
    int xorr = 0;

    // Find the xor of first
    // column for every row
    for (int i = 0; i < N; i++) {
        xorr ^= mat[i][0];
    }

    // If Xorr is 0
    if (xorr != 0)
        return true;

    // Traverse in the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 1; j < M; j++) {

            // Check is atleast
            // 2 distinct elements
            if (mat[i][j] != mat[i][0])
                return true;
        }
    }

    return false;
}

// Driver code
int main()
{
    int mat[N][M] = { { 7, 7, 7 },
                      { 10, 10, 7 } };

    if (check(mat))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG
{
    static int N = 2;
    static int M = 3;

    // Function to check if a number
    // from every row can be selected
    // such that xor of the numbers
    // is greater than zero
    static boolean check(int mat[][])
    {
        int xorr = 0;

        // Find the xor of first
        // column for every row
        for (int i = 0; i < N; i++)
        {
            xorr ^= mat[i] [0];
        }

        // If Xorr is 0
        if (xorr != 0)
            return true;

        // Traverse in the matrix
        for (int i = 0; i < N; i++)
        {
            for (int j = 1; j < M; j++)
            {

                // Check is atleast
                // 2 distinct elements
                if (mat[i] [j] != mat[i] [0])
                    return true;
            }
        }

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {

        int mat[][] = {{ 7, 7, 7 },
                    { 10, 10, 7 }};

        if (check(mat))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
N = 2
M = 3

# Function to check if a number from every row
# can be selected such that xor of the numbers
# is greater than zero
def check(mat):

    xorr = 0

    # Find the xor of first
    # column for every row
    for i in range(N):
        xorr ^= mat[i][0]

    # If Xorr is 0
    if (xorr != 0):
        return True

    # Traverse in the matrix
    for i in range(N):
        for j in range(1, M):

            # Check is atleast
            # 2 distinct elements
            if (mat[i][j] != mat[i][0]):
                return True

    return False

# Driver code
mat = [[ 7, 7, 7 ],
       [ 10, 10, 7 ]]

if (check(mat)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{
    static int N = 2;
    static int M = 3;

    // Function to check if a number
    // from every row can be selected
    // such that xor of the numbers
    // is greater than zero
    static bool check(int [,]mat)
    {
        int xorr = 0;

        // Find the xor of first
        // column for every row
        for (int i = 0; i < N; i++)
        {
            xorr ^= mat[i, 0];
        }

        // If Xorr is 0
        if (xorr != 0)
            return true;

        // Traverse in the matrix
        for (int i = 0; i < N; i++)
        {
            for (int j = 1; j < M; j++)
            {

                // Check is atleast
                // 2 distinct elements
                if (mat[i, j] != mat[i, 0])
                    return true;
            }
        }

        return false;
    }

    // Driver code
    static void Main()
    {
        int [,]mat = {{ 7, 7, 7 },
                      { 10, 10, 7 }};

        if (check(mat))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

$N = 2;
$M = 3;

// Function to check if a number from every row
// can be selected such that xor of the numbers
// is greater than zero
function check($mat)
{

    global $N ;
    global $M ;

    $xorr = 0;

    // Find the xor of first
    // column for every row
    for ($i = 0; $i < $N; $i++)
    {
        $xorr =     $xorr ^ $mat[$i][0];
    }

    // If Xorr is 0
    if ($xorr != 0)
        return true;

    // Traverse in the matrix
    for ($i = 0; $i < $N; $i++)
    {
        for ( $j = 1; $j < $M; $j++)
        {

            // Check is atleast
            // 2 distinct elements
            if ($mat[$i][$j] != $mat[$i][0])
                return true;
        }
    }
    return false;
}

    // Driver code
    $mat = array(array( 7, 7, 7 ),
                    array( 10, 10, 7 ));

    if (check($mat))
        echo "Yes";
    else
        echo "No";

// This code is contributed by Tushil..
?>
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

let N = 2;
let M = 3;

// Function to check if a number from every row
// can be selected such that xor of the numbers
// is greater than zero
function check(mat)
{
    let xorr = 0;

    // Find the xor of first
    // column for every row
    for (let i = 0; i < N; i++) {
        xorr ^= mat[i][0];
    }

    // If Xorr is 0
    if (xorr != 0)
        return true;

    // Traverse in the matrix
    for (let i = 0; i < N; i++) {
        for (let j = 1; j < M; j++) {

            // Check is atleast
            // 2 distinct elements
            if (mat[i][j] != mat[i][0])
                return true;
        }
    }

    return false;
}

// Driver code
    let mat = [ [ 7, 7, 7 ],
                      [ 10, 10, 7 ] ];

    if (check(mat))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
Yes
```