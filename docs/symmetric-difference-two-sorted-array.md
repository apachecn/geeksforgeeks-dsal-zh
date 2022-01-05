# 两个排序数组的对称差

> 原文:[https://www . geeksforgeeks . org/对称-差分-二排序-数组/](https://www.geeksforgeeks.org/symmetric-difference-two-sorted-array/)

有两个排序数组 **arr1** 和 **arr2** 。我们必须找到 Aarr1 和 arr2 的**对称差**。对称差基本上包含两个数组除公共元素之外的所有元素。

```
Symmetric difference of two array is the all 
array elements of both array except the elements 
that are presents in both array.
SymmDiff = (arr1 - arr2) UNION (arr2 - arr1). 
               OR
SymmDiff = (arr1 UNION arr2) - (arr1 INTERSECTION arr2).
```

示例:

```
Input : arr1[] = {2, 4, 5, 7, 8, 10, 12, 15}.
        arr2[] = {5, 8, 11, 12, 14, 15}.
Output : 2 4 7 10 11 14        
        arr1[] - arr2[] = {2, 4, 7, 10}.
        arr[2] - arr1[] = {11, 14}.
        SymmDiff = (arr1[] - arr2[]) UNION 
                   (arr2[] - arr1[]).
                 = {2, 4, 7, 10, 11, 14}.

Input : arr1[] = {1, 3, 5, 8, 15, 27, 35}.
        arr2[] = {5, 7, 8, 11, 15, 18, 35}.
Output : 1 3 7 11 18 27
        arr1[] - arr2[] = {1, 3, 27}.
        arr[2] - arr1[] = {7, 11, 18}.
        SymmDiff = (arr1[] - arr2[]) UNION 
                   (arr2[] - arr1[]).
                 = {1, 3, 7, 11, 18, 27}.
```

一个**简单的解决方案**是逐个遍历两个数组。对于一个数组的每个元素，检查它是否存在于另一个数组中。如果是，那么忽略它，否则打印它。该解的时间复杂度为 O(n*n)
求两个排序数组对称差的高效解类似于合并排序的[合并过程。如果当前两个元素不匹配，我们会同时遍历两个数组并打印较小的元素，然后在具有较小元素的数组中前进。否则我们忽略元素，在两个数组中前进。](https://www.geeksforgeeks.org/merge-sort/)

## C++

```
// C++ program to find the symmetric difference
// of two sorted array.
#include <iostream>
using namespace std;
void symmDiff(int arr1[], int arr2[], int n, int m)
{
    // Traverse both arrays simultaneously.
    int i = 0, j = 0;
    while (i < n && j < m) {

        // Print smaller element and move
        // ahead in array with smaller element
        if (arr1[i] < arr2[j]) {
            cout << arr1[i] << " ";
            i++;
        }
        else if (arr2[j] < arr1[i]) {
            cout << arr2[j] << " ";
            j++;
        }

        // If both elements same, move ahead
        // in both arrays.
        else {
            i++;
            j++;
        }
    }
    while (i < n) {
        cout << arr1[i] << " ";
        i++;
    }
    while (j < m) {
        cout << arr2[j] << " ";
        j++;
    }
}

// Driver code
int main()
{
    int arr1[] = { 2, 4, 5, 7, 8, 10, 12, 15 };
    int arr2[] = { 5, 8, 11, 12, 14, 15 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    int m = sizeof(arr2) / sizeof(arr2[0]);
    symmDiff(arr1, arr2, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the symmetric
// difference of two sorted array.
import java.util.*;
class GFG {
    static void symmDiff(int[] arr1, int[] arr2, int n,
                         int m)
    {
        // Traverse both arrays simultaneously.
        int i = 0, j = 0;
        while (i < n && j < m) {
            // Print smaller element and move
            // ahead in array with smaller element
            if (arr1[i] < arr2[j]) {
                System.out.print(arr1[i] + " ");
                i++;
            }
            else if (arr2[j] < arr1[i]) {
                System.out.print(arr2[j] + " ");
                j++;
            }

            // If both elements same, move ahead
            // in both arrays.
            else {
                i++;
                j++;
            }
        }
        while (i < n) {
            System.out.print(arr1[i] + " ");
            i++;
        }
        while (j < m) {
            System.out.print(arr2[j] + " ");
            j++;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr1 = { 2, 4, 5, 7, 8, 10, 12, 15 };
        int[] arr2 = { 5, 8, 11, 12, 14, 15 };
        int n = arr1.length;
        int m = arr2.length;
        symmDiff(arr1, arr2, n, m);
    }
}
/* This code is contributed by Kriti Shukla */
```

## 蟒蛇 3

```
# Python3 program to
# find the symmetric
# difference of two
# sorted array.

def symmDiff(arr1, arr2, n, m):

    # Traverse both arrays
    # simultaneously.
    i = 0
    j = 0
    while (i < n and j < m):

        # Print smaller element
        # and move ahead in
        # array with smaller
        # element
        if (arr1[i] < arr2[j]):
            print(arr1[i], end=" ")
            i += 1

        elif (arr2[j] < arr1[i]):
            print(arr2[j], end=" ")
            j += 1

        # If both elements
        # same, move ahead
        # in both arrays.
        else:

            i += 1
            j += 1

    while i < n:
        print(arr1[i], end=' ')
        i += 1

    while j < m:
        print(arr2[j], end=' ')
        j += 1

# Driver code
arr1 = [2, 4, 5, 7, 8, 10, 12, 15]
arr2 = [5, 8, 11, 12, 14, 15]
n = len(arr1)
m = len(arr2)

symmDiff(arr1, arr2, n, m)

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find the symmetric
// difference of two sorted array.
using System;

class GFG {

    static void symmDiff(int[] arr1, int[] arr2, int n,
                         int m)
    {

        // Traverse both arrays simultaneously.
        int i = 0, j = 0;

        while (i < n && j < m) {

            // Print smaller element and move
            // ahead in array with smaller element
            if (arr1[i] < arr2[j]) {
                Console.Write(arr1[i] + " ");
                i++;
            }
            else if (arr2[j] < arr1[i]) {
                Console.Write(arr2[j] + " ");
                j++;
            }

            // If both elements same, move ahead
            // in both arrays.
            else {
                i++;
                j++;
            }
        }
        while (i < n) {
            Console.Write(arr1[i] + " ");
            i++;
        }

        while (j < m) {
            Console.Write(arr2[j] + " ");
            j++;
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr1 = { 2, 4, 5, 7, 8, 10, 12, 15 };
        int[] arr2 = { 5, 8, 11, 12, 14, 15 };
        int n = arr1.Length;
        int m = arr2.Length;

        symmDiff(arr1, arr2, n, m);
    }
}

/* This code is contributed by vt_m*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// symmetric difference
// of two sorted array.
function symmDiff($arr1, $arr2,
                       $n, $m)
{

    // Traverse both arrays
    // simultaneously.
    $i = 0; $j = 0;
    while ($i < $n && $j < $m)
    {

        // Print smaller element
        // and move ahead in array
        // with smaller element
        if ($arr1[$i] < $arr2[$j])
        {
            echo($arr1[$i] . " ");
            $i++;
        }
        else if ($arr2[$j] < $arr1[$i])
        {
            echo($arr2[$j] . " ");
            $j++;
        }

        // If both elements same,
        // move ahead in both arrays
        else
        {
            $i++;
            $j++;
        }
    }

    while ($i < $n) {
        echo($arr1[$i] . " ");
        $i++;
    }

    while ($j < $m) {
        echo($arr2[$j] . " ");
        $j++;
    }
}

// Driver code
$arr1 = array(2, 4, 5, 7, 8, 10, 12, 15);
$arr2 = array(5, 8, 11, 12, 14, 15);
$n = sizeof($arr1);
$m = sizeof($arr2);
symmDiff($arr1, $arr2, $n, $m);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the symmetric
    // difference of two sorted array.

    function symmDiff(arr1, arr2, n, m)
    {

        // Traverse both arrays simultaneously.
        let i = 0, j = 0;

        while (i < n && j < m) {

            // Print smaller element and move
            // ahead in array with smaller element
            if (arr1[i] < arr2[j]) {
                document.write(arr1[i] + " ");
                i++;
            }
            else if (arr2[j] < arr1[i]) {
                document.write(arr2[j] + " ");
                j++;
            }

            // If both elements same, move ahead
            // in both arrays.
            else {
                i++;
                j++;
            }
        }
        while (i < n) {
            document.write(arr1[i] + " ");
            i++;
        }

        while (j < m) {
            document.write(arr2[j] + " ");
            j++;
        }
    }

    let arr1 = [ 2, 4, 5, 7, 8, 10, 12, 15 ];
    let arr2 = [ 5, 8, 11, 12, 14, 15 ];
    let n = arr1.length;
    let m = arr2.length;

    symmDiff(arr1, arr2, n, m);

</script>
```

**输出:**

```
2 4 7 10 11 14
```

**时间复杂度:** O(m + n)。
本文由**达曼德拉·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。