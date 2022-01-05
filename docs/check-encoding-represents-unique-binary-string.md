# 检查编码是否代表唯一的二进制字符串

> 原文:[https://www . geesforgeks . org/check-encoding-representative-unique-binary-string/](https://www.geeksforgeeks.org/check-encoding-represents-unique-binary-string/)

给定一个长度为 k 的二进制字符串的编码，任务是找出给定的编码是否唯一地标识了一个二进制字符串。编码包含连续 1 的计数(由 0 分隔)。
例如，11111 的编码为{5}，01101010 的编码为{2，1，1}，111011 的编码为{3，2}。
**例:**

```
Input: encoding[] = {3, 3, 3} 
       Length, k = 12 
Output: No

Explanation: There are more than one possible 
binary strings. The strings are 111011101110
and 011101110111\. Hence “No” 

Input: encoding[] = {3, 3, 2} 
       Length, k = 10 
Output: Yes

Explanation: There is only one possible encoding 
that is 1110111011
```

一种**天真的方法**是取一个空字符串，遍历 n 个整数到编码【0】中给定的 1 个数，然后加 1 个零，然后编码【1】个 1，最后检查字符串长度是否等于 k，然后打印“是”或打印“否”
一种**有效的方法**是将所有 n 个整数相加， 然后加上(n-1)求和，检查它是否等于 K，因为 n-1 将是每 1 之间的零的数量。检查求和是否等于 K，以得到正好一个字符串，否则有更多或没有。

## C++

```
// C++ program to check if given encoding
// represents a single string.
#include <bits/stdc++.h>
using namespace std;

bool isUnique(int a[], int n, int k)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    sum += n - 1;

    // Return true if sum becomes k
    return (sum == k);
}

// Driver Code
int main()
{

int a[] = {3, 3, 3};
int n = sizeof(a) / sizeof(a[0]);
int k = 12;
if (isUnique(a, n, k))
    cout << "Yes";
else
    cout << "No";
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given encoding
// represents a single string.
import java.io.*;

class GFG
{
    static boolean isUnique(int []a, int n, int k)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += a[i];

        sum += n - 1;

        // Return true if sum becomes k
        return (sum == k);
    }

    // Driver Code
    static public void main (String[] args)
    {
        int []a = {3, 3, 3};
        int n = a.length;
        int k = 12;
        if (isUnique(a, n, k))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to check if given
# encoding represents a single string.

def isUnique(a, n, k):
    sum = 0
    for i in range(0, n, 1):
        sum += a[i]

    sum += n - 1

    # Return true if sum becomes k
    return (sum == k)

# Driver Code
if __name__ == '__main__':
    a = [3, 3, 3]
    n = len(a)
    k = 12
    if (isUnique(a, n, k)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surndra_Gangwar
```

## C#

```
// C# program to check if given encoding
// represents a single string.
using System;

class GFG
{
    static bool isUnique(int []a, int n, int k)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += a[i];

        sum += n - 1;

        // Return true if sum becomes k
        return (sum == k);
    }

    // Driver Code
    static public void Main ()
    {
        int []a = {3, 3, 3};
        int n = a.Length;
        int k = 12;
        if (isUnique(a, n, k))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if given encoding
// represents a single string

function isUnique( $a, $n, $k)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $a[$i];

    $sum += $n - 1;

    // Return true if
    // sum becomes k
    return ($sum == $k);
}

// Driver Code
$a = array(3, 3, 3);
$n = count($a);
$k = 12;
if (isUnique($a, $n,$k))
    echo"Yes";
else
    echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to check if given encoding
// represents a single string.
    function isUnique(a , n , k)
    {
        var sum = 0;
        for (i = 0; i < n; i++)
            sum += a[i];

        sum += n - 1;

        // Return true if sum becomes k
        return (sum == k);
    }

    // Driver Code
        var a = [ 3, 3, 3 ];
        var n = a.length;
        var k = 12;
        if (isUnique(a, n, k))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
No
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。