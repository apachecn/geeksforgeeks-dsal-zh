# 给定两个字符串的前缀和后缀的字符串

> 原文:[https://www . geesforgeks . org/由给定两个字符串的前缀和后缀组成的字符串/](https://www.geeksforgeeks.org/string-from-prefix-and-suffix-of-given-two-strings/)

给定两个字符串 **a** 和 **b** ，通过组合字符串 **a** 的前缀和字符串 **b** 的后缀，从这些字符串中形成长度为 l 的新字符串。
**举例:**

```
Input : string a = remuneration
        string b = acquiesce
        length of pre/suffix(l) = 5
Output :remuniesce

Input : adulation
        obstreperous
        6
Output :adulatperous
```

**进场:**
1。获取字符串 a 的前 l 个字母，字符串 b 的最后 l 个字母
2。将两个结果结合起来，这将是结果字符串。

## C++

```
// CPP code to form new string from
// pre/suffix of given strings.
#include<bits/stdc++.h>
using namespace std;

// Returns a string which contains first l
// characters of 'a' and last l characters of 'b'.
string GetPrefixSuffix(string a, string b, int l)
{
    // Getting prefix of first
    // string of given length
    string prefix = a.substr(0, l);

    // length of string b
    int lb = b.length();

    // Calculating suffix of second string
    string suffix = b.substr(lb - l);

    // Concatenating both prefix and suffix
    return (prefix + suffix);
}

// Driver code
int main()
{
    string a = "remuneration" ,
           b = "acquiesce";
    int l = 5;
    cout << GetPrefixSuffix(a, b, l);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to form new string
// from pre/suffix of given strings
import java.io.*;

class GFG
{
    // Returns a string which contains first l
    // characters of 'a' and last l characters of 'b'.
    public static String prefixSuffix(String a,
                                      String b,
                                      int l)
    {
        // Calculating prefix of first
        // string of given length
        String prefix = a.substring(0, l);
        int lb = b.length();

        // Calculating suffix of second
        // string of given length
        String suffix = b.substring(lb - l);
        return (prefix + suffix);
    }

    // Driver code
    public static void main(String args[])
                            throws IOException
    {
        String a = "remuneration" ,
               b = "acquiesce";
        int l = 5;
        System.out.println(prefixSuffix(a, b, l));
    }
}
```

## 蟒蛇 3

```
# Python code to form new from
# pre/suffix of given strings.

# Returns a string which contains first l
# characters of 'a' and last l characters of 'b'.
def GetPrefixSuffix(a, b, l):
    # Getting prefix of first
    # of given length
    prefix = a[: l];

    # length of string b
    lb = len(b);

    # Calculating suffix of second string
    suffix = b[lb - l:];

    # Concatenating both prefix and suffix
    return (prefix + suffix);

# Driver code
a = "remuneration";
b = "acquiesce";
l = 5;
print(GetPrefixSuffix(a, b, l));

# This code contributed by Rajput-Ji
```

## C#

```
// C# Program to form new string
// from pre/suffix of given strings.
using System;

class GFG
{
    // Returns a string which contains first l
    // characters of 'a' and last l characters of 'b'.
    public static String prefixSuffix(String a,
                                      String b,
                                      int l)
    {
        // Calculating prefix of first
        // string of given length
        String prefix = a.Substring(0, l);
        int lb = b.Length;

        // Calculating suffix of second
        // string of given length
        String suffix = b.Substring(lb - l);
        return (prefix + suffix);
    }

    // Driver Code
    public static void Main()
    {
        String a = "remuneration" ,
               b = "acquiesce";
        int l = 5;
        Console.Write(prefixSuffix(a, b, l));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to form new string from
// pre/suffix of given strings.

// Returns a string which contains
// first l characters of 'a' and
// last l characters of 'b'.
function GetPrefixSuffix($a, $b, $l)
{

    // Getting prefix of first
    // string of given length
    $prefix = substr($a, 0, $l);

    // length of string b
    $lb = strlen($b);

    // Calculating suffix of
    // second string
    $suffix = substr($b, $lb - $l);

    // Concatenating both
    // prefix and suffix
    return ($prefix.$suffix);
}

    // Driver code
    $a = "remuneration";
    $b = "acquiesce";
    $l = 5;
    echo GetPrefixSuffix($a, $b, $l);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript Program to form new string
// from pre/suffix of given strings

// Returns a string which contains first l
// characters of 'a' and last l characters of 'b'.
function prefixSuffix(a, b, l)
{
    // Calculating prefix of first
    // string of given length
    var prefix = a.substring(0, l);
    var lb = b.length;

    // Calculating suffix of second
    // string of given length
    var suffix = b.substring(lb - l);
    return (prefix + suffix);
}

// Driver code

var a = "remuneration" ,
        b = "acquiesce";
 var l = 5;
 document.write(prefixSuffix(a, b, l));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
remuniesce
```