# 根据输入字符串中出现的字符生成两个输出字符串。

> 原文:[https://www . geeksforgeeks . org/generate-two-output-strings-取决于出现的情况-character-input-string/](https://www.geeksforgeeks.org/generate-two-output-strings-depending-upon-occurrence-character-input-string/)

给定一个输入字符串 str[]，生成两个输出字符串。其中一个由在输入字符串中只出现一次的字符组成，第二个由多次出现的字符组成。输出字符串必须排序。
**例:**

```
Input : str[] = "geeksforgeeks"
Output : String with characters occurring once:
for
String with characters occurring multiple times:
egks

Input : str[] = "geekspractice"
Output : String with characters occurring once:
agikprst
String with characters occurring multiple times:
ce
```

**方法:**我们总共遵循两步来生成两个输出字符串。
**步骤 1:** 创建一个计数数组，并对给定输入字符串中出现的字符进行计数。
**步骤 2:** 检查每个位置“I”的计数数组，这导致三种可能的情况:
a)如果计数值为 1，则在第一个输出字符串中追加字符。
b)如果计数值大于 1，则在第二个输出字符串中追加字符。
c)如果计数值为 0，则不执行任何操作。
上述方法的时间复杂度为 0(n)。
所需辅助空间为 0(1)。

## C++

```
// CPP program to print two strings
// made of character occurring once
// and multiple times
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 256;

// function to print two strings
// generated from single string one
// with characters occurring onces
// other with character occurring
// multiple of times
void printDuo(string &str)
{
    // initialize hashtable with zero
    // entry
    int countChar[MAX_CHAR] = { 0 };

    // perform hashing for input string
    int n = str.length();
    for (int i = 0; i < n; i++)
        countChar[str[i] - 'a']++;

    // generate string (str1) consisting
    // char occurring once and string
    // (str2) consisting char occurring
    // multiple times
    string str1 = "", str2 = ""; 
    for (int i = 0; i < MAX_CHAR; i++) {
        if (countChar[i] > 1)
            str2 = str2 + (char)(i + 'a');
        else if (countChar[i] == 1)
            str1 = str1 + (char)(i + 'a');
    }

    // print both strings
    cout << "String with characters occurring "
         <<  "once:\n";
    cout << str1 << "\n";
    cout << "String with characters occurring "
         << "multiple times:\n";
    cout << str2 << "\n";
}

// driver program
int main()
{
    string str = "lovetocode";
    printDuo(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print two strings
// made of character occurring once
// and multiple times

class GFG {

    final static int MAX_CHAR = 256;

// function to print two strings
// generated from single string one
// with characters occurring onces
// other with character occurring
// multiple of times
    static void printDuo(String str) {
        // initialize hashtable with zero
        // entry
        int countChar[] = new int[MAX_CHAR];

        // perform hashing for input string
        int n = str.length();
        for (int i = 0; i < n; i++) {
            countChar[str.charAt(i) - 'a']++;
        }

        // generate string (str1) consisting
        // char occurring once and string
        // (str2) consisting char occurring
        // multiple times
        String str1 = "", str2 = "";
        for (int i = 0; i < MAX_CHAR; i++) {
            if (countChar[i] > 1) {
                str2 = str2 + (char) (i + 'a');
            } else if (countChar[i] == 1) {
                str1 = str1 + (char) (i + 'a');
            }
        }

        // print both strings
        System.out.print("String with characters occurring "
                + "once:\n");
        System.out.print(str1 + "\n");
        System.out.print("String with characters occurring "
                + "multiple times:\n");
        System.out.print(str2 + "\n");
        System.out.print("");
    }

// driver program
    public static void main(String[] args) {
        String str = "lovetocode";
        printDuo(str);

    }
}
//this code contributed by 29AJayKumar
```

## 蟒蛇 3

```
# Python3 program to print two strings
# made of character occurring once
# and multiple times

MAX_CHAR = 256

# function to print two strings
# generated from single string one
# with characters occurring onces
# other with character occurring
# multiple of times
def printDuo(string):

    # initialize hashtable with zero
    # entry
    countChar = [0 for i in range(MAX_CHAR)]

    # perform hashing for input string
    n = len(string)
    for i in range(n):
        countChar[ord(string[i]) - ord('a')] += 1

    # generate string (str1) consisting
    # char occurring once and string
    # (str2) consisting char occurring
    # multiple times
    str1 = ""
    str2 = ""
    for i in range(MAX_CHAR):
        if (countChar[i] > 1):
            str2 = str2 + chr(i + ord('a'))
        elif (countChar[i] == 1):
            str1 = str1 + chr(i + ord('a'))

    # print both strings
    print("String with characters occurring once:",
                                        "\n", str1)
    print("String with characters occurring",
               "multiple times:", "\n", str2)

# Driver Code
string = "lovetocode"
printDuo(string)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to print two strings
// made of character occurring once
// and multiple times
using System;

class GFG
{
static int MAX_CHAR = 256;

// function to print two strings
// generated from single string one
// with characters occurring onces
// other with character occurring
// multiple of times
static void printDuo(string str)
{
    // initialize hashtable with zero
    // entry
    int[] countChar = new int[MAX_CHAR];

    // perform hashing for input string
    int n = str.Length;
    for (int i = 0; i < n; i++)
    {
        countChar[str[i] - 'a']++;
    }

    // generate string (str1) consisting
    // char occurring once and string
    // (str2) consisting char occurring
    // multiple times
    string str1 = "", str2 = "";
    for (int i = 0; i < MAX_CHAR; i++)
    {
        if (countChar[i] > 1)
        {
            str2 = str2 + (char) (i + 'a');
        }
        else if (countChar[i] == 1)
        {
            str1 = str1 + (char) (i + 'a');
        }
    }

    // print both strings
    Console.Write("String with characters "+
                       "occurring once:\n");
    Console.Write(str1 + "\n");
    Console.Write("String with characters occurring " +
                                  "multiple times:\n");
    Console.Write(str2 + "\n");
    Console.Write("");
}

// Driver Code
public static void Main()
{
    string str = "lovetocode";
    printDuo(str);
}
}

// This code is contributed by ita_c
```

## java 描述语言

```
<script>

// javascript program to print two strings
// made of character occurring once
// and multiple times

var MAX_CHAR = 256;

// function to print two strings
// generated from single string one
// with characters occurring onces
// other with character occurring
// multiple of times
function printDuo(str)
{
    // initialize hashtable with zero
    // entry
    var countChar = Array(MAX_CHAR).fill(0);

    // perform hashing for input string
    var n = str.length;
    for (var i = 0; i < n; i++)
        countChar[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // generate string (str1) consisting
    // char occurring once and string
    // (str2) consisting char occurring
    // multiple times
    var str1 = "", str2 = ""; 
    for (var i = 0; i < MAX_CHAR; i++) {
        if (countChar[i] > 1)
            str2 = str2 + String.fromCharCode(i + 'a'.charCodeAt(0));
        else if (countChar[i] == 1)
            str1 = str1 + String.fromCharCode(i + 'a'.charCodeAt(0));
    }

    // print both strings
    document.write( "String with characters occurring "
         +  "once:<br>");
    document.write( str1 + "<br>");
    document.write( "String with characters occurring "
         + "multiple times:<br>");
    document.write( str2 + "<br>");
}

// driver program
var str = "lovetocode";
printDuo(str);

</script>
```

**输出:**

```
String with characters occurring once:
cdltv
String with characters occurring multiple times:
eo
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.linkedin.com/in/imanuj/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。