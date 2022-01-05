# 一个产品数组拼图|集合 2 (O(1)空间)

> 原文:[https://www . geesforgeks . org/product-array-拼图-set-2-o1-space/](https://www.geeksforgeeks.org/product-array-puzzle-set-2-o1-space/)

给定 n 个整数的数组 arr[]，构造一个乘积数组 prod[](大小相同)，使得 prod[i]等于 arr[]除 arr[i]之外的所有元素的乘积。求解**无除法运算符**且在 O(n)中。
T3】例:

```
Input: arr[] = {10, 3, 5, 6, 2}
Output: prod[] = {180, 600, 360, 300, 900}
The elements of output array are 
{3*5*6*2, 10*5*6*2, 10*3*6*2, 
10*3*5*2, 10*3*5*6}

Input: arr[] = {1, 2, 1, 3, 4}
Output: prod[] = {24, 12, 24, 8, 6}
The elements of output array are 
{3*4*1*2, 1*1*3*4, 4*3*2*1, 
1*1*4*2, 1*1*3*2}
```

在 [A 产品数组拼图|第 1 集](https://www.geeksforgeeks.org/a-product-array-puzzle/)中已经讨论了 O(n)方法。前面的方法使用额外的 O(n)空间来构建产品数组。
**<u>解决方案 1:</u>** 使用原木属性。
**方法:**在这篇文章中，讨论了一种更好的方法，该方法使用 log 属性来查找数组中除特定索引外的所有元素的乘积。这种方法不使用额外的空间。
*利用对数的性质乘以大数*

```
x = a * b * c * d
log(x) = log(a * b * c * d)
log(x) = log(a) + log(b) + log(c) + log(d)
x = antilog(log(a) + log(b) + log(c) + log(d))
```

所以思路很简单，
遍历数组，找到所有元素的 log 之和，

```
log(a[0]) + log(a[1]) + 
.. + log(a[n-1])
```

然后再次遍历数组，用这个公式找到乘积。

```
antilog((log(a[0]) + log(a[1]) +
 .. + log(a[n-1])) - log(a[i]))
```

这等于除了 a[i]之外的所有元素的乘积，即反对数(和对数(a[i])。

## C++

```
// C++ program for product array puzzle
// with O(n) time and O(1) space.
#include <bits/stdc++.h>
using namespace std;

// epsilon value to maintain precision
#define EPS 1e-9

void productPuzzle(int a[], int n)
{
    // to hold sum of all values
    long double sum = 0;
    for (int i = 0; i < n; i++)
        sum += (long double)log10(a[i]);

    // output product for each index
    // antilog to find original product value
    for (int i = 0; i < n; i++)
        cout << (int)(EPS + pow((long double)10.00,
                                sum - log10(a[i])))
             << " ";
}

// Driver code
int main()
{
    int a[] = { 10, 3, 5, 6, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << "The product array is: \n";
    productPuzzle(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for product array puzzle
// with O(n) time and O(1) space.
public class Array_puzzle_2 {

    // epsilon value to maintain precision
    static final double EPS = 1e-9;

    static void productPuzzle(int a[], int n)
    {
        // to hold sum of all values
        double sum = 0;
        for (int i = 0; i < n; i++)
            sum += Math.log10(a[i]);

        // output product for each index
        // anti log to find original product value
        for (int i = 0; i < n; i++)
            System.out.print(
                (int)(EPS
                      + Math.pow(
                            10.00, sum
                                       - Math.log10(a[i])))
                + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = { 10, 3, 5, 6, 2 };
        int n = a.length;
        System.out.println("The product array is: ");
        productPuzzle(a, n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program for product array puzzle
# with O(n) time and O(1) space.

import math

# epsilon value to maintain precision
EPS = 1e-9

def productPuzzle(a, n):

    # to hold sum of all values
    sum = 0
    for i in range(n):
        sum += math.log10(a[i])

    # output product for each index
    # antilog to find original product value
    for i in range(n):
        print int((EPS + pow(10.00, sum - math.log10(a[i])))),

    return

# Driver code
a = [10, 3, 5, 6, 2 ]
n = len(a)
print "The product array is: "
productPuzzle(a, n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program for product
// array puzzle with O(n)
// time and O(1) space.
using System;
class GFG {

    // epsilon value to
    // maintain precision
    static double EPS = 1e-9;

    static void productPuzzle(int[] a,
                              int n)
    {
        // to hold sum of all values
        double sum = 0;
        for (int i = 0; i < n; i++)
            sum += Math.Log10(a[i]);

        // output product for each
        // index anti log to find
        // original product value
        for (int i = 0; i < n; i++)
            Console.Write((int)(EPS + Math.Pow(10.00, sum - Math.Log10(a[i]))) + " ");
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 10, 3, 5, 6, 2 };
        int n = a.Length;
        Console.WriteLine("The product array is: ");
        productPuzzle(a, n);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for product array puzzle
// with O(n) time and O(1) space.

// epsilon value to maintain precision
$EPS=1e-9;

function productPuzzle($a, $n)
{
    global $EPS;
    // to hold sum of all values
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += (double)log10($a[$i]);

    // output product for each index
    // antilog to find original product value
    for ($i = 0; $i < $n; $i++)
        echo (int)($EPS + pow((double)10.00, $sum - log10($a[$i])))." ";
}

// Driver code

    $a = array(10, 3, 5, 6, 2 );
    $n = count($a);
    echo "The product array is: \n";
    productPuzzle($a, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program for product array puzzle
// with O(n) time and O(1) space.

// epsilon value to maintain precision
var EPS = 1e-9;

function productPuzzle(a , n)
{
    // to hold sum of all values
    var sum = 0;
    for (var i = 0; i < n; i++)
        sum += Math.log10(a[i]);

    // output product for each index
    // anti log to find original product value
    for (var i = 0; i < n; i++)
        document.write(
            parseInt((EPS
                  + Math.pow(
                        10.00, sum
                                   - Math.log10(a[i]))))
            + " ");
}

// Driver code
var a = [ 10, 3, 5, 6, 2 ];
var n = a.length;
document.write("The product array is: ");
productPuzzle(a, n);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
The product array is: 
180 600 360 300 900
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要两次遍历数组。
*   **空间复杂度:** O(1)。
    不需要额外空间。

*这种方法是由 Abhishek Rajput 贡献的。*
**替代方法:**这里有另一种方法通过使用 pow()函数来解决上述问题，不使用除法，在 O(n)时间内有效。
遍历数组，找到数组中所有元素的乘积。将产品存储在变量中。
然后再次遍历数组，使用公式(乘积*幂(a[i]，-1))找到除该数之外的所有元素的乘积

## C++

```
// C++ program for product array puzzle
// with O(n) time and O(1) space.
#include <bits/stdc++.h>
using namespace std;

// Solve function which prints the answer
void solve(int arr[], int n)
{

    // Initialize a variable to store the
    // total product of the array elements
    int prod = 1;
    for (int i = 0; i < n; i++)
        prod *= arr[i];

    // we know x/y mathematically is same
    // as x*(y to power -1)
    for (int i = 0; i < n; i++) {
        cout << (int)(prod * pow(arr[i], -1)) << ' ';
    }
}

// Driver Code
int main()
{
    int arr[] = { 10, 3, 5, 6, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    solve(arr, n);
    return 0;
}

// This code is contributed by Sitesh Roy
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for product array puzzle
// with O(n) time and O(1) space.
public class ArrayPuzzle {

    static void solve(int arr[], int n)
    {
        // Initialize a variable to store the
        // total product of the array elements
        int prod = 1;
        for (int i = 0; i < n; i++)
            prod *= arr[i];

        // we know x/y mathematically is same
        // as x*(y to power -1)
        for (int i = 0; i < n; i++)
            System.out.print(
                (int)prod * Math.pow(arr[i], -1) + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 10, 3, 5, 6, 2 };
        int n = arr.length;
        solve(arr, n);
    }
}
// This code is contributed by Sitesh Roy
```

## 蟒蛇 3

```
# Python program for product array puzzle
# with O(n) time and O(1) space.
def solve(arr, n):

    # Initialize a variable to store the
    # total product of the array elements
    prod = 1
    for i in arr:
        prod *= i

    # we know x / y mathematically is same
    # as x*(y to power -1)
    for i in arr:
        print(int(prod*(i**-1)), end =" ")

# Driver Code
arr = [10, 3, 5, 6, 2]
n = len(arr)
solve(arr, n)

# This code is contributed by Sitesh Roy
```

## C#

```
// C# program for product array puzzle
// with O(n) time and O(1) space.
using System;

class GFG {

public
    class ArrayPuzzle {

        static void solve(int[] arr, int n)
        {
            // Initialize a variable to store the
            // total product of the array elements
            int prod = 1;
            for (int i = 0; i < n; i++)
                prod *= arr[i];

            // we know x/y mathematically is same
            // as x*(y to power -1)
            for (int i = 0; i < n; i++)
                Console.Write(
                    (int)prod * Math.Pow(arr[i], -1) + " ");
        }

        // Driver code
        static public void Main()
        {
            int[] arr = { 10, 3, 5, 6, 2 };
            int n = arr.Length;
            solve(arr, n);
        }
    }
}
// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for product array puzzle
// with O(n) time and O(1) space.

    function solve(arr, n)
    {
        // Initialize a variable to store the
        // total product of the array elements
        let prod = 1;
        for (let i = 0; i < n; i++)
            prod *= arr[i];

        // we know x/y mathematically is same
        // as x*(y to power -1)
        for (let i = 0; i < n; i++)
            document.write(
                prod * Math.pow(arr[i], -1) + " ");
    }

// Driver program
        let arr = [10, 3, 5, 6, 2 ];
        let n = arr.length;
        solve(arr, n);

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
180 600 360 300 900
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要两次遍历数组。
*   **空间复杂度:** O(1)。
    不需要额外空间。

**注意:这种方法假设数组元素不是 0。**
这个方法是由 [**斯特什罗伊**](https://https://auth.geeksforgeeks.org/user/sitesh221b/) 给出的。
如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。