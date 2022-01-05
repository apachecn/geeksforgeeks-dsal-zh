# 从字符串中删除重复项后的字符替换

> 原文:[https://www . geesforgeks . org/character-replacement-string-minimization/](https://www.geeksforgeeks.org/character-replacement-string-minimization/)

给定一个字符串。任务是用出现在原始字符串索引“ *IND* ”处的字符替换最小化字符串的每个字符。最小化的字符串是通过从原始字符串中删除所有重复项并保持元素顺序不变而获得的字符串。

最小化字符串中任何索引的 IND 计算如下:

> **IND =(最小化字符串的 ascii 值的平方)%(原始字符串的长度)**

**示例:**

```
Input : geeks
Output : sesg
Explanation :   minimized string = geks
                length of original string = 5         
                ascii value of g = 103
                IND for g = (103*103) % 5 = 4
                replacement character for g = s 
                character 's' present at index 4 of original string
Similarly,
replacement character for e = e 
replacement character for k = s 
replacement character for s = g 

Input : helloworld
Output : oeoeeoh
```

**方法:**
下面是字符串最小化的分步算法:

```
    1\. Initialize flagchar[26] = {0}
    2\. for i=0 to str.length()-1
    3\.     ch = str[i]
    4\.     if flagchar[ch-97] == 0 then
    5\.         mstr = mstr + ch
    6\.         flagchar[ch-97] = 1
    7\.     End if
    8\. End of loop
    9\. return mstr  // minimized string
```

字符替换算法:

```
    1\. Replace each character of minimized string as described
       in the problem statement and example
    2\. Compute final string 
```

下面是上述方法的实现:

## C++

```
// C++ program for character replacement
// after string minimization
#include <bits/stdc++.h>
using namespace std;

// Function to minimize string
string minimize(string str)
{
    string mstr = " ";
    int l, i, flagchar[26] = { 0 };
    char ch;

    l = str.length();

    // duplicate characters are removed
    for (i = 0; i < str.length(); i++) {
        ch = str.at(i);

        // checks if character has previously occurred or not
        // if not then add it to the minimized string 'mstr'
        if (flagchar[ch - 97] == 0) {
            mstr = mstr + ch;
            flagchar[ch - 97] = 1;
        }
    }

    return mstr; // minimized string
}

// Utility function to print the
// minimized, replaced string
void replaceMinimizeUtil(string str)
{
    string minimizedStr, finalStr = "";
    int i, index, l;
    char ch;
    l = str.length();

    minimizedStr = minimize(str); // minimized string

    // Creating final string by replacing character
    for (i = 0; i < minimizedStr.length(); i++) {
        ch = minimizedStr.at(i);

        // index calculation
        index = (ch * ch) % l;

        finalStr = finalStr + str.at(index);
    }

    cout << "Final string: " << finalStr; // final string
}

// Driver program
int main()
{
    string str = "geeks";

    replaceMinimizeUtil(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for character replacement
// after String minimization

class GFG {
    // Function to minimize String

    static String minimize(String str)
    {
        String mstr = " ";
        int l, i, flagchar[] = new int[26];
        char ch;

        l = str.length();

        // duplicate characters are removed
        for (i = 0; i < str.length(); i++) {
            ch = str.charAt(i);

            // checks if character has previously occurred or not
            // if not then add it to the minimized String 'mstr'
            if (flagchar[ch - 97] == 0) {
                mstr = mstr + ch;
                flagchar[ch - 97] = 1;
            }
        }

        return mstr; // minimized String
    }

    // Utility function to print the
    // minimized, replaced String
    static void replaceMinimizeUtil(String str)
    {
        String minimizedStr, finalStr = "";
        int i, index, l;
        char ch;
        l = str.length();

        minimizedStr = minimize(str); // minimized String

        // Creating final String by replacing character
        for (i = 0; i < minimizedStr.length(); i++) {
            ch = minimizedStr.charAt(i);

            // index calculation
            index = (ch * ch) % l;

            finalStr = finalStr + str.charAt(index);
        }
        // final String
        System.out.println("Final String: " + finalStr);
    }

    // Driver program
    public static void main(String[] args)
    {
        String str = "geeks";

        replaceMinimizeUtil(str);
    }
}
// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 program for character
# replacement after string minimization

# Function to minimize string
def minimize(string):

    mstr = " "
    flagchar = [0] * 26 
    l = len(string)

    # Duplicate characters are removed
    for i in range(0, len(string)):

        ch = string[i]

        # checks if character has previously occurred or not
        # if not then add it to the minimized string 'mstr'
        if flagchar[ord(ch)-97] == 0:

            mstr = mstr + ch
            flagchar[ord(ch)-97] = 1

    return mstr # minimized string

# Utility function to print the
# minimized, replaced string
def replaceMinimizeUtil(string):

    finalStr = ""
    l = len(string)
    minimizedStr = minimize(string) # minimized string

    # Creating final string by replacing character
    for i in range(0, len(minimizedStr)):

        ch = ord(minimizedStr[i])

        # index calculation
        index = (ch * ch) % l
        finalStr = finalStr + string[index]

    print("Final string:", finalStr) # final string

# Driver program
if __name__ == "__main__":

    string = "geeks"
    replaceMinimizeUtil(string)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program for character replacement
// after String minimization
using System;

class GFG {

    // Function to minimize String
    static String minimize(string str)
    {
        string mstr = " ";
        int l, i;
        int[] flagchar = new int[26];
        char ch;

        l = str.Length;

        // duplicate characters are removed
        for (i = 0; i < str.Length; i++) {
            ch = str[i];

            // checks if character has previously
            // occurred or not if not then add it
            // to the minimized String 'mstr'
            if (flagchar[ch - 97] == 0) {
                mstr = mstr + ch;
                flagchar[ch - 97] = 1;
            }
        }

        return mstr; // minimized String
    }

    // Utility function to print the
    // minimized, replaced String
    static void replaceMinimizeUtil(string str)
    {
        string minimizedStr, finalStr = "";
        int i, index, l;
        char ch;
        l = str.Length;

        minimizedStr = minimize(str); // minimized String

        // Creating final String by
        // replacing character
        for (i = 0; i < minimizedStr.Length; i++) {
            ch = minimizedStr[i];

            // index calculation
            index = (ch * ch) % l;

            finalStr = finalStr + str[index];
        }

        // final String
        Console.Write("Final String: " + finalStr);
    }

    // Driver Code
    public static void Main()
    {
        string str = "geeks";

        replaceMinimizeUtil(str);
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for character replacement
// after string minimization

// Function to minimize string
function minimize($str)
{
    $mstr = " ";
    $flagchar=array_fill(0, 26, 0);

    $l = strlen($str);

    // duplicate characters are removed
    for ($i = 0; $i < strlen($str); $i++)
    {
        $ch = $str[$i];

        // checks if character has previously occurred or not
        // if not then add it to the minimized string 'mstr'
        if ($flagchar[ord($ch) - 97] == 0)
        {
            $mstr .=$ch;
            $flagchar[ord($ch) - 97] = 1;
        }
    }

    return $mstr; // minimized string
}

// Utility function to print the
// minimized, replaced string
function replaceMinimizeUtil($str)
{

    $finalStr = "";

    $l = strlen($str);

    $minimizedStr = minimize($str); // minimized string

    // Creating final string by replacing character
    for ($i = 0; $i < strlen($minimizedStr); $i++)
    {
        $ch = $minimizedStr[$i];

        // index calculation
        $index = (ord($ch) * ord($ch)) % $l;

        $finalStr = $finalStr.$str[$index];
    }

    echo "Final string: ".$finalStr; // final string
}

// Driver code
$str = "geeks";

replaceMinimizeUtil($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for character replacement
// after String minimization

// Function to minimize String
function minimize(str)
{
    let mstr = " ";
    let l, i, flagchar = new Array(26);

    for(let i = 0; i < 26; i++)
    {
        flagchar[i] = 0;
    }
    let ch;

    l = str.length;

    // Duplicate characters are removed
    for(i = 0; i < str.length; i++)
    {
        ch = str[i];

        // Checks if character has previously
        // occurred or not if not then add it
        // to the minimized String 'mstr'
        if (flagchar[ch.charCodeAt(0) - 97] == 0)
        {
            mstr = mstr + ch;
            flagchar[ch.charCodeAt(0) - 97] = 1;
        }
    }

    // Minimized String
    return mstr;
}

// Utility function to print the
// minimized, replaced String
function replaceMinimizeUtil(str)
{
    let minimizedStr, finalStr = "";
    let i, index, l;
    let ch;
    l = str.length;

    // Minimized String
    minimizedStr = minimize(str);

    // Creating final String by replacing character
    for(i = 0; i < minimizedStr.length; i++)
    {
        ch = minimizedStr[i].charCodeAt(0);

        // Index calculation
        index = (ch * ch) % l;

        finalStr = finalStr + str[index];
    }

    // Final String
    document.write("Final String: " + finalStr);
}

// Driver code
let str = "geeks";

replaceMinimizeUtil(str);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Final string: ssesg
```

**时间复杂度** : O(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。