# 使用数学运算

检查两个数组是否相互排列

> 原文:[https://www . geeksforgeeks . org/check-if-two-array-is-相互排列-使用数学运算/](https://www.geeksforgeeks.org/check-if-two-arrays-are-permutations-of-each-other-using-mathematical-operation/)

给定两个大小相同的未排序数组**，其中**对于所有 I 为 arr【I】>= 0**，任务是检查两个数组是否是彼此的排列。
**例:**** 

```
Input: arr1[] = {2, 1, 3, 5, 4, 3, 2}
       arr2[] = {3, 2, 2, 4, 5, 3, 1}
Output: Yes

Input: arr1[] = {2, 1, 3, 5}
       arr2[] = {3, 2, 2, 4}
Output: No
```

**已经在[中讨论过，使用**排序**和**散列**检查两个数组是否是彼此的排列。但是在这篇文章中，讨论了一种不同的方法。](https://www.geeksforgeeks.org/check-if-two-arrays-are-permutations-of-each-other/)** 

****进场:****

1.  **遍历第一个数组 A，**加**和**乘**所有元素，分别作为 *Sum1* 和 *Mul1* 存储在变量中。**
2.  **同样，遍历第二个数组 B，**加**和**乘**所有的元素，分别作为 *Sum2* 和 *Mul2* 存储在变量中。**
3.  **现在，比较 sum1、sum2 和 mul1、mul2。如果 *Sum1 == Sum2 和 Mu1 = = Mu2*，那么这两个数组是彼此的排列，否则不是。**

****以下是上述方法的实施:**** 

## **C++**

```
// CPP code to check if arrays
// are permutations of eah other
#include <iostream>
using namespace std;

// Function to check if arrays
// are permutations of each other.
bool arePermutations(int a[], int b[], int n, int m)
{

    int sum1 = 0, sum2 = 0, mul1 = 1, mul2 = 1;

    // Calculating sum and multiply of first array
    for (int i = 0; i < n; i++) {
        sum1 += a[i];
        mul1 *= a[i];
    }

    // Calculating sum and multiply of second array
    for (int i = 0; i < m; i++) {
        sum2 += b[i];
        mul2 *= b[i];
    }

    // If sum and mul of both arrays are equal,
    // return true, else return false.
    return ((sum1 == sum2) && (mul1 == mul2));
}

// Driver code
int main()
{

    int a[] = { 1, 3, 2 };
    int b[] = { 3, 1, 2 };

    int n = sizeof(a) / sizeof(int);
    int m = sizeof(b) / sizeof(int);

    if (arePermutations(a, b, n, m))
        cout << "Yes" << endl;

    else
        cout << "No" << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to check if arrays
// are permutations of eah other

import java.io.*;

class GFG {

// Function to check if arrays
// are permutations of each other.
static boolean arePermutations(int a[], int b[], int n, int m)
{

    int sum1 = 0, sum2 = 0, mul1 = 1, mul2 = 1;

    // Calculating sum and multiply of first array
    for (int i = 0; i < n; i++) {
        sum1 += a[i];
        mul1 *= a[i];
    }

    // Calculating sum and multiply of second array
    for (int i = 0; i < m; i++) {
        sum2 += b[i];
        mul2 *= b[i];
    }

    // If sum and mul of both arrays are equal,
    // return true, else return false.
    return ((sum1 == sum2) && (mul1 == mul2));
}

// Driver code

    public static void main (String[] args) {
            int a[] = { 1, 3, 2 };
    int b[] = { 3, 1, 2 };

    int n = a.length;
    int m = b.length;

    if (arePermutations(a, b, n, m)==true)
        System.out.println( "Yes");

    else
        System.out.println( "No");
    }
}
// This code is contributed by  inder_verma..
```

## **蟒蛇 3**

```
# Python 3 program to check if arrays
# are permutations of eah other

# Function to check if arrays
# are permutations of each other
def arePermutations(a, b, n, m) :

    sum1, sum2, mul1, mul2 = 0, 0, 1, 1

    # Calculating sum and multiply of first array
    for i in range(n) :
        sum1 += a[i]
        mul1 *= a[i]

    # Calculating sum and multiply of second array
    for i in range(m) :
        sum2 += b[i]
        mul2 *= b[i]

    # If sum and mul of both arrays are equal,
    # return true, else return false.
    return((sum1 == sum2) and (mul1 == mul2))

# Driver code    
if __name__ == "__main__" :

    a = [ 1, 3, 2]
    b = [ 3, 1, 2]

    n = len(a)
    m = len(b)

    if arePermutations(a, b, n, m) :
        print("Yes")

    else :
        print("No")

# This code is contributed by ANKITRAI1
```

## **C#**

```
// C# code to check if arrays
// are permutations of eah other
using System;

class GFG
{

// Function to check if arrays
// are permutations of each other.
static bool arePermutations(int[] a, int[] b,
                            int n, int m)
{

    int sum1 = 0, sum2 = 0,
        mul1 = 1, mul2 = 1;

    // Calculating sum and multiply
    // of first array
    for (int i = 0; i < n; i++)
    {
        sum1 += a[i];
        mul1 *= a[i];
    }

    // Calculating sum and multiply
    // of second array
    for (int i = 0; i < m; i++)
    {
        sum2 += b[i];
        mul2 *= b[i];
    }

    // If sum and mul of both arrays
    // are equal, return true, else
    // return false.
    return ((sum1 == sum2) &&
            (mul1 == mul2));
}

// Driver code
public static void Main ()
{
    int[] a = { 1, 3, 2 };
    int[] b = { 3, 1, 2 };

    int n = a.Length;
    int m = b.Length;

    if (arePermutations(a, b, n, m) == true)
        Console.Write( "Yes");

    else
        Console.Write( "No");
}
}

// This code is contributed
// by ChitraNayal
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP code to check if arrays
// are permutations of eah other

// Function to check if arrays
// are permutations of each other.
function arePermutations($a, $b, $n, $m)
{

    $sum1 = 0; $sum2 = 0;
    $mul1 = 1; $mul2 = 1;

    // Calculating sum and multiply
    // of first array
    for ($i = 0; $i < $n; $i++)
    {
        $sum1 += $a[$i];
        $mul1 *= $a[$i];
    }

    // Calculating sum and multiply
    // of second array
    for ($i = 0; $i < $m; $i++)
    {
        $sum2 += $b[$i];
        $mul2 *= $b[$i];
    }

    // If sum and mul of both arrays
    // are equal, return true, else
    // return false.
    return (($sum1 == $sum2) &&
            ($mul1 == $mul2));
}

// Driver code
$a = array( 1, 3, 2 );
$b = array( 3, 1, 2 );

$n = sizeof($a);
$m = sizeof($b);

if (arePermutations($a, $b, $n, $m))
    echo "Yes" . "\n";
else
    echo "No" . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## **java 描述语言**

```
<script>

// JavaScript code to check if arrays
// are permutations of eah other

    // Function to check if arrays
   // are permutations of each other.
    function arePermutations(a,b,n,m)
    {
        let sum1 = 0, sum2 = 0, mul1 = 1, mul2 = 1;

    // Calculating sum and multiply of first array
    for (let i = 0; i < n; i++) {
        sum1 += a[i];
        mul1 *= a[i];
    }

    // Calculating sum and multiply of second array
    for (let i = 0; i < m; i++) {
        sum2 += b[i];
        mul2 *= b[i];
    }

    // If sum and mul of both arrays are equal,
    // return true, else return false.
    return ((sum1 == sum2) && (mul1 == mul2));

    }

    // Driver code
    let a=[1, 3, 2 ];
    let b=[3, 1, 2];

    let n = a.length;
    let m = b.length;

    if (arePermutations(a, b, n, m)==true)
        document.write( "Yes");

    else
        document.write( "No");

// This code is contributed by rag2127

</script>
```

****Output:** 

```
Yes
```**