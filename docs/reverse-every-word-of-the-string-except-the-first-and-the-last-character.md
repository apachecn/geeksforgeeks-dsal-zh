# 颠倒字符串中除第一个和最后一个字符之外的每个单词

> 原文:[https://www . geesforgeks . org/反转字符串中除第一个和最后一个字符之外的每个单词/](https://www.geeksforgeeks.org/reverse-every-word-of-the-string-except-the-first-and-the-last-character/)

给定由一个句子组成的字符串 **str** ，任务是颠倒除单词的第一个和最后一个字符之外的句子的每个单词。

**示例:**

> **输入:** str = "极客为极客"
> T3】输出: gkees 为 gkees
> 
> **输入:** str = "这是一个字符串"
> **输出:** tihs 是一个 snirtg

**方法:**使用 [strtok()](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/) 将字符串分解成单词，现在每个单词取两个指针， **i** 和 **j** 分别指向字符串的第二个和第二个最后一个字符。交换这些字符，然后**增加 i** 和**减少 j** 。重复这些步骤，同时 **i < j** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the given word except
// the first and the last character
string reverseWord(string str)
{
    int len = str.length();

    // Pointer to the second character
    // of the string
    int i = 1;

    // Pointer to the second last
    // character of the string
    int j = str.length() - 2;
    while (i < j) {

        // Swap str[i] and str[j]
        char temp = str[i];
        str[i] = str[j];
        str[j] = temp;
        i++;
        j--;
    }

    return str;
}

// Function to reverse every word of the
// sentence except the first and the
// last character of the words
void reverseWords(char str[])
{
    char* tok = strtok(str, " ");

    // While there are words left
    while (tok != NULL) {

        // Print the reversed word
        cout << reverseWord(tok) << " ";

        // Get the next word
        tok = strtok(NULL, " ");
    }
}

// Driver code
int main()
{
    char str[] = "geeks for geeks";
    reverseWords(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to reverse the given word except
// the first and the last character
static String reverseWord(String str)
{
    int len = str.length();

    // Pointer to the second character
    // of the string
    int i = 1;

    // Pointer to the second last
    // character of the string
    int j = str.length() - 2;

    char[] strchar = str.toCharArray();

    while (i < j)
    {

        // Swap str[i] and str[j]
        char temp = strchar[i];
        strchar[i] = strchar[j];
        strchar[j] = temp;
        i++;
        j--;
    }

    str = new String(strchar);
    return str;
}

// Function to reverse every word of the
// sentence except the first and the
// last character of the words
static void reverseWords(String str)
{
    String[] tok = str.split("\\s");

    // While there are words left
    for(String w:tok)
    {

        // Print the reversed word
        System.out.print(reverseWord(w) + " ");
    }
}

// Driver code
public static void main (String[] args)
{
    String str = "geeks for geeks";
    reverseWords(str);
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to reverse the given word except
# the first and the last character
def reverseWord(Str):

    # len = len(Str)

    # Pointer to the second character
    # of the String
    i = 1

    # Pointer to the second last
    # character of the String
    j = len(Str) - 2
    while (i < j):

        # Swap Str[i] and Str[j]
        temp = Str[i]
        Str[i] = Str[j]
        Str[j] = temp
        i += 1
        j -= 1

    return "".join(Str)

# Function to reverse every word of the
# sentence except the first and the
# last character of the words
def reverseWords(Str):
    Str = Str.split()

    # While there are words left
    for i in Str:

        # Print the reversed word
        j = [h for h in i]
        print(reverseWord(j), end = " ")

# Driver code
Str= "geeks for geeks"
reverseWords(Str)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to reverse the given word except
// the first and the last character
static String reverseWord(String str)
{
    int len = str.Length;

    // Pointer to the second character
    // of the string
    int i = 1;

    // Pointer to the second last
    // character of the string
    int j = str.Length - 2;

    char[] strchar = str.ToCharArray();

    while (i < j)
    {

        // Swap str[i] and str[j]
        char temp = strchar[i];
        strchar[i] = strchar[j];
        strchar[j] = temp;
        i++;
        j--;
    }
    str = new String(strchar);
    return str;
}

// Function to reverse every word of the
// sentence except the first and the
// last character of the words
static void reverseWords(String str)
{
    String[] tok = str.Split(' ');

    // While there are words left
    foreach(String w in tok)
    {

        // Print the reversed word
        Console.Write(reverseWord(w) + " ");
    }
}

// Driver code
public static void Main (String[] args)
{
    String str = "geeks for geeks";
    reverseWords(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach
      // Function to reverse the given word except
      // the first and the last character
      function reverseWord(str) {
        var len = str.length;

        // Pointer to the second character
        // of the string
        var i = 1;

        // Pointer to the second last
        // character of the string
        var j = str.length - 2;

        var strchar = str.split("");

        while (i < j) {
          // Swap str[i] and str[j]
          var temp = strchar[i];
          strchar[i] = strchar[j];
          strchar[j] = temp;
          i++;
          j--;
        }
        str = strchar.join("");
        return str;
      }

      // Function to reverse every word of the
      // sentence except the first and the
      // last character of the words
      function reverseWords(str) {
        var tok = str.split(" ");

        // While there are words left
        for (const w of tok) {
          // Print the reversed word
          document.write(reverseWord(w) + " ");
        }
      }

      // Driver code
      var str = "geeks for geeks";
      reverseWords(str);
</script>
```

**Output:** 

```
gkees for gkees
```