# 检查给定字符串串接后是否可以生成给定字符串

> 原文:[https://www . geesforgeks . org/check-给定字符串是否可以在连接给定字符串后生成/](https://www.geeksforgeeks.org/check-whether-given-string-can-be-generated-after-concatenating-given-strings/)

给定三根弦**弦**、 **A** 和 **B** 。任务是检查 **str = A + B** 还是 **str = B + A** ，其中 **+** 表示串联。
**示例:**

> **输入:** str = "GeeksforGeeks "，A = "Geeksfo "，B = "rGeeks"
> **输出:**是
> str = A+B = " Geeksfo "+" rGeeks " = " GeeksforGeeks "
> **输入:** str = "Delhicapitals "，B = "Delmi "，C = "大写"
> **输出:**否

**进场:**

1.  If **len(str)！= len(A) + len(B)** 则不可能通过串联 **a + b** 或 **b + a** 来生成**字符串**。
2.  否则检查**字符串**是以 **a** 开头，以 **b** 结尾，还是以 **b** 开头，以 **a** 结尾。打印**是**如果其中任何一项为真，则打印**否**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true
// if pre is a prefix of str
bool startsWith(string str, string pre)
{
    int strLen = str.length();
    int preLen = pre.length();
    int i = 0, j = 0;

    // While there are characters to match
    while (i < strLen && j < preLen) {

        // If characters differ at any position
        if (str[i] != pre[j])
            return false;
        i++;
        j++;
    }

    // str starts with pre
    return true;
}

// Function that return true
// if suff is a suffix of str
bool endsWith(string str, string suff)
{
    int i = str.length() - 0;
    int j = suff.length() - 0;

    // While there are characters to match
    while (i >= 0 && j >= 0) {

        // If characters differ at any position
        if (str[i] != suff[j])
            return false;
        i--;
        j--;
    }

    // str ends with suff
    return true;
}

// Function that returns true
// if str = a + b or str = b + a
bool checkString(string str, string a, string b)
{

    // str cannot be generated
    // by concatenating a and b
    if (str.length() != a.length() + b.length())
        return false;

    // If str starts with a
    // i.e. a is a prefix of str
    if (startsWith(str, a)) {

        // Check if the rest of the characters
        // are equal to b i.e. b is a suffix of str
        if (endsWith(str, b))
            return true;
    }

    // If str starts with b
    // i.e. b is a prefix of str
    if (startsWith(str, b)) {

        // Check if the rest of the characters
        // are equal to a i.e. a is a suffix of str
        if (endsWith(str, a))
            return true;
    }

    return false;
}

// Driver code
int main()
{
    string str = "GeeksforGeeks";
    string a = "Geeksfo";
    string b = "rGeeks";

    if (checkString(str, a, b))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that return true
// if pre is a prefix of str
static boolean startsWith(String str, String pre)
{
    int strLen = str.length();
    int preLen = pre.length();
    int i = 0, j = 0;

    // While there are characters to match
    while (i < strLen && j < preLen)
    {

        // If characters differ at any position
        if (str.charAt(i) != pre.charAt(j))
            return false;
        i++;
        j++;
    }

    // str starts with pre
    return true;
}

// Function that return true
// if suff is a suffix of str
static boolean endsWith(String str, String suff)
{
    int i = str.length() - 1;
    int j = suff.length() - 1;

    // While there are characters to match
    while (i >= 0 && j >= 0)
    {

        // If characters differ at any position
        if (str.charAt(i) != suff.charAt(j))
            return false;
        i--;
        j--;
    }

    // str ends with suff
    return true;
}

// Function that returns true
// if str = a + b or str = b + a
static boolean checkString(String str, String a, String b)
{

    // str cannot be generated
    // by concatenating a and b
    if (str.length() != a.length() + b.length())
        return false;

    // If str starts with a
    // i.e. a is a prefix of str
    if (startsWith(str, a))
    {

        // Check if the rest of the characters
        // are equal to b i.e. b is a suffix of str
        if (endsWith(str, b))
            return true;
    }

    // If str starts with b
    // i.e. b is a prefix of str
    if (startsWith(str, b))
    {

        // Check if the rest of the characters
        // are equal to a i.e. a is a suffix of str
        if (endsWith(str, a))
            return true;
    }

    return false;
}

// Driver code
public static void main(String args[])
{
    String str = "GeeksforGeeks";
    String a = "Geeksfo";
    String b = "rGeeks";

    if (checkString(str, a, b))
        System.out.println("Yes");
    else
        System.out.println("No");

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that return true
# if pre is a prefix of str
def startsWith(str, pre):
    strLen = len(str)
    preLen = len(pre)
    i = 0
    j = 0

    # While there are characters to match
    while (i < strLen and j < preLen):

        # If characters differ at any position
        if (str[i] != pre[j]) :
            return False
        i += 1
        j += 1

    # str starts with pre
    return True

# Function that return true
# if suff is a suffix of str
def endsWith(str, suff):
    i = len(str) - 1
    j = len(suff) - 1

    # While there are characters to match
    while (i >= 0 and j >= 0):

        # If characters differ at any position
        if (str[i] != suff[j]):
            return False
        i -= 1
        j -= 1

    # str ends with suff
    return True

# Function that returns true
# if str = a + b or str = b + a
def checkString(str, a, b):

    # str cannot be generated
    # by concatenating a and b
    if (len(str) != len(a) + len(b)):
        return False

    # If str starts with a
    # i.e. a is a prefix of str
    if (startsWith(str, a)):

        # Check if the rest of the characters
        # are equal to b i.e. b is a suffix of str
        if (endsWith(str, b)):
            return True

    # If str starts with b
    # i.e. b is a prefix of str
    if (startsWith(str, b)):

        # Check if the rest of the characters
        # are equal to a i.e. a is a suffix of str
        if (endsWith(str, a)):
            return True

    return False

# Driver code
str = "GeeksforGeeks"
a = "Geeksfo"
b = "rGeeks"

if (checkString(str, a, b)):
    print("Yes")
else:
    print("No")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that return true
// if pre is a prefix of str
static Boolean startsWith(String str,
                          String pre)
{
    int strLen = str.Length;
    int preLen = pre.Length;
    int i = 0, j = 0;

    // While there are characters to match
    while (i < strLen && j < preLen)
    {

        // If characters differ at any position
        if (str[i] != pre[j])
            return false;
        i++;
        j++;
    }

    // str starts with pre
    return true;
}

// Function that return true
// if suff is a suffix of str
static Boolean endsWith(String str,
                        String suff)
{
    int i = str.Length - 1;
    int j = suff.Length - 1;

    // While there are characters to match
    while (i >= 0 && j >= 0)
    {

        // If characters differ at any position
        if (str[i] != suff[j])
            return false;
        i--;
        j--;
    }

    // str ends with suff
    return true;
}

// Function that returns true
// if str = a + b or str = b + a
static Boolean checkString(String str,
                           String a,
                           String b)
{

    // str cannot be generated
    // by concatenating a and b
    if (str.Length != a.Length + b.Length)
        return false;

    // If str starts with a
    // i.e. a is a prefix of str
    if (startsWith(str, a))
    {

        // Check if the rest of the characters
        // are equal to b i.e. b is a suffix of str
        if (endsWith(str, b))
            return true;
    }

    // If str starts with b
    // i.e. b is a prefix of str
    if (startsWith(str, b))
    {

        // Check if the rest of the characters
        // are equal to a i.e. a is a suffix of str
        if (endsWith(str, a))
            return true;
    }

    return false;
}

// Driver code
public static void Main(String []args)
{
    String str = "GeeksforGeeks";
    String a = "Geeksfo";
    String b = "rGeeks";

    if (checkString(str, a, b))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that return true
// if pre is a prefix of str
function startsWith($str, $pre)
{
    $strLen = strlen($str);
    $preLen = strlen($pre);
    $i = 0; $j = 0;

    // While there are characters to match
    while ($i < $strLen && $j < $preLen)
    {

        // If characters differ at any position
        if ($str[$i] != $pre[$j])
            return false;
        $i++;
        $j++;
    }

    // str starts with pre
    return true;
}

// Function that return true
// if suff is a suffix of str
function endsWith($str, $suff)
{
    $i = strlen($str)- 0;
    $j = strlen($suff)- 0;

    // While there are characters to match
    while ($i >= 0 && $j >= 0)
    {

        // I$f characters differ at any position
        if ($str[$i] != $suff[$j])
            return false;
        $i--;
        $j--;
    }

    // str ends with suff
    return true;
}

// Function that returns true
// if str = a + b or str = b + a
function checkString($str, $a, $b)
{

    // str cannot be generated
    // by concatenating a and b
    if (strlen($str) != strlen($a) + strlen($b))
        return false;

    // If str starts with a
    // i.e. a is a prefix of str
    if (startsWith($str, $a))
    {

        // Check if the rest of the characters
        // are equal to b i.e. b is a suffix of str
        if (endsWith($str, $b))
            return true;
    }

    // If str starts with b
    // i.e. b is a prefix of str
    if (startsWith($str, $b))
    {

        // Check if the rest of the characters
        // are equal to a i.e. a is a suffix of str
        if (endsWith($str, $a))
            return true;
    }

    return false;
}

// Driver code
$str = "GeeksforGeeks";
$a = "Geeksfo";
$b = "rGeeks";

if (checkString($str, $a, $b))
    echo "Yes";
else
    echo "No";

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function that return true
    // if pre is a prefix of str
    function startsWith(str, pre)
    {
        let strLen = str.length;
        let preLen = pre.length;
        let i = 0, j = 0;

        // While there are characters to match
        while (i < strLen && j < preLen)
        {

            // If characters differ at any position
            if (str[i] != pre[j])
                return false;
            i++;
            j++;
        }

        // str starts with pre
        return true;
    }

    // Function that return true
    // if suff is a suffix of str
    function endsWith(str, suff)
    {
        let i = str.length - 1;
        let j = suff.length - 1;

        // While there are characters to match
        while (i >= 0 && j >= 0)
        {

            // If characters differ at any position
            if (str[i] != suff[j])
                return false;
            i--;
            j--;
        }

        // str ends with suff
        return true;
    }

    // Function that returns true
    // if str = a + b or str = b + a
    function checkString(str, a, b)
    {

        // str cannot be generated
        // by concatenating a and b
        if (str.length != a.length + b.length)
            return false;

        // If str starts with a
        // i.e. a is a prefix of str
        if (startsWith(str, a))
        {

            // Check if the rest of the characters
            // are equal to b i.e. b is a suffix of str
            if (endsWith(str, b))
                return true;
        }

        // If str starts with b
        // i.e. b is a prefix of str
        if (startsWith(str, b))
        {

            // Check if the rest of the characters
            // are equal to a i.e. a is a suffix of str
            if (endsWith(str, a))
                return true;
        }

        return false;
    }

    let str = "GeeksforGeeks";
    let a = "Geeksfo";
    let b = "rGeeks";

    if (checkString(str, a, b))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)