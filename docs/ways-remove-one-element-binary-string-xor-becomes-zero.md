# 从二进制字符串中删除一个元素，使异或变为零的方法

> 原文:[https://www . geesforgeks . org/way-remove-one-element-binary-string-xor-变成-zero/](https://www.geeksforgeeks.org/ways-remove-one-element-binary-string-xor-becomes-zero/)

给定一个二进制字符串，任务是恰好擦除数组中的一个整数，以便剩余数字的异或为零。任务是计算移除一个元素的方法数量，以便该字符串的异或变成零。
**例:**

```
Input : 10000
Output : 1
We only have 1 ways to 

Input : 10011
Output : 3
There are 3 ways to make XOR 0\. We
can remove any of the three 1's.

Input : 100011100
Output : 5
There are 5 ways to make XOR 0\. We
can remove any of the give 0's
```

一个**简单的解决方法**就是一个个去掉一个元素，然后计算剩余字符串的异或。并计算移除元素使异或为 0 的出现次数。
一个**高效的解决方案**是基于以下事实。如果 1 的计数是奇数，那么我们必须移除 1 以使计数为 0，并且我们可以移除任何 1。如果 1 的计数是偶数，那么异或是 0，我们可以删除任何 0，异或将保持 0。

## C++

```
// C++ program to count number of ways to
// remove an element so that XOR of remaining
// string becomes 0.
#include <bits/stdc++.h>
using namespace std;

// Return number of ways in which XOR become ZERO
// by remove 1 element
int xorZero(string str)
{
    int one_count = 0, zero_count = 0;
    int n = str.length();

    // Counting number of 0 and 1
    for (int i = 0; i < n; i++)
        if (str[i] == '1')
            one_count++;
        else
            zero_count++;

    // If count of ones is even
    // then return count of zero
    // else count of one
    if (one_count % 2 == 0)
        return zero_count;
    return one_count;
}

// Driver Code
int main()
{
    string str = "11111";
    cout << xorZero(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways to
// remove an element so that XOR of remaining
// string becomes 0.
import java.util.*;

class CountWays
{
    // Returns number of ways in which XOR become
    // ZERO by remove 1 element
    static int xorZero(String s)
    {
        int one_count = 0, zero_count = 0;
        char[] str=s.toCharArray();
        int n = str.length;

        // Counting number of 0 and 1
        for (int i = 0; i < n; i++)
            if (str[i] == '1')
                one_count++;
            else
                zero_count++;

        // If count of ones is even
        // then return count of zero
        // else count of one
        if (one_count % 2 == 0)
            return zero_count;
        return one_count;
    }

    // Driver Code to test above function
    public static void main(String[] args)
    {
        String s = "11111";
        System.out.println(xorZero(s)); 
    }
}

// This code is contributed by Mr. Somesh Awasthi
```

## 蟒蛇 3

```
# Python 3 program to count number of
# ways to remove an element so that
# XOR of remaining string becomes 0.

# Return number of ways in which XOR
# become ZERO by remove 1 element
def xorZero(str):
    one_count = 0
    zero_count = 0
    n = len(str)

    # Counting number of 0 and 1
    for i in range(0, n, 1):
        if (str[i] == '1'):
            one_count += 1
        else:
            zero_count += 1

    # If count of ones is even
    # then return count of zero
    # else count of one
    if (one_count % 2 == 0):
        return zero_count
    return one_count

# Driver Code
if __name__ == '__main__':
    str = "11111"
    print(xorZero(str))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count number
// of ways to remove an element
// so that XOR of remaining
// string becomes 0.
using System;

class GFG
{
    // Returns number of ways
    // in which XOR become
    // ZERO by remove 1 element
    static int xorZero(string s)
    {
        int one_count = 0,
            zero_count = 0;

        int n = s.Length;

        // Counting number of 0 and 1
        for (int i = 0; i < n; i++)
            if (s[i] == '1')
                one_count++;
            else
                zero_count++;

        // If count of ones is even
        // then return count of zero
        // else count of one
        if (one_count % 2 == 0)
            return zero_count;
        return one_count;
    }

    // Driver Code
    public static void Main()
    {
        string s = "11111";
        Console.WriteLine(xorZero(s));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of ways to remove an element
// so that XOR of remaining
// string becomes 0.

// Return number of ways in
// which XOR become ZERO
// by remove 1 element

function xorZero($str)
{
    $one_count = 0; $zero_count = 0;
    $n = strlen($str);

    // Counting number of 0 and 1
    for ($i = 0; $i < $n; $i++)
        if ($str[$i] == '1')
            $one_count++;
        else
            $zero_count++;

    // If count of ones is even
    // then return count of zero
    // else count of one
    if ($one_count % 2 == 0)
        return $zero_count;
    return $one_count;
}

// Driver Code
$str = "11111";
echo xorZero($str),"\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript program to count number
    // of ways to remove an element
    // so that XOR of remaining
    // string becomes 0.

    // Returns number of ways
    // in which XOR become
    // ZERO by remove 1 element
    function xorZero(s)
    {
        let one_count = 0, zero_count = 0;

        let n = s.length;

        // Counting number of 0 and 1
        for (let i = 0; i < n; i++)
            if (s[i] == '1')
                one_count++;
            else
                zero_count++;

        // If count of ones is even
        // then return count of zero
        // else count of one
        if (one_count % 2 == 0)
            return zero_count;
        return one_count;
    }

    let s = "11111";
      document.write(xorZero(s));

</script>
```

**输出:**

```
5
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。