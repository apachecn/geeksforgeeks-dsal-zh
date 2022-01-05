# 删除相同情况下的连续字母

> 原文:[https://www . geesforgeks . org/remove-连续字母-哪些字母是同格的/](https://www.geeksforgeeks.org/remove-consecutive-alphabets-which-are-in-same-case/)

给定一个字符串**字符串**，任务是从字符串中删除大小写相同的连续字符，并打印结果字符串。

**示例:**

> **输入:**str = " geeksforgeeks "
> T3】输出: GeFoGe
> 
> **输入:**str = " abcDEFghi "
> T3】输出: aDg

**进场:**

*   按原样打印第一个字符。
*   从第二个字符开始遍历字符串中的所有其他字符。
*   比较当前和以前的字符:
    *   如果当前字符和先前字符的大小写相同，则跳过。
    *   否则打印当前字符。

下面是上述方法的实现:

## C++

```
// C++ program to remove the consecutive characters
// from a string that are in same case
#include <bits/stdc++.h>
using namespace std;

// Function to return the modified string
string removeChars(string s)
{
    string modifiedStr = "";
    modifiedStr += s[0];

    // Traverse through the remaining
    // characters in the string
    for (int i = 1; i < s.length(); i++) {

        // If the current and the previous
        // characters are not in the same
        // case then take the character
        if (isupper(s[i]) && islower(s[i - 1])
            || islower(s[i]) && isupper(s[i - 1]))
            modifiedStr += s[i];
    }

    return modifiedStr;
}

// Driver code
int main()
{
    string s = "GeeksForGeeks";
    cout << removeChars(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove the consecutive characters
// from a string that are in same case

class GFG
{

    // Function to return the modified string
    static String removeChars(String s)
    {
        String modifiedStr = "";
        modifiedStr += s.charAt(0);

        // Traverse through the remaining
        // characters in the string
        for (int i = 1; i < s.length(); i++)
        {

            // If the current and the previous
            // characters are not in the same
            // case then take the character
            if (Character.isUpperCase(s.charAt(i)) && Character.isLowerCase(s.charAt(i - 1)) ||
                Character.isLowerCase(s.charAt(i)) && Character.isUpperCase(s.charAt(i - 1)))
                modifiedStr += s.charAt(i);
        }

        return modifiedStr;
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "GeeksForGeeks";
        System.out.println(removeChars(s));
    }
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 program to remove the consecutive
# characters from a string that are in same case

# Function to return the modified string
def removeChars(s) :

    modifiedStr = ""
    modifiedStr += s[0]

    # Traverse through the remaining
    # characters in the string
    for i in range(1, len(s)) :

        # If the current and the previous
        # characters are not in the same
        # case then take the character
        if (s[i].isupper() and s[i - 1].islower() or
            s[i].islower() and s[i - 1].isupper()) :

            modifiedStr += s[i]

    return modifiedStr

# Driver code
if __name__ == "__main__" :

    s = "GeeksForGeeks"
    print(removeChars(s))

# This code is contributed by Ryuga
```

## C#

```
// C# program to remove the consecutive characters
// from a string that are in same case
using System;

class GFG
{

// Function to return the modified string
static string removeChars(string s)
{
    string modifiedStr = "";
    modifiedStr += s[0];

    // Traverse through the remaining
    // characters in the string
    for (int i = 1; i < s.Length; i++)
    {

        // If the current and the previous
        // characters are not in the same
        // case then take the character
        if (char.IsUpper(s[i]) && char.IsLower(s[i - 1]) ||
            char.IsLower(s[i]) && char.IsUpper(s[i - 1]))
            modifiedStr += s[i];
    }

    return modifiedStr;
}

// Driver code
public static void Main()
{
    string s = "GeeksForGeeks";
    Console.Write(removeChars(s));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to remove the consecutive characters
// from a string that are in same case

// Function to return the modified string
function removeChars($s)
{
    $modifiedStr = "";
    $modifiedStr = $modifiedStr . $s[0];

    // Traverse through the remaining
    // characters in the string
    for ($i = 1; $i < strlen($s); $i++)
    {

        // If the current and the previous
        // characters are not in the same
        // case then take the character
        if (ctype_upper($s[$i]) && ctype_lower($s[$i - 1]) ||
            ctype_lower($s[$i]) && ctype_upper($s[$i - 1]))
            $modifiedStr = $modifiedStr . $s[$i];
    }

    return $modifiedStr;
}

// Driver code
$s = "GeeksForGeeks";
echo removeChars($s);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// JavaScript program to remove
// the consecutive characters
// from a string that are in same case

    // Function to return the modified string
    function removeChars(s)
    {
        let modifiedStr = "";
        modifiedStr += s[0];

        // Traverse through the remaining
        // characters in the string
        for (let i = 1; i < s.length; i++)
        {

            // If the current and the previous
            // characters are not in the same
            // case then take the character
            if (s[i] == (s[i]).toUpperCase() &&
            (s[i - 1])==(s[i - 1]).toLowerCase() ||
                s[i]==s[i].toLowerCase() &&
                (s[i - 1])==(s[i - 1]).toUpperCase())
                modifiedStr += s[i];
        }

        return modifiedStr;
    }

    // Driver code
    let s = "GeeksForGeeks";
    document.write(removeChars(s));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
GeFoGe
```