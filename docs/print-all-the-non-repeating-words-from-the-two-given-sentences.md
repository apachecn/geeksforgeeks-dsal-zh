# 打印两个给定句子中所有不重复的单词

> 原文:[https://www . geeksforgeeks . org/print-两个给定句子中所有不重复的单词/](https://www.geeksforgeeks.org/print-all-the-non-repeating-words-from-the-two-given-sentences/)

给定两个字符串 **A** 和 **B** ，任务是打印两个给定句子中所有不重复的单词。
**例:**

> **输入:** A =“我有蓝笔”，B =“我有红笔”
> **输出:**有蓝有红
> **解释:**
> have、blue、got 和 red 这几个词在同一个句子或另一个句子中都没有重复。
> **输入:** A =“我要停车”，B =“我在停车”
> **输出:**要进去

**方法:**想法是[迭代所有单词](https://www.geeksforgeeks.org/how-to-iterate-through-a-string-word-by-word-in-c/)，检查单词是否重复。因此，可以按照以下步骤计算答案:

1.  [连接两个字符串](https://www.geeksforgeeks.org/methods-to-concatenate-string-in-c-c-with-examples/)并将其存储在另一个字符串变量中。
2.  [从连接的字符串中提取一个单词](https://www.geeksforgeeks.org/program-extract-words-given-string/)。
3.  如果该单词出现在 A 或 B 中，则将其打印出来。否则，继续余下的单词。

以下是上述方法的实现:

## C++

```
// C++ program to print all the
// non-repeating words from the
// two given sentences

#include <bits/stdc++.h>
#include <string.h>
using namespace std;

// Function to print all the
// non-repeating words from the
// two given sentences
void removeRepeating(string s1, string s2)
{
    // Concatenate the two strings
    // into one
    string s3 = s1 + " " + s2 + " ";
    string words = "";
    int i = 0;

    // Iterating over the whole
    // concatenated string
    for (auto x : s3) {
        if (x == ' ') {

            // Searching for the word in A.
            // If while searching, we reach
            // the end of the string, then
            // the word is not present in
            // the string
            if (s1.find(words) == string::npos
                || s2.find(words) == string::npos)
                cout << words;

            // Initialise word for the
            // next iteration
            words = "";
        }
        else {
            words = words + x;
        }
    }
}

// Driver code
int main()
{
    string s1 = "I have go a pen";
    string s2 = "I want to go park";
    removeRepeating(s1, s2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the
// non-repeating words from the
// two given sentences
class GFG{

// Function to print all the
// non-repeating words from the
// two given sentences
static void removeRepeating(String s1, String s2)
{

    // Concatenate the two Strings
    // into one
    String s3 = s1 + " " + s2 + " ";
    String words = "";
    int i = 0;

    // Iterating over the whole
    // concatenated String
    for(char x : s3.toCharArray())
    {
       if (x == ' ')
       {

           // Searching for the word in A.
           // If while searching, we reach
           // the end of the String, then
           // the word is not present in
           // the String
           if (!s1.contains(words) ||
               !s2.contains(words))
               System.out.print(words);

           // Initialise word for the
           // next iteration
           words = " ";
       }
       else
       {
           words = words + x;
       }
    }
}

// Driver code
public static void main(String[] args)
{
    String s1 = "I have go a pen";
    String s2 = "I want to go park";

    removeRepeating(s1, s2);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to print all the
# non-repeating words from the
# two given sentences

# Function to print all the
# non-repeating words from the
# two given sentences
def removeRepeating(s1, s2):

    # Concatenate the two
    # strings into one
    s3 = s1 + " " + s2 + " "
    words = ""
    i = 0

    # Iterating over the whole
    # concatenated string
    for x in s3:
        if (x == ' '):

            # Searching for the word in A.
            # If while searching, we reach
            # the end of the string, then
            # the word is not present in
            # the string
            if (words not in s1 or
                words not in s2):
                print(words, end = "")

            # Initialise word for the
            # next iteration
            words = " "

        else:
            words = words + x

# Driver code
if __name__ == "__main__":

    s1 = "I have go a pen"
    s2 = "I want to go park"
    removeRepeating(s1, s2)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to print all the
// non-repeating words from the
// two given sentences
using System;
class GFG{

// Function to print all the
// non-repeating words from the
// two given sentences
static void removeRepeating(string s1,
                            string s2)
{

    // Concatenate the two Strings
    // into one
    string s3 = s1 + " " + s2 + " ";
    string words = "";
    int i = 0;

    // Iterating over the whole
    // concatenated String
    foreach(char x in s3.ToCharArray())
    {
       if (x == ' ')
       {

           // Searching for the word in A.
           // If while searching, we reach
           // the end of the String, then
           // the word is not present in
           // the String
           if (!s1.Contains(words) ||
               !s2.Contains(words))
               Console.Write(words);

           // Initialise word for the
           // next iteration
           words = " ";
       }
       else
       {
           words = words + x;
       }
    }
}

// Driver code
public static void Main(string[] args)
{
    string s1 = "I have go a pen";
    string s2 = "I want to go park";

    removeRepeating(s1, s2);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to print all the
// non-repeating words from the
// two given sentences

// Function to print all the
// non-repeating words from the
// two given sentences
function removeRepeating(s1,s2)
{

    // Concatenate the two Strings
    // into one
    let s3 = s1 + " " + s2 + " ";
    let words = "";
    let i = 0;

    // Iterating over the whole
    // concatenated String
    let temp = s3.split("")
    for(let x = 0; x < temp.length; x++)
    {
       if (temp[x] == ' ')
       {

           // Searching for the word in A.
           // If while searching, we reach
           // the end of the String, then
           // the word is not present in
           // the String
           if (!s1.includes(words) ||
               !s2.includes(words))
               document.write(words);

           // Initialise word for the
           // next iteration
           words = " ";
       }
       else
       {
           words = words + temp[x];
       }
    }
}

// Driver code
let s1 = "I have go a pen";
let s2 = "I want to go park";
removeRepeating(s1, s2);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
have a pen I want to park
```