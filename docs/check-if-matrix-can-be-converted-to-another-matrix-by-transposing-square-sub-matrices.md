# 检查矩阵是否可以通过置换正方形子矩阵转换成另一个矩阵

> 原文:[https://www . geeksforgeeks . org/check-if-matrix-can-transposing-square-sub-matrix-transposing-to-then-matrix/](https://www.geeksforgeeks.org/check-if-matrix-can-be-converted-to-another-matrix-by-transposing-square-sub-matrices/)

给定两个 **N X M** 整数矩阵。在一次运算中，我们可以将矩阵 1 中的任意正方形子矩阵[转置](https://www.geeksforgeeks.org/program-to-find-transpose-of-a-matrix/)。任务是检查矩阵 1 是否可以通过给定的操作转换成矩阵 2。
**例:**

> **输入:** matrix1[][] = {
> {1，2，3}，
> {4，5，6}，
> {7，8，9}}，
> matrix2[][] = {
> {1，4，7}，
> {2，5，6}，
> {3，8，9}}
> **输出:**是
> 转置整个矩阵，然后我们用转置
> 子矩阵
> **输入:** matrix1[][] = {
> {1，2}，
> {3，4}}，
> matrix2[][] = {
> {1，4}，
> {3，8}}
> **输出:**否

**方法:**对两个矩阵的对角线进行排序并进行比较。如果对角排序后两个矩阵相等，那么矩阵 1 可以转换成矩阵 2。下面的方法是正确的，因为在换位时，数字只能换位到它的任何对角线上。
以下是上述办法的实施情况。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define n 3
#define m 3

// Function that returns true if matrix1
// can be converted to matrix2
// with the given operation
bool check(int a[n][m], int b[n][m])
{

    // Traverse all the diagonals
    // starting at first column
    for (int i = 0; i < n; i++) {
        vector<int> v1, v2;
        int r = i;
        int col = 0;

        // Traverse in diagonal
        while (r >= 0 && col < m) {

            // Store the diagonal elements
            v1.push_back(a[r][col]);
            v2.push_back(b[r][col]);

            // Move up
            r--;
            col++;
        }

        // Sort the elements
        sort(v1.begin(), v1.end());
        sort(v2.begin(), v2.end());

        // Check if they are same
        for (int i = 0; i < v1.size(); i++) {
            if (v1[i] != v2[i])
                return false;
        }
    }

    // Traverse all the diagonals
    // starting at last row
    for (int j = 1; j < m; j++) {
        vector<int> v1, v2;
        int r = n - 1;
        int col = j;

        // Traverse in the diagonal
        while (r >= 0 && col < m) {

            // Store diagonal elements
            v1.push_back(a[r][col]);
            v2.push_back(b[r][col]);
            r--;
            col++;
        }

        // Sort all elements
        sort(v1.begin(), v1.end());
        sort(v2.begin(), v2.end());

        // Check for same
        for (int i = 0; i < v1.size(); i++) {
            if (v1[i] != v2[i])
                return false;
        }
    }

    // If every element matches
    return true;
}

// Driver code
int main()
{
    int a[n][m] = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    int b[n][m] = { { 1, 4, 7 }, { 2, 5, 6 }, { 3, 8, 9 } };

    if (check(a, b))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static final int n = 3;
    static final int m = 3;

    // Function that returns true if matrix1
    // can be converted to matrix2
    // with the given operation
    static boolean check(int a[][], int b[][])
    {

        // Traverse all the diagonals
        // starting at first column
        for (int i = 0; i < n; i++)
        {
            Vector<Integer> v1 = new Vector<Integer>();
            Vector<Integer> v2 = new Vector<Integer>();
            int r = i;
            int col = 0;

            // Traverse in diagonal
            while (r >= 0 && col < m)
            {

                // Store the diagonal elements
                v1.add(a[r][col]);
                v2.add(b[r][col]);

                // Move up
                r--;
                col++;
            }

            // Sort the elements
            Collections.sort(v1);
            Collections.sort(v2);

            // Check if they are same
            for (int j = 0; j < v1.size(); j++)
            {
                if (v1.get(j) != v2.get(j))
                {
                    return false;
                }
            }
        }

        // Traverse all the diagonals
        // starting at last row
        for (int j = 1; j < m; j++)
        {
            Vector<Integer> v1 = new Vector<Integer>();
            Vector<Integer> v2 = new Vector<Integer>();
            int r = n - 1;
            int col = j;

            // Traverse in the diagonal
            while (r >= 0 && col < m)
            {

                // Store diagonal elements
                v1.add(a[r][col]);
                v2.add(b[r][col]);
                r--;
                col++;
            }

            // Sort all elements
            Collections.sort(v1);
            Collections.sort(v2);

            // Check for same
            for (int i = 0; i < v1.size(); i++)
            {
                if (v1.get(i) != v2.get(i))
                {
                    return false;
                }
            }
        }

        // If every element matches
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[][] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        int b[][] = {{1, 4, 7}, {2, 5, 6}, {3, 8, 9}};

        if (check(a, b))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
n = 3
m = 3

# Function that returns true if matrix1
# can be converted to matrix2
# with the given operation
def check(a, b):

    # Traverse all the diagonals
    # starting at first column
    for i in range(n):
        v1 = []
        v2 = []
        r = i
        col = 0

        # Traverse in diagonal
        while (r >= 0 and col < m):

            # Store the diagonal elements
            v1.append(a[r][col])
            v2.append(b[r][col])

            # Move up
            r -= 1
            col += 1

        # Sort the elements
        v1.sort(reverse = False)
        v2.sort(reverse = False)

        # Check if they are same
        for i in range(len(v1)):
            if (v1[i] != v2[i]):
                return False

    # Traverse all the diagonals
    # starting at last row
    for j in range(1, m):
        v1 = []
        v2 = []
        r = n - 1
        col = j

        # Traverse in the diagonal
        while (r >= 0 and col < m):

            # Store diagonal elements
            v1.append(a[r][col])
            v2.append(b[r][col])
            r -= 1
            col += 1

        # Sort all elements
        v1.sort(reverse = False)
        v2.sort(reverse = False)

        # Check for same
        for i in range(len(v1)):
            if (v1[i] != v2[i]):
                return False

    # If every element matches
    return True

# Driver code
if __name__ == '__main__':
    a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    b = [[1, 4, 7], [2, 5, 6], [3, 8, 9]]

    if (check(a, b)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static readonly int n = 3;
    static readonly int m = 3;

    // Function that returns true if matrix1
    // can be converted to matrix2
    // with the given operation
    static bool check(int [,]a, int [,]b)
    {

        // Traverse all the diagonals
        // starting at first column
        for (int i = 0; i < n; i++)
        {
            List<int> v1 = new List<int>();
            List<int> v2 = new List<int>();
            int r = i;
            int col = 0;

            // Traverse in diagonal
            while (r >= 0 && col < m)
            {

                // Store the diagonal elements
                v1.Add(a[r, col]);
                v2.Add(b[r, col]);

                // Move up
                r--;
                col++;
            }

            // Sort the elements
            v1.Sort();
            v2.Sort();

            // Check if they are same
            for (int j = 0; j < v1.Count; j++)
            {
                if (v1[j] != v2[j])
                {
                    return false;
                }
            }
        }

        // Traverse all the diagonals
        // starting at last row
        for (int j = 1; j < m; j++)
        {
            List<int> v1 = new List<int>();
            List<int> v2 = new List<int>();
            int r = n - 1;
            int col = j;

            // Traverse in the diagonal
            while (r >= 0 && col < m)
            {

                // Store diagonal elements
                v1.Add(a[r, col]);
                v2.Add(b[r, col]);
                r--;
                col++;
            }

            // Sort all elements
            v1.Sort();
            v2.Sort();

            // Check for same
            for (int i = 0; i < v1.Count; i++)
            {
                if (v1[i] != v2[i])
                {
                    return false;
                }
            }
        }

        // If every element matches
        return true;
    }

    // Driver code
    public static void Main()
    {
        int [,]a = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        int [,]b = {{1, 4, 7}, {2, 5, 6}, {3, 8, 9}};

        if (check(a, b))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$n = 3;
$m = 3;

// Function that returns true if matrix1
// can be converted to matrix2
// with the given operation
function check($a, $b)
{
    global $n, $m;

    // Traverse all the diagonals
    // starting at first column
    for ($i = 0; $i < $n; $i++)
    {
        $v1 = array();
        $v2 = array();
        $r = $i;
        $col = 0;

        // Traverse in diagonal
        while ($r >= 0 && $col < $m)
        {

            // Store the diagonal elements
            array_push($v1, $a[$r][$col]);
            array_push($v2, $b[$r][$col]);

            // Move up
            $r--;
            $col++;
        }

        // Sort the elements
        sort($v1);
        sort($v2);

        // Check if they are same
        for ($i = 0; $i < count($v1); $i++)
        {
            if ($v1[$i] != $v2[$i])
                return false;
        }
    }

    // Traverse all the diagonals
    // starting at last row
    for ($j = 1; $j < $m; $j++)
    {
        $v1 = array();
        $v2 = array();
        $r = $n - 1;
        $col = $j;

        // Traverse in the diagonal
        while ($r >= 0 && $col < $m)
        {

            // Store diagonal elements
            array_push($v1, $a[$r][$col]);
            array_push($v2, $b[$r][$col]);
            $r--;
            $col++;
        }

        // Sort all elements
        sort($v1);
        sort($v2);

        // Check for same
        for ($i = 0; $i < count($v1); $i++)
        {
            if ($v1[$i] != $v2[$i])
                return false;
        }
    }

    // If every element matches
    return true;
}

// Driver code
$a = array(array( 1, 2, 3 ),
           array( 4, 5, 6 ),
           array( 7, 8, 9 ));
$b = array(array( 1, 4, 7 ),
           array( 2, 5, 6 ),
           array( 3, 8, 9 ));

if (check($a, $b))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var n = 3
var m = 3

// Function that returns true if matrix1
// can be converted to matrix2
// with the given operation
function check(a, b)
{

    // Traverse all the diagonals
    // starting at first column
    for (var i = 0; i < n; i++) {
        var v1 = [], v2 = [];
        var r = i;
        var col = 0;

        // Traverse in diagonal
        while (r >= 0 && col < m) {

            // Store the diagonal elements
            v1.push(a[r][col]);
            v2.push(b[r][col]);

            // Move up
            r--;
            col++;
        }

        // Sort the elements
        v1.sort();
        v2.sort();

        // Check if they are same
        for (var i = 0; i < v1.length; i++) {
            if (v1[i] != v2[i])
                return false;
        }
    }

    // Traverse all the diagonals
    // starting at last row
    for (var j = 1; j < m; j++) {
        var v1 = [], v2 = [];
        var r = n - 1;
        var col = j;

        // Traverse in the diagonal
        while (r >= 0 && col < m) {

            // Store diagonal elements
            v1.push(a[r][col]);
            v2.push(b[r][col]);
            r--;
            col++;
        }

        // Sort all elements
        v1.sort();
        v2.sort();

        // Check for same
        for (var i = 0; i < v1.length; i++) {
            if (v1[i] != v2[i])
                return false;
        }
    }

    // If every element matches
    return true;
}

// Driver code
var a = [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ];
var b = [ [ 1, 4, 7 ], [ 2, 5, 6 ], [ 3, 8, 9 ] ];
if (check(a, b))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N * M * log (max(N，M)))