# 检查‘n’个数字的乘积是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-n-numbers 的乘积是偶数还是奇数/](https://www.geeksforgeeks.org/check-whether-product-of-n-numbers-is-even-or-odd/)

给定一个包含 **n** 个数字的数组 **arr[]** 。问题是检查给定的 **n** 数的乘积是偶数还是奇数。
**举例:**

```
Input : arr[] = {2, 4, 3, 5}
Output : Even
Product = 2 * 4 * 3 * 5 = 120

Input : arr[] = {3, 9, 7, 1}
Output : Odd
```

一个**简单的解决方法**就是先找到乘积，然后检查乘积是偶数还是奇数。这种解决方案会导致大型数组溢出。
更好的解决方案基于以下数学计算事实:

1.  两个偶数的乘积是偶数。
2.  两个奇数的乘积是奇数。
3.  一个偶数和一个奇数的乘积是偶数。

基于以上事实，如果单个偶数出现，那么 **n 个**数的乘积将是偶数，否则是奇数。

## C++

```
// C++ implementation to check whether product of
// 'n' numbers is even or odd
#include <bits/stdc++.h>

using namespace std;

// function to check whether product of
// 'n' numbers is even or odd
bool isProductEven(int arr[], int n)
{
    for (int i = 0; i < n; i++)

        // if a single even number is found, then
        // final product will be an even number
        if ((arr[i] & 1) == 0)
            return true;

    // product is an odd number
    return false;
}

// Driver program to test above
int main()
{
    int arr[] = { 2, 4, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isProductEven(arr, n))
        cout << "Even";
    else
        cout << "Odd";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether product of
// 'n' numbers is even or odd

public class GFG {

    // function to check whether product of
    // 'n' numbers is even or odd
    static boolean isProductEven(int arr[], int n)
    {
        for (int i = 0; i < n; i++)

            // if a single even number is found, then
            // final product will be an even number
            if ((arr[i] & 1) == 0)
                return true;

        // product is an odd number
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
            int arr[] = { 2, 4, 3, 5 };
            int n = arr.length ;
            if (isProductEven(arr, n))
                System.out.println("Even");
            else
                System.out.println("Odd") ;     
    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 implementation to
# check whether product of 'n'
# numbers is even or odd

# function to check whether
# product of 'n' numbers is
# even or odd
def isProductEven(arr, n):

    for i in range(0, n):

        # if a single even number is
        # found, then final product
        # will be an even number
        if ((arr[i] & 1) == 0):
            return True

    # product is an odd number
    return False

# Driver Code
arr = [ 2, 4, 3, 5 ]
n = len(arr)
if (isProductEven(arr, n)):
    print("Even")
else:
    print("Odd")

# This code is contributed
# by ihritik
```

## C#

```
// C# implementation to check
// whether product of 'n'
// numbers is even or odd
using System;

class GFG
{

// function to check whether
// product of 'n' numbers
// is even or odd
static bool isProductEven(int []arr, int n)
{
    for (int i = 0; i < n; i++)

        // if a single even number is
        // found, then final product
        // will be an even number
        if ((arr[i] & 1) == 0)
            return true;

    // product is an odd number
    return false;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 4, 3, 5 };
    int n = arr.Length;
    if (isProductEven(arr, n))
        Console.WriteLine("Even");
    else
        Console.WriteLine("Odd") ;
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether product of 'n' numbers
// is even or odd

// function to check whether
// product of 'n' numbers is
// even or odd
function isProductEven($arr, $n)
{
    for ($i = 0; $i < $n; $i++)

        // if a single even number is
        // found, then final product
        // will be an even number
        if (($arr[$i] & 1) == 0)
            return true;

    // product is an odd number
    return false;
}

// Driver code
$arr = array( 2, 4, 3, 5 );
$n = sizeof($arr);
if (isProductEven($arr, $n))
    echo "Even";
else
    echo "Odd";

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// JavaScript implementation to check whether product of
// 'n' numbers is even or odd

// function to check whether product of
// 'n' numbers is even or odd
function isProductEven(arr, n)
{
    for (let i = 0; i < n; i++)

        // if a single even number is found, then
        // final product will be an even number
        if ((arr[i] & 1) == 0)
            return true;

    // product is an odd number
    return false;
}

// Driver program to test above

    let arr = [ 2, 4, 3, 5 ];
    let n = arr.length;
    if (isProductEven(arr, n))
        document.write("Even");
    else
        document.write("Odd");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
Even
```

**时间复杂度:** O(n)。