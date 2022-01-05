# 计算一个数组的比特数的程序

> 原文:[https://www . geesforgeks . org/program-to-compute-bitonicity of a array/](https://www.geeksforgeeks.org/program-to-calculate-bitonicity-of-an-array/)

给定一组![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")整数。任务是找到给定数组的比特数。
数组 arr[]的比特性可以定义为:

```
B[i] = 0,         if i = 0.
     = B[i-1] + 1, if arr[i] > arr[i-1]
     = B[i-1] - 1, if arr[i] < arr[i-1]
     = B[i-1],     if arr[i] = arr[i-1]    

Bitonicity will be last element of array B[].
```

**示例** :

```
Input : arr[] = {1, 2, 3, 4, 5}
Output : 4

Input : arr[] = {1, 4, 5, 3, 2}
Output : 0
```

假设数组 arr[]的比特性可以定义为:

```
B[i] = 0,         if i = 0.
     = B[i-1] + 1, if arr[i] > arr[i-1]
     = B[i-1] - 1, if arr[i] < arr[i-1]
     = B[i-1],     if arr[i] = arr[i-1]

Bitonicity will be last element of array B[].
```

从上面的表达式可以推导出:

*   数组的比特数最初为 0。
*   如果下一个元素大于上一个元素，则移动到下一个元素时增加 1。
*   如果下一个元素大于上一个元素，则移动到下一个元素时，它会减少 1。

想法是取一个变量![bt = 0  ](img/f12824a00148e88ee3ad09aeb981b775.png "Rendered by QuickLaTeX.com")并开始遍历数组，如果下一个元素大于当前元素，则增加**Bt**1，如果下一个元素小于当前元素，则减少**Bt**1。
以下是上述方法的实施:

## C++

```
// C++ program to find bitonicity
// of an array
#include <iostream>
using namespace std;

// Function to find the bitonicity
// of an array
int findBitonicity(int arr[], int n)
{
    int bt = 0;

    for (int i = 1; i < n; i++) {
        if (arr[i] > arr[i - 1])
            bt++;
        else if (arr[i] < arr[i - 1])
            bt--;
    }

    return bt;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 4, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Bitonicity = " << findBitonicity(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find bitonicity
// of an array
import java.util.*;
import java.lang.*;

class GFG
{

// Function to find the bitonicity
// of an array
static int findBitonicity(int[] arr,
                          int n)
{
    int bt = 0;

    for (int i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            bt++;
        else if (arr[i] < arr[i - 1])
            bt--;
    }

    return bt;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 4, 3 };

    int n = arr.length;

    System.out.print("Bitonicity = " +
              findBitonicity(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 program to find bitonicity
# of an array

# Function to find the bitonicity
# of an array
def findBitonicity(arr, n):
    bt = 0

    for i in range(1, n, 1):
        if (arr[i] > arr[i - 1]):
            bt += 1
        elif (arr[i] < arr[i - 1]):
            bt -= 1

    return bt

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 4, 3]

    n = len(arr)

    print("Bitonicity =",
           findBitonicity(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find bitonicity
// of an array
using System;

class GFG
{
// Function to find the bitonicity
// of an array
static int findBitonicity(int[] arr,
                          int n)
{
    int bt = 0;

    for (int i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            bt++;
        else if (arr[i] < arr[i - 1])
            bt--;
    }

    return bt;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6, 4, 3 };

    int n = arr.Length;

    Console.Write("Bitonicity = " +
                  findBitonicity(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find bitonicity
// of an array

// Function to find the bitonicity
// of an array
function findBitonicity(&$arr, $n)
{
    $bt = 0;

    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i] > $arr[$i - 1])
            $bt++;
        else if ($arr[$i] < $arr[$i - 1])
            $bt--;
    }

    return $bt;
}

// Driver Code
$arr = array(1, 2, 3, 4, 5, 6, 4, 3 );

$n = sizeof($arr);

echo ("Bitonicity = ");
echo findBitonicity($arr, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find bitonicity
// of an array   

// Function to find the bitonicity
// of an array
    function findBitonicity(arr , n)
    {
        var bt = 0;

        for (i = 1; i < n; i++) {
            if (arr[i] > arr[i - 1])
                bt++;
            else if (arr[i] < arr[i - 1])
                bt--;
        }

        return bt;
    }

    // Driver Code

        var arr = [ 1, 2, 3, 4, 5, 6, 4, 3 ];

        var n = arr.length;

        document.write("Bitonicity = " + findBitonicity(arr, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Bitonicity = 3
```