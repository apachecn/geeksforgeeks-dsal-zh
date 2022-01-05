# 对一个数组进行排序，其中排序后的数组的子数组的顺序相反

> 原文:[https://www . geeksforgeeks . org/sort-a-a-array-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-](https://www.geeksforgeeks.org/sort-an-array-where-a-subarray-of-a-sorted-array-is-in-reverse-order/)

给定一个由 N 个数字组成的数组，其中一个子数组按降序排序，数组中的其余数字按升序排序。任务是对一个数组进行排序，排序后的数组的子数组的顺序是相反的。

**示例:**

> **输入:** 2 5 65 55 50 70 90
> **输出:** 2 5 50 55 65 70 90
> 从第 2 个索引到第 4 个索引的子阵列顺序相反。
> 于是子阵列反转，打印排序后的数组。
> 
> **输入:**1 7 6 5 4 3 2 8
> T3】输出: 1 2 3 4 5 6 7 8

一个**天真的做法**将是[排序数组](https://www.geeksforgeeks.org/sorting-algorithms/)并打印数组。**该方法的时间复杂度**将为 0(N log N)。
一种**有效的方法**将是找到并存储反向子阵列的开始索引和结束索引。由于子阵列按降序排列，其余元素按升序排列，因此只有反转子阵列才能对整个阵列进行排序。使用[两个指针接近](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)反转子阵列。

下面是上述方法的实现:

## C++

```
// C++ program to sort an array where
// a subarray of a sorted array
// is in reversed order
#include <bits/stdc++.h>
using namespace std;

// Function to print the sorted array
// by reversing the subarray
void printSorted(int a[], int n)
{
    int front = -1, back = -1;

    // find the starting index of the
    // reversed subarray
    for (int i = 1; i < n; i++) {
        if (a[i] < a[i - 1]) {
            front = i - 1;
            break;
        }
    }

    // find the ending index of the
    // reversed subarray
    for (int i = n - 2; i >= 0; i--) {
        if (a[i] > a[i + 1]) {
            back = i + 1;
            break;
        }
    }

    // if no reversed subarray is present
    if (front == -1 and back == -1) {
        for (int i = 0; i < n; i++)
            cout << a[i] << " ";
        return;
    }

    // swap the reversed subarray
    while (front <= back) {

        // swaps the front and back element
        // using c++ STL
        swap(a[front], a[back]);

        // move the pointers one step
        // ahead and one step back
        front++;
        back--;
    }
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
}

// Driver Code
int main()
{
    int a[] = { 1, 7, 6, 5, 4, 3, 2, 8 };
    int n = sizeof(a) / sizeof(a[0]);
    printSorted(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array where
// a subarray of a sorted array
// is in reversed order
import java.io.*;

class GFG
{

// Function to print the sorted array
// by reversing the subarray
static void printSorted(int a[], int n)
{
    int front = -1, back = -1;

    // find the starting index of the
    // reversed subarray
    for (int i = 1; i < n; i++)
    {
        if (a[i] < a[i - 1])
        {
            front = i - 1;
            break;
        }
    }

    // find the ending index of the
    // reversed subarray
    for (int i = n - 2; i >= 0; i--)
    {
        if (a[i] > a[i + 1])
        {
            back = i + 1;
            break;
        }
    }

    // if no reversed subarray is present
    if (front == -1 && back == -1)
    {
        for (int i = 0; i < n; i++)
            System.out.println(a[i] + " ");
        return;
    }

    // swap the reversed subarray
    while (front <= back)
    {

        // swaps the front and back element
        // using c++ STL
        int temp = a[front];
        a[front] = a[back];
        a[back] = temp;

        // move the pointers one step
        // ahead and one step back
        front++;
        back--;
    }
    for (int i = 0; i < n; i++)
        System.out.print(a[i] + " ");
}

// Driver Code
public static void main (String[] args)
{
    int a[] = { 1, 7, 6, 5, 4, 3, 2, 8 };
    int n = a.length;
    printSorted(a, n);;
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to sort an array where
# a subarray of a sorted array is in
# reversed order

# Function to print the sorted array
# by reversing the subarray
def printSorted(a, n):
    front = -1
    back = -1

    # find the starting index of the
    # reversed subarray
    for i in range(1, n, 1):
        if (a[i] < a[i - 1]):
            front = i - 1
            break

    # find the ending index of the
    # reversed subarray
    i = n - 2
    while(i >= 0):
        if (a[i] > a[i + 1]):
            back = i + 1
            break
        i -= 1

    # if no reversed subarray is present
    if (front == -1 and back == -1):
        for i in range(0, n, 1):
            print(a[i], end = " ")
        return

    # swap the reversed subarray
    while (front <= back):

        # swaps the front and back element
        # using c++ STL
        temp = a[front]
        a[front] = a[back]
        a[back] = temp

        # move the pointers one step
        # ahead and one step back
        front += 1
        back -= 1

    for i in range(0, n, 1):
        print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':
    a = [1, 7, 6, 5, 4, 3, 2, 8]
    n = len(a)
    printSorted(a, n)

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to sort an array where
// a subarray of a sorted array
// is in reversed order
using System;

class GFG
{

// Function to print the sorted array
// by reversing the subarray
static void printSorted(int []a, int n)
{
    int front = -1, back = -1;

    // find the starting index of the
    // reversed subarray
    for (int i = 1; i < n; i++)
    {
        if (a[i] < a[i - 1])
        {
            front = i - 1;
            break;
        }
    }

    // find the ending index of the
    // reversed subarray
    for (int i = n - 2; i >= 0; i--)
    {
        if (a[i] > a[i + 1])
        {
            back = i + 1;
            break;
        }
    }

    // if no reversed subarray is present
    if (front == -1 && back == -1)
    {
        for (int i = 0; i < n; i++)
        {
            Console.Write(a[i] + " ");
        }
        return;
    }

    // swap the reversed subarray
    while (front <= back)
    {

        // swaps the front and back element
        // using c++ STL
        swap(a, front, back);

        // move the pointers one step
        // ahead and one step back
        front++;
        back--;
    }
    for (int i = 0; i < n; i++)
    {
        Console.Write(a[i] + " ");
    }
}

static void swap(int[] a, int front,
                          int back)
{
    int c = a[front];
    a[front] = a[back];
    a[back] = c;
}

// Driver Code
public static void Main()
{
    int []a = {1, 7, 6, 5, 4, 3, 2, 8};
    int n = a.Length;
    printSorted(a, n);
}
}

// This code contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort an array where
// a subarray of a sorted array
// is in reversed order

// Function to print the sorted array
// by reversing the subarray
function printSorted($a, $n)
{
    $front = -1; $back = -1;

    // find the starting index of the
    // reversed subarray
    for ($i = 1; $i < $n; $i++)
    {
        if ($a[$i] < $a[$i - 1])
        {
            $front = $i - 1;
            break;
        }
    }

    // find the ending index of the
    // reversed subarray
    for ($i = $n - 2; $i >= 0; $i--)
    {
        if ($a[$i] > $a[$i + 1])
        {
            $back = $i + 1;
            break;
        }
    }

    // if no reversed subarray is present
    if ($front == -1 && $back == -1)
    {
        for ($i = 0; $i < $n; $i++)
            echo $a[$i] . " ";
        return;
    }

    // swap the reversed subarray
    while ($front <= $back)
    {

        // swaps the front and back element
        // using c++ STL
        $temp = $a[$front];
        $a[$front] = $a[$back];
        $a[$back] = $temp;

        // move the pointers one step
        // ahead and one step back
        $front++;
        $back--;
    }
    for ($i = 0; $i < $n; $i++)
        echo $a[$i] . " ";
}

// Driver Code
$a = array(1, 7, 6, 5, 4, 3, 2, 8);
$n = sizeof($a);
printSorted($a, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript program to sort an array where
// a subarray of a sorted array
// is in reversed order

    // Function to print the sorted array
    // by reversing the subarray
    function printSorted(a , n) {
        var front = -1, back = -1;

        // find the starting index of the
        // reversed subarray
        for (i = 1; i < n; i++) {
            if (a[i] < a[i - 1]) {
                front = i - 1;
                break;
            }
        }

        // find the ending index of the
        // reversed subarray
        for (i = n - 2; i >= 0; i--) {
            if (a[i] > a[i + 1]) {
                back = i + 1;
                break;
            }
        }

        // if no reversed subarray is present
        if (front == -1 && back == -1) {
            for (i = 0; i < n; i++)
                document.write(a[i] + " ");
            return;
        }

        // swap the reversed subarray
        while (front <= back) {

            // swaps the front and back element
            // using c++ STL
            var temp = a[front];
            a[front] = a[back];
            a[back] = temp;

            // move the pointers one step
            // ahead and one step back
            front++;
            back--;
        }
        for (i = 0; i < n; i++)
            document.write(a[i] + " ");
    }

    // Driver Code

        var a = [ 1, 7, 6, 5, 4, 3, 2, 8 ];
        var n = a.length;
        printSorted(a, n);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
1 2 3 4 5 6 7 8
```

**时间复杂度:** O(n)