# 打印一个句子中最长的回文单词

> 原文:[https://www . geesforgeks . org/print-最长-回文-单词-句子/](https://www.geeksforgeeks.org/print-longest-palindrome-word-sentence/)

给定一个字符串 **str** ，任务是打印字符串 **str** 中存在的最长回文单词。
**例:**

> 输入:阿罗拉夫人教马拉雅拉姆语
> 输出:马拉雅拉姆语
> **解释:**该字符串包含三个回文单词(即夫人、阿罗拉、马拉雅拉姆语)，但马拉雅拉姆语的长度大于其他两个。
> 输入:欢迎使用 GeeksforGeeks
> 输出:无回文词
> **解释:**字符串不包含任何回文词，所以输出为无回文词。

**<u>进场:</u>**

*   **longestPalin()** 函数通过提取字符串的每个单词并将其传递给 checkPalin()函数来查找最长的回文单词。在原始字符串中添加额外的空格来提取最后一个单词。
*   **checkPalin()** 函数检查单词是否是回文。如果单词是回文，则返回 true，否则返回 false。它确保空字符串不会被视为回文，因为用户可能会在字符串之间或开头输入多个空格。

## C++

```
/* C++ program to print longest palindrome
word in a sentence and its length*/
#include <iostream>
#include <algorithm>
#include <string>

using namespace std;

// Function to check if a
// word is palindrome
bool checkPalin(string word)
{
    int n = word.length();

    // making the check case
    // case insensitive
    // word = word.toLowerCase();
    transform(word.begin(), word.end(),
              word.begin(), ::tolower);

    // loop to check palindrome
    for (int i = 0; i < n; i++, n--)
        if (word[i] != word[n - 1])
            return false;

    return true;
}

// Function to find longest
// palindrome word
string longestPalin(string str)
{

    // to check last word for palindrome
    str = str + " ";

    // to store each word
    string longestword = "", word = "";

    int length, length1 = 0;
    for (int i = 0; i < str.length(); i++)
    {
        char ch = str[i];

        // extracting each word
        if (ch != ' ')
            word = word + ch;
        else {
            length = word.length();
            if (checkPalin(word) &&
                       length > length1)
            {
                length1 = length;
                longestword = word;
            }

            word = "";
        }
    }

    return longestword;
}

// Driver code
int main()
{
    string s = "My name is ava and i love"
                         " Geeksforgeeks";

    if (longestPalin(s) == "")
        cout<<"No Palindrome"<<" Word";
    else
        cout<<longestPalin(s);
    return 0;
}

// This code is contributed by Manish
// Shaw (manishshaw1)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Java program to print longest palindrome
word in a sentence and its length*/

public class GFG {

    // Function to check if a
    // word is palindrome
    static boolean checkPalin(String word)
    {
        int n = word.length();

        // making the check case
        // case insensitive
        word = word.toLowerCase();

        // loop to check palindrome
        for (int i = 0; i < n; i++, n--)
            if (word.charAt(i) !=
                       word.charAt(n - 1))
                return false;

        return true;
    }

    // Function to find longest
    // palindrome word
    static String longestPalin(String str)
    {
        // to check last word for palindrome
        str = str + " ";

        // to store each word
        String longestword = "", word = "";

        int length, length1 = 0;
        for (int i = 0; i < str.length(); i++)
        {
            char ch = str.charAt(i);

            // extracting each word
            if (ch != ' ')
                word = word + ch;
            else {
                length = word.length();
                if (checkPalin(word) &&
                             length > length1)
                {
                    length1 = length;
                    longestword = word;
                }

                word = "";
            }
        }

        return longestword;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = new String("My name is ava "
                + "and i love Geeksforgeeks");

        if (longestPalin(s) == "")
            System.out.println("No Palindrome"
                            + " Word");
        else
            System.out.println(longestPalin(s));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to print longest palindrome
# word in a sentence and its length

# Function to check if a word is palindrome
def checkPalin(word):

    n = len(word)

    # making the check case
    # case insensitive
    word = word.lower()

    # loop to check palindrome
    for i in range( n):
        if (word[i] != word[n - 1]):
            return False
        n -= 1

    return True

# Function to find longest
# palindrome word
def longestPalin(str):

    # to check last word for palindrome
    str = str + " "

    # to store each word
    longestword = ""
    word = ""

    length1 = 0
    for i in range(len(str)):
        ch = str[i]

        # extracting each word
        if (ch != ' '):
            word = word + ch
        else :
            length = len(word)
            if (checkPalin(word) and
                length > length1):
                length1 = length
                longestword = word

            word = ""

    return longestword

# Driver code
if __name__ == "__main__":

    s = "My name is ava and i love Geeksforgeeks"

    if (longestPalin(s) == ""):
        print("No Palindrome Word")
    else:
        print(longestPalin(s))

# This code is contributed by ita_c
```

## C#

```
/* C# program to print longest palindrome
word in a sentence and its length*/
using System;
class GFG
{
    // Function to check if a
    // word is palindrome
    static bool checkPalin(string word)
    {
        int n = word.Length;

        // making the check case
        // case insensitive
        word = word.ToLower();

        // loop to check palindrome
        for (int i = 0; i < n; i++, n--)
            if (word[i] != word[n - 1])
                return false;

        return true;
    }

    // Function to find longest
    // palindrome word
    static string longestPalin(string str)
    {

        // to check last word for palindrome
        str = str + " ";

        // to store each word
        string longestword = "", word = "";

        int length, length1 = 0;
        for (int i = 0; i < str.Length; i++)
        {
            char ch = str[i];

            // extracting each word
            if (ch != ' ')
                word = word + ch;
            else {
                length = word.Length;
                if (checkPalin(word) &&
                        length > length1)
                {
                    length1 = length;
                    longestword = word;
                }

                word = "";
            }
        }

        return longestword;
    }

    // Driver code
    public static void Main()
    {
        string s = "My name is ava and i"
           + " love Geeksforgeeks";

        if (longestPalin(s) == "")
            Console.Write("No Palindrome Word");
        else
            Console.Write(longestPalin(s));
    }
}

// This code is contributed by Manish
// Shaw (manishshaw1)
```

## java 描述语言

```
<script>
/*Javascript program to print longest palindrome
word in a sentence and its length*/

    // Function to check if a
    // word is palindrome
    function checkPalin(word)
    {
        let n = word.length;

        // making the check case
        // case insensitive
        word = word.toLowerCase();

        // loop to check palindrome
        for (let i = 0; i < n; i++, n--)
            if (word[i] !=
                       word[n-1])
                return false;

        return true;
    }

    // Function to find longest
    // palindrome word
    function longestPalin(str)
    {
        // to check last word for palindrome
        str = str + " ";

        // to store each word
        let longestword = "", word = "";

        let length, length1 = 0;
        for (let i = 0; i < str.length; i++)
        {
            let ch = str[i];

            // extracting each word
            if (ch != ' ')
                word = word + ch;
            else {
                length = word.length;
                if (checkPalin(word) &&
                             length > length1)
                {
                    length1 = length;
                    longestword = word;
                }

                word = "";
            }
        }

        return longestword;
    }

    // Driver code
    let s="My name is ava "
                + "and i love Geeksforgeeks";
    if (longestPalin(s) == "")
        document.write("No Palindrome"
                            + " Word");
    else
        document.write(longestPalin(s));

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
ava
```

#### 方法二:使用 Python 中的 [**排序()**](https://www.geeksforgeeks.org/sorted-function-python/) 方法:

*   其思路是将 [**分裂**](https://www.geeksforgeeks.org/python-string-split/) 的单词串成一个列表。
*   遍历列表并将所有回文单词追加到新列表中
*   使用 sorted()方法按单词长度的递增顺序对新列表进行排序。
*   最后，打印列表中的最后一个字符串。

下面是上述方法的实现。：

## 蟒蛇 3

```
# Python3 program for the above approach
def ispalindrome(string):
    if(string == string[::-1]):
        return True
    else:
        return False

def largestPalin(s):

    # Taking new list
    newlist = []

    # Traverse the list
    for i in s:
        if(ispalindrome(i)):
            newlist.append(i)

    # Using sorted() method
    s = sorted(newlist, key=len)

    # Print last word
    print(s[len(s)-1])

# Driver Code
if __name__ == "__main__":

    # Given string
    s = "My name is ava and i love Geeksforgeeks"

    # Convert string to list
    l = list(s.split(" "))

    largestPalin(l)

# This code is contributed by vikkycirus
```

**输出:**

```
ava
```