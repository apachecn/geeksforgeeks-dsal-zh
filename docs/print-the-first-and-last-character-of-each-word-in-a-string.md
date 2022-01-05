# 打印字符串中每个单词的第一个和最后一个字符

> 原文:[https://www . geesforgeks . org/print-字符串中每个单词的第一个和最后一个字符/](https://www.geeksforgeeks.org/print-the-first-and-last-character-of-each-word-in-a-string/)

给定一个字符串，任务是打印字符串中每个单词的第一个和最后一个字符。
**例:**

```
Input: Geeks for geeks
Output: Gs fr gs

Input: Computer applications
Output: Cr as
```

**接近**T2】

1.  从第一个字母到最后一个字母循环。
2.  打印字符串的第一个和最后一个字母。
3.  如果字符串中有空格，则打印位于空格前和空格后的字符。

下面是上述方法的实现。

## C++

```
// CPP program to print
// the first and last character
// of each word in a String'
#include<bits/stdc++.h>
using namespace std;

// Function to print the first
// and last character of each word.
void FirstAndLast(string str)
{
    int i;

    for (i = 0; i < str.length(); i++)
    {
        // If it is the first word
        // of the string then print it.
        if (i == 0)
            cout<<str[i];

        // If it is the last word of the string
        // then also print it.
        if (i == str.length() - 1)
            cout<<str[i];

        // If there is a space
        // print the successor and predecessor
        // to space.
        if (str[i] == ' ')
        {
            cout<<str[i-1]<<" "<<str[i+1];
        }
    }
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";
    FirstAndLast(str);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// the first and last character
// of each word in a String

class GFG {

    // Function to print the first
    // and last character of each word.
    static void FirstAndLast(String str)
    {
        int i;

        for (i = 0; i < str.length(); i++) {

            // If it is the first word
            // of the string then print it.
            if (i == 0)
                System.out.print(str.charAt(i));

            // If it is the last word of the string
            // then also print it.
            if (i == str.length() - 1)
                System.out.print(str.charAt(i));

            // If there is a space
            // print the successor and predecessor
            // to space.
            if (str.charAt(i) == ' ') {
                System.out.print(str.charAt(i - 1)
                                 + " "
                                 + str.charAt(i + 1));
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "Geeks for Geeks";
        FirstAndLast(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print
# the first and last character
# of each word in a String'

# Function to print the first
# and last character of each word.
def FirstAndLast(string):
    for i in range(len(string)):

        # If it is the first word
        # of the string then print it.
        if i == 0:
            print(string[i], end = "")

        # If it is the last word of the string
        # then also print it.
        if i == len(string) - 1:
            print(string[i], end = "")

        # If there is a space
        # print the successor and predecessor
        # to space.
        if string[i] == " ":
            print(string[i - 1],
                  string[i + 1], end = "")

# Driver code
if __name__ == "__main__":
    string = "Geeks for Geeks"
    FirstAndLast(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print
// the first and last character
// of each word in a String
using System;

class GFG
{

    // Function to print the first
    // and last character of each word.
    static void FirstAndLast(string str)
    {
        int i;

        for (i = 0; i < str.Length; i++)
        {

            // If it is the first word
            // of the string then print it.
            if (i == 0)
                Console.Write(str[i]);

            // If it is the last word of the string
            // then also print it.
            if (i == str.Length - 1)
                Console.Write(str[i]);

            // If there is a space
            // print the successor and predecessor
            // to space.
            if (str[i] == ' ')
            {
                Console.Write(str[i - 1]
                                + " "
                                + str[i + 1]);
            }
        }
    }

    // Driver code
    public static void Main()
    {
        string str = "Geeks for Geeks";
        FirstAndLast(str);
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

      // JavaScript program to print
      // the first and last character
      // of each word in a String'

      // Function to print the first
      // and last character of each word.
      function FirstAndLast(str)
      {
        for (var i = 0; i < str.length; i++)
        {
          // If it is the first word
          // of the string then print it.
          if (i == 0)
          document.write(str[i]);

          // If it is the last word of the string
          // then also print it.
          if (i == str.length - 1)
          document.write(str[i]);

          // If there is a space
          // print the successor and predecessor
          // to space.
          if (str[i] === " ") {
            document.write(str[i - 1] + " " + str[i + 1]);
          }
        }
      }

      // Driver code
      var str = "Geeks for Geeks";
      FirstAndLast(str);

 </script>
```

**Output:** 

```
Gs fr Gs
```