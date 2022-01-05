# 元素在 1 到 n 范围内时不同元素的总和

> 原文:[https://www . geesforgeks . org/sum-distinct-elements-elements-range-1-n/](https://www.geeksforgeeks.org/sum-distinct-elements-elements-range-1-n/)

给定 n 个元素的数组，数组中的每个元素都是 1 到 n 范围内的整数，求数组中所有不同元素的和。

**示例:**

```
Input: arr[] = {5, 1, 2, 4, 6, 7, 3, 6, 7}
Output: 28
The distinct elements in the array are 1, 2, 
3, 4, 5, 6, 7

Input: arr[] = {1, 1, 1}
Output: 1
```

问题在这里已经作为一般问题出现，解决方案也适用于上述情况。但是下面解释了一个更好的方法。
方法是通过使数组元素在这些索引处的元素为负来标记数组元素的出现。例如，a[0] = 1，a[1] = 1，a[2] = 1。
我们检查 a[abs(a[i])-1]是否为> =0，如果是，则将 a[abs(a[i])-1]标记为阴性。即 a[0] = 1 > =0，我们将 a[1-1]标记为 a[0] = -1。接下来，a[1]，检查(abs(a[1]-1)是否为+ve。如果-ve，则表示 a[1]以前已经出现过，否则为该元素的第一次出现。参考以下代码。

## C++

```
// C++ program to find sum of distinct elements
#include <iostream>
using namespace std;

// Returns sum of distinct elements in arr[] assuming
// that elements in a[] are in range from 1 to n.
int sumOfDistinct(int a[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++) {

        // If element appears first time
        if (a[abs(a[i]) - 1] >= 0) {
            sum += abs(a[i]);
            a[abs(a[i]) - 1] *= -1;
        }
    }

    return sum;
}

// Driver code
int main()
{
    int a[] = { 5, 1, 2, 4, 6, 7, 3, 6, 7 };
    int n = sizeof(a)/sizeof(a[0]);
    cout << sumOfDistinct(a, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find sum of distinct
// elements in sorted order
import java.io.*;
import java.util.*;
import java.math.*;

class GFG{

    // Returns sum of distinct elements in arr[]
    // assuming that elements in a[] are in
    // range from 1 to n.
    static int sumOfDistinct(int a[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // If element appears first time
            if (a[Math.abs(a[i]) - 1] >= 0) {
                sum += Math.abs(a[i]);
                a[Math.abs(a[i]) - 1] *= -1;
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = { 5, 1, 2, 4, 6, 7, 3, 6, 7 };
        int n = a.length;
        System.out.println(sumOfDistinct(a, n) );
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to find sum of distinct elements
# in sorted order
import math

# Returns sum of distinct elements in arr[]
# assuming that elements in a[] are in
# range from 1 to n.
def sumOfDistinct(a , n) :
    sum = 0
    i = 0
    while i < n:

        # If element appears first time
        if (a[abs(a[i]) - 1] >= 0) :
            sum = sum + abs(a[i])
            a[abs(a[i]) - 1] = a[abs(a[i]) - 1] * (-1)
        i = i + 1

    return sum;

# Driver code
a = [ 5, 1, 2, 4, 6, 7, 3, 6, 7 ]
n = len(a)
print sumOfDistinct(a, n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find sum of distinct
// elements in sorted order
using System;

class GFG{

    // Returns sum of distinct elements
    // in arr[] assuming that elements
    // in a[] are in range from 1 to n
    static int sumOfDistinct(int []a, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // If element appears first time
            if (a[Math.Abs(a[i]) - 1] >= 0) {
                sum += Math.Abs(a[i]);
                a[Math.Abs(a[i]) - 1] *= - 1;
            }
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int []a = {5, 1, 2, 4, 6, 7, 3, 6, 7};
        int n = a.Length;
        Console.Write(sumOfDistinct(a, n));
    }
}

// This code is contributed by Nitin Mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// distinct elements

// Returns sum of distinct
// elements in arr[] assuming
// that elements in a[] are
// in range from 1 to n.
function sumOfDistinct($a, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // If element appears first time
        if ($a[abs($a[$i]) - 1] >= 0)
        {
            $sum += abs($a[$i]);
            $a[abs($a[$i]) - 1] *= -1;
        }
    }

    return $sum;
}

    // Driver code
    $a = array(5, 1, 2, 4, 6, 7, 3, 6, 7);
    $n = sizeof($a);
    echo sumOfDistinct($a, $n) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// java script  program to find sum of
// distinct elements

// Returns sum of distinct
// elements in arr[] assuming
// that elements in a[] are
// in range from 1 to n.
function sumOfDistinct(a, n)
{
    let sum = 0;
    for (let i = 0; i < n; i++)
    {

        // If element appears first time
        if (a[Math.abs(a[i]) - 1] >= 0) {
                sum += Math.abs(a[i]);
                a[Math.abs(a[i]) - 1] *= -1;
            }
    }

    return sum;
}

    // Driver code
    let a = [5, 1, 2, 4, 6, 7, 3, 6, 7];
    let n = a.length;
    document.write( sumOfDistinct(a, n));

//contributed by bobby

</script>
```

输出:

```
28
```

时间复杂度:O(n)
辅助空间:O(1)
本文由**艾克塔·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。