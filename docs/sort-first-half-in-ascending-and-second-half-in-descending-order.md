# 前半部分按升序排序，后半部分按降序排序| 1

> 原文:[https://www . geesforgeks . org/sort-升序前半部分和降序后半部分/](https://www.geeksforgeeks.org/sort-first-half-in-ascending-and-second-half-in-descending-order/)

给定一个整数数组，将数组的前半部分按升序排序，后半部分按降序排序。
**例:**

```
Input : arr[] = {5, 2, 4, 7, 9, 3, 1, 6, 8}
Output : arr[] = {1, 2, 3, 4, 9, 8, 7, 6, 5}

Input : arr[] = {1, 2, 3, 4, 5, 6}
Output : arr[] = {1, 2, 3, 6, 5, 4}
```

**算法:**
1。给定数组排序。
2。运行一个循环，直到数组长度的一半，并打印排序数组的元素。
3。从数组的最后一个索引到数组的中间运行一个循环，并以相反的顺序打印元素。
以下为相同的实现。

## C++

```
// C++ program to print first half in
// ascending order and the second half
// in descending order
#include <bits/stdc++.h>
using namespace std;

// function to print half of the array in
// ascending order and the other half in
// descending order
void printOrder(int arr[], int n)
{
    // sorting the array
    sort(arr, arr + n);

    // printing first half in ascending
    // order
    for (int i = 0; i < n / 2; i++)
        cout << arr[i] << " ";   

    // printing second half in descending
    // order
    for (int j = n - 1; j >= n / 2; j--)
        cout << arr[j] << " ";    
}

// driver code
int main()
{
    int arr[] = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printOrder(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print first half in
// ascending order and the second half
// in descending order
import java.util.*;

class GFG
{
// function to print half of the array in
// ascending order and the other half in
// descending order
static void printOrder(int[] arr, int n)
{
    // sorting the array
    Arrays.sort(arr);

    // printing first half in ascending
    // order
    for (int i = 0; i < n / 2; i++)
        System.out.print(arr[i]+" ");

    // printing second half in descending
    // order
    for (int j = n - 1; j >= n / 2; j--)
    System.out.print(arr[j]+" ");

}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
    int n = arr.length;
    printOrder(arr, n);

}
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 计算机编程语言

```
# Python program to print first half in
# ascending order and the second half
# in descending order

# function to print half of the array in
# ascending order and the other half in
# descending order
def printOrder(arr,n) :

    # sorting the array
    arr.sort()

    # printing first half in ascending
    # order
    i = 0
    while (i< n/ 2 ) :
        print arr[i],
        i = i + 1

    # printing second half in descending
    # order
    j = n - 1
    while j >= n / 2 :
        print arr[j],
        j = j - 1

# Driver code
arr = [5, 4, 6, 2, 1, 3, 8, 9, 7]
n = len(arr)
printOrder(arr, n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to print first half in
// ascending order and the second half
// in descending order
using System;

class GFG {

    // function to print half of the array in
    // ascending order and the other half in
    // descending order
    static void printOrder(int[] arr, int n)
    {

        // sorting the array
        Array.Sort(arr);

        // printing first half in ascending
        // order
        for (int i = 0; i < n / 2; i++)
            Console.Write(arr[i] + " ");

        // printing second half in descending
        // order
        for (int j = n - 1; j >= n / 2; j--)
            Console.Write(arr[j] + " ");
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 5, 4, 6, 2, 1, 3, 8, 9, 7 };
        int n = arr.Length;

        printOrder(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print first half in
// ascending order and the second half
// in descending order

// function to print half of the array in
// ascending order and the other half in
// descending order
function printOrder($arr, $n)
{

    // sorting the array
    sort($arr);

    // printing first half
    // in ascending order
    for ($i = 0; $i < intval($n / 2); $i++)
        echo $arr[$i] . " ";

    // printing second half
    // in descending order
    for ($j = $n - 1; $j >= intval($n / 2); $j--)
        echo $arr[$j] . " ";    
}

    // Driver Code
    $arr = array(5, 4, 6, 2, 1,
                    3, 8, 9, 7);
    $n = count($arr);
    printOrder($arr, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// javascript program to print first half in
// ascending order and the second half
// in descending order

    // function to print half of the array in
    // ascending order and the other half in
    // descending order
    function printOrder(arr , n)
    {
        // sorting the array
        arr.sort();

        // printing first half in ascending
        // order
        for (i = 0; i < parseInt(n / 2); i++)
            document.write(arr[i] + " ");

        // printing second half in descending
        // order
        for (j = n - 1; j >= parseInt(n / 2); j--)
            document.write(arr[j] + " ");

    }

    // Driver code

        var arr = [ 5, 4, 6, 2, 1, 3, 8, 9, 7 ];
        var n = arr.length;
        printOrder(arr, n);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
1 2 3 4 9 8 7 6 5
```