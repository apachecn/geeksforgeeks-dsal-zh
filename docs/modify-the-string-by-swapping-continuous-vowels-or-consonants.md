# 通过交换连续的元音或辅音来修改字符串

> 原文:[https://www . geesforgeks . org/通过交换连续元音或辅音来修改字符串/](https://www.geeksforgeeks.org/modify-the-string-by-swapping-continuous-vowels-or-consonants/)

给定一根弦**弦**。任务是通过交换两个相邻的字符来修改字符串，如果它们都是元音或者都是辅音。
**例:**

> **输入:**str = " geesforgeks "
> **输出:**geesfkogreesk
> g**ee**ksforgeks 中的字母‘e’和‘e’是元音，因此它们被交换，因此字符串变成**geesforgeks**。
> gee**ks**中的字母“k”和“s”是辅音，因此它们被交换，因此字符串成为**geeskfurgeks**。
> gees**KF**orge kek 中的字母“k”和“f”是辅音，因此它们被交换，因此字符串变成**geesfkorkeeks**。
> geesfko**rg**eek 中的字母“r”和“g”是辅音，因此它们被交换，因此字符串变成了 **geeskfogreeks** 。
> geeskwoger**ee**ks 中的字母“e”和“e”是元音，因此它们被交换，因此字符串变成**geeskwogreeks**。
> geeskfogree**ks**中的字母“k”和“s”是元音字母，因此它们会互换，因此字符串会变成 **geeskfogreesk** 。
> **输入:** str = "gefeg"
> **输出:** gefeg
> 无连续元音或辅音。

**进场:**

*   遍历字符串中的字符。
*   考虑当前字符和下一个字符。
*   如果两个字符都是辅音或者两个字符都是元音。
*   然后交换角色。
*   否则继续这个过程，直到字符串结束。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a character is a vowel
bool isVowel(char c)
{
    c = tolower(c);
    if (c == 'a' || c == 'e' || c == 'i'
                 || c == 'o' || c == 'u')
        return true;
    return false;
}

// Function to swap two consecutively
// repeated vowels or consonants
string swapRepeated(string str)
{
    // Traverse through the length of the string
    for (int i = 0; i < str.length() - 1; i++) {

        // Check if the two consecutive characters
        // are vowels or consonants
        if ((isVowel(str[i]) && isVowel(str[i + 1]))
            || (!isVowel(str[i]) && !isVowel(str[i + 1])))

            // swap the two characters
            swap(str[i], str[i + 1]);
    }

    return str;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    cout << swapRepeated(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to check if a
    // character is a vowel
    static boolean isVowel(char c)
    {
        c = Character.toLowerCase(c);
        if (c == 'a' || c == 'e' || c == 'i'
                    || c == 'o' || c == 'u')
        {
            return true;
        }
        return false;
    }

    // Function to swap two consecutively
    // repeated vowels or consonants
    static String swapRepeated(char str[])
    {

        // Traverse through the
        // length of the string
        for (int i = 0; i < str.length - 1; i++)
        {
            char c = 0;

            // Check if the two consecutive characters
            // are vowels or consonants
            if ((isVowel(str[i]) && isVowel(str[i + 1]))
                || (!isVowel(str[i]) && !isVowel(str[i + 1])))
            {

                // swap the two characters
                c = str[i];
                str[i] = str[i + 1];
                str[i + 1] = c;
            }
        }
        return String.valueOf(str);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println(swapRepeated(str.toCharArray()));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check if a character is a vowel
def isVowel(c) :
    c = c.lower();
    if (c == 'a' or c == 'e' or c == 'i'
                 or c == 'o' or c == 'u') :
        return True;
    return False;

# Function to swap two consecutively
# repeated vowels or consonants
def swapRepeated(string) :

    # Traverse through the length of the string
    for i in range(len(string) - 1) :

        # Check if the two consecutive characters
        # are vowels or consonants
        if ((isVowel(string[i]) and isVowel(string[i + 1])) or
        (not(isVowel(string[i])) and not(isVowel(string[i + 1])))) :

            # swap the two characters
            (string[i],
             string[i + 1]) = (string[i + 1],
                               string[i]);

    string = "".join(string)
    return string;

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";

    print(swapRepeated(list(string)));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to check if a
    // character is a vowel
    static bool isVowel(char c)
    {
        c = char.ToLower(c);
        if (c == 'a' || c == 'e' || c == 'i'
                    || c == 'o' || c == 'u')
        {
            return true;
        }
        return false;
    }

    // Function to swap two consecutively
    // repeated vowels or consonants
    static String swapRepeated(char []str)
    {

        // Traverse through the
        // length of the string
        for (int i = 0; i < str.Length - 1; i++)
        {
            char c = (char)0;

            // Check if the two consecutive characters
            // are vowels or consonants
            if ((isVowel(str[i]) && isVowel(str[i + 1]))
                || (!isVowel(str[i]) && !isVowel(str[i + 1])))
            {

                // swap the two characters
                c = str[i];
                str[i] = str[i + 1];
                str[i + 1] = c;
            }
        }
        return String.Join("",str);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        Console.WriteLine(swapRepeated(str.ToCharArray()));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the above approach

// Function to check if a character is a vowel
function isVowel($c)
{
    $c = strtolower($c);
    if ($c == 'a' || $c == 'e' || $c == 'i'
                || $c == 'o' || $c == 'u')
        return true;
    return false;
}

// Function to swap two consecutively
// repeated vowels or consonants
function swapRepeated($str)
{
    // Traverse through the length of the string
    for ($i = 0; $i < strlen($str) - 1; $i++) {

        // Check if the two consecutive characters
        // are vowels or consonants
        if ((isVowel($str[$i]) && isVowel($str[$i + 1]))
            || (!isVowel($str[$i]) && !isVowel($str[$i + 1])))
        {
            // swap the two characters
            $t = $str[$i];
            $str[$i]= $str[$i + 1];
            $str[$i+1] = $t;
        }
    }

    return $str;
}

    // Driver code

    $str = "geeksforgeeks";

    echo swapRepeated($str);
    return 0;

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach
      // Function to check if a
      // character is a vowel
      function isVowel(c) {
        c = c.toLowerCase();
        if (c === "a" || c === "e" || c === "i" || c === "o" || c === "u") {
          return true;
        }
        return false;
      }

      // Function to swap two consecutively
      // repeated vowels or consonants
      function swapRepeated(str) {
        // Traverse through the
        // length of the string
        for (var i = 0; i < str.length - 1; i++) {
          // Check if the two consecutive characters
          // are vowels or consonants
          if (
            (isVowel(str[i]) && isVowel(str[i + 1])) ||
            (!isVowel(str[i]) && !isVowel(str[i + 1]))
          ) {
            // swap the two characters
            var c = str[i];
            str[i] = str[i + 1];
            str[i + 1] = c;
          }
        }
        return str.join("");
      }

      // Driver code
      var str = "geeksforgeeks";
      document.write(swapRepeated(str.split("")));
    </script>
```

**Output:** 

```
geesfkogreesk
```