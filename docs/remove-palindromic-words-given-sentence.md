# 删除给定句子中的所有回文单词

> 原文:[https://www . geesforgeks . org/remove-回文-单词-给定-句子/](https://www.geeksforgeeks.org/remove-palindromic-words-given-sentence/)

给了一句**串**。问题是从给定的句子中去掉所有的回文单词。
**例:**

```
Input : str = "Text contains malayalam and level words"
Output : Text contains and words

Input : str = "abc bcd"
Output : abc bcd
```

**做法:**一个一个摘抄所有单词。检查当前单词是否不是回文，然后将其添加到最后一个字符串中。
**算法:**

```
removePalinWords(str, n)
    Initialize final_str = "", word = ""
    str = str + " "

    for i = 0 to n-1
        if str[i] != ' ', then
        word = word + str[i]
    else 
        if (!(isPalindrome(word)), then
            final_str += word + " "
        word = ""

    return final_str
```

**ispalindome()**函数用于检查给定的字符串是否为回文。参考[这篇](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)帖子。

## C++

```
// C++ implementation to remove all the
// palindromic words from the given sentence
#include <bits/stdc++.h>
using namespace std;

// function to check if 'str' is palindrome
bool isPalindrome(string str) {
  int i = 0, j = str.size() - 1;

  // traversing from both the ends
  while (i < j)

    // not palindrome
    if (str[i++] != str[j--])
      return false;

  // palindrome
  return true;
}

// function to remove all the palindromic words
// from the given sentence
string removePalinWords(string str) {

  // 'final_str' to store the final string and
  // 'word' to one by one store each word of 'str'
  string final_str = "", word = "";

  // add space at the end of 'str'
  str = str + " ";
  int n = str.size();

  // traversing 'str'
  for (int i = 0; i < n; i++) {

    // accumulating characters of the current word
    if (str[i] != ' ')
      word = word + str[i];

    else {

      // if 'word' is not palindrome then a
      // add it to 'final_str'
      if (!(isPalindrome(word)))
        final_str += word + " ";

      // reset
      word = "";
    }
  }

  // required final string
  return final_str;
}

// Driver program to test above
int main() {
  string str = "Text contains malayalam and level words";
  cout << removePalinWords(str);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to remove all the
// palindromic words from the given sentence

class GFG
{
    // function to check if 'str' is palindrome
    static boolean isPalindrome(String str)
    {
        int i = 0, j = str.length() - 1;

        // traversing from both the ends
        while (i < j)
        {
            // not palindrome
            if (str.charAt(i++) != str.charAt(j--))
            return false;
        }
        // palindrome
        return true;
    }

    // function to remove all the palindromic words
    // from the given sentence
    static String removePalinWords(String str)
    {

        // 'final_str' to store the final string and
        // 'word' to one by one store each word of 'str'
        String final_str = "", word = "";

        // add space at the end of 'str'
        str = str + " ";
        int n = str.length();

        // traversing 'str'
        for (int i = 0; i < n; i++)
        {

            // accumulating characters of the current word
            if (str.charAt(i) != ' ')
            word = word + str.charAt(i);

            else
            {

                // if 'word' is not palindrome then a
                // add it to 'final_str'
                if (!(isPalindrome(word)))
                    final_str += word + " ";

                // reset
                word = "";
            }
        }

        // required final string
        return final_str;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "Text contains malayalam and level words";
    System.out.print(removePalinWords(str));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to remove all the
# palindromic words from the given sentence

# function to check if 'str' is palindrome
def isPalindrome(string) :
    i = 0; j = len(string) - 1;

    # traversing from both the ends
    while (i < j) :

        # not palindrome
        if (string[i] != string[j]) :
            return False;
        i += 1;
        j -= 1;

    # palindrome
    return True;

# function to remove all the palindromic words
# from the given sentence
def removePalinWords(string) :

    # 'final_str' to store the final string and
    # 'word' to one by one store each word of 'str'
    final_str = ""; word = "";

    # add space at the end of 'str'
    string = string + " ";
    n = len(string);

    # traversing 'str'
    for i in range(n) :

        # accumulating characters of the current word
        if (string[i] != ' ') :
            word = word + string[i];

        else :

            # if 'word' is not palindrome then a
            # add it to 'final_str'
            if (not (isPalindrome(word))) :
                final_str += word + " ";

            # reset
            word = "";

    # required final string
    return final_str;

# Driver Code
if __name__ == "__main__" :

    string = "Text contains malayalam and level words";
    print(removePalinWords(string));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to remove all the
// palindromic words from the given sentence
using System;

class GFG {

    // function to check if 'str' is
    // palindrome
    static bool isPalindrome(string str)
    {
        int i = 0, j = str.Length - 1;

        // traversing from both the ends
        while (i < j)
        {

            // not palindrome
            if (str[i++] != str[j--])
            return false;
        }

        // palindrome
        return true;
    }

    // function to remove all the
    // palindromic words from the
    // given sentence
    static String removePalinWords(string str)
    {

        // 'final_str' to store the final
        // string and 'word' to one by one
        // store each word of 'str'
        string final_str = "", word = "";

        // add space at the end of 'str'
        str = str + " ";
        int n = str.Length;

        // traversing 'str'
        for (int i = 0; i < n; i++)
        {

            // accumulating characters of
            // the current word
            if (str[i] != ' ')
                word = word + str[i];
            else
            {

                // if 'word' is not palindrome
                // then a add it to 'final_str'
                if (!(isPalindrome(word)))
                    final_str += word + " ";

                // reset
                word = "";
            }
        }

        // required final string
        return final_str;
    }

    // Driver code
    public static void Main ()
    {
        string str = "Text contains malayalam "
                           + "and level words";
        Console.WriteLine(removePalinWords(str));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// Javascript implementation to remove all the
// palindromic words from the given sentence

// function to check if 'str' is palindrome
function isPalindrome(str) {
  var i = 0, j = str.length - 1;

  // traversing from both the ends
  while (i < j)

    // not palindrome
    if (str[i++] != str[j--])
      return false;

  // palindrome
  return true;
}

// function to remove all the palindromic words
// from the given sentence
function removePalinWords(str) {

  // 'final_str' to store the final string and
  // 'word' to one by one store each word of 'str'
  var final_str = "", word = "";

  // add space at the end of 'str'
  str = str + " ";
  var n = str.length;

  // traversing 'str'
  for (var i = 0; i < n; i++) {

    // accumulating characters of the current word
    if (str[i] != ' ')
      word = word + str[i];

    else {

      // if 'word' is not palindrome then a
      // add it to 'final_str'
      if (!(isPalindrome(word)))
        final_str += word + " ";

      // reset
      word = "";
    }
  }

  // required final string
  return final_str;
}

// Driver program to test above
var str = "Text contains malayalam and level words";
document.write( removePalinWords(str));

// This code is contributed by itsok.
</script>
```

**Output**

```
Text contains and words 
```