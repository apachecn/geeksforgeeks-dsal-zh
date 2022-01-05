# 计算字符串中给定字符出现次数的程序

> 原文:[https://www . geesforgeks . org/program-count-occurrence-给定字符串/](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/)

给定一个字符串和一个字符，任务是创建一个函数来计算字符串中给定字符的出现次数。

**示例:**

```
Input : str = "geeksforgeeks"
         c = 'e'
Output : 4
'e' appears four times in str.

Input : str = "abccdefgaa"
          c = 'a' 
Output : 3
'a' appears three times in str.
```

## C++

```
// C++ program to count occurrences of a given
// character
#include <iostream>
#include <string>
using namespace std;

// Function that return count of the given
// character in the string
int count(string s, char c)
{
    // Count variable
    int res = 0;

    for (int i=0;i<s.length();i++)

        // checking character in string
        if (s[i] == c)
            res++;

    return res;
}

// Driver code
int main()
{
    string str= "geeksforgeeks";
    char c = 'e';
    cout << count(str, c) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to count occurrences
// of a character

class GFG
{
    // Method that return count of the given
    // character in the string
    public static int count(String s, char c)
    {
        int res = 0;

        for (int i=0; i<s.length(); i++)
        {
            // checking character in string
            if (s.charAt(i) == c)
            res++;
        }
        return res;
    }

    // Driver method
    public static void main(String args[])
    {
        String str= "geeksforgeeks";
        char c = 'e';
        System.out.println(count(str, c));
    }
}
```

## 蟒蛇 3

```
# Python program to count occurrences
# of a given character

# Method that return count of the
# given character in the string
def count(s, c) :

    # Count variable
    res = 0

    for i in range(len(s)) :

        # Checking character in string
        if (s[i] == c):
            res = res + 1
    return res

# Driver code
str= "geeksforgeeks"
c = 'e'
print(count(str, c))

# This code is contributed by "rishabh_jain".
```

## C#

```
// C# program to count occurrences
// of a character
using System;

public class GFG {

    // Method that return count of the given
    // character in the string
    public static int count(string s, char c)
    {
        int res = 0;

        for (int i = 0; i < s.Length; i++)
        {

            // checking character in string
            if (s[i] == c)
            res++;
        }

        return res;
    }

    // Driver method
    public static void Main()
    {
        string str = "geeksforgeeks";
        char c = 'e';

        Console.WriteLine(count(str, c));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// occurrences of a given
// character

// Function that return count of
// the given character in the string
function count($s, $c)
{

    // Count variable
    $res = 0;

    for ($i = 0; $i < strlen($s); $i++)

        // checking character in string
        if ($s[$i] == $c)
            $res++;

    return $res;
}

    // Driver Code
    $str= "geeksforgeeks";
    $c = 'e';
    echo count($str, $c) ;
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JAVASCRIPT program to count occurrences
// of a character
    // Method that return count of the given
    // character in the string
    function count(s, c)
    {
        let res = 0;

        for (let i = 0; i < s.length; i++)
        {
            // checking character in string
            if (s.charAt(i) == c)
            res++;
        }
        return res;
    }

    // Driver method  
        let str= "geeksforgeeks";
        let c = 'e';
        document.write(count(str, c));

 // This code is contributed by shivanisinghss2110      
 </script>
```

```
4
```

**在 C++中使用直接函数**

## C

```
// CPP program to count occurrences of
// a character using library
#include<bits/stdc++.h>
using namespace std;

// Driver code
int main()
{
    string str = "geeksforgeeks";
    char c = 'e';

    // Count returns number of occurrences of
    // c between two given positions provided
    // as two iterators.
    cout << count(str.begin(), str.end(), c);
    return 0;
}
```

**输出:**

```
4
```

**使用递归**

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
      static int countinString(char ch, String s)
    {
          //base case;
        if(s.length()==0)
            return 0;
          int count = 0;

          //checking if the first character of
          //the given string is that character
          //or not
          if(s.charAt(0)==ch)
          count++;

          //this will count the occurrence of
          //given character in the string
          //from index 1 to the last
          //index of the string
          count+=countinString(ch,s.substring(1));

        return count;
    }
    public static void main (String[] args) {
        String str= "geeksforgeeks";
        char c = 'e';
        System.out.println(countinString(c,str));
    }
}
```

## C#

```
/*package whatever //do not write package name here */
using System;
public class GFG {
      static int countinString(char ch, String s)
    {
          // base case;
        if(s.Length == 0)
            return 0;
          int count = 0;

          // checking if the first character of
          // the given string is that character
          // or not
          if(s[0] == ch)
          count++;

          // this will count the occurrence of
          // given character in the string
          // from index 1 to the last
          // index of the string
          count += countinString(ch,s.Substring(1));

        return count;
    }

  // Driver code
    public static void Main(String[] args) {
        String str= "geeksforgeeks";
        char c = 'e';
        Console.WriteLine(countinString(c,str));
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
/*package whatever //do not write package name here */

    function countinString( ch, s)
    {
        // base case;
        if (s.length == 0)
            return 0;
        var count = 0;

        // checking if the first character of
        // the given string is that character
        // or not
        if (s[0] == ch)
            count++;

        // this will count the occurrence of
        // given character in the string
        // from index 1 to the last
        // index of the string
        count += countinString(ch, s.substring(1));

        return count;
    }

        var str = "geeksforgeeks";
        var c = 'e';
        document.write(countinString(c, str));

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
4
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。