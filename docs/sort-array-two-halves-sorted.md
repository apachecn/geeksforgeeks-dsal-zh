# 当一个数组的两半被排序时排序

> 原文:[https://www.geeksforgeeks.org/sort-array-two-halves-sorted/](https://www.geeksforgeeks.org/sort-array-two-halves-sorted/)

给定一个整数数组，该数组的前半部分和后半部分都被排序。任务是将数组的两个排序部分合并成一个排序数组。

**示例:**

```
Input : A[] = { 2, 3, 8, -1, 7, 10 }
Output : -1, 2, 3, 7, 8, 10 

Input : A[] = {-4, 6, 9, -1, 3 }
Output : -4, -1, 3, 6, 9
```

**方法 1:** 一个**简单的解决方案**是使用内置函数对数组进行排序(一般是快速排序的一种实现)。
以下是上述方法的实施:

## C++

```
// C++ program to Merge two sorted halves of
// array Into Single Sorted Array
#include <bits/stdc++.h>
using namespace std;

void mergeTwoHalf(int A[], int n)
{
    // Sort the given array using sort STL
    sort(A, A + n);
}

// Driver code
int main()
{
    int A[] = { 2, 3, 8, -1, 7, 10 };
    int n = sizeof(A) / sizeof(A[0]);
    mergeTwoHalf(A, n);

    // Print sorted Array
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Merge two sorted halves of
// array Into Single Sorted Array
import java.io.*;
import java.util.*;

class GFG {

    static void mergeTwoHalf(int[] A, int n)
    {
        // Sort the given array using sort STL
        Arrays.sort(A);
    }

    // Driver code
    static public void main(String[] args)
    {
        int[] A = { 2, 3, 8, -1, 7, 10 };
        int n = A.length;
        mergeTwoHalf(A, n);

        // Print sorted Array
        for (int i = 0; i < n; i++)
            System.out.print(A[i] + " ");
    }
}

// This code is contributed by vt_m .
```

## 计算机编程语言

```
# Python program to Merge two sorted
# halves of array Into Single Sorted Array

def mergeTwoHalf(A, n):

    # Sort the given array using sort STL
    A.sort()

# Driver Code
if __name__ == '__main__':
    A = [2, 3, 8, -1, 7, 10]
    n = len(A)
    mergeTwoHalf(A, n)

    # Print sorted Array
    for i in range(n):
        print(A[i], end=" ")

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to Merge two sorted halves of
// array Into Single Sorted Array
using System;

class GFG {

    static void mergeTwoHalf(int[] A, int n)
    {
        // Sort the given array using sort STL
        Array.Sort(A);
    }

    // Driver code
    static public void Main()
    {
        int[] A = { 2, 3, 8, -1, 7, 10 };
        int n = A.Length;
        mergeTwoHalf(A, n);

        // Print sorted Array
        for (int i = 0; i < n; i++)
            Console.Write(A[i] + " ");
    }
}

// This code is contributed by vt_m .
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Merge two sorted halves
// of array Into Single Sorted Array

function mergeTwoHalf(&$A, $n)
{
    // Sort the given array using sort STL
    sort($A, 0);
}

// Driver Code
$A = array(2, 3, 8, -1, 7, 10);
$n = sizeof($A);
mergeTwoHalf($A, $n);

// Print sorted Array
for ($i = 0; $i < $n; $i++)
    echo $A[$i] . " ";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to Merge two sorted halves of
// array Into Single Sorted Array

function mergeTwoHalf(A, n)
{
    // Sort the given array using sort function
    A.sort((a,b) => a-b);
}

// Driver code
var A = [ 2, 3, 8, -1, 7, 10 ];
var n = A.length;
mergeTwoHalf(A, n);

// Print sorted Array
for (var i = 0; i < n; i++)
    document.write( A[i] + " ");

// This code is contributed by itsok.
</script>
```

**Output**

```
-1 2 3 7 8 10
```