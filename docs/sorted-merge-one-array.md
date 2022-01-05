# 排序合并在一个数组中

> 原文:[https://www.geeksforgeeks.org/sorted-merge-one-array/](https://www.geeksforgeeks.org/sorted-merge-one-array/)

给定两个排序的数组 A 和 B，其中 A 在末尾有足够大的缓冲区来保存 B。
按排序顺序将 B 合并到 A 中。
**例:**

```
Input : a[] = {10, 12, 13, 14, 18, NA, NA, NA, NA, NA}   
        b[] = {16, 17, 19, 20, 22};;
Output : a[] = {10, 12, 13, 14, 16, 17, 18, 19, 20, 22}
```

一种方法是通过将较小的元素插入到 A 的前面来合并两个数组，但是这种方法的问题是我们必须在每次插入后将每个元素向右移动。
因此，我们可以通过比较哪个元素更小来比较哪个元素更大，然后将该元素插入到 a 的末尾。
下面是上述方法的解决方案。

## C++

```
// Merging b[] into a[]
#include <bits/stdc++.h>
using namespace std;
#define NA -1

void sortedMerge(int a[], int b[], int n, int m) {
  int i = n - 1;
  int j = m - 1;

  int lastIndex = n + m - 1;

  /* Merge a and b, starting from last element
     in each */
  while (j >= 0) {

    /* End of a is greater than end of b */
    if (i >= 0 && a[i] > b[j]) {
      a[lastIndex] = a[i]; // Copy Element
      i--;
    } else {
      a[lastIndex] = b[j]; // Copy Element
      j--;
    }
    lastIndex--; // Move indices
  }
}

/* Helper function to print the array */
void printArray(int *arr, int n) {
  cout << "Array A after merging B in sorted"
        " order : " << endl;
  for (int i = 0; i < n; i++)
    cout << arr[i] << " ";
}

int main() {
  int a[] = {10, 12, 13, 14, 18, NA, NA, NA, NA, NA};
  int n = 5;
  int size_a = 10;
  int b[] = {16, 17, 19, 20, 22};
  int m = 5;
  sortedMerge(a, b, n, m);
  printArray(a, size_a);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to merge B
// into A in sorted order.
import java.io.*;

class GFG
{
    static int NA =-1;
    static void sortedMerge(int a[], int b[], int n, int m)
    {
        int i = n - 1;
        int j = m - 1;

        int lastIndex = n + m - 1;

        // Merge a and b, starting
        // from last element in each
        while (j >= 0)
        {

            /* End of a is greater than end of b */
            if (i >= 0 && a[i] > b[j])
            {
                // Copy Element
                a[lastIndex] = a[i];
                i--;
            } else
            { 
                // Copy Element
                a[lastIndex] = b[j];
                j--;
            }
            // Move indices
            lastIndex--;
        }
    }

    // Helper function to print the array
    static void printArray(int arr[], int n)
    {
        System.out.println ( "Array A after merging B in sorted order : " ) ;
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] +" ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = {10, 12, 13, 14, 18, NA, NA, NA, NA, NA};
        int n = 5;
        int size_a = 10;
        int b[] = {16, 17, 19, 20, 22};
        int m = 5;
        sortedMerge(a, b, n, m);
        printArray(a, size_a);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to merge B
# into A in sorted order.

NA = -1

# Merging b[] into a[]
def sortedMerge(a, b, n, m):

    i = n - 1
    j = m - 1

    lastIndex = n + m - 1

    # Merge a and b, starting from last
    # element in each
    while (j >= 0) :

        # End of a is greater than end
        # of b
        if (i >= 0 and a[i] > b[j]):

            # Copy Element
            a[lastIndex] = a[i]
            i -= 1
        else:

             # Copy Element
            a[lastIndex] = b[j]
            j -= 1

        # Move indices
        lastIndex-= 1

# Helper function to print
# the array
def printArray(arr, n):

    print("Array A after merging B in sorted order : ")

    for i in range(0, n):
        print(arr[i], end =" ")

size_a = 10

a = [10, 12, 13, 14, 18, NA, NA, NA, NA, NA]
n = 5

b = [16, 17, 19, 20, 22]
m = 5

sortedMerge(a, b, n, m)
printArray(a, size_a)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to merge B into A in
// sorted order.
using System;

class GFG {

    static int NA =-1;
    static void sortedMerge(int []a, int []b,
                                 int n, int m)
    {
        int i = n - 1;
        int j = m - 1;

        int lastIndex = n + m - 1;

        // Merge a and b, starting
        // from last element in each
        while (j >= 0)
        {

            /* End of a is greater than
            end of b */
            if (i >= 0 && a[i] > b[j])
            {

                // Copy Element
                a[lastIndex] = a[i];
                i--;
            }

            else
            {

                // Copy Element
                a[lastIndex] = b[j];
                j--;
            }

            // Move indices
            lastIndex--;
        }
    }

    // Helper function to print the array
    static void printArray(int []arr, int n)
    {

        Console.WriteLine ( "Array A after "
        + "merging B in sorted order : " ) ;

        for (int i = 0; i < n; i++)
            Console.Write(arr[i] +" ");
    }

    // Driver code
    public static void Main ()
    {
        int []a = {10, 12, 13, 14, 18, NA,
                           NA, NA, NA, NA};
        int n = 5;
        int size_a = 10;
        int []b = {16, 17, 19, 20, 22};
        int m = 5;

        sortedMerge(a, b, n, m);

        printArray(a, size_a);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to merge B into A in
// sorted order.

// Merging b[] into a[]
function sortedMerge($a, $b, $n, $m)
{
    $i = $n - 1;
    $j = $m - 1;

    $lastIndex = $n + $m - 1;

    /* Merge a and b, starting from
       last element in each */
    while ($j >= 0)
    {

        /* End of a is greater than end of b */
        if ($i >= 0 && $a[$i] > $b[$j])
        {
            $a[$lastIndex] = $a[$i]; // Copy Element
            $i--;
        }
        else
        {
            $a[$lastIndex] = $b[$j]; // Copy Element
            $j--;
        }
        $lastIndex--; // Move indices
    }
    return $a;
}

/* Helper function to print the array */
function printArray($arr, $n)
{
    echo "Array A after merging B in sorted";
        echo " order : \n";
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Driver Code
$a = array(10, 12, 13, 14, 18,
          -1, -1, -1, -1, -1);
$n = 5;
$size_a = 10;

$b = array(16, 17, 19, 20, 22);
$m = 5;
$c = sortedMerge($a, $b, $n, $m);
printArray($c, $size_a);

// This code is contributed by Rajput-Ji.
?>
```

## java 描述语言

```
<script>
// Javascript program to merge B into A in
// sorted order.

// Merging b[] into a[]
function sortedMerge(a, b, n, m) {
    let i = n - 1;
    let j = m - 1;

    let lastIndex = n + m - 1;

    /* Merge a and b, starting from
    last element in each */
    while (j >= 0) {

        /* End of a is greater than end of b */
        if (i >= 0 && a[i] > b[j]) {
            a[lastIndex] = a[i]; // Copy Element
            i--;
        }
        else {
            a[lastIndex] = b[j]; // Copy Element
            j--;
        }
        lastIndex--; // Move indices
    }
    return a;
}

/* Helper function to print the array */
function printArray(arr, n) {
    document.write("Array A after merging B in sorted");
    document.write(" order : <br>");
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver Code
let a = [10, 12, 13, 14, 18,
    -1, -1, -1, -1, -1];
let n = 5;
let size_a = 10;

let b = new Array(16, 17, 19, 20, 22);
let m = 5;
let c = sortedMerge(a, b, n, m);
printArray(c, size_a);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
Array A after merging B in sorted order : 
10 12 13 14 16 17 18 19 20 22
```

**时间复杂度为 O(m+n)。**