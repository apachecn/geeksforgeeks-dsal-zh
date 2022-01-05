# 在以大写字母开头的单词之间留出空格

> 原文:[https://www . geesforgeks . org/put-spaces-word-start-大写-字母/](https://www.geeksforgeeks.org/put-spaces-words-starting-capital-letters/)

给你一组基本上是一个句子的字符。然而，不同的单词之间没有空格，每个单词的第一个字母都是大写的。您需要在以下修改后打印这句话:
(i)在这些单词之间放一个空格。
(二)将大写字母转换为小写字母。

**示例:**

```
Input : BruceWayneIsBatman
Output : bruce wayne is batman

Input :  You
Output :  you
```

我们检查当前字符是否为大写，然后打印" "(空格)并将其转换为小写。

## C++

```
// C++ program to put spaces between words starting
// with capital letters.
#include <iostream>
using namespace std;

// Function to amend the sentence
void amendSentence(string str)
{
    // Traverse the string
    for(int i=0; i < str.length(); i++)
    {
        // Convert to lowercase if its
        // an uppercase character
        if (str[i]>='A' && str[i]<='Z')
        {
            str[i]=str[i]+32;

            // Print space before it
            // if its an uppercase character
            if (i != 0)
                cout << " ";

            // Print the character
            cout << str[i];
        }

        // if lowercase character
        // then just print
        else
            cout << str[i];
    }
}

// Driver code
int main()
{
    string str ="BruceWayneIsBatman";
    amendSentence(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to put spaces between words starting
// with capital letters.

import java.util.*;
import java.lang.*;
import java.io.*;

class AddSpaceinSentence
{
    // Function to amend the sentence
    public static void amendSentence(String sstr)
    {
        char[] str=sstr.toCharArray();

        // Traverse the string
        for (int i=0; i < str.length; i++)
        {
            // Convert to lowercase if its
            // an uppercase character
            if (str[i]>='A' && str[i]<='Z')
            {
                str[i] = (char)(str[i]+32);

                // Print space before it
                // if its an uppercase character
                if (i != 0)
                    System.out.print(" ");

                // Print the character
                System.out.print(str[i]);
            }

            // if lowercase character
            // then just print
            else
            System.out.print(str[i]);
        }
    }    

    // Driver Code
    public static void main (String[] args)
    {
        String str ="BruceWayneIsBatman";
        amendSentence(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to put spaces between words
# starting with capital letters.

# Function to amend the sentence
def amendSentence(string):
    string = list(string)

    # Traverse the string
    for i in range(len(string)):

        # Convert to lowercase if its
        # an uppercase character
        if string[i] >= 'A' and string[i] <= 'Z':
            string[i] = chr(ord(string[i]) + 32)

            # Print space before it
            # if its an uppercase character
            if i != 0:
                print(" ", end = "")

            # Print the character
            print(string[i], end = "")

        # if lowercase character
        # then just print
        else:
            print(string[i], end = "")

# Driver Code
if __name__ == "__main__":
    string = "BruceWayneIsBatman"
    amendSentence(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to put spaces between words
// starting with capital letters.
using System;

public class GFG {

    // Function to amend the sentence
    public static void amendSentence(string sstr)
    {
        char[] str = sstr.ToCharArray();

        // Traverse the string
        for (int i = 0; i < str.Length; i++)
        {

            // Convert to lowercase if its
            // an uppercase character
            if (str[i] >= 'A' && str[i] <= 'Z')
            {
                str[i] = (char)(str[i] + 32);

                // Print space before it
                // if its an uppercase
                // character
                if (i != 0)
                    Console.Write(" ");

                // Print the character
                Console.Write(str[i]);
            }

            // if lowercase character
            // then just print
            else
                Console.Write(str[i]);
        }
    }

    // Driver Code
    public static void Main ()
    {
        string str ="BruceWayneIsBatman";

        amendSentence(str);
    }

}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>

    // JavaScript program to put spaces between words
    // starting with capital letters.

    // Function to amend the sentence
    function amendSentence(sstr)
    {
        let str = sstr.split('');

        // Traverse the string
        for (let i = 0; i < str.length; i++)
        {

            // Convert to lowercase if its
            // an uppercase character
            if (str[i].charCodeAt() >= 'A'.charCodeAt() &&
            str[i].charCodeAt() <= 'Z'.charCodeAt())
            {
              str[i] =
              String.fromCharCode(str[i].charCodeAt() + 32);

                // Print space before it
                // if its an uppercase
                // character
                if (i != 0)
                    document.write(" ");

                // Print the character
                document.write(str[i]);
            }

            // if lowercase character
            // then just print
            else
                document.write(str[i]);
        }
    }

    let str ="BruceWayneIsBatman";

      amendSentence(str);

</script>
```

**输出:**

```
bruce wayne is batman
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。