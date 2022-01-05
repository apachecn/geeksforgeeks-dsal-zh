# 从数组中删除前导零

> 原文:[https://www . geesforgeks . org/从数组中移除前导零/](https://www.geeksforgeeks.org/remove-leading-zeros-from-an-array/)

给定一个由 N 个数字组成的数组，任务是从数组中移除所有前导零。
**例:**

```
Input : arr[] = {0, 0, 0, 1, 2, 3} 
Output : 1 2 3 

Input : arr[] = {0, 0, 0, 1, 0, 2, 3} 
Output : 1 0 2 3 
```

**方法:**标记给定数组中第一个非零数字的索引。将从该索引到末尾的数字存储在不同的数组中。一旦所有数字都存储在不同的容器中，就打印数组。
以下是上述办法的实施情况:

## C++

```
// C++ program to print the array
// removing the leading zeros
#include <bits/stdc++.h>
using namespace std;

// Function to print the array by
// removing leading zeros
void removeZeros(int a[], int n)
{

    // index to store the first
    // non-zero number
    int ind = -1;

    // traverse in the array and find the first
    // non-zero number
    for (int i = 0; i < n; i++) {
        if (a[i] != 0) {
            ind = i;
            break;
        }
    }

    // if no non-zero number is there
    if (ind == -1) {
        cout << "Array has leading zeros only";
        return;
    }

    // Create an array to store
    // numbers apart from leading zeros
    int b[n - ind];

    // store the numbers removing leading zeros
    for (int i = 0; i < n - ind; i++)
        b[i] = a[ind + i];

    // print the array
    for (int i = 0; i < n - ind; i++)
        cout << b[i] << " ";
}

// Driver Code
int main()
{
    int a[] = { 0, 0, 0, 1, 2, 0, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    removeZeros(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the array
// removing the leading zeros
import java.util.*;

class solution
{

// Function to print the array by
// removing leading zeros
static void removeZeros(int[] a, int n)
{

    // index to store the first
    // non-zero number
    int ind = -1;

    // traverse in the array and find the first
    // non-zero number
    for (int i = 0; i < n; i++) {
        if (a[i] != 0) {
            ind = i;
            break;
        }
    }

    // if no non-zero number is there
    if (ind == -1) {
        System.out.print("Array has leading zeros only");
        return;
    }

    // Create an array to store
    // numbers apart from leading zeros
    int[] b = new int[n - ind];

    // store the numbers removing leading zeros
    for (int i = 0; i < n - ind; i++)
        b[i] = a[ind + i];

    // print the array
    for (int i = 0; i < n - ind; i++)
        System.out.print(b[i]+" ");
}

// Driver Code
public static void main(String args[])
{
    int[] a = { 0, 0, 0, 1, 2, 0, 3 };
    int n = a.length;
    removeZeros(a, n);

}
}
```

## 蟒蛇 3

```
# Python3 program to print
# the array removing
# the leading zeros

# Function to print the
# array by removing
# leading zeros
def removeZeros(a, n):

    # index to store the
    # first non-zero number
    ind = -1;

    # traverse in the array
    # and find the first
    # non-zero number
    for i in range(n):
        if (a[i] != 0):
            ind = i;
            break;

    # if no non-zero
    # number is there
    if (ind == -1):
        print("Array has leading zeros only");
        return;

    # Create an array to store
    # numbers apart from leading
    # zeros b[n - ind];
    b=[0]*(n - ind);

    # store the numbers
    # removing leading zeros
    for i in range(n - ind):
        b[i] = a[ind + i];

    # print the array
    for i in range(n - ind):
        print( b[i] , end=" ");

# Driver Code
a = [0, 0, 0, 1, 2, 0, 3];
n = len(a);
removeZeros(a, n);

# This code is contributed by mits
```

## C#

```
// C# program to print the array
// removing the leading zeros
using System;

class solution
{

// Function to print the array by
// removing leading zeros
static void removeZeros(int[] a, int n)
{

    // index to store the first
    // non-zero number
    int ind = -1;

    // traverse in the array and find the first
    // non-zero number
    for (int i = 0; i < n; i++)
    {
        if (a[i] != 0)
        {
            ind = i;
            break;
        }
    }

    // if no non-zero number is there
    if (ind == -1)
    {
        Console.Write("Array has leading zeros only");
        return;
    }

    // Create an array to store
    // numbers apart from leading zeros
    int[] b = new int[n - ind];

    // store the numbers removing leading zeros
    for (int i = 0; i < n - ind; i++)
        b[i] = a[ind + i];

    // print the array
    for (int i = 0; i < n - ind; i++)
        Console.Write(b[i]+" ");
}

// Driver Code
public static void Main(String []args)
{
    int[] a = { 0, 0, 0, 1, 2, 0, 3 };
    int n = a.Length;
    removeZeros(a, n);
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the array removing
// the leading zeros

// Function to print the
// array by removing
// leading zeros
function removeZeros($a, $n)
{

    // index to store the
    // first non-zero number
    $ind = -1;

    // traverse in the array
    // and find the first
    // non-zero number
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] != 0)
        {
            $ind = $i;
            break;
        }
    }

    // if no non-zero
    // number is there
    if ($ind == -1)
    {
        echo "Array has leading " .
                      "zeros only";
        return;
    }

    // Create an array to store
    // numbers apart from leading
    // zeros b[n - ind];

    // store the numbers
    // removing leading zeros
    for ($i = 0; $i < $n - $ind; $i++)
        $b[$i] = $a[$ind + $i];

    // print the array
    for ($i = 0; $i < $n - $ind; $i++)
        echo $b[$i] , " ";
}

// Driver Code
$a = array(0, 0, 0, 1, 2, 0, 3);
$n = sizeof($a);
removeZeros($a, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to print the array
// removing the leading zeros

    // Function to print the array by
    // removing leading zeros
    function removeZeros(a , n) {

        // index to store the first
        // non-zero number
        var ind = -1;

        // traverse in the array and
        // find the first
        // non-zero number
        for (i = 0; i < n; i++) {
            if (a[i] != 0) {
                ind = i;
                break;
            }
        }

        // if no non-zero number is there
        if (ind == -1) {
            document.write("Array has leading zeros only");
            return;
        }

        // Create an array to store
        // numbers apart from leading zeros
        var b = Array(n - ind).fill(0);

        // store the numbers removing leading zeros
        for (i = 0; i < n - ind; i++)
            b[i] = a[ind + i];

        // print the array
        for (i = 0; i < n - ind; i++)
            document.write(b[i] + " ");
    }

    // Driver Code

        var a = [ 0, 0, 0, 1, 2, 0, 3 ];
        var n = a.length;
        removeZeros(a, n);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
1 2 0 3
```