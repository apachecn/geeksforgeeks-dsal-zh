# 从给定的三个排序数组中找到三个最接近的元素

> 原文:[https://www . geeksforgeeks . org/find-从给定的三个排序数组中找到三个最接近的元素/](https://www.geeksforgeeks.org/find-three-closest-elements-from-given-three-sorted-arrays/)

给定三个排序的数组 A[]、B[]、C[]，分别从 A、B、C 中找出 3 个元素 I、j、k，使得 max(ABS(A[I]–B[j])、ABS(B[j]–C[k])、ABS(C[k]–A[I])最小化。这里 abs()表示绝对值。

**示例:**

```
Input: A[] = {1, 4, 10}
       B[] = {2, 15, 20}
       C[] = {10, 12}
Output: 10 15 10
10 from A, 15 from B and 10 from C

Input: A[] = {20, 24, 100}
       B[] = {2, 19, 22, 79, 800}
       C[] = {10, 12, 23, 24, 119}
Output: 24 22 23
24 from A, 22 from B and 23 from C
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**

A **简单的解决方案**是运行三个嵌套循环来考虑来自 A、B 和 C 的所有三元组，计算每个三元组的 max(ABS(A[I]–B[j])、ABS(B[j]–C[k])、ABS(C[k]–A[I])的值，并返回所有值的最小值。该解决方案的时间复杂度为 0(n<sup>3</sup>

一个更好的解决方案是使用二分搜索法。
1)迭代 A[]，
a)的所有元素，求 B[]，C[]中刚好小于等于的元素二分搜索法，注意区别。
2)对 B[]和 C[]重复步骤 1。
3)返回整体最小值。
该方案的时间复杂度为 O(nLogn)

**有效解**设‘p’为 A[]的大小，‘q’为 B[]的大小，‘r’为 C[]的大小

```
1)   Start with i=0, j=0 and k=0 (Three index variables for A,
                                  B and C respectively)

//  p, q and r are sizes of A[], B[] and C[] respectively.
2)   Do following while i < p and j < q and k < r
    a) Find min and maximum of A[i], B[j] and C[k]
    b) Compute diff = max(X, Y, Z) - min(A[i], B[j], C[k]).
    c) If new result is less than current result, change 
       it to the new result.
    d) Increment the pointer of the array which contains 
       the minimum.
```

请注意，我们增加具有最小值的数组的指针，因为我们的目标是减少差异。增加最大指针会增加差异。增加第二个最大指针可能会增加差异。

## C++

```
// C++ program to find 3 elements such that max(abs(A[i]-B[j]), abs(B[j]-
// C[k]), abs(C[k]-A[i])) is minimized.

#include<bits/stdc++.h>
using namespace std;

void findClosest(int A[], int B[], int C[], int p, int q, int r)
{

    int diff = INT_MAX;  // Initialize min diff

    // Initialize result
    int res_i =0, res_j = 0, res_k = 0;

    // Traverse arrays
    int i=0,j=0,k=0;
    while (i < p && j < q && k < r)
    {
        // Find minimum and maximum of current three elements
        int minimum = min(A[i], min(B[j], C[k]));
        int maximum = max(A[i], max(B[j], C[k]));

        // Update result if current diff is less than the min
        // diff so far
        if (maximum-minimum < diff)
        {
             res_i = i, res_j = j, res_k = k;
             diff = maximum - minimum;
        }

        // We can't get less than 0 as values are absolute
        if (diff == 0) break;

        // Increment index of array with smallest value
        if (A[i] == minimum) i++;
        else if (B[j] == minimum) j++;
        else k++;
    }

    // Print result
    cout << A[res_i] << " " << B[res_j] << " " << C[res_k];
}

// Driver program
int main()
{
    int A[] = {1, 4, 10};
    int B[] = {2, 15, 20};
    int C[] = {10, 12};

    int p = sizeof A / sizeof A[0];
    int q = sizeof B / sizeof B[0];
    int r = sizeof C / sizeof C[0];

    findClosest(A, B, C, p, q, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 3 elements such
// that max(abs(A[i]-B[j]), abs(B[j]-C[k]),
// abs(C[k]-A[i])) is minimized.
import java.io.*;

class GFG {

    static void findClosest(int A[], int B[], int C[],
                                  int p, int q, int r)
    {
        int diff = Integer.MAX_VALUE; // Initialize min diff

        // Initialize result
        int res_i =0, res_j = 0, res_k = 0;

        // Traverse arrays
        int i = 0, j = 0, k = 0;
        while (i < p && j < q && k < r)
        {
            // Find minimum and maximum of current three elements
            int minimum = Math.min(A[i],
                          Math.min(B[j], C[k]));
            int maximum = Math.max(A[i],
                          Math.max(B[j], C[k]));

            // Update result if current diff is
            // less than the min diff so far
            if (maximum-minimum < diff)
            {
                res_i = i;
                res_j = j;
                res_k = k;
                diff = maximum - minimum;
            }

            // We can't get less than 0
            // as values are absolute
            if (diff == 0) break;

            // Increment index of array
            // with smallest value
            if (A[i] == minimum) i++;
            else if (B[j] == minimum) j++;
            else k++;
        }

        // Print result
        System.out.println(A[res_i] + " " +
                           B[res_j] + " " + C[res_k]);
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = {1, 4, 10};
        int B[] = {2, 15, 20};
        int C[] = {10, 12};

        int p = A.length;
        int q = B.length;
        int r = C.length;

        // Function calling
        findClosest(A, B, C, p, q, r);
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python program to find 3 elements such
# that max(abs(A[i]-B[j]), abs(B[j]- C[k]),
# abs(C[k]-A[i])) is minimized.
import sys

def findCloset(A, B, C, p, q, r):

    # Initialize min diff
    diff = sys.maxsize

    res_i = 0
    res_j = 0
    res_k = 0

    # Traverse Array
    i = 0
    j = 0
    k = 0
    while(i < p and j < q and k < r):

        # Find minimum and maximum of
        # current three elements
        minimum = min(A[i], min(B[j], C[k]))
        maximum = max(A[i], max(B[j], C[k]));

        # Update result if current diff is
        # less than the min diff so far
        if maximum-minimum < diff:
            res_i = i
            res_j = j
            res_k = k
            diff = maximum - minimum;

        # We can 't get less than 0 as
        # values are absolute
        if diff == 0:
            break

        # Increment index of array with
        # smallest value
        if A[i] == minimum:
            i = i+1
        elif B[j] == minimum:
            j = j+1
        else:
            k = k+1

    # Print result
    print(A[res_i], " ", B[res_j], " ", C[res_k])

# Driver Program
A = [1, 4, 10]
B = [2, 15, 20]
C = [10, 12]

p = len(A)
q = len(B)
r = len(C)

findCloset(A,B,C,p,q,r)

# This code is contributed by Shrikant13.
```

## C#

```
// C# program to find 3 elements
// such that max(abs(A[i]-B[j]),
// abs(B[j]-C[k]), abs(C[k]-A[i]))
// is minimized.
using System;

class GFG
{
    static void findClosest(int []A, int []B,
                            int []C, int p,
                            int q, int r)
    {
        // Initialize min diff
        int diff = int.MaxValue;

        // Initialize result
        int res_i = 0,
            res_j = 0,
            res_k = 0;

        // Traverse arrays
        int i = 0, j = 0, k = 0;
        while (i < p && j < q && k < r)
        {
            // Find minimum and maximum
            // of current three elements
            int minimum = Math.Min(A[i],
                          Math.Min(B[j], C[k]));
            int maximum = Math.Max(A[i],
                          Math.Max(B[j], C[k]));

            // Update result if current
            // diff is less than the min
            // diff so far
            if (maximum - minimum < diff)
            {
                res_i = i;
                res_j = j;
                res_k = k;
                diff = maximum - minimum;
            }

            // We can't get less than 0
            // as values are absolute
            if (diff == 0) break;

            // Increment index of array
            // with smallest value
            if (A[i] == minimum) i++;
            else if (B[j] == minimum) j++;
            else k++;
        }

        // Print result
        Console.WriteLine(A[res_i] + " " +
                          B[res_j] + " " +
                          C[res_k]);
    }

    // Driver code
    public static void Main ()
    {
        int []A = {1, 4, 10};
        int []B = {2, 15, 20};
        int []C = {10, 12};

        int p = A.Length;
        int q = B.Length;
        int r = C.Length;

        // Function calling
        findClosest(A, B, C, p, q, r);
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 3 elements such
// that max(abs(A[i]-B[j]), abs(B[j]-
// C[k]), abs(C[k]-A[i])) is minimized.

function findClosest($A, $B, $C, $p, $q, $r)
{

    $diff = PHP_INT_MAX; // Initialize min diff

    // Initialize result
    $res_i = 0;
    $res_j = 0;
    $res_k = 0;

    // Traverse arrays
    $i = 0;
    $j = 0;
    $k = 0;
    while ($i < $p && $j < $q && $k < $r)
    {
        // Find minimum and maximum of
        // current three elements
        $minimum = min($A[$i], min($B[$j], $C[$k]));
        $maximum = max($A[$i], max($B[$j], $C[$k]));

        // Update result if current diff is
        // less than the min diff so far
        if ($maximum-$minimum < $diff)
        {
            $res_i = $i; $res_j = $j; $res_k = $k;
            $diff = $maximum - $minimum;
        }

        // We can't get less than 0 as
        // values are absolute
        if ($diff == 0) break;

        // Increment index of array with
        // smallest value
        if ($A[$i] == $minimum) $i++;
        else if ($B[$j] == $minimum) $j++;
        else $k++;
    }

    // Print result
    echo $A[$res_i] , " ", $B[$res_j],
                      " ", $C[$res_k];
}

// Driver Code
$A = array(1, 4, 10);
$B = array(2, 15, 20);
$C = array(10, 12);

$p = sizeof($A);
$q = sizeof($B);
$r = sizeof($C);

findClosest($A, $B, $C, $p, $q, $r);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>
     // JavaScript program to find 3 elements
     // such that max(abs(A[i]-B[j]), abs(B[j]-
     // C[k]), abs(C[k]-A[i])) is minimized.

     function findClosest(A, B, C, p, q, r)
     {
       var diff = Math.pow(10, 9); // Initialize min diff

       // Initialize result
       var res_i = 0,
         res_j = 0,
         res_k = 0;

       // Traverse arrays
       var i = 0,
         j = 0,
         k = 0;
       while (i < p && j < q && k < r)
       {

         // Find minimum and maximum of current three elements
         var minimum = Math.min(A[i], Math.min(B[j], C[k]));
         var maximum = Math.max(A[i], Math.max(B[j], C[k]));

         // Update result if current diff is less than the min
         // diff so far
         if (maximum - minimum < diff)
         {
           (res_i = i), (res_j = j), (res_k = k);
           diff = maximum - minimum;
         }

         // We can't get less than 0 as values are absolute
         if (diff == 0) break;

         // Increment index of array with smallest value
         if (A[i] == minimum)
             i++;
         else if (B[j] == minimum)
             j++;
         else
             k++;
       }

       // Print result
       document.write(A[res_i] + " " + B[res_j] + " " + C[res_k]);
     }

     // Driver program
     var A = [1, 4, 10];
     var B = [2, 15, 20];
     var C = [10, 12];

     var p = A.length;
     var q = B.length;
     var r = C.length;

     findClosest(A, B, C, p, q, r);

     // This code is contributed by rdtank.
   </script>
```

**输出:**

```
10 15 10
```

该解的时间复杂度为 O(p + q + r)，其中 p、q 和 r 分别为 A[]、B[]、C[]。
感谢 Gaurav Ahirwar 提出上述解决方案。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。