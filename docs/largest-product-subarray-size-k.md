# k 尺寸子阵列的最大乘积

> 原文:[https://www . geesforgeks . org/maximum-product-subarray-size-k/](https://www.geeksforgeeks.org/largest-product-subarray-size-k/)

给定一个由 n 个正整数和一个整数 k 组成的数组，求大小为 k 的最大乘积子数组，即求数组中 k 个连续元素的最大乘积，其中 k <= n.
**例:**

```
Input: arr[] = {1, 5, 9, 8, 2, 4,
                 1, 8, 1, 2} 
       k = 6
Output:   4608  
The subarray is {9, 8, 2, 4, 1, 8}

Input: arr[] = {1, 5, 9, 8, 2, 4, 1, 8, 1, 2}
       k = 4
Output:   720  
The subarray is {5, 9, 8, 2}

Input: arr[] = {2, 5, 8, 1, 1, 3};
       k = 3             
Output:   80  
The subarray is {2, 5, 8}
```

**方法 1(简单:O(n*k))**
一种简单的方法是逐个考虑 k 大小的所有子阵列。这种方法需要两个循环，因此复杂度为 0(n * k)。
**方法 2(高效:O(n))**
我们可以在 O(n)中求解，利用这样一个事实:如果我们有以前子阵列的乘积可用，那么大小为 k 的子阵列的乘积可以在 O(1)时间内计算出来。

```
curr_product = (prev_product / arr[i-1]) * arr[i + k -1]

prev_product : Product of subarray of size k beginning 
               with arr[i-1]

curr_product : Product of subarray of size k beginning 
               with arr[i]
```

这样，我们可以只在一次遍历中计算出最大 k 大小的子阵积。下面是 C++实现的思路。

## C++

```
// C++ program to find the maximum product of a subarray
// of size k.
#include <bits/stdc++.h>
using namespace std;

// This function returns maximum product of a subarray
// of size k in given arrar, arr[0..n-1]. This function
// assumes that k is smaller than or equal to n.
int findMaxProduct(int arr[], int n, int k)
{
    // Initialize the MaxProduct to 1, as all elements
    // in the array are positive
    int MaxProduct = 1;
    for (int i=0; i<k; i++)
        MaxProduct *= arr[i];

    int prev_product = MaxProduct;

    // Consider every product beginning with arr[i]
    // where i varies from 1 to n-k-1
    for (int i=1; i<=n-k; i++)
    {
        int curr_product = (prev_product/arr[i-1]) *
                            arr[i+k-1];
        MaxProduct = max(MaxProduct, curr_product);
        prev_product = curr_product;
    }

    // Return the maximum product found
    return MaxProduct;
}

// Driver code
int main()
{
    int arr1[] = {1, 5, 9, 8, 2, 4, 1, 8, 1, 2};
    int k = 6;
    int n = sizeof(arr1)/sizeof(arr1[0]);
    cout << findMaxProduct(arr1, n, k) << endl;

    k = 4;
    cout << findMaxProduct(arr1, n, k) << endl;

    int arr2[] = {2, 5, 8, 1, 1, 3};
    k = 3;
    n = sizeof(arr2)/sizeof(arr2[0]);
    cout << findMaxProduct(arr2, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum product of a subarray
// of size k
import java.io.*;
import java.util.*;

class GFG
{
    // Function returns maximum product of a subarray
    // of size k in given arrar, arr[0..n-1]. This function
    // assumes that k is smaller than or equal to n.
    static int findMaxProduct(int arr[], int n, int k)
    {
        // Initialize the MaxProduct to 1, as all elements
        // in the array are positive
        int MaxProduct = 1;
        for (int i=0; i<k; i++)
            MaxProduct *= arr[i];

        int prev_product = MaxProduct;

        // Consider every product beginning with arr[i]
        // where i varies from 1 to n-k-1
        for (int i=1; i<=n-k; i++)
        {
            int curr_product = (prev_product/arr[i-1]) *
                                arr[i+k-1];
            MaxProduct = Math.max(MaxProduct, curr_product);
            prev_product = curr_product;
        }

        // Return the maximum product found
        return MaxProduct;
    }

    // driver program
    public static void main (String[] args)
    {
        int arr1[] = {1, 5, 9, 8, 2, 4, 1, 8, 1, 2};
        int k = 6;
        int n = arr1.length;
        System.out.println(findMaxProduct(arr1, n, k));

        k = 4;
        System.out.println(findMaxProduct(arr1, n, k));

        int arr2[] = {2, 5, 8, 1, 1, 3};
        k = 3;
        n = arr2.length;
        System.out.println(findMaxProduct(arr2, n, k));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to find the maximum
# product of a subarray of size k.

# This function returns maximum product
# of a subarray of size k in given arrar,
# arr[0..n-1]. This function assumes
# that k is smaller than or equal to n.
def findMaxProduct(arr, n, k) :

    # Initialize the MaxProduct to 1,
    # as all elements in the array
    # are positive
    MaxProduct = 1
    for i in range(0, k) :
        MaxProduct = MaxProduct * arr[i]

    prev_product = MaxProduct

    # Consider every product beginning
    # with arr[i] where i varies from
    # 1 to n-k-1
    for i in range(1, n - k + 1) :
        curr_product = (prev_product // arr[i-1]) * arr[i+k-1]
        MaxProduct = max(MaxProduct, curr_product)
        prev_product = curr_product

    # Return the maximum product found
    return MaxProduct

# Driver code
arr1 = [1, 5, 9, 8, 2, 4, 1, 8, 1, 2]
k = 6
n = len(arr1)
print (findMaxProduct(arr1, n, k) )
k = 4
print (findMaxProduct(arr1, n, k))

arr2 = [2, 5, 8, 1, 1, 3]
k = 3
n = len(arr2)

print(findMaxProduct(arr2, n, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find the maximum
// product of a subarray of size k
using System;

class GFG
{
    // Function returns maximum
    // product of a subarray of
    // size k in given arrar,
    // arr[0..n-1]. This function
    // assumes that k is smaller
    // than or equal to n.
    static int findMaxProduct(int []arr,
                              int n, int k)
    {
        // Initialize the MaxProduct
        // to 1, as all elements
        // in the array are positive
        int MaxProduct = 1;
        for (int i = 0; i < k; i++)
            MaxProduct *= arr[i];

        int prev_product = MaxProduct;

        // Consider every product beginning
        // with arr[i] where i varies from
        // 1 to n-k-1
        for (int i = 1; i <= n - k; i++)
        {
            int curr_product = (prev_product /
                                 arr[i - 1]) *
                                 arr[i + k - 1];
            MaxProduct = Math.Max(MaxProduct,
                                  curr_product);
            prev_product = curr_product;
        }

        // Return the maximum
        // product found
        return MaxProduct;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr1 = {1, 5, 9, 8, 2,
                      4, 1, 8, 1, 2};
        int k = 6;
        int n = arr1.Length;
        Console.WriteLine(findMaxProduct(arr1, n, k));

        k = 4;
        Console.WriteLine(findMaxProduct(arr1, n, k));

        int []arr2 = {2, 5, 8, 1, 1, 3};
        k = 3;
        n = arr2.Length;
        Console.WriteLine(findMaxProduct(arr2, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// product of a subarray of size k.

// This function returns maximum
// product of a subarray of size
// k in given arrar, arr[0..n-1].
// This function assumes that k
// is smaller than or equal to n.
function findMaxProduct( $arr, $n, $k)
{

    // Initialize the MaxProduct to
    // 1, as all elements
    // in the array are positive
    $MaxProduct = 1;
    for($i = 0; $i < $k; $i++)
        $MaxProduct *= $arr[$i];

    $prev_product = $MaxProduct;

    // Consider every product
    // beginning with arr[i]
    // where i varies from 1
    // to n-k-1
    for($i = 1; $i < $n - $k; $i++)
    {
        $curr_product = ($prev_product / $arr[$i - 1]) *
                                       $arr[$i + $k - 1];
        $MaxProduct = max($MaxProduct, $curr_product);
        $prev_product = $curr_product;
    }

    // Return the maximum
    // product found
    return $MaxProduct;
}

    // Driver code
    $arr1 = array(1, 5, 9, 8, 2, 4, 1, 8, 1, 2);
    $k = 6;
    $n = count($arr1);
    echo findMaxProduct($arr1, $n, $k),"\n" ;

    $k = 4;
    echo findMaxProduct($arr1, $n, $k),"\n";

    $arr2 = array(2, 5, 8, 1, 1, 3);
    $k = 3;
    $n = count($arr2);
    echo findMaxProduct($arr2, $n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find the maximum
    // product of a subarray of size k

    // Function returns maximum
    // product of a subarray of
    // size k in given arrar,
    // arr[0..n-1]. This function
    // assumes that k is smaller
    // than or equal to n.
    function findMaxProduct(arr, n, k)
    {
        // Initialize the MaxProduct
        // to 1, as all elements
        // in the array are positive
        let MaxProduct = 1;
        for (let i = 0; i < k; i++)
            MaxProduct *= arr[i];

        let prev_product = MaxProduct;

        // Consider every product beginning
        // with arr[i] where i varies from
        // 1 to n-k-1
        for (let i = 1; i <= n - k; i++)
        {
            let curr_product =
            (prev_product / arr[i - 1]) * arr[i + k - 1];
            MaxProduct = Math.max(MaxProduct, curr_product);
            prev_product = curr_product;
        }

        // Return the maximum
        // product found
        return MaxProduct;
    }

    let arr1 = [1, 5, 9, 8, 2, 4, 1, 8, 1, 2];
    let k = 6;
    let n = arr1.length;
    document.write(findMaxProduct(arr1, n, k) + "</br>");

    k = 4;
    document.write(findMaxProduct(arr1, n, k) + "</br>");

    let arr2 = [2, 5, 8, 1, 1, 3];
    k = 3;
    n = arr2.length;
    document.write(findMaxProduct(arr2, n, k) + "</br>");

</script>
```

**输出:**

```
4608
720
80
```

本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。