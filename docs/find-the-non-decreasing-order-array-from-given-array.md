# 从给定数组中找到非递减顺序数组

> 原文:[https://www . geeksforgeeks . org/从给定数组中查找非递减顺序数组/](https://www.geeksforgeeks.org/find-the-non-decreasing-order-array-from-given-array/)

给定一个大小为 **N / 2** 的数组 **A[]** ，任务是构建大小为 N 的数组 **B[]** ，使得:

1.  B[]按非递减顺序排序。
2.  a[I]= B[I]+B[n–I+1]。

**注:**阵 **A[]** 给出的方式是，答案总是可能的。
**例:**

> **输入:** A[] = {3，4 }
> T3】输出:0 1 3 3
> T6】输入: A[] = {4，1 }
> T9】输出:0 1 4

**进场:**我们来呈现以下贪婪进场。数字将成对恢复 **(B[0]、B[n–1])**、 **(B[1]、B[n–2])**等。因此，我们可以对当前对的值有一些限制(满足排序结果的标准)。
最初，**l = 0****r = 10<sup>9</sup>**更新为**l = a[I]****r = a[n–I+1]**。让 **l** 在答案中成为最小可能。以 **a[i] = max(l，b[I]–r)**和**r = b[I]–l**为例，选择 **l** 的方式使得 **l** 和 **r** 都在限制范围内，并且 **l** 也是最小可能的。
如果 **l** 大于 1，我们将向上移动 **l** 极限，向下移动 **r** 极限，为以后的选择留下更少的自由。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print
// the contents of the array
void printArr(int b[], int n)
{
    for (int i = 0; i < n; i++)
        cout << b[i] << " ";
}

// Function to build array B[]
void ModifiedArray(int a[], int n)
{
    // Lower and upper limits
    int l = 0, r = INT_MAX;

    // To store the required array
    int b[n] = { 0 };

    // Apply greedy approach
    for (int i = 0; i < n / 2; i++) {
        b[i] = max(l, a[i] - r);
        b[n - i - 1] = a[i] - b[i];
        l = b[i];
        r = b[n - i - 1];
    }

    // Print the built array b[]
    printArr(b, n);
}

// Driver code
int main()
{
    int a[] = { 5, 6 };
    int n = sizeof(a) / sizeof(a[0]);
    ModifiedArray(a, 2 * n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{
    // Utility function to print
    // the contents of the array
    void printArr(int b[], int n)
    {
        for (int i = 0; i < n; i++)
        {
             System.out.print(" " + b[i] + " ");
         }
    }

    // Function to build array B[]
    void ModifiedArray(int a[], int n)
    {
        // Lower and upper limits
        int l = 0, r = Integer.MAX_VALUE;

        // To store the required array
        int[] b = new int[n];

    // Apply greedy approach
    for (int i = 0; i < n / 2; i++) {
        b[i] = Math.max(l, a[i] - r);
        b[n - i - 1] = a[i] - b[i];
        l = b[i];
        r = b[n - i - 1];
    }

    // Print the built array b[]
    printArr(b, n);
}   
// Driver code
public static void main(String args[])
{
   int a[] = { 5, 6 };
   int n = a.length ;
   solution s=new solution();
   s.ModifiedArray(a, 2 * n);

}
}
//This code is contributed by Shivi_Aggarwal
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import sys

# Utility function to print the
# contents of the array
def printArr(b, n):
    for i in range(0, n, 1):
        print(b[i], end = " ")

# Function to build array B[]
def ModifiedArray(a, n):

    # Lower and upper limits
    l = 0
    r = sys.maxsize

    # To store the required array
    b = [0 for i in range(n)]

    # Apply greedy approach
    for i in range(0, int(n / 2), 1):
        b[i] = max(l, a[i] - r)
        b[n - i - 1] = a[i] - b[i]
        l = b[i]
        r = b[n - i - 1]

    # Print the built array b[]
    printArr(b, n)

# Driver code
if __name__ == '__main__':
    a = [5, 6]
    n = len(a)
    ModifiedArray(a, 2 * n)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of the approach

using System;

public class GFG{

// Utility function to print
// the contents of the array
static void printArr(int []b, int n)
    {
        for (int i = 0; i < n; i++)
        {
            Console.Write(" " + b[i] + " ");
        }
    }

    // Function to build array B[]
static    void ModifiedArray(int []a, int n)
    {
        // Lower and upper limits
        int l = 0, r = int.MaxValue;

        // To store the required array
        int[] b = new int[n];

    // Apply greedy approach
    for (int i = 0; i < n / 2; i++) {
        b[i] = Math.Max(l, a[i] - r);
        b[n - i - 1] = a[i] - b[i];
        l = b[i];
        r = b[n - i - 1];
    }

    // Print the built array b[]
    printArr(b, n);
}

        // Driver code
    static public void Main (){
    int []a = { 5, 6 };
    int n = a.Length;
    ModifiedArray(a, 2 * n);
    }
}
// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to print the
// contents of the array
function printArr($b, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $b[$i] . " ";
}

// Function to build array B[]
function ModifiedArray($a, $n)
{
    // Lower and upper limits
    $l = 0; $r = PHP_INT_MAX;

    // To store the required array
    $b = array(0);

    // Apply greedy approach
    for ($i = 0; $i < $n / 2; $i++)
    {
        $b[$i] = max($l, $a[$i] - $r);
        $b[$n - $i - 1] = $a[$i] - $b[$i];
        $l = $b[$i];
        $r = $b[$n - $i - 1];
    }

    // Print the built array b[]
    printArr($b, $n);
}

// Driver code
$a = array( 5, 6 );
$n = sizeof($a);
ModifiedArray($a, 2 * $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program of the above approach

    // Utility function to print
    // the contents of the array
    function printArr(b, n)
    {
        for (let i = 0; i < n; i++)
        {
             document.write(" " + b[i] + " ");
         }
    }

    // Function to build array B[]
    function ModifiedArray(a, n)
    {
        // Lower and upper limits
        let l = 0, r = Number.MAX_VALUE;

        // To store the required array
        let b = Array(n).fill(0);

    // Apply greedy approach
    for (let i = 0; i < n / 2; i++) {
        b[i] = Math.max(l, a[i] - r);
        b[n - i - 1] = a[i] - b[i];
        l = b[i];
        r = b[n - i - 1];
    }

    // Print the built array b[]
    printArr(b, n);
}

// Driver code

    let a = [ 5, 6 ];
   let n = a.length ;
   ModifiedArray(a, 2 * n);

</script>
```

**Output:** 

```
0 1 5 5
```