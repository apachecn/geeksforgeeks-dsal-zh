# 缺少字符组成字符串 Pangram

> 原文:[https://www . geesforgeks . org/missing-characters-make-string-pang ram/](https://www.geeksforgeeks.org/missing-characters-make-string-pangram/)

[Pangram](https://www.geeksforgeeks.org/pangram-checking/) 是包含英语字母表中每个字母的句子。给定一个字符串，查找该字符串中缺少的所有字符，即可以使该字符串成为 Pangram 的字符。我们需要按字母顺序打印输出。

**示例:**

```
Input : welcome to geeksforgeeks
Output : abdhijnpquvxyz

Input : The quick brown fox jumps
Output : adglvyz
```

我们已经讨论了[庞加莱检查](https://www.geeksforgeeks.org/pangram-checking/)。这个想法是相似的，我们遍历一个给定的字符串并标记所有访问过的字符。最后，我们打印所有未被访问的字符。

小写和大写字符被认为是相同的。

## C++

```
// C++ program to find characters that needs
// to be added to make Pangram
#include<bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Returns characters that needs to be added
// to make str
string missingChars(string str)
{
    // A boolean array to store characters
    // present in string.
    bool present[MAX_CHAR] = {false};

    // Traverse string and mark characters
    // present in string.
    for (int i=0; i<str.length(); i++)
    {
        if (str[i] >= 'a' && str[i] <= 'z')
            present[str[i]-'a'] = true;
        else if (str[i] >= 'A' && str[i] <= 'Z')
            present[str[i]-'A'] = true;
    }

    // Store missing characters in alphabetic
    // order.
    string res = "";
    for (int i=0; i<MAX_CHAR; i++)
        if (present[i] == false)
            res.push_back((char)(i+'a'));

    return res;
}

// Driver program
int main()
{
    string str = "The quick brown fox jumps "
                 "over the dog";
    cout << missingChars(str);
    return 0;
}       
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find characters that
// needs to be added to make Pangram
import java.io.*;
import java.util.ArrayList;

class GFG{

private static ArrayList<Character>missingChars(
    String str, int strLength)
{
    final int MAX_CHARS = 26;

    // A boolean array to store characters
    // present in string.
    boolean[] present = new boolean[MAX_CHARS];
    ArrayList<Character> charsList = new ArrayList<>();

    // Traverse string and mark characters
    // present in string.
    for(int i = 0; i < strLength; i++)
    {
        if ('A' <= str.charAt(i) &&
                   str.charAt(i) <= 'Z')
            present[str.charAt(i) - 'A'] = true;
        else if ('a' <= str.charAt(i) &&
                        str.charAt(i) <= 'z')
            present[str.charAt(i) - 'a'] = true;
    }

    // Store missing characters in alphabetic
    // order.
    for(int i = 0; i < MAX_CHARS; i++)
    {
        if (present[i] == false)
            charsList.add((char)(i + 'a'));
    }
    return charsList;
}

// Driver Code
public static void main(String[] args)
{
    String str = "The quick brown fox jumps " +
                 "over the dog";

    ArrayList<Character> missing = GFG.missingChars(
        str, str.length());

    if (missing.size() >= 1)
    {
        for(Character character : missing)
        {
            System.out.print(character);
        }
    }
}
}

// This code is contributed by theSardul
```

## 蟒蛇 3

```
# Python3 program to find characters
# that needs to be added to make Pangram
MAX_CHAR = 26

# Returns characters that needs
# to be added to make str
def missingChars(Str):

    # A boolean array to store characters
    # present in string.
    present = [False for i in range(MAX_CHAR)]

    # Traverse string and mark characters
    # present in string.
    for i in range(len(Str)):
        if (Str[i] >= 'a' and Str[i] <= 'z'):
            present[ord(Str[i]) - ord('a')] = True
        elif (Str[i] >= 'A' and Str[i] <= 'Z'):
            present[ord(Str[i]) - ord('A')] = True

    # Store missing characters in alphabetic
    # order.
    res = ""

    for i in range(MAX_CHAR):
        if (present[i] == False):
            res += chr(i + ord('a'))

    return res

# Driver code
Str = "The quick brown fox jumps over the dog"

print(missingChars(Str))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find characters that
// needs to be added to make Pangram
using System.Collections.Generic;
using System;
class GFG{

static List<char>missingChars (String str,
                               int strLength)
{
  int MAX_CHARS = 26;

  // A boolean array to store
  // characters present in string.
  bool[] present = new bool[MAX_CHARS];
  List<char>charsList = new List<char>();

  // Traverse string and mark
  // characters present in string.
  for(int i = 0; i < strLength; i++)
  {
    if ('A' <= str[i] &&
        str[i] <= 'Z')
      present[str[i] - 'A'] = true;
    else if ('a' <= str[i] &&
             str[i] <= 'z')
      present[str[i] - 'a'] = true;
  }

  // Store missing characters
  // in alphabetic order.
  for(int i = 0; i < 26; i++)
  {
    if (present[i] == false)
    {
      charsList.Add((char)(i + 'a'));
    }
  }
  return charsList;
}

// Driver Code
public static void Main()
{
  String str = "The quick brown fox jumps over the dog";
  List<char> missing = missingChars(str,
                                    str.Length);
  if (missing.Count >= 1)
  {
    foreach (var i in missing)
    {
      Console.Write(i);
    }
  }
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
    // Javascript program to find characters that
    // needs to be added to make Pangram

    function missingChars (str, strLength)
    {
      let MAX_CHARS = 26;

      // A boolean array to store
      // characters present in string.
      let present = new Array(MAX_CHARS);
      present.fill(false);
      let charsList = [];

      // Traverse string and mark
      // characters present in string.
      for(let i = 0; i < strLength; i++)
      {
        if ('A'.charCodeAt() <= str[i].charCodeAt() && str[i].charCodeAt() <= 'Z'.charCodeAt())
          present[str[i].charCodeAt() - 'A'.charCodeAt()] = true;
        else if ('a'.charCodeAt() <= str[i].charCodeAt() && str[i].charCodeAt() <= 'z'.charCodeAt())
          present[str[i].charCodeAt() - 'a'.charCodeAt()] = true;
      }

      // Store missing characters
      // in alphabetic order.
      for(let i = 0; i < 26; i++)
      {
        if (present[i] == false)
        {
          charsList.push(String.fromCharCode(i + 'a'.charCodeAt()));
        }
      }
      return charsList;
    }

    let str = "The quick brown fox jumps over the dog";
    let missing = missingChars(str, str.length);
    if (missing.length >= 1)
    {
      for(let i = 0; i < missing.length; i++)
      {
        document.write(missing[i]);
      }
    }

// This code is contributed by mukesh07.
</script>
```

**输出:**

```
alyz
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

https://youtu . be/vqgoxv 8fb 1 e