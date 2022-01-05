# 将所有搞笑文字打印成一串

> 原文:[https://www.geeksforgeeks.org/funny-string/](https://www.geeksforgeeks.org/funny-string/)

我们被判了刑。我们的任务是打印出那个句子中所有有趣的单词/字符串。

#### 什么是搞笑词？

反转给定的字符串。迭代字符串中的每个字符，比较位置 0 和 1、1 和 2、2 和 3 等字符的 ASCII 值的绝对差异，直到结束。如果两个字符串的绝对差异列表相同，则它们是有趣的，否则不是。

**示例:**

```
Input  : HKMNPS
Output : Yes
Let r be the reverse of original string s
s = "HKMNPS"
r = "SPNMKH"  
|H-K| = 3  = |S-P|         
|K-M| = 2  = |P-N|     
|M-N| = 1  = |N-M|
|N-P| = 2  = |M-K|
|P-S| = 3  = |K-H|
Since each comparison is equal so given string is funny

Input  : bdwy 
Output : No 
```

注:每一个[回文串](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)都是搞笑串，但不是反过来。

这个想法是将字符串拆分成单词。对于每个单词，从两端遍历并比较相邻字符之间的差异。

## C++

```
// C++ pprogram to print all
// funny words in a string
#include <bits/stdc++.h>
using namespace std;

bool checkFunny(string word)
{
    int i = 1;
    int j = word.length() - 2;
    for (int i = 0; i < word.length(); i++)
        word[i] = tolower(word[i]);

    while (i <= j)
    {
        if (abs(word[i] -
                word[i - 1]) != abs(word[j] -
                                    word[j + 1]))
            return false;
        i++;
        j--;
    }
    return true;
}

void printFunnyWords(string str)
{

    // to extract last word of sentence
    str += " ";

    // to word stores each word of sentence
    string word = "";

    for (int i = 0; i < str.length(); i++)
    {
        char ch = str[i];

        // extracting each wor
        if (ch != ' ')
            word += ch;
        else
        {
            if (checkFunny(word))
                cout << word << endl;
            word = "";
        }
    }
}

// Driver Code
int main()
{
    printFunnyWords("Miss Arora teaches us malayalam bdwy ");

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Funny {
    static boolean checkFunny(String word)
    {
        int i = 1;
        int j = word.length() - 2;
        word = word.toLowerCase();
        while (i <= j) {
            if ((Math.abs(word.charAt(i) - word.charAt(i - 1))) !=
                   Math.abs((word.charAt(j) - word.charAt(j + 1))))
                return false;
            i++;
            j--;
        }
        return true;
    }

    static void printFunnyWords(String str)
    {
        // to extract last word of sentence
        str = str + " ";

        // to word stores each word of sentence
        String word = "";

        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);

            // extracting each word
            if (ch != ' ')
                word = word + ch;
            else {
                if (Funny.checkFunny(word))
                    System.out.println(word);
                word = "";
            }
        }
    }

    public static void main(String[] args)
    {
        Funny.printFunnyWords("Miss Arora teaches us malayalam bdwy ");
    }
}
```

## 蟒蛇 3

```
# Python program to print all funny words in a string
def checkFunny(word):
    i = 1
    j = len(word) - 2
    word = word.lower()

    while (i <= j):
        if ((abs(ord(word[i]) - ord(word[i - 1])))
           != abs((ord(word[j]) - ord(word[j + 1])))):
            return False
        i = i + 1
        j = j - 1
    return True

def printFunnyWords(str):

    # to extract last word of sentence
    str = str + " "

    # to word stores each word of sentence
    word = ""
    i = 0
    for i in range(len(str)):
        ch = str[i]

        # extracting each word
        if (ch != ' '):
            word = word + ch
        else:
            if (checkFunny(word)):
                print (word)
            word = ""

# Driver code
printFunnyWords("Miss Arora teaches us malayalam bdwy ")

# This code is contributed by Prateek Bajaj
```

## C#

```
// C# program to print funny string
using System;

class GFG
{
public static bool checkFunny(string word)
{
    int i = 1;
    int j = word.Length - 2;
    word = word.ToLower();
    while (i <= j)
    {
        if ((Math.Abs(word[i] -
                      word[i - 1])) != Math.Abs((word[j] -
                                                 word[j + 1])))
        {
            return false;
        }
        i++;
        j--;
    }
    return true;
}

public static void printFunnyWords(string str)
{
    // to extract last word of sentence
    str = str + " ";

    // to word stores each word of sentence
    string word = "";

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
            if (GFG.checkFunny(word))
            {
                Console.WriteLine(word);
            }
            word = "";
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    GFG.printFunnyWords("Miss Arora teaches us " +
                               "malayalam bdwy ");
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript pprogram to print all
// funny words in a string

function checkFunny(word)
{
    var i = 1;
    var j = word.length - 2;
    word= (word.toLowerCase());

    while (i <= j)
    {
        if (Math.abs(word[i].charCodeAt(0) -
                word[i - 1].charCodeAt(0)) !=
                    Math.abs(word[j].charCodeAt(0) -
                                    word[j + 1].charCodeAt(0)))
            return false;
        i++;
        j--;
    }
    return true;
}

function printFunnyWords(str)
{

    // to extract last word of sentence
    str += " ";

    // to word stores each word of sentence
    var word = "";

    for (var i = 0; i < str.length; i++)
    {
        var ch = str[i];

        // extracting each wor
        if (ch != ' ')
            word += ch;
        else
        {
            if (checkFunny(word))
                document.write( word + "<br>");
            word = "";
        }
    }
}

// Driver Code
printFunnyWords("Miss Arora teaches us malayalam bdwy ");

</script>
```

**Output:** 

```
Arora
us
malayalam
bdwy
```