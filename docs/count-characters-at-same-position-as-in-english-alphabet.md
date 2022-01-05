# 计算与英文字母相同位置的字符数

> 原文:[https://www . geeksforgeeks . org/count-与英文字母相同位置的字符/](https://www.geeksforgeeks.org/count-characters-at-same-position-as-in-english-alphabet/)

给定一串小写和大写字符，任务是找出有多少字符与英语字母表中的字符处于相同的位置。
**例:**

```
Input:  ABcED 
Output :  3
First three characters are at same position
as in English alphabets.

Input:  geeksforgeeks 
Output :  1
Only 'f' is at same position as in English
alphabet

Input :  alphabetical 
Output :  3
```

为此，我们可以有简单的方法:

```
1) Initialize result as 0.
2) Traverse input string and do following for every 
   character str[i]
     a) If 'i' is same as str[i] - 'a' or same as 
        str[i] - 'A', then do result++
3) Return result
```

## C++

```
// C++ program to find number of characters at same
// position as in English alphabets
#include<bits/stdc++.h>
using namespace std;

int findCount(string str)
{
    int result = 0;

    // Traverse input string
    for (int i = 0 ; i < str.size(); i++)

        // Check that index of characters of string is
        // same as of English alphabets by using ASCII
        // values and the fact that all lower case
        // alphabetic characters come together in same
        // order in ASCII table.  And same is true for
        // upper case.
        if (i == (str[i] - 'a') || i == (str[i] - 'A'))
            result++;

    return result;
}

// Driver code
int main()
{
    string str = "AbgdeF";
    cout << findCount(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// characters at same position
// as in English alphabets
class GFG
{

    static int findCount(String str)
    {
        int result = 0;

        // Traverse input string
        for (int i = 0; i < str.length(); i++)

        // Check that index of characters
        // of string is same as of English
        // alphabets by using ASCII values
        // and the fact that all lower case
        // alphabetic characters come together
        // in same order in ASCII table. And
        // same is true for upper case.
        {
            if (i == (str.charAt(i) - 'a')
                    || i == (str.charAt(i) - 'A'))
            {
                result++;
            }
        }
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "AbgdeF";
        System.out.print(findCount(str));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python program to find number of
# characters at same position as
# in English alphabets

# Function to count the number of
# characters at same position as
# in English alphabets
def findCount(str):
    result = 0

    # Traverse the input string
    for i in range(len(str)):

        # Check that index of characters of string is
        # same as of English alphabets by using ASCII
        # values and the fact that all lower case
        # alphabetic characters come together in same
        # order in ASCII table. And same is true for
        # upper case.
        if ((i == ord(str[i]) - ord('a')) or
            (i == ord(str[i]) - ord('A'))):
            result += 1
    return result

# Driver Code
str = 'AbgdeF'
print(findCount(str))

# This code is contributed
# by SamyuktaSHegde
```

## C#

```
// C# program to find number of
// characters at same position
// as in English alphabets
using System;

class GFG
{
static int findCount(string str)
{
    int result = 0;

    // Traverse input string
    for (int i = 0 ; i < str.Length; i++)

        // Check that index of characters
        // of string is same as of English
        // alphabets by using ASCII values
        // and the fact that all lower case
        // alphabetic characters come together
        // in same order in ASCII table. And
        // same is true for upper case.
        if (i == (str[i] - 'a') ||
            i == (str[i] - 'A'))
            result++;

    return result;
}

// Driver code
public static void Main()
{
    string str = "AbgdeF";
    Console.Write(findCount(str));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// characters at same position as
// in English alphabets

// Function to count the number of
// characters at same position as
// in English alphabets
function findCount($str)
{
    $result = 0;

    // Traverse the input string
    for ($i = 0; $i < strlen($str); $i++)
    {

        // Check that index of characters of string is
        // same as of English alphabets by using ASCII
        // values and the fact that all lower case
        // alphabetic characters come together in same
        // order in ASCII table. And same is true for
        // upper case.
        if (($i == ord($str[$i]) - ord('a')) or
            ($i == ord($str[$i]) - ord('A')))
            $result += 1;
    }
    return $result;
}

// Driver Code
$str = "AbgdeF";
print(findCount($str))

// This code has been contributed by 29AjayKumar
?>
```

## java 描述语言

```
<script>
      // JavaScript program to find number of characters at same
      // position as in English alphabets

      function findCount(str) {
        var result = 0;

        // Traverse input string
        for (var i = 0; i < str.length; i++)
          // Check that index of characters of string is
          // same as of English alphabets by using ASCII
          // values and the fact that all lower case
          // alphabetic characters come together in same
          // order in ASCII table. And same is true for
          // upper case.
          if (
            i === str[i].charCodeAt(0) - "a".charCodeAt(0) ||
            i === str[i].charCodeAt(0) - "A".charCodeAt(0)
          )
            result++;

        return result;
      }

      // Driver code
      var str = "AbgdeF";
      document.write(findCount(str));
    </script>
```

**输出:**

```
 5
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。