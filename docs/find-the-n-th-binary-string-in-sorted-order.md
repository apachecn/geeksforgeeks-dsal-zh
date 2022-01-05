# 按照排序顺序找到第 n 个二进制字符串

> 原文:[https://www . geesforgeks . org/find-the-n-th-binary-string-in-sorted-order/](https://www.geeksforgeeks.org/find-the-n-th-binary-string-in-sorted-order/)

给定一个正整数 **n** ，任务是在以下两个符号 **a** 和 **b** 上的所有可能字符串的无限列表中找到第 **n <sup>第</sup>个**个字符串，这两个符号按字典顺序排序。

> a、b、aa、ab、ba、bb、aaa、aab、aba、abb、baa、bab、bbb、yyyy、……

**示例:**

> **输入:**n = 6
> T3】输出: bb
> 
> **输入:**n = 11
> T3】输出:咩

一种**简单的方法**是生成直到 **n** 的所有字符串，然后确定 **n <sup>th</sup>** 字符串。然而，该方法不适用于大数值的 **n** 。

一种**有效的方法**是基于这样的事实，即使用 2 个符号可以生成的长度为 k 的字符串的数量是**2<sup>k</sup>T5。基于此，我们可以根据列表中字符串长度的实际索引(n)来计算相对索引。当列表被排序时，在第 **n <sup>个</sup>** 索引处的字符串可以很容易地使用相对索引的二进制形式来确定。以下公式用于计算，**

> 相对指数= n+1–2<sup>楼层(原木(n+1))</sup>T2】

**考虑以下示例:**

> 让 **n = 11** 然后**楼(原木(n + 1)) = 3** 。
> 这表明索引 **n** 由长度为 3 的字符串组成，长度为 3 的字符串从**(2<sup>3</sup>–1)=第 7 个索引**和第 7 个索引包含字符串“aaa”。
> 因此，**相对指数= 11+1–2<sup>3</sup>= 4**。
> 这是相对于 **7** 的指数。现在，索引 **n = 11** 处的字符串可以简单地从相对索引 **4** 的二进制解释中获得。
> 此处 **0** 表示**a****1**表示 **b** 。下表说明了这一点:

<figure class="table">

| 相对指数 | 二进制的 | 线 |
| --- | --- | --- |
| Zero | 000 | 美国汽车协会 |
| one | 001 | 飞机失事管理局 |
| Two | 010 | 阿伯 |
| three | 011 | 横丝 |
| **4** | **100** | **咩** |
| five | One hundred and one | 巴布（女子名） |
| six | One hundred and ten | 工商管理学学士 |
| seven | One hundred and eleven | 血脑屏障 |

</figure>

因此，出现在第 11 个索引(**相对索引 4** )的字符串是“baa”

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the nth string in the required sequence
string obtain_str(ll n)
{

    // Length of the resultant string
    ll len = (int)log2(n + 1);

    // Relative index
    ll rel_ind = n + 1 - pow(2, len);

    ll i = 0;
    string str = "";
    for (i = 0; i < len; i++) {

        // Initial string of length len consists of
        // all a's since the list is sorted
        str += 'a';
    }

    i = 0;

    // Convert relative index to Binary form and set
    // 0 = a and 1 = b
    while (rel_ind > 0) {
        if (rel_ind % 2 == 1)
            str[i] = 'b';
        rel_ind /= 2;
        i++;
    }

    // Reverse and return the string
    reverse(str.begin(), str.end());
    return str;
}

// Driver function
int main()
{
    ll n = 11;
    cout << obtain_str(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the above approach
import java.io.*;
import java.util.*;
class Gfg {

    // Function to return the nth string in the required sequence
    static String obtain_str(int n)
    {
        // Length of the resultant string
        int len = (int)Math.floor((Math.log(n + 1) / Math.log(2)));

        // Relative Index
        int rel_ind = n + 1 - (int)Math.pow(2, len);

        int i = 0;
        StringBuilder str = new StringBuilder();
        for (i = 0; i < len; i++) {

            // Initial string of length len consists of
            // all a's since the list is sorted
            str.append('a');
        }

        i = 0;

        // Convert relative index to Binary form and set
        // 0 = a and 1 = b
        while (rel_ind > 0) {
            if (rel_ind % 2 == 1)
                str.setCharAt(i, 'b');
            rel_ind /= 2;
            i++;
        }

        // Reverse and return the string
        str = str.reverse();
        return str.toString();
    }

    // Driver function
    public static void main(String args[])
    {
        int n = 11;
        System.out.print(obtain_str(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# from math lib import log2 function
from math import log2

# Function to return the nth string
# in the required sequence
def obtain_str(n) :

    # Length of the resultant string
    length = int(log2(n + 1))

    # Relative index
    rel_ind = n + 1 - pow(2, length)

    i = 0
    string = ""

    for i in range(length) :

        # Initial string of length len consists
        # of all a's since the list is sorted
        string += 'a'

    i = 0

    string_list = list(string)

    # Convert relative index to Binary
    # form and set 0 = a and 1 = b
    while (rel_ind > 0) :
        if (rel_ind % 2 == 1) :
            string_list[i] = 'b'

        rel_ind //= 2
        i += 1

    # Reverse and return the string
    string_list.reverse()
    string = "".join(string_list)

    return string

# Driver Code
if __name__ == "__main__" :

    n = 11
    print(obtain_str(n))

# This code is contributed by Ryuga
```

## C#

```
// C# Implementation of the above approach
using System;
using System.Text;

class GFG
{

    // Function to return the nth string
    // in the required sequence
    static String obtain_str(int n)
    {
        // Length of the resultant string
        int len = (int)Math.Floor((Math.Log(n + 1) /
                                    Math.Log(2)));

        // Relative Index
        int rel_ind = n + 1 - (int)Math.Pow(2, len);

        int i = 0;
        StringBuilder str = new StringBuilder();
        for (i = 0; i < len; i++)
        {

            // Initial string of length len consists of
            // all a's since the list is sorted
            str.Append('a');
        }

        i = 0;

        // Convert relative index to Binary form and set
        // 0 = a and 1 = b
        while (rel_ind > 0)
        {
            if (rel_ind % 2 == 1)
                str[i]='b';
            rel_ind /= 2;
            i++;
        }

        // Reverse and return the string
        return reverse(str.ToString());
    }

    static String reverse(String input)
    {
        char[] a = input.ToCharArray();
        int l, r = a.Length - 1;
        for (l = 0; l < r; l++, r--)
        {
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.Join("", a);
    }

    // Driver function
    public static void Main(String []args)
    {
        int n = 11;
        Console.Write(obtain_str(n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the nth string
// in the required sequence
function obtain_str($n)
{

    // Length of the resultant string
    $len = (int)(log($n + 1) / log(2));

    // Relative index
    $rel_ind = $n + 1 - pow(2, $len);

    $i = 0;
    $str = "";
    for ($i = 0; $i < $len; $i++)
    {

        // Initial string of length len
        // consists of all a's since the
        // list is sorted
        $str .= 'a';
    }

    $i = 0;

    // Convert relative index to Binary
    // form and set 0 = a and 1 = b
    while ($rel_ind > 0)
    {
        if ($rel_ind % 2 == 1)
            $str[$i] = 'b';
        $rel_ind = (int)($rel_ind / 2);
        $i++;
    }

    // Reverse and return the string
    return strrev($str);
}

// Driver Code
$n = 11;
echo obtain_str($n);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript Implementation of the above approach

// Function to return the nth string
// in the required sequence
function obtain_str(n)
{

    // Length of the resultant string
    let len = Math.floor((Math.log(n + 1) /
                          Math.log(2)));

    // Relative Index
    let rel_ind = n + 1 - Math.pow(2, len);

    let i = 0;
    let str = [];

    for(i = 0; i < len; i++)
    {

        // Initial string of length len consists of
        // all a's since the list is sorted
        str.push('a');
    }

    i = 0;

    // Convert relative index to Binary
    // form and set 0 = a and 1 = b
    while (rel_ind > 0)
    {
        if (rel_ind % 2 == 1)
            str[i]='b';

        rel_ind = parseInt(rel_ind / 2, 10);
        i++;
    }

    // Reverse and return the string
    return reverse(str.join(""));
}

function reverse(input)
{
    let a = input.split('');
    let l, r = a.length - 1;

    for(l = 0; l < r; l++, r--)
    {
        let temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return a.join("");
}

// Driver code
let n = 11;

document.write(obtain_str(n));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
baa
```