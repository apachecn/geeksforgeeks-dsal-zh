# 所有可能子集乘积之和

> 原文:[https://www . geeksforgeeks . org/sum-products-可能的子集/](https://www.geeksforgeeks.org/sum-products-possible-subsets/)

给定 n 个非负整数的数组。任务是找到所有可能子集的元素乘积的和。可以假设子集内的数字很小，计算积不会导致算术溢出。
**例:**

```
Input : arr[] = {1, 2, 3}
Output : 23
Possible Subset are: 1, 2, 3, {1, 2}, {1, 3}, 
                     {2, 3}, {1, 2, 3}
Products of elements in above subsets :
1, 2, 3, 2, 3, 6, 6
Sum of all products = 1 + 2 + 3 + 2 + 3 + 6 + 6 
                    = 23
```

**天真法:**简单的方法是[逐个生成所有可能的子集](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)并计算所有元素的和。这种方法的时间复杂度是指数级的，因为总共有 2 个 <sup>n 个</sup>–1 个子集。
一种**有效的方法**是将整个问题归纳成某种模式。假设我们有两个数字 a 和 b。我们可以把所有可能的子集乘积写成:-

```
   = a + b + ab 
   = a(1+b) + b + 1 - 1 
   = a(1+b) + (1+b) - 1 
   = (a + 1) * (b + 1) - 1
   = (1+a) * (1 + b) - 1
```

现在取三个数字 a、b、c:-

```
   = a + b + c + ab + bc + ca + abc 
   = a + ac + b + bc + ab + abc + c + 1 - 1
   = a(1+c) + b(1+c) + ab(1+c) + c + 1 - 1
   = (a + b + ab + 1)(1+c) - 1 
   = (1+a) * (1+b) * (1+c) - 1  
```

上述模式可以推广到 n 个数字。
以下是上述思路的实现:

## C++

```
// C++ program to find sum of product of
// all subsets.
#include <bits/stdc++.h>
using namespace std;

// Returns sum of products of all subsets
// of arr[0..n-1]
int productOfSubsetSums(int arr[], int n)
{
    int ans = 1;
    for (int i = 0; i < n; ++i )
        ans = ans * (arr[i] + 1);
    return ans-1;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4};
    int n = sizeof(arr)/sizeof arr[0];
    cout << productOfSubsetSums(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of product of
// all subsets.

public class Subset
{
    // Returns sum of products of all subsets
    // of arr[0..n-1]
    static int productOfSubsetSums(int arr[], int n)
    {
        int ans = 1;
        for (int i = 0; i < n; ++i )
            ans = ans * (arr[i] + 1);
        return ans-1;
    }

    public static void main (String[] args)
    {
        int arr[] = {1, 2, 3, 4};
        int n = arr.length;
        System.out.println(productOfSubsetSums(arr, n));
    }
}

// This code is contributed by Saket Kumar
```

## 蟒蛇 3

```
# Python3 program to
# find sum of product of
# all subsets.

# Returns sum of products
# of all subsets
# of arr[0..n-1]
def productOfSubsetSums(arr, n):
    ans = 1;
    for i in range(0,n):
        ans = ans * (arr[i] + 1)
    return ans-1

# Driver code
arr = [1, 2, 3, 4]
n = len(arr)

print (productOfSubsetSums(arr, n))

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// C# program to find sum of
// product of all subsets.
using System;

public class Subset
{

    // Returns sum of products of all
    // subsets of arr[0..n-1]
    static int productOfSubsetSums(int []arr, int n)
    {
        int ans = 1;
        for (int i = 0; i < n; ++i )
            ans = ans * (arr[i] + 1);
        return ans-1;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {1, 2, 3, 4};
        int n = arr.Length;
        Console.Write(productOfSubsetSums(arr, n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// product of all subsets.

// Returns sum of products of
// all subsets of arr[0..n-1]
function productOfSubsetSums($arr, $n)
{
    $ans = 1;
    for ($i = 0; $i < $n; ++$i )
        $ans = $ans * ($arr[$i] + 1);
    return $ans-1;
}

// Driver code
$arr = array(1, 2, 3, 4);
$n = sizeof($arr);
echo(productOfSubsetSums($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of product of
// all subsets.

// Returns sum of products of all subsets
// of arr[0..n-1]
function productOfSubsetSums(arr, n)
{
    let ans = 1;
    for (let i = 0; i < n; ++i )
        ans = ans * (arr[i] + 1);
    return ans-1;
}

// Driver code

    let arr = [1, 2, 3, 4];
    let n = arr.length;
    document.write(productOfSubsetSums(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
 119 
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。