# 一个句子中最长单词长度的程序

> 原文:[https://www . geesforgeks . org/program-display-number-characters-long-word-句子/](https://www.geeksforgeeks.org/program-display-number-characters-longest-word-sentence/)

给定一个字符串，我们必须找到输入字符串中最长的单词，然后计算这个单词中的字符数。

**示例:**

```
Input  : A computer science portal for geeks
Output : Longest word's length = 8 
```

```
Input  : I am an intern at geeksforgeeks
Output : Longest word's length = 13
```

想法很简单，我们遍历给定的字符串。如果我们找到单词的结尾，我们会比较结尾单词的长度和结果。否则，我们增加当前单词的长度。

## C++

```
// C++ program to find the number of
// charters in the longest word in
// the sentence.
#include <iostream>
using namespace std;

int LongestWordLength(string str)
{

    int n = str.length();
    int res = 0, curr_len = 0, i;

    for (int i = 0; i < n; i++) {

        // If current character is
        // not end of current word.
        if (str[i] != ' ')
            curr_len++;

        // If end of word is found
        else {
            res = max(res, curr_len);
            curr_len = 0;
        }
    }

    // We do max one more time to
    // consider last word as there
    // won't be any space after
    // last word.
    return max(res, curr_len);
}

// Driver function
int main()
{
    string s =
    "I am an intern at geeksforgeeks";

    cout << LongestWordLength(s);
    return 0;
}

// This code is contributed by
// Smitha Dinesh Semwal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of charters
// in the longest word in the sentence.
import java.util.*;

class LongestWordLength
{
    static int LongestWordLength(String str)
    {
    int n = str.length();
    int res = 0, curr_len = 0;
    for (int i = 0; i < n; i++)
    {
        // If current character is not
        // end of current word.
        if (str.charAt(i) != ' ')
            curr_len++;

        // If end of word is found
        else
        {
            res = Math.max(res, curr_len);
            curr_len = 0;
        }
    }

    // We do max one more time to consider
    // last word as there won't be any space
    // after last word.
    return Math.max(res, curr_len);
    }

    public static void main(String[] args)
    {
        String s = "I am an intern at geeksforgeeks";
        System.out.println(LongestWordLength(s));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the
# number of charters in the
# longest word in the sentence.
def LongestWordLength(str):

    n = len(str)
    res = 0; curr_len = 0

    for i in range(0, n):

        # If current character is
        # not end of current word.
        if (str[i] != ' '):
            curr_len += 1

        # If end of word is found
        else:
            res = max(res, curr_len)
            curr_len = 0

    # We do max one more time to consider
    # last word as there won't be any space
    # after last word.
    return max(res, curr_len)

# Driver Code
s = "I am an intern at geeksforgeeks"
print(LongestWordLength(s))

# This code is contribute by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find the number of charters
// in the longest word in the sentence.
using System;

class GFG {

    static int LongestWordLength(string str)
    {
        int n = str.Length;
        int res = 0, curr_len = 0;
        for (int i = 0; i < n; i++)
        {

            // If current character is not
            // end of current word.
            if (str[i] != ' ')
                curr_len++;

            // If end of word is found
            else
            {
                res = Math.Max(res, curr_len);
                curr_len = 0;
            }
        }

        // We do max one more time to consider
        // last word as there won't be any space
        // after last word.
        return Math.Max(res, curr_len);
    }

    public static void Main()
    {
        string s = "I am an intern at geeksforgeeks";
        Console.Write(LongestWordLength(s));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// number of charters in
// the longest word in the
// sentence.

function LongestWordLength($str)
{

    $n = strlen($str);
    $res = 0; $curr_len = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // If current character is
        // not end of current word.
        if ($str[$i] != ' ')
            $curr_len++;

        // If end of word is found
        else
        {
            $res = max($res, $curr_len);
            $curr_len = 0;
        }
    }

    // We do max one more
    // time to consider last
    // word as there won't
    // be any space after
    // last word.
    return max($res, $curr_len);
}

// Driver Code
$s = "I am an intern at geeksforgeeks";

echo (LongestWordLength($s));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
      // JavaScript program to find the number of charters
      // in the longest word in the sentence.
      function LongestWordLength(str)
      {
        var n = str.length;
        var res = 0,
          curr_len = 0;
        for (var i = 0; i < n; i++)
        {

          // If current character is not
          // end of current word.
          if (str[i] !== " ") curr_len++;
          // If end of word is found
          else
          {
            res = Math.max(res, curr_len);
            curr_len = 0;
          }
        }

        // We do max one more time to consider
        // last word as there won't be any space
        // after last word.
        return Math.max(res, curr_len);
      }

      var s = "I am an intern at geeksforgeeks";
      document.write(LongestWordLength(s));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
13
```

**另一种方法:**

## C++14

```
// C++ program to find the number of charters
// in the longest word in the sentence.
#include<bits/stdc++.h>
using namespace std;

int LongestWordLength(string str)
{
    int counter = 0;
    string words[100];
    for (short i = 0; i < str.length(); i++)
    {
        if (str[i] == ' ')
            counter++;
        else
            words[counter] += str[i];
    }

    int length = 0;

    for(string word:words)
    {
        if(length < word.length())
        {
            length = word.length();
        }
    }
    return length;
}

// Driver code
int main()
{
    string str = "I am an intern at geeksforgeeks";

    cout << (LongestWordLength(str));
}

// This code contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of charters
// in the longest word in the sentence.
class GFG {

    static int LongestWordLength(String str)
    {
        String[] words = str.split(" ");
        int length = 0;

        for(String word:words){
            if(length < word.length()){
                length = word.length();
            }
        }
        return length;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "I am an intern at geeksforgeeks";

        System.out.println(LongestWordLength(str));
    }
}
```

## 蟒蛇 3

```
# Python program to find the number of characters
# in the longest word in the sentence.

def longestWordLength(string):

    length = 0

    # Finding longest word in sentence
    for word in string.split():
        if(len(word) > length):
            length = len(word)

    return length

# Driver Code
string = "I am an intern at geeksforgeeks"
print(longestWordLength(string))

# This code is contributed by Vivekkumar Singh
```

## C#

```
// C# program to find the
// number of charters in
// the longest word in
// the sentence.
using System;

class GFG
{
    static int LongestWordLength(string str)
    {
        String[] words = str.Split(' ');
        int length = 0;

        for(int i = 0; i < words.Length; i++)
        {
            if(length < words[i].Length)
            {
                length = words[i].Length;
            }
        }
        return length;
    }

    // Driver code
    static void Main()
    {
        string str = "I am an intern at geeksforgeeks";

        Console.Write(LongestWordLength(str));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

**Output:** 

```
13
```