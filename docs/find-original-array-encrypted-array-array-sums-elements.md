# 从加密数组(其他元素之和的数组)中找到原始数组

> 原文:[https://www . geesforgeks . org/find-origin-array-encrypted-array-sums-elements/](https://www.geeksforgeeks.org/find-original-array-encrypted-array-array-sums-elements/)

从给定的大小为 n 的加密数组中查找原始数组。加密数组是通过用剩余数组元素的总和替换原始数组的每个元素而获得的。
**例:**

```
Input :  arr[] = {10, 14, 12, 13, 11}
Output : {5, 1, 3, 2, 4}
Original array {5, 1, 3, 2, 4}
Encrypted array is obtained as:
= {1+3+2+4, 5+3+2+4, 5+1+2+4, 5+1+3+4, 5+1+3+2}
= {10, 14, 12, 13, 11}
Each element of original array is replaced by the 
sum of the remaining array elements.  

Input : arr[] = {95, 107, 103, 88, 110, 87}
Output : {23, 11, 15, 30, 8, 31}
```

该方法完全基于算术观察，如下所示:

```
Let n = 4, and
the original array be ori[] = {a, b, c, d}
encrypted array is given as:
arr[] = {b+c+d, a+c+d, a+b+d, a+b+c}

Elements of encrypted array are :
arr[0] = (b+c+d), arr[1] = (a+c+d), 
arr[2] = (a+b+d), arr[3] = (a+b+c)
add up all the elements
sum =  arr[0] + arr[1] + arr[2] + arr[3]
       = (b+c+d) + (a+c+d) + (a+b+d) + (a+b+c)
       = 3(a+b+c+d) 
Sum of elements of ori[] = sum / n-1
                        = sum/3 
                        = (a+b+c+d)
Thus, for a given encrypted array arr[] of size n, the sum of 
the elements of the original array ori[] can be calculated as:
sum =  (arr[0]+arr[1]+....+arr[n-1]) / (n-1)

Then, elements of ori[] are calculated as:
ori[0] = sum - arr[0]
ori[1] = sum - arr[1] 
        .
        .
ori[n-1] = sum - arr[n-1]                      
```

下面是以上步骤的实现。

## C++

```
// C++ implementation to find original array
// from the encrypted array
#include <bits/stdc++.h>
using namespace std;

// Finds and prints the elements of the original
// array
void findAndPrintOriginalArray(int arr[], int n)
{
    // total sum of elements
    // of encrypted array
    int arr_sum = 0;
    for (int i=0; i<n; i++)
        arr_sum += arr[i];

    // total sum of elements
    // of original array
    arr_sum = arr_sum/(n-1);

    // calculating and displaying
    // elements of original array
    for (int i=0; i<n; i++)
        cout << (arr_sum - arr[i]) << " ";
}

// Driver program to test above
int main()
{
    int arr[] = {10, 14, 12, 13, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    findAndPrintOriginalArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

    // Finds and prints the elements of the original
    // array
    static void findAndPrintOriginalArray(int arr[], int n)
    {

        // total sum of elements
        // of encrypted array
        int arr_sum = 0;
        for (int i = 0; i < n; i++) {
            arr_sum += arr[i];
        }

        // total sum of elements
        // of original array
        arr_sum = arr_sum / (n - 1);

        // calculating and displaying
        // elements of original array
        for (int i = 0; i < n; i++) {
            System.out.print(arr_sum - arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 10, 14, 12, 13, 11 };
        int n = arr.length;
        findAndPrintOriginalArray(arr, n);
    }
}

// This code is contributed by rj13to.
```

## 蟒蛇 3

```
# Python 3 implementation to find
# original array from the encrypted
# array

# Finds and prints the elements of
# the original array
def findAndPrintOriginalArray(arr, n):

    # total sum of elements
    # of encrypted array
    arr_sum = 0
    for i in range(0, n):
        arr_sum += arr[i]

    # total sum of elements
    # of original array
    arr_sum = int(arr_sum / (n - 1))

    # calculating and displaying
    # elements of original array
    for i in range(0, n):
        print((arr_sum - arr[i]),
                       end = " ")

# Driver program to test above
arr = [10, 14, 12, 13, 11]
n = len(arr)
findAndPrintOriginalArray(arr, n)

# This code is contributed By Smitha
```

## C#

```
// C# program to find original
// array from the encrypted array
using System;

class GFG {

    // Finds and prints the elements
    // of the original array
    static void findAndPrintOriginalArray(int []arr,
                                          int n)
    {

        // total sum of elements
        // of encrypted array
        int arr_sum = 0;
        for (int i = 0; i < n; i++)
            arr_sum += arr[i];

        // total sum of elements
        // of original array
        arr_sum = arr_sum / (n - 1);

        // calculating and displaying
        // elements of original array
        for (int i = 0; i < n; i++)
        Console.Write(arr_sum - arr[i] + " ");
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []arr = {10, 14, 12, 13, 11};
        int n =arr.Length;
        findAndPrintOriginalArray(arr, n);
    }
}

// This code is contributed by parashar...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// original array from the
// encrypted array

// Finds and prints the elements
// of the original array
function findAndPrintOriginalArray($arr, $n)
{
    // total sum of elements
    // of encrypted array
    $arr_sum = 0;
    for ( $i = 0; $i < $n; $i++)
        $arr_sum += $arr[$i];

    // total sum of elements
    // of original array
    $arr_sum = $arr_sum / ($n - 1);

    // calculating and displaying
    // elements of original array
    for ( $i = 0; $i < $n; $i++)
        echo $arr_sum - $arr[$i] , " ";
}

// Driver Code
$arr = array(10, 14, 12, 13, 11);
$n = count($arr);
findAndPrintOriginalArray($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find original
    // array from the encrypted array

    // Finds and prints the elements
    // of the original array
    function findAndPrintOriginalArray(arr, n)
    {

        // total sum of elements
        // of encrypted array
        let arr_sum = 0;
        for (let i = 0; i < n; i++)
            arr_sum += arr[i];

        // total sum of elements
        // of original array
        arr_sum = parseInt(arr_sum / (n - 1), 10);

        // calculating and displaying
        // elements of original array
        for (let i = 0; i < n; i++)
            document.write(arr_sum - arr[i] + " ");
    }

    let arr = [10, 14, 12, 13, 11];
    let n =arr.length;
    findAndPrintOriginalArray(arr, n);

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
5 1 3 2 4
```

**时间复杂度:** O(N)

**辅助空间:** O(1)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。