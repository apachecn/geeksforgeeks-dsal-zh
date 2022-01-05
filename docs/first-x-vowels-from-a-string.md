# 字符串中的前 X 个元音

> 原文:[https://www.geeksforgeeks.org/first-x-vowels-from-a-string/](https://www.geeksforgeeks.org/first-x-vowels-from-a-string/)

给定一个字符串 **str** 和一个整数 **X** ，任务是从 **str** 中找到并打印第一个 **X** 元音。如果 **str** 中的元音总数为 **< X** ，则打印 **-1** 。

**示例:**

> **输入:** str = "GeeksForGeeks "，X = 3
> **输出:**EEO
> “e”、“e”和“o”是给定字符串中的前三个元音。
> 
> **输入:** str = "softcopy "，X = 5
> **输出:** -1
> 元音总计数为 2，即‘o’和‘o’

**方法:**逐字符遍历字符串，检查当前字符是否为元音。如果当前字符是一个元音，则将其连接到结果字符串，**结果**。如果在任何时候合成字符串的长度变为 **X** ，则打印字符串**结果**，否则最终打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a character is vowel
bool isVowel(char c)
{
    c = tolower(c);
    if (c == 'a' || c == 'e' || c == 'i'
        || c == 'o' || c == 'u')
        return true;
    return false;
}

// Function to return first X vowels
string firstXvowels(string s, int x)
{
    // String to store first X vowels
    string result = "";
    for (int i = 0; i < s.length(); i++) {

        // If s[i] is a vowel then
        // append it to the result
        if (isVowel(s[i]))
            result += s[i];

        // If the desired length is reached
        if (result.length() == x) {
            return result;
        }
    }

    // If total vowels are < X
    return "-1";
}

// Driver code
int main()
{
    string str = "GeeksForGeeks";
    int x = 3;

    cout << firstXvowels(str, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

public class GFG{

    // Function to check if a character is vowel
    static boolean isVowel(char c)
    {
        c = Character.toLowerCase(c) ;
        if (c == 'a' || c == 'e' || c == 'i'
            || c == 'o' || c == 'u')
            return true;
        return false;
    }

    // Function to return first X vowels
    static String firstXvowels(String s, int x)
    {
        // String to store first X vowels
        String result = "";
        for (int i = 0; i < s.length(); i++) {

            // If s[i] is a vowel then
            // append it to the result
            if (isVowel(s.charAt(i)))
                result += s.charAt(i);

            // If the desired length is reached
            if (result.length() == x) {
                return result;
            }
        }

        // If total vowels are < X
        return "-1";
    }

    // Driver code
    public static void main(String []args)
    {
        String str = "GeeksForGeeks";
        int x = 3;

        System.out.println(firstXvowels(str, x)) ;
    }
    // This code is contributed by Ryuga
    }
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to check if a character is vowel
def isVowel(c):
    c = c.lower()
    if (c == 'a' or c == 'e' or
        c == 'i' or c == 'o' or c == 'u'):
        return True
    return False

# Function to return first X vowels
def firstXvowels(s, x):

    # String to store first X vowels
    result = ""
    for i in range(0, len(s), 1):

        # If s[i] is a vowel then
        # append it to the result
        if (isVowel(s[i])):
            result += s[i]

        # If the desired length is reached
        if (len(result) == x):
            return result

    # If total vowels are < X
    return "-1"

# Driver code
if __name__ == '__main__':
    str = "GeeksForGeeks"
    x = 3

    print(firstXvowels(str, x))

# This code is implemented by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to check if a
// character is vowel
static bool isVowel(char c)
{
    c = Char.ToLower(c) ;
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return true;
    return false;
}

// Function to return first X vowels
static string firstXvowels(string s, int x)
{
    // String to store first X vowels
    string result = "";
    for (int i = 0; i < s.Length; i++)
    {

        // If s[i] is a vowel then
        // append it to the result
        if (isVowel(s[i]))
            result += s[i];

        // If the desired length is reached
        if (result.Length == x)
        {
            return result;
        }
    }

    // If total vowels are < X
    return "-1";
}

// Driver code
public static void Main()
{
    string str = "GeeksForGeeks";
    int x = 3;

    Console.WriteLine(firstXvowels(str, x)) ;
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to check if a character is vowel
function isVowel($c)
{
    $c = strtolower($c);
    if ($c == 'a' || $c == 'e' ||
        $c == 'i' || $c == 'o' || $c == 'u')
        return true;
    return false;
}

// Function to return first X vowels
function firstXvowels($s, $x)
{
    // String to store first X vowels
    $result = "";
    for ($i = 0; $i < strlen($s); $i++)
    {

        // If s[i] is a vowel then
        // append it to the result
        if (isVowel($s[$i]))
            $result .= $s[$i];

        // If the desired length is reached
        if (strlen($result) == $x)
        {
            return $result;
        }

    }

    // If total vowels are < X
    return "-1";
}

// Driver code
$str = "GeeksForGeeks";
$x = 3;

echo firstXvowels($str, $x);

// This code is contributed
// by princiraj1992
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check if a character is vowel
function isVowel(c)
{
    c = (c.toLowerCase());
    if (c == 'a' || c == 'e' || c == 'i'
        || c == 'o' || c == 'u')
        return true;
    return false;
}

// Function to return first X vowels
function firstXvowels(s, x)
{
    // String to store first X vowels
    var result = "";
    for (var i = 0; i < s.length; i++) {

        // If s[i] is a vowel then
        // append it to the result
        if (isVowel(s[i]))
            result += s[i];

        // If the desired length is reached
        if (result.length == x) {
            return result;
        }
    }

    // If total vowels are < X
    return "-1";
}

// Driver code
var str = "GeeksForGeeks";
var x = 3;
document.write( firstXvowels(str, x));

</script>
```

**Output:** 

```
eeo
```

**时间复杂度:** O(n)这里，n 是字符串的长度。