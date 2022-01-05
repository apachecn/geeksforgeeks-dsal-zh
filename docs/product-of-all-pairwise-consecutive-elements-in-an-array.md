# 数组中所有成对连续元素的乘积

> 原文:[https://www . geesforgeks . org/全成对连续数组元素乘积/](https://www.geeksforgeeks.org/product-of-all-pairwise-consecutive-elements-in-an-array/)

给定 N 个元素的整数数组。任务是打印所有成对连续元素的乘积。
大小为 N 的数组的成对连续对是 **(a[i]，a[i+1])** 对于所有的![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")范围从 **0 到 N-2** 
**示例** :

```
Input  : arr[] = {8, 5, 4, 3, 15, 20}
Output : 40, 20, 12, 45, 300

Input  : arr[] = {5, 10, 15, 20}
Output : 50, 150, 300
```

解决方案是遍历数组，计算并打印每对的乘积(arr[i]，arr[i+1])。
以下是该方法的实现:

## C++

```
// C++ program to print the
// product of the consecutive elements.
#include <iostream>
using namespace std;

// Function to print pairwise
// consecutive product
void pairwiseProduct(int arr[], int n)
{
    int prod = 1;
    for (int i = 0; i < n - 1; i++) {

        // multiply the alternate numbers
        prod = arr[i] * arr[i + 1];
        printf(" %d ", prod);
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 10, 15, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pairwiseProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the product
// of the consecutive elements.
import java .io.*;

class GFG
{
// Function to print pairwise
// consecutive product
static void pairwiseProduct(int[] arr,
                            int n)
{
    int prod = 1;
    for (int i = 0; i < n - 1; i++)
    {

        // multiply the alternate numbers
        prod = arr[i] * arr[i + 1];
        System.out.print(prod + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 4, 10, 15, 5, 6 };
    int n = arr.length;

    pairwiseProduct(arr, n);
}
}

// This code is contributed
// by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to print the
# product of the consecutive elements.

# Function to print pairwise
# consecutive product
def pairwiseProduct( arr, n):

    prod = 1
    for i in range(n - 1) :

        # multiply the alternate numbers
        prod = arr[i] * arr[i + 1]
        print(prod, end = " ")

# Driver Code
if __name__=="__main__":

    arr = [ 4, 10, 15, 5, 6 ]
    n = len(arr)

    pairwiseProduct(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print the product
// of the consecutive elements.
using System;

class GFG
{
// Function to print pairwise
// consecutive product
static void pairwiseProduct(int[] arr,
                            int n)
{
    int prod = 1;
    for (int i = 0; i < n - 1; i++)
    {

        // multiply the alternate numbers
        prod = arr[i] * arr[i + 1];
        Console.Write(prod + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 4, 10, 15, 5, 6 };
    int n = arr.Length;

    pairwiseProduct(arr, n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the
// product of the consecutive elements.

// Function to print pairwise
// consecutive product
function pairwiseProduct(&$arr, $n)
{
    $prod = 1;
    for ($i = 0; $i < $n - 1; $i++)
    {

        // multiply the alternate numbers
        $prod = $arr[$i] * $arr[$i + 1];
        echo ($prod);
        echo (" ");
    }
}

// Driver Code
$arr = array(4, 10, 15, 5, 6 );
$n = sizeof($arr);

pairwiseProduct($arr, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to print the
// product of the consecutive elements.

// Function to print pairwise
// consecutive product
function pairwiseProduct( arr,  n)
{
    let prod = 1;
    for (let i = 0; i < n - 1; i++) {

        // multiply the alternate numbers
        prod = arr[i] * arr[i + 1];
        document.write(prod + " ");;
    }
}

    // driver code
    let arr = [ 4, 10, 15, 5, 6 ];
    let n = arr.length;
    pairwiseProduct(arr, n);

   // This code is contributed by jana_sayantan.
</script>
```

**Output:** 

```
40  150  75  30
```

**时间复杂度:** O(n)