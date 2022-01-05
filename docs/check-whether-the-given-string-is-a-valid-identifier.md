# 检查给定的字符串是否是有效的标识符

> 原文:[https://www . geesforgeks . org/check-给定字符串是否是有效标识符/](https://www.geeksforgeeks.org/check-whether-the-given-string-is-a-valid-identifier/)

给定一个字符串 **str** ，任务是检查该字符串是否是有效的标识符。为了符合有效标识符的条件，字符串必须满足以下条件:

1.  它必须以下划线(_) 或范围 **['a '，' z']** 和 **['A '，' Z']** 中的任何字符开头。
2.  字符串中不能有任何空格。
3.  并且，第一个字符之后的所有后续字符不得包含任何特殊字符，如 **$** 、 **#** 、 **%** 等。

**示例:**

> **输入:**str = " 123 geeks 123 "
> **输出:**有效
> **输入:** str = "123geeks_"
> **输出:**无效

**方法:**逐字符遍历字符串，检查是否满足所有要求，使其成为有效标识符，即第一个字符只能是“_”或英文字母，其余字符不得是空格或任何特殊字符。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if str
// is a valid identifier
bool isValid(string str, int n)
{

    // If first character is invalid
    if (!((str[0] >= 'a' && str[0] <= 'z')
          || (str[0] >= 'A' && str[0] <= 'Z')
          || str[0] == '_'))
        return false;

    // Traverse the string for the rest of the characters
    for (int i = 1; i < str.length(); i++) {
        if (!((str[i] >= 'a' && str[i] <= 'z')
              || (str[i] >= 'A' && str[i] <= 'Z')
              || (str[i] >= '0' && str[i] <= '9')
              || str[i] == '_'))
            return false;
    }

    // String is a valid identifier
    return true;
}

// Driver code
int main()
{
    string str = "_geeks123";
    int n = str.length();

    if (isValid(str, n))
        cout << "Valid";
    else
        cout << "Invalid";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if str
// is a valid identifier
static boolean isValid(String str, int n)
{

    // If first character is invalid
    if (!((str.charAt(0) >= 'a' && str.charAt(0) <= 'z')
        || (str.charAt(0)>= 'A' && str.charAt(0) <= 'Z')
        || str.charAt(0) == '_'))
        return false;

    // Traverse the string for the rest of the characters
    for (int i = 1; i < str.length(); i++)
    {
        if (!((str.charAt(i) >= 'a' && str.charAt(i) <= 'z')
            || (str.charAt(i) >= 'A' && str.charAt(i) <= 'Z')
            || (str.charAt(i) >= '0' && str.charAt(i) <= '9')
            || str.charAt(i) == '_'))
            return false;
    }

    // String is a valid identifier
    return true;
}

// Driver code
public static void main(String args[])
{
    String str = "_geeks123";
    int n = str.length();

    if (isValid(str, n))
        System.out.println("Valid");
    else
        System.out.println("Invalid");
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if str1
# is a valid identifier
def isValid(str1, n):

    # If first character is invalid
    if (((ord(str1[0]) >= ord('a') and
          ord(str1[0]) <= ord('z')) or
         (ord(str1[0]) >= ord('A') and
          ord(str1[0]) <= ord('Z')) or
          ord(str1[0]) == ord('_')) == False):
        return False

    # Traverse the for the rest of the characters
    for i in range(1, len(str1)):
        if (((ord(str1[i]) >= ord('a') and
              ord(str1[i]) <= ord('z')) or
             (ord(str1[i]) >= ord('A') and
              ord(str1[i]) <= ord('Z')) or
             (ord(str1[i]) >= ord('0') and
              ord(str1[i]) <= ord('9')) or
              ord(str1[i]) == ord('_')) == False):
            return False

    # is a valid identifier
    return True

# Driver code
str1 = "_geeks123"
n = len(str1)

if (isValid(str1, n)):
    print("Valid")
else:
    print("Invalid")

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if str
// is a valid identifier
static bool isValid(String str, int n)
{
    // If first character is invalid
    if (!((str[0] >= 'a' && str[0] <= 'z')
        || (str[0] >= 'A' && str[0] <= 'Z')
        || str[0] == '_'))
        return false;

    // Traverse the string for the rest of the characters
    for (int i = 1; i < str.Length; i++)
    {
        if (!((str[i] >= 'a' && str[i] <= 'z')
            || (str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= '0' && str[i] <= '9')
            || str[i] == '_'))
            return false;
    }

    // String is a valid identifier
    return true;
}

// Driver code
public static void Main(String []args)
{
    String str = "_geeks123";
    int n = str.Length;

    if (isValid(str, n))
        Console.WriteLine("Valid");
    else
        Console.WriteLine("Invalid");
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if str
// is a valid identifier
function isValid($str, $n)
{

    // If first character is invalid
    if (!(($str[0] >= 'a' && $str[0] <= 'z') ||
          ($str[0] >= 'A' && $str[0] <= 'Z') ||
           $str[0] == '_'))
        return false;

    // Traverse the string
    // for the rest of the characters
    for ($i = 1; $i < strlen($str); $i++)
    {
        if (!(($str[$i] >= 'a' && $str[$i] <= 'z') ||
              ($str[$i] >= 'A' && $str[$i] <= 'Z') ||
              ($str[$i] >= '0' && $str[$i] <= '9') ||
               $str[$i] == '_'))
            return false;
    }

    // String is a valid identifier
    return true;
}

// Driver code
$str = "_geeks123";
$n = strlen($str);

if (isValid($str,$n))
    print("Valid");
else
    print("Invalid");

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true if str
// is a valid identifier
function isValid(str,n)
{
    // If first character is invalid
    if (!((str[0] >= 'a' && str[0] <= 'z')
        || (str[0]>= 'A' && str[0] <= 'Z')
        || str[0] == '_'))
        return false;

    // Traverse the string for the rest of the characters
    for (let i = 1; i < str.length; i++)
    {
        if (!((str[i] >= 'a' && str[i] <= 'z')
            || (str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= '0' && str[i] <= '9')
            || str[i] == '_'))
            return false;
    }

    // String is a valid identifier
    return true;
}

    // Driver code
    let str = "_geeks123";
    let n = str.length;

    if (isValid(str, n))
        document.write("Valid");
    else
        document.write("Invalid");

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Valid
```