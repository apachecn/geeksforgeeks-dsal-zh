# 两组笛卡尔乘积

> 原文:[https://www.geeksforgeeks.org/cartesian-product-two-sets/](https://www.geeksforgeeks.org/cartesian-product-two-sets/)

设 A 和 B 是两个集合，笛卡儿积 **A × B** 是 A 和 B
中所有有序元素对的集合 **A × B = {{x，y} : x ∈ A，y∈B }**T5】

> 设 A = {a，B，c}和 B = {d，e，f}
> 两个集合的笛卡儿积为
> A x B = {a，d}，{a，e}，{a，f}，{b，d}，{b，f}，{c，d}，{c，e}，{c，e}，{ c，f}}
> A 有 3 个元素，B 也有 3 个元素。笛卡尔乘积有 3×3 = 9 个元素。
> 一般来说，如果集合 A 中有 m 个元素，集合 B 中有 n 个元素，那么笛卡儿积中的元素个数就是 **m x n**

**给定两个有限非空集合，编写程序打印笛卡儿积。**
**例:**

```
Input : A = {1, 2}, B = {3, 4}
Output : A × B = {{1, 3}, {1, 4}, {2, 3}, {2, 4}}

Input  : A = {1, 2, 3} B = {4, 5, 6}
Output : A × B = {{1, 4}, {1, 5}, {1, 6}, {2, 4}, 
         {2, 5}, {2, 6}, {3, 4}, {3, 5}, {3, 6}}
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ Program to find the Cartesian Product of Two Sets
#include <stdio.h>

void findCart(int arr1[], int arr2[], int n, int n1)
{
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n1; j++)
            printf("{%d, %d}, ", arr1[i], arr2[j]);
}

int main()
{
    int arr1[] = { 1, 2, 3 }; // first set
    int arr2[] = { 4, 5, 6 }; // second set
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    findCart(arr1, arr2, n1, n2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// Cartesian Product of Two Sets
import java.io.*;
import java.util.*;

class GFG {

    static void findCart(int arr1[], int arr2[],
                                    int n, int n1)
    {
        for (int i = 0; i < n; i++)
          for (int j = 0; j < n1; j++)
            System.out.print("{"+ arr1[i]+", "
                             + arr2[j]+"}, ");
    }
    // Driver code
    public static void main (String[] args) {

        // first set
        int arr1[] = { 1, 2, 3 };

        // second set
        int arr2[] = { 4, 5, 6 };

        int n1 = arr1.length;
        int n2 = arr2.length;
        findCart(arr1, arr2, n1, n2);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 Program to find the
# Cartesian Product of Two Sets

def findCart(arr1, arr2, n, n1):

    for i in range(0,n):
        for j in range(0,n1):
            print("{",arr1[i],", ",arr2[j],"}, ",sep="",end="")

# Driver code
arr1 = [ 1, 2, 3 ] # first set
arr2 = [ 4, 5, 6 ] # second set

n1 = len(arr1) # sizeof(arr1[0])
n2 = len(arr2) # sizeof(arr2[0]);

findCart(arr1, arr2, n1, n2);

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// C# Program to find the
// Cartesian Product of Two Sets
using System;

class GFG {

    static void findCart(int []arr1, int []arr2,
                                    int n, int n1)
    {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n1; j++)
                Console.Write("{" + arr1[i] + ", "
                                + arr2[j] + "}, ");
    }

    // Driver code
    public static void Main () {

        // first set
        int []arr1 = { 1, 2, 3 };

        // second set
        int []arr2 = { 4, 5, 6 };

        int n1 = arr1.Length;
        int n2 = arr2.Length;

        findCart(arr1, arr2, n1, n2);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// Cartesian Product of Two Sets

function findCart($arr1, $arr2, $n, $n1)
{
    for ($i = 0; $i < $n; $i++)
        for ( $j = 0; $j < $n1; $j++)
            echo "{", $arr1[$i] ," , ",
                      $arr2[$j], "}",",";
}

// Driver Code

// first set
$arr1 = array ( 1, 2, 3 );

// second set
$arr2 = array ( 4, 5, 6 );
$n1 = sizeof($arr1) ;
$n2 = sizeof($arr2);
findCart($arr1, $arr2, $n1, $n2);

// This code is contributed by m_kit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find the
// Cartesian Product of Two Set

    function findCart(arr1, arr2, n, n1)
    {
        for (let i = 0; i < n; i++)
          for (let j = 0; j < n1; j++)
            document.write("{"+ arr1[i]+", "
                             + arr2[j]+"}, ");
    }

// Driver Code

        // first set
        let arr1 = [ 1, 2, 3 ];

        // second set
        let arr2 = [4, 5, 6 ];

        let n1 = arr1.length;
        let n2 = arr2.length;
        findCart(arr1, arr2, n1, n2);

       // This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
{{1, 4}, {1, 5}, {1, 6}, {2, 4}, {2, 5}, {2, 6}, {3, 4}, {3, 5}, {3, 6}}
```

**实例:**
1)一套扑克牌是一个四元集与一套十三元集的笛卡尔乘积。
2)二维坐标系是两组实数的笛卡尔乘积。
**参考:**
[https://en.wikipedia.org/wiki/Cartesian_product](https://en.wikipedia.org/wiki/Cartesian_product)