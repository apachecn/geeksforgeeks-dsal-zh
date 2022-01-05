# 检查给定的字符串是否是 K 周期的

> 原文:[https://www . geeksforgeeks . org/check-if-给定字符串-k-periodic/](https://www.geeksforgeeks.org/check-if-the-given-string-is-k-periodic/)

给定一个字符串 **str** 和一个整数 **K** ，任务是检查给定的字符串是否为 **K 周期**。如果字符串是子字符串**字符串【0…k-1】**的重复，即字符串**“ababab”**是 **2 周期**，则字符串是 k 周期的。打印**是**如果给定字符串是 k 周期的，则打印**否**。

**示例:**

> **输入:** str = "geeksgeeks "，k = 5
> **输出:**是
> 重复长度为 k 的前缀即“geeks”即可生成给定字符串
> 
> **输入:** str = "geeksforgeeks "，k = 3
> **输出:**否

**方式:**从子串**str【k，2k-1】**、**str【2k，3k-1】**等开始，检查这些子串是否都等于长度为 **k** 的串的前缀，即**str【0，k-1】**。如果所有这些子字符串的条件都为真，则打印**是**否则打印**否**。
以下是上述方法的实施:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // Function that return true if sub-string
    // of length k starting at index i is also
    // a prefix of the string
    bool isPrefix(string str, int len, int i, int k)
    {
        // k length sub-string cannot start at index i
        if (i + k > len)
            return false;
        for (int j = 0; j < k; j++)
        {

            // Character mismatch between the prefix
            // and the sub-string starting at index i
            if (str[i] != str[j])
                return false;
            i++;
        }
        return true;
    }

    // Function that returns true if str is K-periodic
    bool isKPeriodic(string str, int len, int k)
    {
        // Check whether all the sub-strings
        // str[0, k-1], str[k, 2k-1] ... are equal
        // to the k length prefix of the string
        for (int i = k; i < len; i += k)
            if (!isPrefix(str, len, i, k))
                return false;
        return true;
    }

    // Driver code
    int main()
    {
        string str = "geeksgeeks";
        int len = str.length();
        int k = 5;

        if (isKPeriodic(str, len, k))
        cout << ("Yes");
        else
        cout << ("No");
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that return true if sub-string
    // of length k starting at index i is also
    // a prefix of the string
    static boolean isPrefix(String str, int len, int i, int k)
    {
        // k length sub-string cannot start at index i
        if (i + k > len)
            return false;
        for (int j = 0; j < k; j++) {

            // Character mismatch between the prefix
            // and the sub-string starting at index i
            if (str.charAt(i) != str.charAt(j))
                return false;
            i++;
        }
        return true;
    }

    // Function that returns true if str is K-periodic
    static boolean isKPeriodic(String str, int len, int k)
    {
        // Check whether all the sub-strings
        // str[0, k-1], str[k, 2k-1] ... are equal
        // to the k length prefix of the string
        for (int i = k; i < len; i += k)
            if (!isPrefix(str, len, i, k))
                return false;
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksgeeks";
        int len = str.length();
        int k = 5;

        if (isKPeriodic(str, len, k))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if sub-string
# of length k starting at index i
# is also a prefix of the string
def isPrefix(string, length, i, k):

    # k length sub-string cannot
    # start at index i
    if i + k > length:
        return False

    for j in range(0, k):

        # Character mismatch between the prefix
        # and the sub-string starting at index i
        if string[i] != string[j]:
            return False
        i += 1

    return True

# Function that returns true if
# str is K-periodic
def isKPeriodic(string, length, k):

    # Check whether all the sub-strings
    # str[0, k-1], str[k, 2k-1] ... are equal
    # to the k length prefix of the string
    for i in range(k, length, k):
        if isPrefix(string, length, i, k) == False:
            return False
    return True

# Driver code
if __name__ == "__main__":

    string = "geeksgeeks"
    length = len(string)
    k = 5

    if isKPeriodic(string, length, k) == True:
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that return true if sub-string
    // of length k starting at index i is also
    // a prefix of the string
    static bool isPrefix(String str, int len, int i, int k)
    {
        // k length sub-string cannot start at index i
        if (i + k > len)
            return false;
        for (int j = 0; j < k; j++)
        {

            // Character mismatch between the prefix
            // and the sub-string starting at index i
            if (str[i] != str[j])
                return false;
            i++;
        }
        return true;
    }

    // Function that returns true if str is K-periodic
    static bool isKPeriodic(String str, int len, int k)
    {
        // Check whether all the sub-strings
        // str[0, k-1], str[k, 2k-1] ... are equal
        // to the k length prefix of the string
        for (int i = k; i < len; i += k)
            if (!isPrefix(str, len, i, k))
                return false;
        return true;
    }

    // Driver code
    public static void Main()
    {
        String str = "geeksgeeks";
        int len = str.Length;
        int k = 5;

        if (isKPeriodic(str, len, k))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that return true if sub-
// of length $k starting at index $i
// is also a prefix of the string
function isPrefix($str, $len, $i, $k)
{

    // $k length sub- cannot start at index $i
    if ($i + $k > $len)
        return false;
    for ( $j = 0; $j < $k; $j++)
    {

        // Character mismatch between the prefix
        // and the sub- starting at index $i
        if ($str[$i] != $str[$j])
            return false;
        $i++;
    }
    return true;
}

// Function that returns true if $str is K-periodic
function isKPeriodic($str, $len, $k)
{
    // Check whether all the sub-strings
    // $str[0, $k-1], $str[$k, 2k-1] ... are equal
    // to the $k length prefix of the
    for ($i = $k; $i < $len; $i += $k)
        if (!isPrefix($str, $len, $i, $k))
            return false;
    return true;
}

// Driver code
$str = "geeksgeeks";
$len = strlen($str);
$k = 5;

if (isKPeriodic($str, $len, $k))
    echo ("Yes");
else
    echo ("No");

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// js implementation of the approach

// Function that return true if sub-string
// of length k starting at index i is also
// a prefix of the string
function isPrefix(str, len, i, k){
    // k length sub-string cannot start at index i
    if (i + k > len)
        return false;
    for (let j = 0; j < k; j++)
    {

        // Character mismatch between the prefix
        // and the sub-string starting at index i
        if (str[i] != str[j])
            return false;
        i++;
    }
    return true;
}

// Function that returns true if str is K-periodic
function isKPeriodic(str, len, k)
{
    // Check whether all the sub-strings
    // str[0, k-1], str[k, 2k-1] ... are equal
    // to the k length prefix of the string
    for (let i = k; i < len; i += k)
        if (!isPrefix(str, len, i, k))
            return false;
    return true;
}

// Driver code

let str = "geeksgeeks";
let len = str.length;
let k = 5;

if (isKPeriodic(str, len, k))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(K * log(len))
**辅助空间:** O(1)