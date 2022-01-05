# 打印字母倒数的程序

> 原文:[https://www . geesforgeks . org/program-print-互惠-letters/](https://www.geeksforgeeks.org/program-print-reciprocal-letters/)

给定一个字符串 S，我们需要找到它的倒数。字母的倒数是通过找到字母和第一个字母“A”的位置之间的差异来找到的。然后从字母“Z”开始移动相同的步数。经过以上步骤，我们得出的特征是相互的。
Z 的倒数是 A，反之亦然，因为如果你颠倒字母表的位置，A 就会在 Z 的位置上。
同样，T 是 G 的倒数，J 是 q 的倒数。
**例:**

```
Input  :    PRAKHAR
Output :    KIZPSZI

Input  :    VARUN
Output :    EZIFM
```

只要用一个给出每个字符倒数的数学公式

> 倒数(x)= ASCII(' Z ')–ASCII(x)+ASCII(' A ')
> Z 和 A 的 ASCII 值会根据
> 的大小写发生变化。

## C++

```
// CPP program to find Reciprocal string
#include <bits/stdc++.h>
using namespace std;

// To print reciprocal string
void reciprcalString(string word)
{
    char ch;
    for (int i = 0; i < word.length(); i++) {
        // converting uppercase character
        // To reciprocal character
        // display the character
        if (isupper(word[i])) {
            ch = 'Z' - word[i] + 'A';
            cout << ch;
        }

        // converting lowercase character
        // To reciprocal character
        // display the character
        else if (islower(word[i])) {
            ch = 'z' - word[i] + 'a';
            cout << ch;
        }

        else {
            cout << word[i];
        }
    }
}

// Driver function
int main()
{
    string s = "Geeks for Geeks";
    cout << "The reciprocal of " << s
         << " is - " << endl;
    reciprcalString(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to illustrate...
// Reciprocal Letters
import java.io.*;
import java.math.*;
import java.text.*;
import java.util.*;
import java.util.regex.*;

public class GFG {

    // function to print
    // the reciprocal
    static void Reciprcalstring(String word)
    {
        char ch;
        for (int i = 0; i < word.length(); i++) {
            ch = word.charAt(i);

            // Checking if the character
            // is a letter or not
            if (Character.isLetter(ch)) {

                // converting lowercase character
                // To reciprocal character
                if (Character.isLowerCase(ch)) {
                    ch = (char)(122 - (int)(ch) + 97);
                }
                // converting uppercase character
                // To reciprocal character
                else if (Character.isUpperCase(ch)) {
                    ch = (char)(90 - (int)(ch) + 65);
                }
            }

            // display each character
            System.out.print(ch);
        }
    }

    // Driver function
    public static void main(String[] args)
    {
        // static input
        String s = "Geeks for Geeks";
        System.out.print("The reciprocal of " + s + " is - "
                         + "\n");

        // calling the function
        Reciprcalstring(s);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find Reciprocal string

# to check for UPPERCASE
def isupper(ch):
    if ch >= 'A' and ch <= 'Z':
        return True
    return False

# to check for LOWERCASE
def islower(ch):
    if ch >= 'a' and ch <= 'z':
        return True
    return False

# To print reciprocal string
def reciprocalString(word):
    ch = ''
    for i in range(len(word)):

        # converting uppercase character
        # To reciprocal character
        # display the character
        if isupper(word[i]):
            ch = chr(ord('Z') -
                     ord(word[i]) + ord('A'))
            print(ch, end = "")

        # converting lowercase character
        # To reciprocal character
        # display the character
        elif islower(word[i]):
            ch = chr(ord('z') -
                     ord(word[i]) + ord('a'))
            print(ch, end = "")
        else:
            print(word[i], end = "")

# Driver Code
if __name__ == "__main__":
    s = "Geeks for Geeks"
    print("The reciprocal of", s, "is - ")
    reciprocalString(s)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find Reciprocal string
using System;

class GFG {

    // function to print the reciprocal
    static void Reciprcalstring(string word)
    {
        char ch;
        for (int i = 0; i < word.Length; i++) {
            ch = word[i];

            // Checking if the character
            // is a letter or not
            if (Char.IsLetter(ch) && ch < 128) {

                // converting lowercase character
                // To reciprocal character
                if (char.IsLower(ch)) {
                    ch = (char)(122 - (int)(ch) + 97);
                }

                // converting uppercase character
                // To reciprocal character
                else if (char.IsUpper(ch)) {
                    ch = (char)(90 - (int)(ch) + 65);
                }
            }

            // display each character
            Console.Write(ch);
        }
    }

    // Driver function
    public static void Main()
    {
        string s = "Geeks for Geeks";
        Console.Write("The reciprocal of " + s +
                               " is - " + "\n");

        // calling the function
        Reciprcalstring(s);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// Reciprocal string

function check_lowercase_string($string)
{
    return ($string === strtolower($string));
}

function check_uppercase_string($string)
{
    return ($string === strtoupper($string));
}

// function to print
// the reciprocal
function Reciprcalstring($word)
{
    $ch;
    for ($i = 0; $i < strlen($word); $i++)
    {
        $ch = $word[$i];

        // Check if space,
        // then print it
        if($ch == ' ')
            echo ($ch);

        // converting lowercase character
        // To reciprocal character
        else if (check_lowercase_string($ch))
        {
            $ch = chr(122 -
                      ord($ch) + 97);
        }

        // converting uppercase character
        // To reciprocal character
        else if (check_uppercase_string($ch))
        {
            $ch = chr(90 -
                      ord($ch) + 65);
        }

        // display each
        // character
        echo ($ch);
    }
}

// Driver Code
$s = "Geeks for Geeks";
echo ("The reciprocal of ".
       $s. " is - ". "\n");

// calling the function
Reciprcalstring($s);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// javascript program to illustrate...
// Reciprocal Letters
function isLetter(ch){
    if(ch>='a' && ch<='z' || ch>='A' && ch<='Z')
    return true;
    else
    return
    false;
}
function isLowerCase(ch){
    if(ch>='a' && ch<='z')
    return true;
    else
    return
    false;
}
function isUpperCase(ch){
    if( ch>='A' && ch<='Z')
    return true;
    else
    return
    false;
}

    // function to print
    // the reciprocal
    function Reciprcalstring( word) {
        var  ch;
        for (var i = 0; i < word.length; i++) {
            ch = word.charAt(i);

            // Checking if the character
            // is a letter or not
            if (isLetter(ch)) {

                // converting lowercase character
                // To reciprocal character
                if (isLowerCase(ch)) {
                    ch =String.fromCharCode(122 -ch.charCodeAt(0) + 97);
                }
                // converting uppercase character
                // To reciprocal character
                else if (isUpperCase(ch)) {
                    ch =String.fromCharCode(90- ch.charCodeAt(0) + 65);

                }
            }

            // display each character
            document.write(ch);
        }
    }

    // Driver function

        //  input
        var s = "Geeks for Geeks";
        document.write("The reciprocal of " + s + " is - " + "<br\>");

        // calling the function
        Reciprcalstring(s);

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
The reciprocal of Geeks for Geeks is - 
Tvvph uli Tvvph
```