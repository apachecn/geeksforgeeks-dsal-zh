# 两个数组乘积的最小和

> 原文:[https://www . geesforgeks . org/mini-sum-product-two-arrays/](https://www.geeksforgeeks.org/minimum-sum-product-two-arrays/)

假设第一个数组允许 k 次修改，求两个相同大小数组乘积的最小和。在每次修改中，第一个数组的一个数组元素可以增加或减少 2。
示例:

```
Input : a[] = {1, 2, -3}
        b[]  = {-2, 3, -5}
           k = 5
Output : -31
Explanation:
Here n = 3 and k = 5\. 
So, we modified a[2], which is -3 and 
increased it by 10 (as 5 modifications 
are allowed).
Final sum will be :
(1 * -2) + (2 * 3) + (7 * -5)
   -2    +    6    -    35
             -31
(which is the minimum sum of the array 
with given conditions)

Input : a[] = {2, 3, 4, 5, 4}
        b[] = {3, 4, 2, 3, 2}
Output : 25
Explanation: 
Here, total numbers are 5 and total 
modifications allowed are 3\. So, modify 
a[1], which is 3 and decreased it by 6 
(as 3 modifications are allowed).
Final sum will be :
(2 * 3) + (-3 * 4) + (4 * 2) + (5 * 3) + (4 * 2)
   6    –    12    +    8    +    15   +    8
                        25
(which is the minimum sum of the array with 
given conditions)
```

因为我们需要最小化乘积和，所以我们找到最大乘积并减少它。通过举一些例子，我们观察到只对一个元素做 2*k 的改变就足以得到最小和。基于这一观察，我们认为每个元素都是我们应用所有 k 操作的元素，并跟踪将结果减少到最小的元素。

## C++

```
// CPP program to find minimum sum of product
// of two arrays with k operations allowed on
// first array.
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum product
int minproduct(int a[], int b[], int n, int k)
{
    int diff = 0, res = 0;
    int temp;
    for (int i = 0; i < n; i++) {

        // Find product of current elements and update
        // result.
        int pro = a[i] * b[i];
        res = res + pro;

        // If both product and b[i] are negative,
        // we must increase value of a[i] to minimize
        // result.
        if (pro < 0 && b[i] < 0)
            temp = (a[i] + 2 * k) * b[i];

        // If both product and a[i] are negative,
        // we must decrease value of a[i] to minimize
        // result.
        else if (pro < 0 && a[i] < 0)
            temp = (a[i] - 2 * k) * b[i];

        // Similar to above two cases for positive
        // product.
        else if (pro > 0 && a[i] < 0)
            temp = (a[i] + 2 * k) * b[i];
        else if (pro > 0 && a[i] > 0)
            temp = (a[i] - 2 * k) * b[i];

        // Check if current difference becomes higher
        // than the maximum difference so far.
        int d = abs(pro - temp);
        if (d > diff)
            diff = d;       
    }

    return res - diff;
}

// Driver function
int main()
{
    int a[] = { 2, 3, 4, 5, 4 };
    int b[] = { 3, 4, 2, 3, 2 };
    int n = 5, k = 3;
    cout << minproduct(a, b, n, k)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum sum
// of product of two arrays with k
// operations allowed on first array.
import java.math.*;

class GFG {

// Function to find the minimum product
static int minproduct(int a[], int b[], int n,
                                       int k)
{
    int diff = 0, res = 0;
    int temp = 0;
    for (int i = 0; i < n; i++) {

        // Find product of current elements
        // and update result.
        int pro = a[i] * b[i];
        res = res + pro;

        // If both product and b[i] are
        // negative, we must increase value
        // of a[i] to minimize result.
        if (pro < 0 && b[i] < 0)
            temp = (a[i] + 2 * k) * b[i];

        // If both product and a[i] are
        // negative, we must decrease value
        // of a[i] to minimize result.
        else if (pro < 0 && a[i] < 0)
            temp = (a[i] - 2 * k) * b[i];

        // Similar to above two cases
        // for positive product.
        else if (pro > 0 && a[i] < 0)
            temp = (a[i] + 2 * k) * b[i];
        else if (pro > 0 && a[i] > 0)
            temp = (a[i] - 2 * k) * b[i];

        // Check if current difference
        // becomes higher than the maximum
        // difference so far.
        int d = Math.abs(pro - temp);
        if (d > diff)
            diff = d;    
    }

    return res - diff;
}

// Driver function
public static void main(String[] args)
{
    int a[] = { 2, 3, 4, 5, 4 };
    int b[] = { 3, 4, 2, 3, 2 };
    int n = 5, k = 3;
    System.out.println(minproduct(a, b, n, k));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python program to find
# minimum sum of product
# of two arrays with k
# operations allowed on
# first array.

# Function to find the minimum product
def minproduct(a,b,n,k):

    diff = 0
    res = 0
    for i in range(n):

        # Find product of current
        # elements and update result.
        pro = a[i] * b[i]
        res = res + pro

        # If both product and
        # b[i] are negative,
        # we must increase value
        # of a[i] to minimize result.
        if (pro < 0 and b[i] < 0):
            temp = (a[i] + 2 * k) * b[i]

        # If both product and
        # a[i] are negative,
        # we must decrease value
        # of a[i] to minimize result.
        elif (pro < 0 and a[i] < 0):
            temp = (a[i] - 2 * k) * b[i]

        # Similar to above two cases
        # for positive product.
        elif (pro > 0 and a[i] < 0):
            temp = (a[i] + 2 * k) * b[i]
        elif (pro > 0 and a[i] > 0):
            temp = (a[i] - 2 * k) * b[i]

        # Check if current difference
        # becomes higher
        # than the maximum difference so far.
        d = abs(pro - temp)

        if (d > diff):
            diff = d      
    return res - diff

# Driver function
a = [ 2, 3, 4, 5, 4 ]
b = [ 3, 4, 2, 3, 2 ]
n = 5
k = 3

print(minproduct(a, b, n, k))

# This code is contributed
# by Azkia Anam.
```

## C#

```
// C# program to find minimum sum
// of product of two arrays with k
// operations allowed on first array.
using System;

class GFG {

    // Function to find the minimum product
    static int minproduct(int []a, int []b,
                                int n, int k)
    {
        int diff = 0, res = 0;
        int temp = 0;
        for (int i = 0; i < n; i++)
        {

            // Find product of current elements
            // and update result.
            int pro = a[i] * b[i];
            res = res + pro;

            // If both product and b[i] are
            // negative, we must increase value
            // of a[i] to minimize result.
            if (pro < 0 && b[i] < 0)
                temp = (a[i] + 2 * k) * b[i];

            // If both product and a[i] are
            // negative, we must decrease value
            // of a[i] to minimize result.
            else if (pro < 0 && a[i] < 0)
                temp = (a[i] - 2 * k) * b[i];

            // Similar to above two cases
            // for positive product.
            else if (pro > 0 && a[i] < 0)
                temp = (a[i] + 2 * k) * b[i];
            else if (pro > 0 && a[i] > 0)
                temp = (a[i] - 2 * k) * b[i];

            // Check if current difference
            // becomes higher than the maximum
            // difference so far.
            int d = Math.Abs(pro - temp);
            if (d > diff)
                diff = d;
        }

        return res - diff;
    }

    // Driver function
    public static void Main()
    {
        int []a = { 2, 3, 4, 5, 4 };
        int []b = { 3, 4, 2, 3, 2 };
        int n = 5, k = 3;

        Console.WriteLine(minproduct(a, b, n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum sum of product
// of two arrays with k operations allowed on
// first array.

// Function to find the minimum product
function minproduct( $a, $b, $n, $k)
{
    $diff = 0; $res = 0;
    $temp;
    for ( $i = 0; $i < $n; $i++) {

        // Find product of current
        // elements and update
        // result.
        $pro = $a[$i] * $b[$i];
        $res = $res + $pro;

        // If both product and b[i]
        // are negative, we must
        // increase value of a[i]
        // to minimize result.
        if ($pro < 0 and $b[$i] < 0)
            $temp = ($a[$i] + 2 * $k) *
                                 $b[$i];

        // If both product and
        // a[i] are negative,
        // we must decrease value
        // of a[i] to minimize
        // result.
        else if ($pro < 0 and $a[$i] < 0)
            $temp = ($a[$i] - 2 * $k) * $b[$i];

        // Similar to above two
        // cases for positive
        // product.
        else if ($pro > 0 and $a[$i] < 0)
            $temp = ($a[$i] + 2 * $k) * $b[$i];
        else if ($pro > 0 and $a[$i] > 0)
            $temp = ($a[$i] - 2 * $k) * $b[$i];

        // Check if current difference becomes higher
        // than the maximum difference so far.
        $d = abs($pro - $temp);
        if ($d > $diff)
            $diff = $d;
    }

    return $res - $diff;
}

    // Driver Code
    $a = array(2, 3, 4, 5, 4 ,0);
    $b =array(3, 4, 2, 3, 2);
    $n = 5;
    $k = 3;
    echo minproduct($a, $b, $n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum sum
// of product of two arrays with k
// operations allowed on first array.

// Function to find the minimum product
function minproduct(a, b, n, k)
{
    let diff = 0, res = 0;
    let temp = 0;
    for (let i = 0; i < n; i++)
    {

        // Find product of current elements
        // and update result.
        let pro = a[i] * b[i];
        res = res + pro;

        // If both product and b[i] are
        // negative, we must increase value
        // of a[i] to minimize result.
        if (pro < 0 && b[i] < 0)
            temp = (a[i] + 2 * k) * b[i];

        // If both product and a[i] are
        // negative, we must decrease value
        // of a[i] to minimize result.
        else if (pro < 0 && a[i] < 0)
            temp = (a[i] - 2 * k) * b[i];

        // Similar to above two cases
        // for positive product.
        else if (pro > 0 && a[i] < 0)
            temp = (a[i] + 2 * k) * b[i];
        else if (pro > 0 && a[i] > 0)
            temp = (a[i] - 2 * k) * b[i];

        // Check if current difference
        // becomes higher than the maximum
        // difference so far.
        let d = Math.abs(pro - temp);
        if (d > diff)
            diff = d;   
    }

    return res - diff;
}

// Driver code
        let a = [ 2, 3, 4, 5, 4 ];
    let b = [ 3, 4, 2, 3, 2 ];
    let n = 5, k = 3;
    document.write(minproduct(a, b, n, k));

   // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
25
```

本文由 **Abhishek Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。