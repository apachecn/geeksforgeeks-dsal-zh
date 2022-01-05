# 统计一个句子中的回文单词

> 原文:[https://www . geesforgeks . org/Java-program-count-number-回文-word-句子/](https://www.geeksforgeeks.org/java-program-count-number-palindrome-words-sentence/)

给定一个字符串 **str** ，任务是计算字符串 **str** 中的回文单词。
**例:**

```
Input : Madam Arora teaches malayalam
Output : 3
The string contains three palindrome words (i.e.,
Madam, Arora, malayalam) so the count is three.

Input : Nitin speaks malayalam
Output : 2
The string contains two palindrome words (i.e.,
Nitin, malayalam) so the count is two.
```

**countPalin()** 函数通过提取字符串的每个单词并将其传递给 **checkPalin()** 函数来计算回文单词的数量。在原始字符串中添加额外的空格来提取最后一个单词。
**checkPalin()** 功能检查单词回文。如果单词是回文，则返回 1，否则返回 0。它确保空字符串不会被视为回文，因为用户可能会在字符串之间或开头输入多个空格。

## C++

```
/*C++ program to count number of palindrome
words in a sentence*/
#include <bits/stdc++.h>
using namespace std;

// Function to check if a word is
// palindrome
bool checkPalin(string word)
{
    int n = word.length();
    transform(word.begin(), word.end(), word.begin(), ::tolower);

    for (int i = 0; i < n; i++,n--)
    if (word.at(i) != word.at(n - 1))
        return false;    
    return true;
}

// Function to count palindrome words
int countPalin(string str)
{        
    // to check last word for palindrome
    str = str + " ";

    // to store each word
    string word = "";
    int count = 0;
    for (int i = 0; i < str.length(); i++)
    {
        char ch = str.at(i);

        // extracting each word
        if (ch != ' ')
            word = word + ch;
        else {
            if (checkPalin(word))
                count++;
            word = "";
        }
    }

    return count;
}

// Driver code
int main()
{

    cout<<countPalin("Madam Arora teaches malayalam")<<endl;

    cout<<countPalin("Nitin speaks malayalam")<<endl;
}

// This code is contributed by nidhi16bcs2007
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Java program to count number of palindrome
words in a sentence*/
class GFG {

    // Function to check if a word is
    // palindrome
    static boolean checkPalin(String word)
    {
        int n = word.length();
        word = word.toLowerCase();
        for (int i=0; i<n; i++,n--)
           if (word.charAt(i) != word.charAt(n - 1))
              return false;      
        return true;
    }

    // Function to count palindrome words
    static int countPalin(String str)
    {       
        // to check last word for palindrome
        str = str + " ";

        // to store each word
        String word = "";
        int count = 0;
        for (int i = 0; i < str.length(); i++)
        {
            char ch = str.charAt(i);

            // extracting each word
            if (ch != ' ')
                word = word + ch;
            else {
                if (checkPalin(word))
                    count++;
                word = "";
            }
        }

        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.println(countPalin("Madam "
                  + "Arora teaches malayalam"));

        System.out.println(countPalin("Nitin "
                        + "speaks malayalam"));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count number of
# palindrome words in a sentence

# Function to check if a word is palindrome
def checkPalin(word):
    if word.lower() == word.lower()[::-1]:
        return True

# Function to count palindrome words
def countPalin(str):
    count = 0

    # splitting each word as spaces as
    # delimiter and storing it into a list
    listOfWords = str.split(" ")

    # Iterating every element from list
    # and checking if it is a palindrome.
    for elements in listOfWords:
        if (checkPalin(elements)):

            # if the word is a palindrome
            # increment the count.
            count += 1
    print (count)

# Driver code
countPalin("Madam Arora teaches malayalam")
countPalin("Nitin speaks malayalam")

# This code is contributed
# by Ronit Shrivastava.
```

## C#

```
// C# program to count number of
// palindrome words in a sentence
using System;

class GFG
{

// Function to check if a word is
// palindrome
public static bool checkPalin(string word)
{
    int n = word.Length;
    word = word.ToLower();
    for (int i = 0; i < n; i++,n--)
    {
    if (word[i] != word[n - 1])
    {
        return false;
    }
    }
    return true;
}

// Function to count palindrome words
public static int countPalin(string str)
{
    // to check last word for palindrome
    str = str + " ";

    // to store each word
    string word = "";
    int count = 0;
    for (int i = 0; i < str.Length; i++)
    {
        char ch = str[i];

        // extracting each word
        if (ch != ' ')
        {
            word = word + ch;
        }
        else
        {
            if (checkPalin(word))
            {
                count++;
            }
            word = "";
        }
    }

    return count;
}

// Driver code
public static void Main(string[] args)
{
    Console.WriteLine(countPalin("Madam " +
               "Arora teaches malayalam"));

    Console.WriteLine(countPalin("Nitin " +
                      "speaks malayalam"));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

/*Javascript program to count number of palindrome
words in a sentence*/

// Function to check if a word is
// palindrome
function checkPalin(word)
{
    var n = word.length
    word = word.toLowerCase();

    for (var i = 0; i < n; i++,n--)
    if (word[i] != word[n - 1])
        return false;    
    return true;
}

// Function to count palindrome words
function countPalin( str)
{        
    // to check last word for palindrome
    str = str + " ";

    // to store each word
    var word = "";
    var count = 0;
    for (var i = 0; i < str.length; i++)
    {
        var ch = str[i];

        // extracting each word
        if (ch != ' ')
            word = word + ch;
        else {
            if (checkPalin(word))
                count++;
            word = "";
        }
    }

    return count;
}

// Driver code
document.write( countPalin("Madam Arora teaches malayalam") + "<br>");

document.write( countPalin("Nitin speaks malayalam"));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
2
```

https://youtu.be/z

-5HChTA0ME