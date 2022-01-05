# 求数组 arr[]

中 ABS(I–j)* min(arr[I]，arr[j])的最大值

> 原文:[https://www . geesforgeks . org/find-absi-j-minari-arrj-in-a-arr/](https://www.geeksforgeeks.org/find-maximum-value-of-absi-j-minarri-arrj-in-an-array-arr/)

给定 n 个不同元素的数组。求数组中两个数的最小值与其位置的绝对差乘积的最大值，即求 ABS(I–j)* min(arr[I]，arr[j])的最大值，其中 I 和 j 从 0 到 n-1 不等。

**示例:**

```
Input : arr[] = {3, 2, 1, 4}
Output: 9
// arr[0] = 3 and arr[3] = 4 minimum of them is 3 and 
// absolute difference between their position is 
// abs(0-3) = 3\. So product is 3*3 = 9

Input : arr[] = {8, 1, 9, 4}
Output: 16
// arr[0] = 8 and arr[2] = 9 minimum of them is 8 and 
// absolute difference between their position is 
// abs(0-2) = 2\. So product is 8*2 = 16 
```

这个问题的一个**简单解法**就是把每个元素一个一个的拿过来，和右边的元素比较。然后计算它们的最小值和它们的指数之间的绝对差的乘积，并使结果最大化。这种方法的时间复杂度是 O(n^2).

一个**有效的解决方案**以线性时间复杂度解决了这个问题。我们取两个迭代器**左=0** 和**右=n-1** ，比较元素 arr[左]和 arr[右]。

```
left = 0, right = n-1
maxProduct = -INF
While (left < right)
    If arr[Left] < arr[right] 
        currProduct = arr[Left]*(right-Left) 
        Left++ . 
    If arr[right] < arr[Left] 
        currProduct = arr[Right]*(Right-Left) 
        Right-- . 

    maxProduct = max(maxProduct, currProduct)
```

以下是上述想法的实现。

## C++

```
// C++ implementation of code
#include<bits/stdc++.h>
using namespace std;

// Function to calculate maximum value of
// abs(i - j) * min(arr[i], arr[j]) in arr[]
int Maximum_Product(int arr[], int n)
{
    int maxProduct = INT_MIN; // Initialize result
    int currProduct; // product of current pair

    // loop  until they meet with each other
    int Left = 0, right = n-1;
    while (Left < right)
    {
        if (arr[Left] < arr[right])
        {
            currProduct = arr[Left]*(right-Left);
            Left++;
        }
        else // arr[right] is smaller
        {
            currProduct = arr[right]*(right-Left);
            right--;
        }

        // maximizing the product
        maxProduct = max(maxProduct, currProduct)
    }

    return maxProduct;
}

// Driver program to test the case
int main()
{
    int arr[] = {8, 1, 9, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << Maximum_Product(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of code
import java.util.*;

class GFG {

    // Function to calculate maximum value of
    // abs(i - j) * min(arr[i], arr[j]) in arr[]
    static int Maximum_Product(int arr[], int n) {

    // Initialize result
    int maxProduct = Integer.MIN_VALUE;

    // product of current pair
    int currProduct;           

    // loop until they meet with each other
    int Left = 0, right = n - 1;
    while (Left < right) {
    if (arr[Left] < arr[right]) {
        currProduct = arr[Left] * (right - Left);
        Left++;
    }

    // arr[right] is smaller
    else
    {
        currProduct = arr[right] * (right - Left);
        right--;
    }

    // maximizing the product
    maxProduct = Math.max(maxProduct, currProduct);
    }

    return maxProduct;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {8, 1, 9, 4};
    int n = arr.length;
    System.out.print(Maximum_Product(arr, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python implementation of code
# Function to calculate
# maximum value of
# abs(i - j) * min(arr[i],
# arr[j]) in arr[]
def Maximum_Product(arr,n):

    # Initialize result
    maxProduct = -2147483648

    # product of current pair
    currProduct=0

    # loop until they meet with each other
    Left = 0
    right = n-1
    while (Left < right):

        if (arr[Left] < arr[right]):

            currProduct = arr[Left]*(right-Left)
            Left+=1

        else:

            # arr[right] is smaller
            currProduct = arr[right]*(right-Left)
            right-=1

        # maximizing the product
        maxProduct = max(maxProduct, currProduct)

    return maxProduct

# Driver code

arr = [8, 1, 9, 4]
n = len(arr)

print(Maximum_Product(arr,n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation of code
using System;

class GFG {

// Function to calculate maximum
// value of abs(i - j) * min(arr[i],
// arr[j]) in arr[]
static int Maximum_Product(int []arr,
                           int n)
{

    // Initialize result
    int maxProduct = int.MinValue;

    // product of current pair
    int currProduct;        

    // loop until they meet
    // with each other
    int Left = 0, right = n - 1;
    while (Left < right) {
    if (arr[Left] < arr[right])
    {
        currProduct = arr[Left] *
                      (right - Left);
        Left++;
    }

    // arr[right] is smaller
    else
    {
        currProduct = arr[right] *
                      (right - Left);
        right--;
    }

    // maximizing the product
    maxProduct = Math.Max(maxProduct,
                          currProduct);
    }

    return maxProduct;
}

// Driver code
public static void Main()
{
    int []arr = {8, 1, 9, 4};
    int n = arr.Length;
    Console.Write(Maximum_Product(arr, n));
}
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of code

// Function to calculate
// maximum value of
// abs(i - j) * min(arr[i],
// arr[j]) in arr[]
function Maximum_Product($arr, $n)
{
    $INT_MIN = 0;

    // Initialize result
    $maxProduct = $INT_MIN;

    // product of current pair
    $currProduct;

    // loop until they meet
    // with each other
    $Left = 0; $right = $n - 1;
    while ($Left < $right)
    {
        if ($arr[$Left] < $arr[$right])
        {
            $currProduct = $arr[$Left] *
                          ($right - $Left);
            $Left++;
        }

        // arr[right] is smaller
        else
        {
            $currProduct = $arr[$right] *
                          ($right - $Left);
            $right--;
        }

        // maximizing the product
        $maxProduct = max($maxProduct,
                          $currProduct);
    }

    return $maxProduct;
}

// Driver Code
$arr = array(8, 1, 9, 4);
$n = sizeof($arr) / sizeof($arr[0]);
echo Maximum_Product($arr, $n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of code

// Function to calculate
// maximum value of
// abs(i - j) * min(arr[i],
// arr[j]) in arr[]
function Maximum_Product(arr, n)
{
    let INT_MIN = 0;

    // Initialize result
    let maxProduct = INT_MIN;

    // Product of current pair
    let currProduct;

    // Loop until they meet
    // with each other
    let Left = 0, right = n - 1;
    while (Left < right)
    {
        if (arr[Left] < arr[right])
        {
            currProduct = arr[Left] *
                 (right - Left);
            Left++;
        }

        // arr[right] is smaller
        else
        {
            currProduct = arr[right] *
                 (right - Left);
            right--;
        }

        // Maximizing the product
        maxProduct = Math.max(maxProduct,
                              currProduct);
    }
    return maxProduct;
}

// Driver Code
let arr = new Array(8, 1, 9, 4);
let n = arr.length;
document.write(Maximum_Product(arr, n));

// This code is contributed by Saurabh Jaiswal

</script>
```

**输出:**

```
 16
```

**这是如何工作的？**
重要的是要表明我们没有错过上面线性算法中的任何潜在对，也就是说，我们需要表明做左++或右——不会导致我们会得到更高 maxProduct 值的情况。
请注意，我们总是与(右-左)相乘。

1)如果当前左边的 arr[left]< arr[right], then smaller values of **right**没有用，因为它们不能产生更高的 maxProduct 值(因为我们用 arr[left]乘以(right–left))。如果 arr[left]大于其左侧的任何元素会怎样。在这种情况下，必须找到具有当前权限的更好的元素对。因此，我们可以安全地增加左，而不会错过任何更好的左电流对。

2)当 arr[右]< arr[左]时，类似的参数也适用。

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。