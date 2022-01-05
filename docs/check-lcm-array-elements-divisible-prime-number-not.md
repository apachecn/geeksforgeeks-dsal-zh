# 检查数组元素的 LCM 是否能被素数整除

> 原文:[https://www . geesforgeks . org/check-LCM-array-elements-整除-质数-not/](https://www.geeksforgeeks.org/check-lcm-array-elements-divisible-prime-number-not/)

给定一个数组和一个数 k，任务是找出数组的 LCM 是否能被 k 整除。
**例:**

```
Input : int[] a = {10, 20, 15, 25}
              k = 3
Output : true

Input : int[] a = {24, 21, 45, 57, 36};
              k = 23;
Output : false
```

一个简单的解决方法是首先[找到数组元素](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)的 LCM，然后检查 LCM 是否能被 k 整除。
在这里，不计算数的 LCM，我们可以发现一个数的数组的 LCM 可以被素数 k 整除，也可以不被素数 k 整除。如果数组中的任意一个数可以被素数 k 整除，那么这个数的 LCM 也可以被素数 k 整除

## C++

```
// C++ program to find LCM of
// array of number is divisible
// by a prime number k or not
#include<iostream>
using namespace std;

// Function to check any number of
// array is divisible by k or not
bool func(int a[], int k, int n)
{
    // If any array element is divisible
    // by k, then LCM of whole array
    // should also be divisible.
    for (int i = 0; i < n; i++)
        if (a[i] % k == 0)
        return true;
    return false;
}

// Driver Code
int main()
{
    int a[] = {14, 27, 38, 76, 84};
    int k = 19;
    bool res = func(a, k, 5);
    if(res)
    cout<<"true";
    else
    cout<<"false";
    return 0;
}

// This code is contributed
// by Mr. Somesh Awasthi
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCM of
// array of number is divisible
// by a prime number k or not
import java.lang.*;
import java.util.*;

class GFG
{
    // Function to check any number
    // of array is divisible by k or not
    static boolean func( int a[], int k)
    {
        // If any array element is divisible
        // by k, then LCM of whole array
        // should also be divisible.
        for (int i = 0; i < a.length; i++)
            if (a[i] % k == 0)
            return true;
        return false;
    }

    // Driver Code
    public static void main(String args[])
    {
        int[] a = {14, 27, 38, 76, 84};
        int k = 19;
        boolean res = func(a, k);
        System.out.println(res);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find LCM
# of array of number is divisible
# by a prime number k or not

# Function to check any number of
# array is divisible by k or not
def func( a, k, n) :

    # If any array element is
    # divisible by k, then LCM
    # of whole array should also
    # be divisible.
    for i in range(0, n) :
        if ( a[i] % k == 0):
            return True

# Driver Code
a = [14, 27, 38, 76, 84]
k = 19
res = func(a, k, 5)

if(res) :
    print("true")
else :
    print("false")

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find LCM of array
// of number is divisible by a prime
// number k or not
using System;

class GFG
{

    // Function to check any number of
    // array is divisible by k or not
    static bool func(int []a, int k)
    {

        // If any array element is
        // divisible by k, then LCM
        // of whole array should also
        // be divisible.
        for (int i = 0; i < a.Length; i++)
            if (a[i] % k == 0)
            return true;
        return false;
    }

    // Driver code
    public static void Main()
    {
        int []a = {14, 27, 38, 76, 84};
        int k = 19;
        bool res = func(a, k);
        Console.Write(res);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find LCM of
// array of number is divisible
// by a prime number k or not

// Function to check any number of
// array is divisible by k or not
function func( $a, $k, $n)
{
    // If any array element is divisible
    // by k, then LCM of whole array
    // should also be divisible.
    for ($i = 0; $i < $n; $i++)
        if ($a[$i] % $k == 0)
        return true;
    return false;
}

// Driver Code
$a = array(14, 27, 38, 76, 84);
$k = 19;
$res = func($a, $k, 5);

if($res)
echo"true";
else
echo"false";

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// javascript program to find LCM of
// array of number is divisible
// by a prime number k or not

    // Function to check any number
    // of array is divisible by k or not
    function func(a , k)
    {

        // If any array element is divisible
        // by k, then LCM of whole array
        // should also be divisible.
        for (let i = 0; i < a.length; i++)
            if (a[i] % k == 0)
                return true;
        return false;
    }

    // Driver Code

        let a = [ 14, 27, 38, 76, 84 ];
        var k = 19;
        let res = func(a, k);
        document.write(res);

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
 true
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。