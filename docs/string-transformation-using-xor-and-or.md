# 使用异或和或的字符串转换

> 原文:[https://www . geesforgeks . org/string-transformation-use-xor-and-or/](https://www.geeksforgeeks.org/string-transformation-using-xor-and-or/)

给定两个二进制字符串。任务是通过多次执行给定的操作来检查字符串 s1 是否可以转换为字符串 s2。

*   选择字符串 s1 中任意两个相邻的字符，用 a^b 替换其中一个，用 a ![\oplus ](img/5344a83929a321ff0ed0387f956956bc.png "Rendered by QuickLaTeX.com") b (a 或 b)替换另一个。

**示例:**

> **输入:**S1 =“11”，S2 =“10”
> **输出:**是
> 选择两个相邻字符，将 s2[0]替换为 s1[0] ![\oplus  ](img/290920f59367bd65a77d4691be9d6c08.png "Rendered by QuickLaTeX.com") s1[1]，将 s2[1]替换为 s1[0]^s1[1]
> **输入:**S1 =“000”，S2 =“101”
> **输出:**否

**方法:**下面给出的表格解释了异或和或运算的所有可能性。

<figure class="table">

| X | Y | X^Y | X ![\oplus  ](img/290920f59367bd65a77d4691be9d6c08.png "Rendered by QuickLaTeX.com") Y |
| --- | --- | --- | --- |
| Zero | Zero | Zero | Zero |
| Zero | one | one | one |
| one | Zero | one | one |
| one | one | Zero | one |

</figure>

如果两个字符串都只包含 0，并且它们的长度相同，那么转换是可能的，因为两个相邻的 0 将只产生 0，而与对它所做的操作无关。如果两个字符串都有 1，请按照以下步骤检查 String1 是否可以转换为 String2。

*   检查长度是否相等
*   检查两个字符串是否都至少为 1，因为如果两个字符串都至少为 1，则所有转换都是可能的，这可以在表中看到

如果以上两个条件都成立，就有可能转换 String1 可以转换为 String2。
以下是上述方法的实施:

## C++

```
// C++ program to check if string1 can be
// converted to string2 using XOR and OR operations
#include <bits/stdc++.h>
using namespace std;

// function to check if conversion is possible or not
bool solve(string s1, string s2)
{
    bool flag1 = 0, flag2 = 0;

    // if lengths are different
    if (s1.length() != s2.length())
        return false;

    int l = s1.length();

    // iterate to check if both strings have 1
    for (int i = 0; i < l; i++) {

        // to check if there is
        // even one 1 in string s1
        if (s1[i] == '1')
            flag1 = 1;

        // to check if there is even
        // one 1 in string s2
        if (s2[i] == '1')
            flag2 = 1;

        if (flag1 && flag2)
            return true;
    }
     //if both strings have only '0'
     if(!flag1&&!flag2)
            return true;
    // if both string do not have a '1'.
    return false;
}

// Driver code
int main()
{
    string s1 = "100101";
    string s2 = "100000";

    if (solve(s1, s2))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// string1 can be converted
// to string2 using XOR and
// OR operations
import java.io.*;
import java.util.*;

class GFG
{

// function to check if
// conversion is possible
// or not
static boolean solve(String s1,
                     String s2)
{
    boolean flag1 = false,
            flag2 = false;

    // if lengths are different
    if (s1.length() != s2.length())
        return false;

    int l = s1.length();

    // iterate to check if
    // both strings have 1
    for (int i = 0; i < l; i++)
    {

        // to check if there is
        // even one 1 in string s1
        if (s1.charAt(i) == '1')
            flag1 = true;

        // to check if there is even
        // one 1 in string s2
        if (s2.charAt(i) == '1')
            flag2 = true;

        if (flag1 == true &&
            flag2 == true)
            return true;
    }
     //if both strings have only '0'
     if(!flag1&&!flag2)
            return true;
    // if both string do
    // not have a '1'.
    return false;
}

// Driver code
public static void main(String args[])
{
    String s1 = "100101";
    String s2 = "100000";

    if (solve(s1, s2) == true)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}
```

## 蟒蛇 3

```
# Python3 program to check
# if string1 can be converted
# to string2 using XOR and
# OR operations

# function to check if
# conversion is possible or not
def solve(s1, s2):
    flag1 = 0
    flag2 = 0

# if lengths are different
    if (len(s1) != len(s2)):
        return False

    l = len(s1)

# iterate to check if
# both strings have 1
    for i in range (0, l):

    # to check if there is
    # even one 1 in string s1
        if (s1[i] == '1'):
            flag1 = 1;

    # to check if there is even
    # one 1 in string s2
        if (s2[i] == '1'):
            flag2 = 1

    # if both string
    # do not have a '1'.
        if (flag1 & flag2):
            return True

        if(!flag1 & !flag2):
            return True
    return False

# Driver code
s1 = "100101"
s2 = "100000"

if solve(s1, s2):
    print( "Yes")
else:
    print("No")

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to check if
// string1 can be converted
// to string2 using XOR and
// OR operations
using System;

class GFG
{

// function to check if
// conversion is possible
// or not
static bool solve(String s1,
                  String s2)
{
    bool flag1 = false,
         flag2 = false;

    // if lengths are different
    if (s1.Length != s2.Length)
        return false;

    int l = s1.Length;

    // iterate to check if
    // both strings have 1
    for (int i = 0; i < l; i++)
    {

        // to check if there is
        // even one 1 in string s1
        if (s1[i] == '1')
            flag1 = true;

        // to check if there is even
        // one 1 in string s2
        if (s2[i] == '1')
            flag2 = true;

        if (flag1 == true &&
            flag2 == true)
            return true;
    }

     //if both strings have only '0'
     if(!flag1&&!flag2)
            return true;
    // if both string do
    // not have a '1'.
    return false;
}

// Driver code
public static void Main()
{
    String s1 = "100101";
    String s2 = "100000";

    if (solve(s1, s2) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if string1
// can be converted to string2
// using XOR and OR operations

// function to check if conversion
// is possible or not
function solve($s1, $s2)
{

    // if lengths are different
    if (strlen($s1) != strlen($s2))
        return false;

    $l = strlen($s1);

    // iterate to check if
    // both strings have 1
    for ($i = 0; $i < 1; $i++)
    {

        // to check if there is
        // even one 1 in string s1
        if ($s1[$i] == '1')
            $flag1 = 1;

        // to check if there is even
        // one 1 in string s2
        if ($s2[$i] == '1')
            $flag2 = 1;

        if (!$flag1 && !$flag2)
            return true;
    }

    // if both string do
    // not have a '1'.
    return false;
}

// Driver code
$s1 = "100101";
$s2 = "100000";

if (solve($s1, $s2))
        echo("Yes");
    else
        echo("No");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to check if string1 can be
// converted to string2 using XOR and OR operations

// function to check if conversion is possible or not
function solve(s1, s2)
{
    let flag1 = 0, flag2 = 0;

    // if lengths are different
    if (s1.length != s2.length)
        return false;

    let l = s1.length;

    // iterate to check if both strings have 1
    for (let i = 0; i < l; i++) {

        // to check if there is
        // even one 1 in string s1
        if (s1[i] == '1')
            flag1 = 1;

        // to check if there is even
        // one 1 in string s2
        if (s2[i] == '1')
            flag2 = 1;

        if (flag1 && flag2)
            return true;
    }
     //if both strings have only '0'
     if(!flag1&&!flag2)
            return true;
    // if both string do not have a '1'.
    return false;
}

// Driver code
    let s1 = "100101";
    let s2 = "100000";

    if (solve(s1, s2))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(n)，其中 n 为输入字符串的长度。