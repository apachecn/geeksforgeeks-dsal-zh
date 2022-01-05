# 不能被另一个数组的任何元素整除的数组元素

> 原文:[https://www . geesforgeks . org/check-elements-array-divide-至少-1-element-array/](https://www.geeksforgeeks.org/check-elements-array-divide-atleast-1-element-array/)

给定两个数组 A[]和 B[]，编写一个高效的代码来确定 B[]的每个元素是否能被 A[]的至少 1 个元素整除。显示 B[]的那些不能被 A[]中的任何元素整除的元素。
**例:**

```
Input : A[] = {100, 200, 400, 100, 600}
        B[] = {45, 90, 48, 1000, 3000}
Output : 45, 90, 48 
The output elements are those that are 
not divisible by any element of A[].
```

**方法一(天真实现)**

*   遍历 B[]的每个元素。
*   检查它是否能被至少 1 个 A[]元素整除。如果不能被任何除尽，那么就打印出来。

## C++

```
// C++ code for naive implementation
#include<iostream>
using namespace std;

// Function for checking the condition
// with 2 loops
void printNonDivisible(int A[], int B[],
                          int n, int m)
{
    for (int i = 0; i < m; i++)
    {
        int j = 0;
        for (j = 0; j < n; j++)
            if( B[i] % A[j] == 0 )
                break;

        // If none of the elements in A[]
        // divided B[i]
        if (j == n)
            cout << B[i] << endl;
    }
}

// Driver code
int main()
{
    int A[] = {100, 200, 400, 100};
    int n = sizeof(A)/sizeof(A[0]);
    int B[] = {190, 200, 87, 600, 800};
    int m = sizeof(B)/sizeof(B[0]);
    printNonDivisible(A, B, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for naive implementation
import java.io.*;

public class GFG {

// Function for checking the condition
// with 2 loops
static void printNonDivisible(int []A, int []B,
                              int n, int m)
{

    for (int i = 0; i < m; i++)
    {
        int j = 0;
        for (j = 0; j < n; j++)
            if( B[i] % A[j] == 0 )
                break;

        // If none of the elements
        // in A[] divided B[i]
        if (j == n)
            System.out.println(B[i]);
    }
}

    // Driver code
    static public void main (String[] args)
    {
        int []A = {100, 200, 400, 100};
        int n = A.length;

        int []B = {190, 200, 87, 600, 800};
        int m = B.length;

        printNonDivisible(A, B, n, m);
    }
}

// This code is contributed by vt_m .
```

## 蟒蛇 3

```
# Python3 code for naive implementation
import math as mt

# Function for checking the condition
# with 2 loops
def printNonDivisible(A, B, n, m):

    for i in range(m):
        j = 0
        for j in range(n):
            if(B[i] % A[j] == 0):
                break

        # If none of the elements in A[]
        # divided B[i]
        if (j == n - 1):
            print(B[i])

# Driver code
A = [100, 200, 400, 100]
n = len(A)
B = [190, 200, 87, 600, 800]
m = len(B)
printNonDivisible(A, B, n, m)

# This code is contributed by#
# mohit kumar 29
```

## C#

```
// C# code for naive implementation
using System;

public class GFG {

// Function for checking the
// condition with 2 loops
static void printNonDivisible(int []A, int []B,
                              int n, int m)
{

    for (int i = 0; i < m; i++)
    {
        int j = 0;
        for (j = 0; j < n; j++)
            if( B[i] % A[j] == 0 )
                break;

        // If none of the elements
        // in A[] divided B[i]
        if (j == n)
            Console.WriteLine(B[i]);
    }
}

    // Driver code
    static public void Main ()
    {
        int []A = {100, 200, 400, 100};
        int n = A.Length;
        int []B = {190, 200, 87, 600, 800};
        int m = B.Length;
        printNonDivisible(A, B, n, m);
    }
}

// This code is contributed by vt_m .
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for naive implementation

// Function for checking
// the condition with 2 loops
function printNonDivisible($A, $B,
                           $n, $m)
{
    for ($i = 0; $i < $m; $i++)
    {
        $j = 0;
        for ($j = 0; $j < $n; $j++)
            if( $B[$i] % $A[$j] == 0 )
                break;

        // If none of the elements
        // in A[] divided B[i]
        if ($j == $n)
            echo $B[$i], "\n";
    }
}

// Driver code
$A= array (100, 200, 400, 100);
$n = sizeof($A);
$B = array (190, 200, 87, 600, 800);
$m = sizeof($B);

printNonDivisible($A, $B, $n, $m);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript code for naive implementation

    // Function for checking the
    // condition with 2 loops
    function printNonDivisible(A, B, n, m)
    {

        for (let i = 0; i < m; i++)
        {
            let j = 0;
            for (j = 0; j < n; j++)
                if( B[i] % A[j] == 0 )
                    break;

            // If none of the elements
            // in A[] divided B[i]
            if (j == n)
                document.write(B[i] + "</br>");
        }
    }

    let A = [100, 200, 400, 100];
    let n = A.length;
    let B = [190, 200, 87, 600, 800];
    let m = B.length;
    printNonDivisible(A, B, n, m);

</script>
```

**输出:**

```
190
87
```

**时间复杂度:-**O(n * m)
T3】辅助空间:- O(1)
**方法 2(元素少时有效)**

*   保持一个数组标记[]来标记 A[]中数字的倍数。
*   标记 A[]中所有元素的所有倍数，直到最大值为 B[]。
*   检查 B[]中每个元素 n 的标记[B[i]]值是否不为 0，如果未标记，则打印。

## C++

```
// CPP code for improved implementation
#include<bits/stdc++.h>
using namespace std;

// Function for printing all elements of B[]
// that are not divisible by any element of A[]
void printNonDivisible(int A[], int B[], int n,
                                         int m)
{
    // Find maximum element in B[]
    int maxB = 0;
    for (int i = 0; i < m; i++)
        if (B[i] > maxB)
            maxB = B[i];

    // Initialize all multiples as marked
    int mark[maxB];
    memset(mark, 0, sizeof(mark));

    // Marking the multiples of all the
    // elements of the array.
    for (int i = 0; i < n; i++)
        for (int x = A[i]; x <= maxB; x += A[i])
            mark[x]++;

    // Print not marked elements
    for (int i = 0; i < m; i++)
        if (! mark[B[i]])
            cout << B[i] << endl;
}

// Driver function
int main()
{
    int A[] = {100, 200, 400, 100};
    int n = sizeof(A)/sizeof(A[0]);
    int B[] = {190, 200, 87, 600, 800};
    int m = sizeof(B)/sizeof(B[0]);
    printNonDivisible(A, B, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for improved implementation
import java.io.*;

class GFG
{

// Function for printing all elements of B[]
// that are not divisible by any element of A[]
static void printNonDivisible(int []A, int []B,
                                    int n,int m)
{
    // Find maximum element in B[]
    int maxB = 0;
    for (int i = 0; i < m; i++)
        if (B[i] > maxB)
            maxB = B[i];

    // Initialize all multiples as marked

    int [] mark = new int[maxB + 1];
    for(int i = 0; i < maxB; i++)
        mark[i]=0;

    // Marking the multiples of all the
    // elements of the array.
    for (int i = 0; i < n; i++)
        for (int x = A[i]; x <= maxB; x += A[i])
            mark[x]++;

    // Print not marked elements
    for (int i = 0; i < m; i++)
        if (mark[B[i]] == 0)
            System.out.println(B[i]);
}

// Driver code
static public void main(String[] args)
{
    int []A= {100, 200, 400, 100};
    int n = A.length;
    int []B= {190, 200, 87, 600, 800};
    int m = B.length;
    printNonDivisible(A, B, n, m);
}
}

// This code is contributed by Mohit Kumar.
```

## 蟒蛇 3

```
# Python 3 code for improved implementation

# Function for printing all elements of B[]
# that are not divisible by any element of A[]
def printNonDivisible(A, B, n, m):

    # Find maximum element in B[]
    maxB = 0
    for i in range(0, m, 1):
        if (B[i] > maxB):
            maxB = B[i]

    # Initialize all multiples as marked
    mark = [0 for i in range(maxB)]

    # Marking the multiples of all
    # the elements of the array.
    for i in range(0, n, 1):
        for x in range(A[i], maxB, A[i]):
            mark[x] += 1

    # Print not marked elements
    for i in range(0, m - 1, 1):
        if (mark[B[i]] == 0):
            print(B[i])

# Driver Code
if __name__ == '__main__':
    A = [100, 200, 400, 100]
    n = len(A)
    B = [190, 200, 87, 600, 800]
    m = len(B)
    printNonDivisible(A, B, n, m)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# code for improved implementation
using System;

class GFG
{

// Function for printing all elements of []B
// that are not divisible by any element of []A
static void printNonDivisible(int []A, int []B,
                                    int n, int m)
{
    // Find maximum element in []B
    int maxB = 0;
    for (int i = 0; i < m; i++)
        if (B[i] > maxB)
            maxB = B[i];

    // Initialize all multiples as marked
    int [] mark = new int[maxB + 1];
    for(int i = 0; i < maxB; i++)
        mark[i] = 0;

    // Marking the multiples of all the
    // elements of the array.
    for (int i = 0; i < n; i++)
        for (int x = A[i]; x <= maxB; x += A[i])
            mark[x]++;

    // Print not marked elements
    for (int i = 0; i < m; i++)
        if (mark[B[i]] == 0)
            Console.WriteLine(B[i]);
}

// Driver code
static public void Main(String[] args)
{
    int []A= {100, 200, 400, 100};
    int n = A.Length;
    int []B= {190, 200, 87, 600, 800};
    int m = B.Length;
    printNonDivisible(A, B, n, m);
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for improved implementation

// Function for printing all elements of B[]
// that are not divisible by any element of A[]
function printNonDivisible($A, $B, $n, $m)
{

    // Find maximum element in B[]
    $maxB = 0;
    for ($i = 0; $i < $m; $i++)
    {
        if ($B[$i] > $maxB)
            $maxB = $B[$i];
    }

    // Initialize all multiples as marked
    $mark = array();
    for ($i = 0; $i < $maxB; $i++)
    {
        $mark[] = "0";
    }

    // Marking the multiples of all
    // the elements of the array.
    for ($i = 0; $i < $n; $i++)
    {
        for ($x = $A[$i]; $x < $maxB;
                          $x += $A[$i])
        {
            $mark[$x] += 1;
        }
    }

    // Print not marked elements
    for ($i = 0; $i < $m - 1; $i++)
    {
        if ($mark[$B[$i]] == 0)
            echo "$B[$i]\n";
    }
}

// Driver Code
$A = array(100, 200, 400, 100);
$n = count($A);
$B = array(190, 200, 87, 600, 800);
$m = count($B);
printNonDivisible($A, $B, $n, $m);

// This code is contributed by
// Srathore
?>
```

## java 描述语言

```
<script>

    // Javascript code for improved implementation

    // Function for printing all elements of []B
    // that are not divisible by any element of []A
    function printNonDivisible(A, B, n, m)
    {
        // Find maximum element in []B
        let maxB = 0;
        for (let i = 0; i < m; i++)
            if (B[i] > maxB)
                maxB = B[i];

        // Initialize all multiples as marked
        let mark = new Array(maxB + 1);
        for(let i = 0; i < maxB; i++)
            mark[i] = 0;

        // Marking the multiples of all the
        // elements of the array.
        for (let i = 0; i < n; i++)
            for (let x = A[i]; x <= maxB; x += A[i])
                mark[x]++;

        // Print not marked elements
        for (let i = 0; i < m; i++)
            if (mark[B[i]] == 0)
                document.write(B[i] + "</br>");
    }

    let A= [100, 200, 400, 100];
    let n = A.length;
    let B= [190, 200, 87, 600, 800];
    let m = B.length;
    printNonDivisible(A, B, n, m);

</script>
```

**输出:**

```
190
87
```

**时间复杂度:-**O(m+n *(max(B[]/min(A[])))
**辅助空间:-**O(n)+O(m)+O(max(B[])
本文由 **Sakshi Tiwari** 供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。