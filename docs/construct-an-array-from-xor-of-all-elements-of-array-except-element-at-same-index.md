# 从数组中除同一索引处的元素外的所有元素的异或来构造数组

> 原文:[https://www . geeksforgeeks . org/从数组的所有元素的异或中构造一个数组-同一索引处的元素除外/](https://www.geeksforgeeks.org/construct-an-array-from-xor-of-all-elements-of-array-except-element-at-same-index/)

给定一个有 n 个正元素的数组 A[]。创建另一个数组 B[]如 B[i]的任务是对数组 A[]中除 A[i]以外的所有元素进行异或运算。
**例:**

```
Input : A[] = {2, 1, 5, 9}
Output : B[] = {13, 14, 10, 6}

Input : A[] = {2, 1, 3, 6}
Output : B[] = {4, 7, 5, 0}
```

**天真的做法:**
我们可以简单的把 B[i]算成 A[]除了 A[i]之外的所有元素的异或，算成

```
for (int i = 0; i < n; i++)
{
    B[i] = 0;
    for (int j = 0; j < n; j++)
        if ( i != j)
            B[i] ^= A[j];
}
```

这种天真方法的时间复杂度是 O (n^2).
这个幼稚方法的辅助空间是 O (n)。
**优化方法:**
首先计算数组 A[]的所有元素的 XOR，说“xor”，对于数组 A[]的每个元素，计算 **A[i] = xor ^ A[i]** 。

```
int xor = 0;
for (int i = 0; i < n; i++)
    xor ^= A[i];

for (int i = 0; i < n; i++)
        A[i] = xor ^ A[i];
```

这种方法的时间复杂度为 0(n)。
该方法的辅助空间为 O (1)。

## C++

```
// C++ program to construct array from
// XOR of elements of given array
#include <bits/stdc++.h>
using namespace std;

// function to construct new array
void constructXOR(int A[], int n)
{
    // calculate xor of array
    int XOR = 0;
    for (int i = 0; i < n; i++)
        XOR ^= A[i];

    // update array
    for (int i = 0; i < n; i++)
        A[i] = XOR ^ A[i];
}

// Driver code
int main()
{
    int A[] = { 2, 4, 1, 3, 5};
    int n = sizeof(A) / sizeof(A[0]);
    constructXOR(A, n);

    // print result
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct array from
// XOR of elements of given array
class GFG
{

    // function to construct new array
    static void constructXOR(int A[], int n)
    {

        // calculate xor of array
        int XOR = 0;
        for (int i = 0; i < n; i++)
            XOR ^= A[i];

        // update array
        for (int i = 0; i < n; i++)
            A[i] = XOR ^ A[i];
    }

    // Driver code
    public static void main(String[] args)
    {
        int A[] = { 2, 4, 1, 3, 5};
        int n = A.length;
        constructXOR(A, n);

        // print result
        for (int i = 0; i < n; i++)
            System.out.print(A[i] + " ");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to construct
# array from XOR of elements
# of given array

# function to construct new array
def constructXOR(A, n):

    # calculate xor of array
    XOR = 0
    for i in range(0, n):
        XOR ^= A[i]

    # update array
    for i in range(0, n):
        A[i] = XOR ^ A[i]

# Driver code
A = [ 2, 4, 1, 3, 5 ]
n = len(A)
constructXOR(A, n)

# print result
for i in range(0,n):
    print(A[i], end =" ")

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to construct array from
// XOR of elements of given array
using System;

class GFG
{

    // function to construct new array
    static void constructXOR(int []A, int n)
    {

        // calculate xor of array
        int XOR = 0;
        for (int i = 0; i < n; i++)
            XOR ^= A[i];

        // update array
        for (int i = 0; i < n; i++)
            A[i] = XOR ^ A[i];
    }

    // Driver code
    public static void Main()
    {
        int []A = { 2, 4, 1, 3, 5};
        int n = A.Length;
        constructXOR(A, n);

        // print result
        for (int i = 0; i < n; i++)
        Console.Write(A[i] + " ");
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to construct array from
// XOR of elements of given array

// function to construct new array
function constructXOR(&$A, $n)
{
    // calculate xor of array
    $XOR = 0;
    for ($i = 0; $i < $n; $i++)
        $XOR ^= $A[$i];

    // update array
    for ($i = 0; $i < $n; $i++)
        $A[$i] = $XOR ^ $A[$i];
}

// Driver code
$A = array( 2, 4, 1, 3, 5);
$n = sizeof($A);
constructXOR($A, $n);

// print result
for ($i = 0; $i < $n; $i++)
    echo $A[$i] ." ";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to construct array from
// XOR of elements of given array

// function to construct new array
function constructXOR(A, n)
{
    // calculate xor of array
    let XOR = 0;
    for (let i = 0; i < n; i++)
        XOR ^= A[i];

    // update array
    for (let i = 0; i < n; i++)
        A[i] = XOR ^ A[i];
}

// Driver code
    let A = [ 2, 4, 1, 3, 5];
    let n = A.length;
    constructXOR(A, n);

    // print result
    for (let i = 0; i < n; i++)
        document.write(A[i] + " ");

// This code is contributed by Surbhi Tyagi.

</script>
```

输出:

```
3 5 0 2 4
```

**相关问题:**
[一品阵拼图](https://www.geeksforgeeks.org/a-product-array-puzzle/)
本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。