# 检查二进制字符串是否包含连续的相同内容

> 原文:[https://www . geesforgeks . org/check-if-a-binary-string-contains-continuous-同或不同/](https://www.geeksforgeeks.org/check-if-a-binary-string-contains-consecutive-same-or-not/)

给定一个二进制字符串**字符串**，由字符**“0”**和**“1”**组成。任务是找出字符串是否有效。只有当字符是交替的，即没有两个连续的字符相同时，字符串才有效。
**举例:**

> **输入:** str[] = "010101"
> **输出:**有效
> **输入:** str[] = "010010"
> **输出:**无效

**方法:**开始逐字符遍历字符串，如果有任意两个相等的连续字符，则打印**无效**否则最终打印**有效**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true is str is valid
bool isValid(string str, int len)
{

    // Assuming the string is binary
    // If any two consecutive characters are equal
    // then the string is invalid
    for (int i = 1; i < len; i++) {
        if (str[i] == str[i - 1])
            return false;
    }

    // If the string is alternating
    return true;
}

// Driver code
int main()
{
    string str = "0110";
    int len = str.length();

    if (isValid(str, len))
        cout << "Valid";
    else
        cout << "Invalid";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class gfg
{

// Function that returns true is str is valid
static boolean isValid(String str, int len)
{

    // Assuming the string is binary
    // If any two consecutive
    // characters are equal
    // then the string is invalid
    for (int i = 1; i < len; i++)
    {
        if (str.charAt(i) == str.charAt(i - 1))
            return false;
    }

    // If the string is alternating
    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "0110";
    int len = str.length();

    if (isValid(str, len))
        System.out.println("Valid");
    else
        System.out.println("Invalid");
}
}

// This code is Contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true is str is valid
def isValid(string, length):

    # Assuming the string is binary
    # If any two consecutive characters
    # are equal then the string is invalid
    for i in range(1, length):
        if string[i] == string[i - 1]:
            return False

    # If the string is alternating
    return True

# Driver code
if __name__ == "__main__":

    string = "0110"
    length = len(string)

    if isValid(string, length):
        print("Valid")
    else:
        print("Invalid")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class gfg
{

// Function that returns true is str is valid
static bool isValid(string str, int len)
{

    // Assuming the string is binary
    // If any two consecutive
    // characters are equal
    // then the string is invalid
    for (int i = 1; i < len; i++)
    {
        if (str[i] == str[i - 1])
            return false;
    }

    // If the string is alternating
    return true;
}

// Driver code
public static void Main()
{
    string str = "0110";
    int len = str.Length;

    if (isValid(str, len))
        Console.Write("Valid");
    else
        Console.Write("Invalid");
}
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true is str is valid
function isValid($str, $len)
{

    // Assuming the string is binary
    // If any two consecutive characters
    // are equal then the string is invalid
    for ($i = 1; $i < $len; $i++)
    {
        if ($str[$i] == $str[$i - 1])
            return false;
    }

    // If the string is alternating
    return true;
}

// Driver code
$str = "0110";
$len = strlen($str);

if (isValid($str, $len))
    echo "Valid";
else
    echo "Invalid";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true is str is valid
function isValid(str,len)
{
    // Assuming the string is binary
    // If any two consecutive
    // characters are equal
    // then the string is invalid
    for (let i = 1; i < len; i++)
    {
        if (str[i] == str[i - 1])
            return false;
    }

    // If the string is alternating
    return true;
}

// Driver code
let str = "0110";
let len = str.length;

if (isValid(str, len))
    document.write("Valid");
else
    document.write("Invalid");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Invalid
```