# 用空格替换字符串的所有出现位置

> 原文:[https://www . geesforgeks . org/用空格替换所有出现的字符串/](https://www.geeksforgeeks.org/replace-all-occurrences-of-a-string-with-space/)

给定一个字符串和一个子字符串，任务是用空格替换所有出现的子字符串。我们还需要删除由此产生的尾随空格和前导空格。

**示例:**

> **输入:** str = "LIELIEILIEAMLIECOOL "，sub = "LIE"
> **输出:**我是 COOL
> 通过用空格替换 **Str** 中所有出现的 **Sub** ，我们提取秘密消息为**我是 COOL。**
> 
> **输入:** str = "XYZAXYZBXYZC "，sub = "XYZ"
> **输出:** ABC
> 通过用空格替换 **Str** 中所有出现的 **Sub** ，我们将秘密消息提取为 **ABC。**

**进场:**

*   在给定的字符串字符串中，用空格替换所有出现的 Sub。
*   删除字符串开头和结尾不需要的空格。
*   打印修改后的字符串。

以下是上述方法的实现:

## C++

```
// C++ implementation to extract 
// the secret message
#include <bits/stdc++.h>
using namespace std;

// Trim method implementation to remove 
// trailing and leading white-spaces
string trim(const string &s)
{
    auto start = s.begin();
    while (start != s.end() && 
           isspace(*start))
        start++;

    auto end = s.end();
    do
    {
        end--;
    } while (distance(start, end) > 0 && 
                    isspace(*end));

    return string(start, end + 1);
}

// Function to extract the secret message
string extractSecretMessage(string str, 
                            string sub)
{
    // Replacing all occurrences of
    // Sub in Str by empty spaces
    size_t pos;
    while ((pos = str.find(sub)) != string::npos)
        str.replace(pos, 3, " ");

    // Removing unwanted spaces in the
    // start and end of the string
    str = trim(str);

    return str;
}

// Driver code
int main(int argc, char const *argv[])
{
    string str = "LIELIEILIEAMLIECOOL";
    string sub = "LIE";
    cout << extractSecretMessage(str, sub) 
         << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to extract the secret message
import java.io.*;
import java.util.*;

class GFG {

    // Function to extract the secret message
    static String extractSecretMessage(String Str, String Sub)
    {
        // Replacing all occurrences of
        // Sub in Str by empty spaces
        Str = Str.replaceAll(Sub, " ");

        // Removing unwanted spaces in the
        // start and end of the string
        Str = Str.trim();

        return Str;
    }

    // Driver code
    public static void main(String args[])
    {
        String Str = "LIELIEILIEAMLIECOOL";
        String Sub = "LIE";
        System.out.println(extractSecretMessage(Str, Sub));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to extract
# the secret message

# Function to extract the secret message
def extractSecretMessage(Str, Sub):

    # Replacing all occurrences of
    # Sub in Str by empty spaces
    Str= Str.replace(Sub, " ")

    # Removing unwanted spaces in the
    # start and end of the string

    return Str.strip()

# Driver code
Str = "LIELIEILIEAMLIECOOL"
Sub = "LIE"
print(extractSecretMessage(Str, Sub))

# This code is contributed 
# by ihritik
```

## C#

```
// C# implementation to extract the 
// secret message 
using System;

class GFG 
{ 

// Function to extract the secret message 
static string extractSecretMessage(string Str, 
                                   string Sub) 
{ 
    // Replacing all occurrences of 
    // Sub in Str by empty spaces 
    Str = Str.Replace(Sub, " "); 

    // Removing unwanted spaces in the 
    // start and end of the string 
    Str = Str.Trim(); 

    return Str; 
} 

// Driver code 
public static void Main() 
{ 
    string Str = "LIELIEILIEAMLIECOOL"; 
    string Sub = "LIE"; 
    Console.WriteLine(extractSecretMessage(Str, Sub)); 
} 
} 

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to extract the 
// secret message

// Function to extract the secret message
function extractSecretMessage($Str, $Sub)
{
    // Replacing all occurrences of
    // Sub in Str by empty spaces
    $Str = str_replace($Sub, " ", $Str);

    // Removing unwanted spaces in the
    // start and end of the string

    return trim($Str);
}

// Driver code
$Str = "LIELIEILIEAMLIECOOL";
$Sub = "LIE";
echo extractSecretMessage($Str, $Sub);

// This code is contributed 
// by ihritik
?>
```

**Output:**

```
I AM COOL

```