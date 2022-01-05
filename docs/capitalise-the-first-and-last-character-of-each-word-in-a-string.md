# 将字符串中每个单词的第一个和最后一个字符大写

> 原文:[https://www . geesforgeks . org/资本化-字符串中每个单词的第一个和最后一个字符/](https://www.geeksforgeeks.org/capitalise-the-first-and-last-character-of-each-word-in-a-string/)

给定字符串，任务是大写字符串中每个单词的第一个和最后一个字符。
**例:**

```
Input: Geeks for geeks
Output: GeekS FoR GeekS

Input: Geeksforgeeks is best
Output: GeeksforgeekS IS BesT
```

**接近**T2】

*   创建字符串的字符数组
*   从第一个字母到最后一个字母循环。
*   检查字符是单词的开头还是结尾
*   检查字符是否为小写字母。
*   如果是，则大写字符串的字符。

下面是上述方法的实现。

## C++

```
// CPP program to capitalise the first
// and last character of each word in a string.
#include<bits/stdc++.h>
using namespace std;

string FirstAndLast(string str)
{

    // Create an equivalent string
    // of the given string
    string ch = str;
    for (int i = 0; i < ch.length(); i++)
    {

        // k stores index of first character
        // and i is going to store index of last
        // character.
        int k = i;
        while (i < ch.length() && ch[i] != ' ')
            i++;

        // Check if the character is a small letter
        // If yes, then Capitalise
        ch[k] = (char)(ch[k] >= 'a' && ch[k] <= 'z'
                        ? ((int)ch[k] - 32)
                        : (int)ch[k]);
        ch[i - 1] = (char)(ch[i - 1] >= 'a' && ch[i - 1] <= 'z'
                            ? ((int)ch[i - 1] - 32)
                            : (int)ch[i - 1]);
    }

    return ch;
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";
    cout << str << "\n";
    cout << FirstAndLast(str);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to capitalise the first
// and last character of each word in a string.

class GFG {
    static String FirstAndLast(String str)
    {

        // Create an equivalent char array
        // of given string
        char[] ch = str.toCharArray();
        for (int i = 0; i < ch.length; i++) {

            // k stores index of first character
            // and i is going to store index of last
            // character.
            int k = i;
            while (i < ch.length && ch[i] != ' ')
                i++;

            // Check if the character is a small letter
            // If yes, then Capitalise
            ch[k] = (char)(ch[k] >= 'a' && ch[k] <= 'z'
                               ? ((int)ch[k] - 32)
                               : (int)ch[k]);
            ch[i - 1] = (char)(ch[i - 1] >= 'a' && ch[i - 1] <= 'z'
                                   ? ((int)ch[i - 1] - 32)
                                   : (int)ch[i - 1]);
        }

        return new String(ch);
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "Geeks for Geeks";
        System.out.println(str);
        System.out.println(FirstAndLast(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program to capitalise the first
# and last character of each word in a string.
def FirstAndLast(string) :

    # Create an equivalent char array
    # of given string
    ch = list(string);

    i = 0 ;
    while i < len(ch):

        # k stores index of first character
        # and i is going to store index of last
        # character.
        k = i;

        while (i < len(ch) and ch[i] != ' ') :
            i += 1;

        # Check if the character is a small letter
        # If yes, then Capitalise
        if (ord(ch[k]) >= 97 and
            ord(ch[k]) <= 122 ):
            ch[k] = chr(ord(ch[k]) - 32);
        else :
            ch[k] = ch[k]

        if (ord(ch[i - 1]) >= 90 and
            ord(ch[i - 1]) <= 122 ):
            ch[i - 1] = chr(ord(ch[i - 1]) - 32);
        else :
            ch[i - 1] = ch[i - 1]

        i += 1

    return "" . join(ch);

# Driver code
if __name__ == "__main__" :

    string = "Geeks for Geeks";

    print(string);
    print(FirstAndLast(string));

# This code is contributed by Ryuga
```

## C#

```
// C# program to remove the first
// and last character of each word in a string.
using System;

class GFG
{
    static String FirstAndLast(String str)
    {

        // Create an equivalent char array
        // of given string
        char[] ch = str.ToCharArray();
        for (int i = 0; i < ch.Length; i++)
        {

            // k stores index of first character
            // and i is going to store index of last
            // character.
            int k = i;
            while (i < ch.Length && ch[i] != ' ')
                i++;

            // Check if the character is a small letter
            // If yes, then Capitalise
            ch[k] = (char)(ch[k] >= 'a' && ch[k] <= 'z'
                            ? ((int)ch[k] - 32)
                            : (int)ch[k]);
            ch[i - 1] = (char)(ch[i - 1] >= 'a' && ch[i - 1] <= 'z'
                                ? ((int)ch[i - 1] - 32)
                                : (int)ch[i - 1]);
        }

        return new String(ch);
    }

    // Driver code
    public static void Main(String []args)
    {
        String str = "Geeks for Geeks";
        Console.WriteLine(str);
        Console.WriteLine(FirstAndLast(str));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to capitalise the first
// and last character of each word in a string.

function FirstAndLast($str)
{

    // Create an equivalent string
    // of the given string
    $ch = $str;
    for ($i = 0; $i < strlen($ch); $i++)
    {

        // $k stores index of first character
        // and $i is going to store index of last
        // character.
        $k = $i;
        while ($i < strlen($ch) && $ch[$i] != ' ')
            $i++;

        // Check if the character is a small letter
        // If yes, then Capitalise
        $ch[$k] = chr(($ch[$k] >= 'a' && $ch[$k] <= 'z')
                    ? (ord($ch[$k]) - 32) : (ord($ch[$k])));
        $ch[$i - 1] = chr(($ch[$i - 1] >= 'a' && $ch[$i - 1] <= 'z' )
                    ? (ord($ch[$i - 1]) - 32) : (ord($ch[$i - 1])));
    }

    return $ch;
}

// Driver code

$str = "Geeks for Geeks";
echo $str, "\n";
echo FirstAndLast($str);

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>

// JavaScript program to capitalise the first
// and last character of each word in a string.

function FirstAndLast(str)
{

    // Create an equivalent string
    // of the given string
    var ch = str.split('');
    for (var i = 0; i < ch.length; i++)
    {

        // k stores index of first character
        // and i is going to store index of last
        // character.
        var k = i;
        while (i < ch.length && ch[i] != ' ')
            i++;

        // Check if the character is a small letter
        // If yes, then Capitalise
        ch[k] = String.fromCharCode(ch[k] >= 'a' &&
        ch[k] <= 'z' ? (ch[k].charCodeAt(0) - 32)
                     : ch[k].charCodeAt(0));
        ch[i - 1] = String.fromCharCode(ch[i - 1] >= 'a'
        && ch[i - 1] <= 'z'? (ch[i - 1].charCodeAt(0) - 32)
                            : ch[i - 1].charCodeAt(0));
    }

    return ch.join('');
}

// Driver code

var str = "Geeks for Geeks";
document.write( str + "<br>");
document.write( FirstAndLast(str));

</script>
```

**Output:** 

```
Geeks for Geeks
GeekS FoR GeekS
```