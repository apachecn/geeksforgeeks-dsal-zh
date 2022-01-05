# 删除字符串中每个单词的第一个和最后一个字符

> 原文:[https://www . geesforgeks . org/移除字符串中每个单词的第一个和最后一个字符/](https://www.geeksforgeeks.org/remove-the-first-and-last-character-of-each-word-in-a-string/)

给定字符串，任务是删除字符串中每个单词的第一个和最后一个字符。
**例:**

```
Input: Geeks for geeks
Output: eek o eek

Input: Geeksforgeeks is best
Output: eeksforgeek  es
```

**接近**T2】

*   根据空格分割字符串
*   从第一个字母到最后一个字母循环。
*   检查字符是单词的开头还是结尾
*   从字符串中删除该字符。

下面是上述方法的实现。

## C++

```
// C++ program to remove the first
// and last character of each word in a string.
#include<bits/stdc++.h>
using namespace std;

string FirstAndLast(string str)
{
    // add a space to the end of the string
    str+=" ";

    string res="",w="";

    // traverse the string and extract words
    for(int i=0;i<str.length();i++)
    {
        if(str[i]==' ')
        {
            // excluding the first and
            // last character
            res +=w.substr(1,w.length()-2)+" ";

            // clear the word
            w="";
        }
        else
        {
            // else add the character to word
            w+=str[i];
        }
    }

    return res;
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";
    cout << (str) << endl;
    cout << FirstAndLast(str) << endl;
    return 0;
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove the first
// and last character of each word in a string.

import java.util.*;

class GFG {
    static String FirstAndLast(String str)
    {

        // Split the String based on the space
        String[] arrOfStr = str.split(" ");

        // String to store the resultant String
        String res = "";

        // Traverse the words and
        // remove the first and last letter
        for (String a : arrOfStr) {
            res += a.substring(1, a.length() - 1) + " ";
        }

        return res;
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
# Python3 program to remove the first
# and last character of each word in a string.

def FirstAndLast(string) :

    # Split the String based on the space
    arrOfStr = string.split();

    # String to store the resultant String
    res = "";

    # Traverse the words and
    # remove the first and last letter
    for a in arrOfStr :
        res += a[1:len(a) - 1] + " ";

    return res;

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

        // Split the String based on the space
        String[] arrOfStr = str.Split(' ');

        // String to store the resultant String
        String res = "";

        // Traverse the words and
        // remove the first and last letter
        foreach (String a in arrOfStr)
        {
            res += a.Substring(1, a.Length-2) + " ";
        }

        return res;
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
// PHP program to remove the first
// and last character of each word in a string.

function FirstAndLast($str)
{
    // add a space to the end of the string
    $str .=" ";

    $res = (string) NULL;
    $w = (string) NULL;

    // traverse the string and extract words
    for($i=0; $i< strlen($str); $i++)
    {
        if($str[$i]== ' ')
        {
            // excluding the first and
            // last character
            $res .=substr($w, 1 ,strlen($w)-2) ;
            $res .= " ";

            // clear the word
            $w= (string) NULL;
        }
        else
        {
            // else add the character to word
            $w .=$str[$i];
        }
    }

    return $res;
}

// Driver code

$str = "Geeks for Geeks";
echo $str , "\n";
echo FirstAndLast($str);

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>

      // JavaScript program to remove the first
      // and last character of each word in a string.
      function FirstAndLast(str) {
        // add a space to the end of the string
        str += " ";

        var res = "",
          w = "";

        // traverse the string and extract words
        for (var i = 0; i < str.length; i++)
        {
          if (str[i] === " ") {
            // excluding the first and
            // last character

            res += w.substring(1, w.length - 1) + " ";

            // clear the word
            w = "";
          } else {
            // else add the character to word
            w += str[i];
          }
        }

        return res;
      }

      // Driver code
      var str = "Geeks for Geeks";
      document.write(str + "<br>");
      document.write(FirstAndLast(str) + "<br>");

</script>
```

**Output:** 

```
Geeks for Geeks
eek o eek
```