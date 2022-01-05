# 上一个较大的元素

> 原文:[https://www.geeksforgeeks.org/previous-greater-element/](https://www.geeksforgeeks.org/previous-greater-element/)

给定一个不同元素的数组，为每个元素找到上一个更大的元素。如果上一个较大的元素不存在，打印-1。
**例:**

```
Input : arr[] = {10, 4, 2, 20, 40, 12, 30}
Output :         -1, 10, 4, -1, -1, 40, 40

Input : arr[] = {10, 20, 30, 40}
Output :        -1, -1, -1, -1

Input : arr[] = {40, 30, 20, 10}
Output :        -1, 40, 30, 20
```

预期时间复杂度:O(n)

一个简单的解决方案是运行两个嵌套循环。外部循环逐个选取元素。内部循环，找到更大的前一个元素。

## C++

```
// C++ program previous greater element
// A naive solution to print previous greater
// element for every element in an array.
#include <bits/stdc++.h>
using namespace std;

void prevGreater(int arr[], int n)
{
    // Previous greater for first element never
    // exists, so we print -1.
    cout << "-1, ";

    // Let us process remaining elements.
    for (int i = 1; i < n; i++) {

        // Find first element on left side
        // that is greater than arr[i].
        int j;
        for (j = i-1; j >= 0; j--) {
            if (arr[i] < arr[j]) {
            cout << arr[j] << ", ";
            break;
            }            
        }

        // If all elements on left are smaller.
        if (j == -1)
        cout << "-1, ";
    }
}
// Driver code
int main()
{
    int arr[] = { 10, 4, 2, 20, 40, 12, 30 };
    int n = sizeof(arr) / sizeof(arr[0]);
    prevGreater(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program previous greater element
// A naive solution to print
// previous greater element
// for every element in an array.
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
static void prevGreater(int arr[],
                        int n)
{
    // Previous greater for
    // first element never
    // exists, so we print -1.
    System.out.print("-1, ");

    // Let us process
    // remaining elements.
    for (int i = 1; i < n; i++)
    {

        // Find first element on
        // left side that is
        // greater than arr[i].
        int j;
        for (j = i-1; j >= 0; j--)
        {
            if (arr[i] < arr[j])
            {
            System.out.print(arr[j] + ", ");
            break;
            }            
        }

        // If all elements on
        // left are smaller.
        if (j == -1)
        System.out.print("-1, ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {10, 4, 2, 20, 40, 12, 30};
    int n = arr.length;
    prevGreater(arr, n);
}
}
```

## 蟒蛇 3

```
# Python 3 program previous greater element
# A naive solution to print previous greater
# element for every element in an array.
def prevGreater(arr, n) :

    # Previous greater for first element never
    # exists, so we print -1.
    print("-1",end = ", ")

    # Let us process remaining elements.
    for i in range(1, n) :
        flag = 0

        # Find first element on left side
        # that is greater than arr[i].
        for j in range(i-1, -1, -1) :
            if arr[i] < arr[j] :
                print(arr[j],end = ", ")
                flag = 1
                break

        # If all elements on left are smaller.
        if j == 0 and flag == 0:
            print("-1",end = ", ")

# Driver code
if __name__ == "__main__" :
    arr = [10, 4, 2, 20, 40, 12, 30]
    n = len(arr)
    prevGreater(arr, n)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program previous greater element
// A naive solution to print
// previous greater element
// for every element in an array.

using System;
class GFG
{
static void prevGreater(int[] arr,
                        int n)
{
    // Previous greater for
    // first element never
    // exists, so we print -1.
    Console.Write("-1, ");

    // Let us process
    // remaining elements.
    for (int i = 1; i < n; i++)
    {

        // Find first element on
        // left side that is
        // greater than arr[i].
        int j;
        for (j = i-1; j >= 0; j--)
        {
            if (arr[i] < arr[j])
            {
            Console.Write(arr[j] + ", ");
            break;
            }            
        }

        // If all elements on
        // left are smaller.
        if (j == -1)
        Console.Write("-1, ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = {10, 4, 2, 20, 40, 12, 30};
    int n = arr.Length;
    prevGreater(arr, n);
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program previous greater element
// A naive solution to print previous greater
// element for every element in an array.

function prevGreater(&$arr,$n)
{
    // Previous greater for first element never
    // exists, so we print -1.
    echo( "-1, ");

    // Let us process remaining elements.
    for ($i = 1; $i < $n; $i++)
    {

        // Find first element on left side
        // that is greater than arr[i].
        for ($j = $i-1; $j >= 0; $j--)
    {
            if ($arr[$i] < $arr[$j])
        {
            echo($arr[$j]);
        echo( ", ");
            break;
            }            
        }

        // If all elements on left are smaller.
        if ($j == -1)
        echo("-1, ");
    }
}

// Driver code
$arr = array(10, 4, 2, 20, 40, 12, 30);
$n = sizeof($arr) ;
prevGreater($arr, $n);

//This code is contributed by Shivi_Aggarwal.

?>
```

## java 描述语言

```
<script>
// Javascript program previous greater element
// A naive solution to print
// previous greater element
// for every element in an array.

    function prevGreater(arr,n)
    {
        // Previous greater for
    // first element never
    // exists, so we print -1.
    document.write("-1, ");

    // Let us process
    // remaining elements.
    for (let i = 1; i < n; i++)
    {

        // Find first element on
        // left side that is
        // greater than arr[i].
        let j;
        for (j = i-1; j >= 0; j--)
        {
            if (arr[i] < arr[j])
            {
            document.write(arr[j] + ", ");
            break;
            }            
        }

        // If all elements on
        // left are smaller.
        if (j == -1)
        document.write("-1, ");
    }
    }

    // Driver Code
    let arr=[10, 4, 2, 20, 40, 12, 30];
    let n = arr.length;
    prevGreater(arr, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
-1, 10, 4, -1, -1, 40, 40
```