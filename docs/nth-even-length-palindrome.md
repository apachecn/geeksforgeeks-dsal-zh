# 第 n 个偶数长度回文

> 原文:[https://www.geeksforgeeks.org/nth-even-length-palindrome/](https://www.geeksforgeeks.org/nth-even-length-palindrome/)

给定一个 n 为字符串的数，求第 n 个偶数长度的正回文数。

**示例:**

```
Input : n = "1"
Output : 11
1st even-length palindrome is 11 .

Input : n = "10"
Output : 1001
The first 10 even-length palindrome numbers are 11, 22, 
33, 44, 55, 66, 77, 88, 99 and 1001.
```

因为它是一个偶数长度的回文，所以它的前半部分应该等于后半部分的倒数，长度是 2，4，6，8 …为了计算第 n 个回文，让我们看看第 10 个偶数长度的回文数字 11，22，33，44，55，66，77，88，99 和 1001。这里，**第 n 个回文是 nn '其中 n '是 n** 的反义词。**因此我们只需要以连续的方式写 n 和 n ’,其中 n’是 n 的反义词**。

下面是这个方法的实现。

## C++

```
// C++ program to find n=th even length string.
#include <bits/stdc++.h>
using namespace std;

// Function to find nth even length Palindrome
string evenlength(string n)
{
    // string r to store resultant
    // palindrome. Initialize same as s
    string res = n;

    // In this loop string r stores
    // reverse of string s after the
    // string s in consecutive manner .
    for (int j = n.length() - 1; j >= 0; --j)
        res += n[j];

    return res;
}

// Driver code
int main()
{
    string n = "10";

    // Function call
    cout << evenlength(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth even length Palindrome
import java.io.*;

class GFG
{
    // Function to find nth even length Palindrome
    static String evenlength(String n)
    {
        // string r to store resultant
        // palindrome. Initialize same as s
        String res = n;

        // In this loop string r stores
        // reverse of string s after the
        // string s in consecutive manner
        for (int j = n.length() - 1; j >= 0; --j)
            res += n.charAt(j);

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String n = "10";

        // Function call
        System.out.println(evenlength(n));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to find n=th even
# length string.
import math as mt

# Function to find nth even length
# Palindrome

def evenlength(n):

    # string r to store resultant
    # palindrome. Initialize same as s
    res = n

    # In this loop string r stores
    # reverse of string s after the
    # string s in consecutive manner .
    for j in range(len(n) - 1, -1, -1):
        res += n[j]

    return res

# Driver code
n = "10"

# Function call
print(evenlength(n))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to find nth even
// length Palindrome
using System;

class GFG {

    // Function to find nth even
    // length Palindrome
    static string evenlength(string n)
    {

        // string r to store resultant
        // palindrome. Initialize same
        // as s
        string res = n;

        // In this loop string r stores
        // reverse of string s after
        // the string s in consecutive
        // manner
        for (int j = n.Length - 1; j >= 0; --j)
            res += n[j];

        return res;
    }

    // Driver code
    public static void Main()
    {
        string n = "10";

        // Function call
        Console.WriteLine(evenlength(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n=th even length string.

// Function to find nth even length Palindrome
function evenlength($n)
{
    // string r to store resultant
    // palindrome. Initialize same as s
    $res = $n;

    // In this loop string r stores
    // reverse of string s after the
    // string s in consecutive manner .
    for ($j = strlen($n) - 1; $j >= 0; --$j)
        $res = $res . $n[$j];

    return $res;
}

// Driver code
$n = "10";

// Function call
echo evenlength($n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find nth even length Palindrome

    // Function to find nth even length Palindrome
    function evenlength(n)
    {
        // string r to store resultant
        // palindrome. Initialize same as s
        let res = n;

        // In this loop string r stores
        // reverse of string s after the
        // string s in consecutive manner
        for (let j = n.length - 1; j >= 0; --j)
            res += n[j];

        return res;
    }

    // Driver code
    let n = "10";
    // Function call
    document.write(evenlength(n));

    //This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
1001
```

**时间复杂度:** O(n)

本文由 **Surya Priy** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。