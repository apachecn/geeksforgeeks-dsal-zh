# 用 O(1)个额外空间交替排列正&负项目|设置 2

> 原文:[https://www . geesforgeks . org/rearray-array-in-alternating-正-负-items-with-O1-extra-space-set-2/](https://www.geeksforgeeks.org/rearrange-array-in-alternating-positive-negative-items-with-o1-extra-space-set-2/)

给定一组正数和负数，以交替的方式排列它们，使得每个正数后面跟着负数，反之亦然。输出中元素的顺序无关紧要。额外的正或负元素应该移动到末尾。

**示例:**

```
Input :
arr[] = {-2, 3, 4, -1}
Output :
arr[] = {-2, 3, -1, 4} OR {-1, 3, -2, 4} OR ..

Input :
arr[] = {-2, 3, 1}
Output :
arr[] = {-2, 3, 1} OR {-2, 1, 3} 

Input : 
arr[] = {-5, 3, 4, 5, -6, -2, 8, 9, -1, -4}
Output :
arr[] = {-5, 3, -2, 5, -6, 4, -4, 9, -1, 8} 
        OR ..
```

**方法 1:**

1.  首先，按非递增顺序对数组进行排序。然后我们将计算正整数和负整数的数量。
2.  然后在奇数位置交换一个负数和一个正数，直到我们达到我们的条件。
3.  这将重新排列数组元素，因为我们正在对数组进行排序，并根据需要从左到右访问元素。

下面是上述方法的实现:

## C++

```
// Below is the implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function which works in the condition
// when number of negative numbers are
// lesser or equal than positive numbers
void fill1(int a[], int neg, int pos)
{
    if (neg % 2 == 1)
    {
        for(int i = 1; i < neg; i += 2)
        {
            int c = a[i];
            int d = a[i + neg];
            int temp = c;
            a[i] = d;
            a[i + neg] = temp;
        }
    }
    else
    {
        for(int i = 1; i <= neg; i += 2)
        {
            int c = a[i];
            int d = a[i + neg - 1];
            int temp = c;
            a[i] = d;
            a[i + neg - 1] = temp;
        }
    }
}

// Function which works in the condition
// when number of negative numbers are
// greater than positive numbers
void fill2(int a[], int neg, int pos)
{
    if (pos % 2 == 1)
    {
        for(int i = 1; i < pos; i += 2)
        {
            int c = a[i];
            int d = a[i + pos];
            int temp = c;
            a[i] = d;
            a[i + pos] = temp;
        }
    }
    else
    {
        for(int i = 1; i <= pos; i += 2)
        {
            int c = a[i];
            int d = a[i + pos - 1];
            int temp = c;
            a[i] = d;
            a[i + pos - 1] = temp;
        }
    }
}

// Reverse the array
void reverse(int a[], int n)
{
    int i, k, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Print the array
void print(int a[], int n)
{
    for(int i = 0; i < n; i++)
        cout << a[i] << " ";

    cout << endl;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, -4, -1, 6, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Given array is ";
    print(arr, n);

    int neg = 0, pos = 0;
    for(int i = 0; i < n; i++)
    {
        if (arr[i] < 0)
            neg++;
        else
            pos++;
    }

    // Sort the array
    sort(arr, arr + n);

    if (neg <= pos)
    {
        fill1(arr, neg, pos);
    }
    else
    {

        // Reverse the array in this condition
        reverse(arr, n);
        fill2(arr, neg, pos);
    }
    cout << "Rearranged array is  ";
    print(arr, n);
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Below is the implementation of the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
public class Main {

    // function which works in the condition when number of
    // negative numbers are lesser or equal than positive
    // numbers
    static void fill1(int a[], int neg, int pos)
    {
        if (neg % 2 == 1) {
            for (int i = 1; i < neg; i += 2) {
                int c = a[i];
                int d = a[i + neg];
                int temp = c;
                a[i] = d;
                a[i + neg] = temp;
            }
        }
        else {
            for (int i = 1; i <= neg; i += 2) {
                int c = a[i];
                int d = a[i + neg - 1];
                int temp = c;
                a[i] = d;
                a[i + neg - 1] = temp;
            }
        }
    }

    // Function which works in the condition when number of
    // negative numbers are greater than positive numbers
    static void fill2(int a[], int neg, int pos)
    {
        if (pos % 2 == 1) {
            for (int i = 1; i < pos; i += 2) {
                int c = a[i];
                int d = a[i + pos];
                int temp = c;
                a[i] = d;
                a[i + pos] = temp;
            }
        }
        else {
            for (int i = 1; i <= pos; i += 2) {
                int c = a[i];
                int d = a[i + pos - 1];
                int temp = c;
                a[i] = d;
                a[i + pos - 1] = temp;
            }
        }
    }

    // Reverse the array
    static void reverse(int a[], int n)
    {
        int i, k, t;
        for (i = 0; i < n / 2; i++) {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Print the array
    static void print(int a[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
        System.out.println();
    }

    // Driver Code
    public static void main(String[] args)
        throws java.lang.Exception
    {
        // Given array
        int[] arr = { 2, 3, -4, -1, 6, -9 };
        int n = arr.length;
        System.out.println("Given array is  ");
        print(arr, n);
        int neg = 0, pos = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] < 0)
                neg++;
            else
                pos++;
        }
        // Sort the array
        Arrays.sort(arr);

        if (neg <= pos) {
            fill1(arr, neg, pos);
        }
        else {
            // reverse the array in this condition
            reverse(arr, n);
            fill2(arr, neg, pos);
        }
        System.out.println("Rearranged array is  ");
        print(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function which works in the condition
# when number of negative numbers are
# lesser or equal than positive numbers
def fill1(a, neg, pos) :

    if (neg % 2 == 1)  :
        for i in range(1, neg, 2):
            c = a[i]
            d = a[i + neg]
            temp = c
            a[i] = d
            a[i + neg] = temp

    else   :
         for i in range(1, neg+1, 2):
            c = a[i]
            d = a[i + neg - 1]
            temp = c
            a[i] = d
            a[i + neg - 1] = temp

# Function which works in the condition
# when number of negative numbers are
# greater than positive numbers
def fill2(a, neg, pos):
    if (pos % 2 == 1) :
         for i in range(1, pos, 2):
            c = a[i]
            d = a[i + pos]
            temp = c
            a[i] = d
            a[i + pos] = temp

    else  :
        for i in range(1, pos+1, 2):
            c = a[i]
            d = a[i + pos - 1]
            temp = c
            a[i] = d
            a[i + pos - 1] = temp

# Reverse the array
def reverse(a, n) :

    for i in range(n / 2):
        t = a[i]
        a[i] = a[n - i - 1]
        a[n - i - 1] = t

# Prthe array
def printt(a, n):
    for i in range(n):
        print(a[i], end = " ")

    print()

# Driver code
if __name__ == "__main__":

    arr = [ 2, 3, -4, -1, 6, -9 ]
    n = len(arr)
    print("Given array is ")
    printt(arr, n)

    neg = 0
    pos = 0
    for i in range(0, n):
        if (arr[i] < 0):
            neg += 1
        else:
            pos += 1

    # Sort the array
    arr.sort()

    if (neg <= pos) :
        fill1(arr, neg, pos)

    else  :

        # Reverse the array in this condition
        reverse(arr, n)
        fill2(arr, neg, pos)

    print("Rearranged array is  ")
    printt(arr, n)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG {

    // function which works in the condition when number of
    // negative numbers are lesser or equal than positive
    // numbers
    static void fill1(int[] a, int neg, int pos)
    {
        if (neg % 2 == 1) {
            for (int i = 1; i < neg; i += 2) {
                int c = a[i];
                int d = a[i + neg];
                int temp = c;
                a[i] = d;
                a[i + neg] = temp;
            }
        }
        else {
            for (int i = 1; i <= neg; i += 2) {
                int c = a[i];
                int d = a[i + neg - 1];
                int temp = c;
                a[i] = d;
                a[i + neg - 1] = temp;
            }
        }
    }

    // Function which works in the condition when number of
    // negative numbers are greater than positive numbers
    static void fill2(int[] a, int neg, int pos)
    {
        if (pos % 2 == 1) {
            for (int i = 1; i < pos; i += 2) {
                int c = a[i];
                int d = a[i + pos];
                int temp = c;
                a[i] = d;
                a[i + pos] = temp;
            }
        }
        else {
            for (int i = 1; i <= pos; i += 2) {
                int c = a[i];
                int d = a[i + pos - 1];
                int temp = c;
                a[i] = d;
                a[i + pos - 1] = temp;
            }
        }
    }

    // Reverse the array
    static void reverse(int[] a, int n)
    {
        int i, k, t;
        for (i = 0; i < n / 2; i++) {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Print the array
    static void print(int[] a, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(a[i] + " ");
        Console.WriteLine();
    }

// Driver Code
public static void Main (string[] args) {

     // Given array
        int[] arr = { 2, 3, -4, -1, 6, -9 };
        int n = arr.Length;
        Console.WriteLine("Given array is  ");
        print(arr, n);
        int neg = 0, pos = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] < 0)
                neg++;
            else
                pos++;
        }

        // Sort the array
        Array.Sort(arr);

        if (neg <= pos) {
            fill1(arr, neg, pos);
        }
        else {
            // reverse the array in this condition
            reverse(arr, n);
            fill2(arr, neg, pos);
        }
        Console.WriteLine("Rearranged array is  ");
        print(arr, n);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Below is the implementation of the above approach

// Function which works in the condition
// when number of negative numbers are
// lesser or equal than positive numbers
function fill1(a, neg, pos)
{
    if (neg % 2 == 1)
    {
        for (let i = 1; i < neg; i += 2)
        {
            let c = a[i];
            let d = a[i + neg];
            let temp = c;
            a[i] = d;
            a[i + neg] = temp;
        }
    }
    else
    {
        for(let i = 1; i <= neg; i += 2)
        {
            let c = a[i];
            let d = a[i + neg - 1];
            let temp = c;
            a[i] = d;
            a[i + neg - 1] = temp;
        }
    }
}

// Function which works in the condition
// when number of negative numbers are
// greater than positive numbers
function fill2(a, neg, pos)
{
    if (pos % 2 == 1)
    {
        for (let i = 1; i < pos; i += 2)
        {
            let c = a[i];
            let d = a[i + pos];
            let temp = c;
            a[i] = d;
            a[i + pos] = temp;
        }
    }
    else
    {
        for(let i = 1; i <= pos; i += 2)
        {
            let c = a[i];
            let d = a[i + pos - 1];
            let temp = c;
            a[i] = d;
            a[i + pos - 1] = temp;
        }
    }
}

// Reverse the array
function reverse(a, n)
{
    let i, k, t;
    for(i = 0; i < parseInt(n / 2); i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Print the array
function print(a, n)
{
    for(let i = 0; i < n; i++)
        document.write(a[i] + " ");

    document.write('<br>');
}

// Driver code
var arr = [ 2, 3, -4, -1, 6, -9 ];
let n = arr.length;
document.write("Given array is ");
print(arr, n);
let neg = 0, pos = 0;

for(let i = 0; i < n; i++)
{
    if (arr[i] < 0)
        neg++;
    else
        pos++;
}

// Sort the array
arr.sort(function (a, b){return a - b;});

if (neg <= pos)
{
    fill1(arr, neg, pos);
}
else
{

    // Reverse the array in this condition
    reverse(arr, n);
    fill2(arr, neg, pos);
}
document.write("Rearranged array is  ");
print(arr, n);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
Given array is  
2 3 -4 -1 6 -9 
Rearranged array is  
-9 3 -1 2 -4 6
```

**时间复杂度:** O(N*logN)

**空间复杂度:** O(1)

**高效方法:**
我们已经讨论了一个 O(n <sup>2</sup> )解决方案，它保持了数组中的出现顺序[这里](https://www.geeksforgeeks.org/rearrange-array-alternating-positive-negative-items-o1-extra-space/)。如果允许我们改变出现的顺序，我们可以在 O(n)时间和 O(1)空间中解决这个问题。
思路是对数组进行处理，在 O(n)时间内将所有负值移至末尾。在所有负值都移动到最后后，我们可以很容易地在交替的正&负项中重新排列数组。在这个步骤中，我们基本上从下一个负元素交换偶数位置的下一个正元素。

以下是上述想法的实现。

## C++

```
// C++ program to rearrange
// array in alternating
// positive & negative items
// with O(1) extra space
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange positive and negative
// integers in alternate fashion. The below
// solution doesn't maintain original order of
// elements
void rearrange(int arr[], int n)
{
    int i = 0, j = n-1;

    // shift all negative values to the end
    while (i < j) {
        while (i <= n - 1 and arr[i] > 0)
            i += 1;
        while (j >= 0 and arr[j] < 0)
            j -= 1;
        if (i < j )
            swap(arr[i], arr[j]);
    }

    // i has index of leftmost
    // negative element
    if (i == 0 || i == n)
        return;

    // start with first positive
    // element at index 0

    // Rearrange array in alternating
    // positive &
    // negative items
    int k = 0;
    while (k < n && i < n ) {
        // swap next positive
        // element at even position
        // from next negative element.
        swap(arr[k], arr[i]);
        i = i + 1;
        k = k + 2;
    }
}

// Utility function to print an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, -4, -1, 6, -9 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Given array is \n";
    printArray(arr, n);

    rearrange(arr, n);

    cout << "Rearranged array is \n";
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange
// array in alternating
// positive & negative
// items with O(1) extra space
class GFG {

    // Function to rearrange positive and negative
    // integers in alternate fashion. The below
    // solution doesn't maintain original order of
    // elements
    static void rearrange(int arr[], int n)
    {
        int i = 0, j = n - 1;

        // shift all negative values to the end
        while (i < j) {
            while (i <= n - 1 && arr[i] > 0)
                i += 1;
            while (j >= 0 && arr[j] < 0)
                j -= 1;
            if (i < j)
                swap(arr, i, j);
        }

        // i has index of leftmost negative element
        if (i == 0 || i == n)
            return;

        // start with first positive
        // element at index 0

        // Rearrange array in alternating positive &
        // negative items
        int k = 0;
        while (k < n && i < n) {
            // swap next positive element
            // at even position
            // from next negative element.
            swap(arr, k, i);
            i = i + 1;
            k = k + 2;
        }
    }

    // Utility function to print an array
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
        System.out.println("");
    }

    static void swap(int arr[], int index1, int index2)
    {
        int c = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = c;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, -4, -1, 6, -9 };

        int n = arr.length;

        System.out.println("Given array is ");
        printArray(arr, n);

        rearrange(arr, n);

        System.out.println("Rearranged array is ");
        printArray(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to rearrange array
# in alternating positive & negative
# items with O(1) extra space

# Function to rearrange positive and
# negative integers in alternate fashion.
# The below solution does not maintain
# original order of elements

def rearrange(arr, n):
    i = 0
    j = n - 1

    # shift all negative values
    # to the end
    while (i < j):

        while (i <= n - 1 and arr[i] > 0):
            i += 1
        while (j >= 0 and arr[j] < 0):
            j -= 1

        if (i < j):
            temp = arr[i]
            arr[i] = arr[j]
            arr[j] = temp

    # i has index of leftmost
    # negative element
    if (i == 0 or i == n):
        return 0

    # start with first positive element
    # at index 0

    # Rearrange array in alternating
    # positive & negative items
    k = 0
    while (k < n and i < n):

        # swap next positive element at even
        # position from next negative element.
        temp = arr[k]
        arr[k] = arr[i]
        arr[i] = temp
        i = i + 1
        k = k + 2

# Utility function to print an array

def printArray(arr, n):
    for i in range(n):
        print(arr[i], end=" ")
    print("\n")

# Driver code
arr = [2, 3]

n = len(arr)

print("Given array is")
printArray(arr, n)

rearrange(arr, n)

print("Rearranged array is")
printArray(arr, n)

# This code is contributed
# Princi Singh
```

## C#

```
// C# program to rearrange array
// in alternating positive & negative
// items with O(1) extra space
using System;

class GFG {

    // Function to rearrange positive and
    // negative integers in alternate fashion.
    // The below solution doesn't maintain
    // original order of elements
    static void rearrange(int[] arr, int n)
    {
        int i = 0, j = n - 1;

        // shift all negative values
        // to the end
        while (i < j) {
            while (i <= n - 1 && arr[i] > 0)
                i += 1;
            while (j >= 0 && arr[j] < 0)
                j -= 1;
            if (i < j)
                swap(arr, i, j);
        }

        // i has index of leftmost
        // negative element
        if (i == 0 || i == n)
            return;

        // start with first positive
        // element at index 0

        // Rearrange array in alternating
        // positive & negative items
        int k = 0;
        while (k < n && i < n) {
            // swap next positive element
            // at even position from next
            // negative element.
            swap(arr, k, i);
            i = i + 1;
            k = k + 2;
        }
    }

    // Utility function to print an array
    static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine("");
    }

    static void swap(int[] arr, int index1, int index2)
    {
        int c = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = c;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 3, -4, -1, 6, -9 };

        int n = arr.Length;

        Console.WriteLine("Given array is ");
        printArray(arr, n);

        rearrange(arr, n);

        Console.WriteLine("Rearranged array is ");
        printArray(arr, n);
    }
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to rearrange array
// in alternating positive & negative
// items with O(1) extra space

// Function to rearrange positive and
// negative integers in alternate fashion.
// The below solution doesn't maintain
// original order of elements
function rearrange(&$arr, $n)
{
    $i = 0;
    $j = $n - 1;

    // shift all negative values
    // to the end
    while ($i < $j)
    {

        while($i <= $n - 1 and $arr[$i] > 0)
            ++$i;
        while ($j >= 0 and $arr[$j] < 0)
            --$j;

        if ($i < $j)
        {
            $temp = $arr[$i];
            $arr[$i] = $arr[$j];
            $arr[$j] = $temp;
        }        
    }

    // i has index of leftmost
    // negative element
    if ($i == 0 || $i == $n)
        return;

    // start with first positive element
    // at index 0

    // Rearrange array in alternating
    // positive & negative items
    $k = 0;
    while ($k < $n && $i < $n)
    {
        // swap next positive element at even
        // position from next negative element.
        $temp = $arr[$k];
        $arr[$k] = $arr[$i];
        $arr[$i] = $temp;
        $i = $i + 1;
        $k = $k + 2;
    }
}

// Utility function to print an array
function printArray(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    echo $arr[$i] . " ";
    echo "\n";
}

// Driver code
$arr = array(2, 3, -4, -1, 6, -9);

$n = sizeof($arr);

echo "Given array is \n";
printArray($arr, $n);

rearrange($arr, $n);

echo "Rearranged array is \n";
printArray($arr, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to rearrange
// array in alternating
// positive & negative
// items with O(1) extra space

// Function to rearrange positive and negative
// integers in alternate fashion. The below
// solution doesn't maintain original order of
// elements
function rearrange(arr,n)
{
    let i = 0, j = n - 1;

    // Shift all negative values to the end
    while (i < j)
    {
        while(i <= n - 1 && arr[i] > 0)
            i += 1;
        while (j >= 0 && arr[j] < 0)
            j -= 1;

        if (i < j)
            swap(arr, i,j);
    }

    // i has index of leftmost negative element
    if (i == 0 || i == n)
        return;

    // Start with first positive
    // element at index 0

    // Rearrange array in alternating
    // positive & negative items
    let k = 0;
    while (k < n && i < n)
    {

        // Swap next positive element
        // at even position
        // from next negative element.
        swap(arr, k, i);
        i = i + 1;
        k = k + 2;
    }
}

// Utility function to print an array
function printArray(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");

    document.write("<br>");
}

function swap(arr, index1, index2)
{
    let c = arr[index1];
    arr[index1] = arr[index2];
    arr[index2] = c;
}

// Driver code
let arr = [ 2, 3, -4, -1, 6, -9 ];
let n = arr.length;

document.write("Given array is <br>");

printArray(arr, n);
rearrange(arr, n);

document.write("Rearranged array is <br>");
printArray(arr, n);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Given array is 
2 3 -4 -1 6 -9 
Rearranged array is 
-1 3 -4 2 -9 6
```

**时间复杂度:** O(N)

**空间复杂度:** O(1)

本文由**阿迪蒂亚·戈尔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。