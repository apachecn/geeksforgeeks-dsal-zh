# 两个排序数组的第 K 个元素

> 原文:[https://www . geeksforgeeks . org/k-th-element-two-sorted-arrays/](https://www.geeksforgeeks.org/k-th-element-two-sorted-arrays/)

给定两个大小分别为 m 和 n 的排序数组，您的任务是找到位于最终排序数组的第 k 个位置的元素。

**示例:**

```
Input : Array 1 - 2 3 6 7 9
        Array 2 - 1 4 8 10
        k = 5
Output : 6
Explanation: The final sorted array would be -
1, 2, 3, 4, 6, 7, 8, 9, 10
The 5th element of this array is 6.

Input : Array 1 - 100 112 256 349 770
        Array 2 - 72 86 113 119 265 445 892
        k = 7
Output : 256
Explanation: Final sorted array is -
72, 86, 100, 112, 113, 119, 256, 265, 349, 445, 770, 892
7th element of this array is 256.
```

**基本方法**
由于给了我们两个排序的数组，我们可以使用合并技术得到最终的合并数组。由此，我们简单地去 k 指数。

## C++

```
// Program to find kth element from two sorted arrays
#include <iostream>
using namespace std;

int kth(int arr1[], int arr2[], int m, int n, int k)
{
    int sorted1[m + n];
    int i = 0, j = 0, d = 0;
    while (i < m && j < n)
    {
        if (arr1[i] < arr2[j])
            sorted1[d++] = arr1[i++];
        else
            sorted1[d++] = arr2[j++];
    }
    while (i < m)
        sorted1[d++] = arr1[i++];
    while (j < n)
        sorted1[d++] = arr2[j++];
    return sorted1[k - 1];
}

// Driver Code
int main()
{
    int arr1[5] = {2, 3, 6, 7, 9};
    int arr2[4] = {1, 4, 8, 10};
    int k = 5;
    cout << kth(arr1, arr2, 5, 4, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find kth element
// from two sorted arrays

class Main
{
    static int kth(int arr1[], int arr2[], int m, int n, int k)
    {
        int[] sorted1 = new int[m + n];
        int i = 0, j = 0, d = 0;
        while (i < m && j < n)
        {
            if (arr1[i] < arr2[j])
                sorted1[d++] = arr1[i++];
            else
                sorted1[d++] = arr2[j++];
        }
        while (i < m)
            sorted1[d++] = arr1[i++];
        while (j < n)
            sorted1[d++] = arr2[j++];
        return sorted1[k - 1];
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr1[] = {2, 3, 6, 7, 9};
        int arr2[] = {1, 4, 8, 10};
        int k = 5;
        System.out.print(kth(arr1, arr2, 5, 4, k));
    }
}

/* This code is contributed by Harsh Agarwal */
```

## 蟒蛇 3

```
# Program to find kth element
# from two sorted arrays

def kth(arr1, arr2, m, n, k):

    sorted1 = [0] * (m + n)
    i = 0
    j = 0
    d = 0
    while (i < m and j < n):

        if (arr1[i] < arr2[j]):
            sorted1[d] = arr1[i]
            i += 1
        else:
            sorted1[d] = arr2[j]
            j += 1
        d += 1

    while (i < m):
        sorted1[d] = arr1[i]
        d += 1
        i += 1
    while (j < n):
        sorted1[d] = arr2[j]
        d += 1
        j += 1
    return sorted1[k - 1]

# Driver code
arr1 = [2, 3, 6, 7, 9]
arr2 = [1, 4, 8, 10]
k = 5
print(kth(arr1, arr2, 5, 4, k))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# Program to find kth element
// from two sorted arrays
class GFG {
    static int kth(int[] arr1, int[] arr2, int m, int n,
                   int k)
    {
        int[] sorted1 = new int[m + n];
        int i = 0, j = 0, d = 0;
        while (i < m && j < n) {
            if (arr1[i] < arr2[j])
                sorted1[d++] = arr1[i++];
            else
                sorted1[d++] = arr2[j++];
        }
        while (i < m)
            sorted1[d++] = arr1[i++];
        while (j < n)
            sorted1[d++] = arr2[j++];
        return sorted1[k - 1];
    }

    // Driver Code
    static void Main()
    {
        int[] arr1 = { 2, 3, 6, 7, 9 };
        int[] arr2 = { 1, 4, 8, 10 };
        int k = 5;
        System.Console.WriteLine(kth(arr1, arr2, 5, 4, k));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find kth
// element from two
// sorted arrays

function kth($arr1, $arr2,
             $m, $n, $k)
{
    $sorted1[$m + $n] = 0;
    $i = 0;
    $j = 0;
    $d = 0;
    while ($i < $m && $j < $n)
    {
        if ($arr1[$i] < $arr2[$j])
            $sorted1[$d++] = $arr1[$i++];
        else
            $sorted1[$d++] = $arr2[$j++];
    }
    while ($i < $m)
        $sorted1[$d++] = $arr1[$i++];
    while ($j < $n)
        $sorted1[$d++] = $arr2[$j++];
    return $sorted1[$k - 1];
}

// Driver Code
$arr1 = array(2, 3, 6, 7, 9);
$arr2 = array(1, 4, 8, 10);
$k = 5;
echo kth($arr1, $arr2, 5, 4, $k);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find kth element
// from two sorted arrays

    function kth(arr1 , arr2 , m , n , k) {
        var sorted1 = Array(m + n).fill(0);
        var i = 0, j = 0, d = 0;
        while (i < m && j < n) {
            if (arr1[i] < arr2[j])
                sorted1[d++] = arr1[i++];
            else
                sorted1[d++] = arr2[j++];
        }
        while (i < m)
            sorted1[d++] = arr1[i++];
        while (j < n)
            sorted1[d++] = arr2[j++];
        return sorted1[k - 1];
    }

    // Driver Code

        var arr1 = [ 2, 3, 6, 7, 9 ];
        var arr2 = [ 1, 4, 8, 10 ];
        var k = 5;
        document.write(kth(arr1, arr2, 5, 4, k));

// This code contributed by umadevi9616

</script>
```

**Output**

```
6
```