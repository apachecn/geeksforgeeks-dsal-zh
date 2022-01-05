# 找到一个字符串的字典上最大的回文子序列

> 原文:[https://www . geeksforgeeks . org/find-按字典顺序排列的最大回文串子序列/](https://www.geeksforgeeks.org/find-the-lexicographically-largest-palindromic-subsequence-of-a-string/)

给一根绳子![S   ](img/f409421b1f2ffe66c34db63c9be7eba9.png "Rendered by QuickLaTeX.com")。任务是找到作为回文的字符串的字典上最大的子序列。
**例:**

```
Input : str = "abrakadabra"
Output : rr

Input : str = "geeksforgeeks"
Output : ss
```

这个想法是观察一个字符 **a** 如果它的 ASCII 值大于 **b** 的 ASCII 值，那么这个字符在字典上被认为比一个字符 **b** 大。
由于字符串必须是回文，字符串应该只包含最大的字符，就好像我们在第一个和最后一个字符之间放置任何其他较小的字符，那么它将使字符串在字典上更小。
要找到字典上最大的子序列，首先找到给定字符串中最大的字符，并将其在原始字符串中出现的所有字符追加，以形成结果子序列字符串。
以下是上述方法的实施:

## C++

```
// CPP program to find the largest
// palindromic subsequence

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// palindromic subsequence
string largestPalinSub(string s)
{
    string res;

    char mx = s[0];

    // Find the largest character
    for (int i = 1; i < s.length(); i++)
        mx = max(mx, s[i]);

    // Append all occurrences of largest character
    // to the resultant string
    for (int i = 0; i < s.length(); i++)
        if (s[i] == mx)
            res += s[i];

    return res;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";

    cout << largestPalinSub(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest
// palindromic subsequence
class GFG
{

// Function to find the largest
// palindromic subsequence
static String largestPalinSub(String s)
{
    String res = "";
    char mx = s.charAt(0);

    // Find the largest character
    for (int i = 1; i < s.length(); i++)
        mx = (char)Math.max((int)mx,
                  (int)s.charAt(i));

    // Append all occurrences of largest
    // character to the resultant string
    for (int i = 0; i < s.length(); i++)
        if (s.charAt(i) == mx)
            res += s.charAt(i);

    return res;
}

// Driver Code
public static void main(String []args)
{
    String s = "geeksforgeeks";
    System.out.println(largestPalinSub(s));
}
}

// This code is contributed by
// Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program to find the largest
# palindromic subsequence

# Function to find the largest
# palindromic subsequence
def largestPalinSub(s):

    res = ""
    mx = s[0]

    # Find the largest character
    for i in range(1, len(s)):
        mx = max(mx, s[i])

    # Append all occurrences of largest
    # character to the resultant string
    for i in range(0, len(s)):
        if s[i] == mx:
            res += s[i]

    return res

# Driver Code
if __name__ == "__main__":

    s = "geeksforgeeks"
    print(largestPalinSub(s))

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program to find the largest
// palindromic subsequence
using System;

class GFG
{

    // Function to find the largest
    // palindromic subsequence
    static string largestPalinSub(string s)
    {
        string res = "";
        char mx = s[0];

        // Find the largest character
        for (int i = 1; i < s.Length; i++)
            mx = (char)Math.Max((int)mx,
                    (int)s[i]);

        // Append all occurrences of largest
        // character to the resultant string
        for (int i = 0; i < s.Length; i++)
            if (s[i] == mx)
                res += s[i];

        return res;
    }

    // Driver Code
    public static void Main()
    {
        string s = "geeksforgeeks";
        Console.WriteLine(largestPalinSub(s));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to find the largest
// palindromic subsequence

// Function to find the largest
// palindromic subsequence
function largestPalinSub($s)
{
    $res="";

    $mx = $s[0];

    // Find the largest character
    for ($i = 1; $i < strlen($s); $i++)
    {
        $mx = max($mx, $s[$i]);

    }

    // Append all occurrences of largest character
    // to the resultant string
    for ($i = 0; $i < strlen($s); $i++)
    {
        if ($s[$i] == $mx)
        {
            $res.=$s[$i];
        }
    }

    return $res;
}

// Driver Code
$s = "geeksforgeeks";
echo(largestPalinSub($s));

// This code is contributed by princiraj1992
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find the largest
    // palindromic subsequence

    // Function to find the largest
    // palindromic subsequence
    function largestPalinSub(s)
    {
        let res = "";
        let mx = s[0];

        // Find the largest character
        for (let i = 1; i < s.length; i++)
            mx = String.fromCharCode(Math.max(mx.charCodeAt(),
            s[i].charCodeAt()));

        // Append all occurrences of largest
        // character to the resultant string
        for (let i = 0; i < s.length; i++)
            if (s[i] == mx)
                res += s[i];

        return res;
    }

    let s = "geeksforgeeks";
      document.write(largestPalinSub(s));

</script>
```

**Output:** 

```
ss
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。
**辅助空间:** O(1)