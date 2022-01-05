# 查找字符串中最小和最大单词的程序

> 原文:[https://www . geesforgeks . org/program-find-minist-maximum-word-string/](https://www.geeksforgeeks.org/program-find-smallest-largest-word-string/)

给定一个字符串，找出其中最小和最大长度的单词。
**例:**

```
Input : "This is a test string"
Output : Minimum length word: is
         Maximum length word: string

Input : "GeeksforGeeks A computer Science portal for Geeks"
Output : Minimum length word: A
         Maximum length word: GeeksforGeeks
```

**接近**

这个想法是保持一个开始指数 **si** 和一个结束指数 **ei** 。

*   si 指向一个新单词的开头，我们使用 ei 遍历字符串。
*   每当遇到空格或' 0 '字符时，我们使用(ei–si)计算当前单词的长度，并将其与迄今为止的最小和最大长度进行比较。
    *   如果少，更新**最小长度**和**最小起始索引**(指向最小长度字的起始)。
    *   如果更大，更新**最大长度**和**最大起始索引**(指向最大长度单词的起始处)。
*   最后更新 minWord 和 maxWord 这两个已经通过引用发送的输出字符串，子字符串分别从 min_start_index 和 max_start_index 开始，长度分别为 min_length 和 max_length。

## C++

```
// CPP Program to find Smallest and
// Largest Word in a String
#include<iostream>
#include<cstring>
using namespace std;

void minMaxLengthWords(string input, string &minWord, string &maxWord)
{
    // minWord and maxWord are received by reference
    // and not by value
    // will be used to store and return output
    int len = input.length();
    int si = 0, ei = 0;

    int min_length = len, min_start_index = 0, max_length = 0, max_start_index = 0;

    // Loop while input string is not empty
    while (ei <= len)
    {
        if (ei < len && input[ei] != ' ')
            ei++;

        else
        {
            // end of a word
            // find curr word length
            int curr_length = ei - si;

            if (curr_length < min_length)
            {
                min_length = curr_length;
                min_start_index = si;
            }

            if (curr_length > max_length)
            {
                max_length = curr_length;
                max_start_index = si;
            }
            ei++;
            si = ei;
        }
    }

    // store minimum and maximum length words
    minWord = input.substr(min_start_index, min_length);
    maxWord = input.substr(max_start_index, max_length);
}

// Driver code
int main()
{
    string a = "GeeksforGeeks A Computer Science portal for Geeks";
    string minWord, maxWord;
    minMaxLengthWords(a, minWord, maxWord);

    // to take input in string use getline(cin, a);
    cout << "Minimum length word: "
        << minWord << endl
        << "Maximum length word: "
        << maxWord << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Smallest and
// Largest Word in a String
class GFG
{

    static String minWord = "", maxWord = "";

    static void minMaxLengthWords(String input)
    {
          input=input.trim();//Triming any space before the String else space at start would be consider as smallest word     
        // minWord and maxWord are received by reference
        // and not by value
        // will be used to store and return output

        int len = input.length();
        int si = 0, ei = 0;
        int min_length = len, min_start_index = 0,
              max_length = 0, max_start_index = 0;

        // Loop while input string is not empty
        while (ei <= len)
        {
            if (ei < len && input.charAt(ei) != ' ')
            {
                ei++;
            }
            else
            {
                // end of a word
                // find curr word length
                int curr_length = ei - si;

                if (curr_length < min_length)
                {
                    min_length = curr_length;
                    min_start_index = si;
                }

                if (curr_length > max_length)
                {
                    max_length = curr_length;
                    max_start_index = si;
                }
                ei++;
                si = ei;
            }
        }

        // store minimum and maximum length words
        minWord = input.substring(min_start_index, min_start_index + min_length);
        maxWord = input.substring(max_start_index, max_start_index+max_length);//Earlier  code was not working if the largests word is inbetween String
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "GeeksforGeeks A Computer Science portal for Geeks";

        minMaxLengthWords(a);

        // to take input in string use getline(cin, a);
        System.out.print("Minimum length word: "
                + minWord
                + "\nMaximum length word: "
                + maxWord);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find Smallest and
# Largest Word in a String

# defining the method to find the longest
# word and the shortest word
def minMaxLengthWords(inp):
    length = len(inp)
    si = ei = 0
    min_length = length
    min_start_index = max_length = max_start_index = 0

    # loop to find the length and stating index
    # of both longest and shortest words
    while ei <= length:
        if (ei < length) and (inp[ei] != " "):
            ei += 1
        else:
            curr_length = ei - si

            # condition checking for the shortest word
            if curr_length < min_length:
                min_length = curr_length
                min_start_index = si

            # condition for the longest word
            if curr_length > max_length:
                max_length = curr_length
                max_start_index = si
            ei += 1
            si = ei

    # extracting the shortest word using
    # it's starting index and length    
    minWord = inp[min_start_index :
                  min_start_index + min_length]

    # extracting the longest word using
    # it's starting index and length    
    maxWord = inp[max_start_index : max_length]

    # printing the final result
    print("Minimum length word: ", minWord)
    print ("Maximum length word: ", maxWord)

# Driver Code

# Using this string to test our code
a = "GeeksforGeeks A Computer Science portal for Geeks"
minMaxLengthWords(a)

# This code is contributed by Animesh_Gupta
```

## C#

```
// C# Program to find Smallest and
// Largest Word in a String
using System;

class GFG
{

    static String minWord = "", maxWord = "";

    static void minMaxLengthWords(String input)
    {
        // minWord and maxWord are received by reference
        // and not by value
        // will be used to store and return output
        int len = input.Length;
        int si = 0, ei = 0;
        int min_length = len, min_start_index = 0,
            max_length = 0, max_start_index = 0;

        // Loop while input string is not empty
        while (ei <= len)
        {
            if (ei < len && input[ei] != ' ')
            {
                ei++;
            }
            else
            {
                // end of a word
                // find curr word length
                int curr_length = ei - si;

                if (curr_length < min_length)
                {
                    min_length = curr_length;
                    min_start_index = si;
                }

                if (curr_length > max_length)
                {
                    max_length = curr_length;
                    max_start_index = si;
                }
                ei++;
                si = ei;
            }
        }

        // store minimum and maximum length words
        minWord = input.Substring(min_start_index, min_length);
        maxWord = input.Substring(max_start_index, max_length);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String a = "GeeksforGeeks A Computer Science portal for Geeks";

        minMaxLengthWords(a);

        // to take input in string use getline(cin, a);
        Console.Write("Minimum length word: "
                + minWord
                + "\nMaximum length word: "
                + maxWord);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program to find Smallest and
// Largest Word in a String

let minWord = "";
let maxWord = "";

function minMaxLengthWords(input)
{
    // minWord and maxWord are received by reference
    // and not by value
    // will be used to store and return output
    let len = input.length;
    let si = 0, ei = 0;
    let min_length = len;
    let min_start_index = 0;
    let max_length = 0;
    let max_start_index = 0;

    // Loop while input string is not empty
    while (ei <= len)
    {
        if (ei < len && input[ei] != ' ')
        {
            ei++;
        }
        else
        {
            // end of a word
            // find curr word length
            let curr_length = ei - si;

            if (curr_length < min_length)
            {
                min_length = curr_length;
                min_start_index = si;
            }

            if (curr_length > max_length)
            {
                max_length = curr_length;
                max_start_index = si;
            }
            ei++;
            si = ei;
        }
    }

    // store minimum and maximum length words
    minWord =
    input.substring(min_start_index,min_start_index + min_length);

    maxWord =
    input.substring(max_start_index, max_length);

}

// Driver code

let a = "GeeksforGeeks A Computer Science portal for Geeks";

minMaxLengthWords(a);

// to take input in string use getline(cin, a);
document.write("Minimum length word: "
        + minWord+"<br>"
        + "Maximum length word:  "
        + maxWord);

</script>
```

**Output**

```
Minimum length word: A
Maximum length word: GeeksforGeeks
```

本文由**阿迪提·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。