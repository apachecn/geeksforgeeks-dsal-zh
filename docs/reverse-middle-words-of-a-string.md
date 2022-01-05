# 反转一个字符串的中间单词

> 原文:[https://www . geeksforgeeks . org/reverse-中间单词串/](https://www.geeksforgeeks.org/reverse-middle-words-of-a-string/)

给定一个字符串 **str** ，打印除第一个和最后一个单词之外的所有单词。

**示例:**

```
Input  : Hi how are you geeks 
Output  : Hi woh era uoy geeks

Input : I am fine
Output : I ma fine
```

1.  打印第一个单词。
2.  对于剩余的中间单词，在到达末尾后打印每个单词的背面。这将打印除最后一个单词以外的所有单词的背面。
3.  打印最后一个单词。

## C++

```
// CPP program to print reverse of all words
// except the corner words.
#include <bits/stdc++.h>
using namespace std;

void printReverse(string str)
{
    // Print first word
    int i = 0;
    for (i = 0; i < str.length() && str[i] != ' '; i++)
        cout << str[i];

    // Print middle words
    string word = "";
    for (; i < str.length(); i++) {

        if (str[i] != ' ')
            word += str[i];
        else {
            reverse(word.begin(), word.end());
            cout << word << " ";
            word = "";
        }
    }

    // Print last word
    cout << word << " ";
}

int main()
{
    string str = "Hi how are you geeks";
    printReverse(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print reverse of all words
// except the corner words.

public class GFG{

static void printReverse(String str)
    {
        // Print first word
        int i = 0;
        for (i = 0; i < str.length() && str.charAt(i) != ' '; i++)
            System.out.print(str.charAt(i)) ;

        // Print middle words
        String word = "";

        for (; i < str.length(); i++) {

            if (str.charAt(i) != ' ')
                word += str.charAt(i);

            else {
                    System.out.print(new StringBuilder(word).
                                reverse().toString() + " ");
                    word = "";
            }
        }

        // Print last word
        System.out.print(word + " ");
    }

    public static void main(String []args)
    {
        String str = "Hi how are you geeks";
        printReverse(str);
    }

// This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 program to print reverse of all words
# except the corner words.
def printReverse(s):

    #Taking all the words in a list
    l = [s for s in s.split(' ')]

    #printing the first word as it is
    print(l[0], end = ' ')

    for i in range(1, len(l)-1):

        #printing middle words reversed
        print(l[i][::-1], end = ' ')

    #printing the last word as it is
    print(l[len(l)-1])

s = "Hi how are you geeks"
printReverse(s)
```

## C#

```
// C# program to print reverse of all words
// except the corner words.
using System;
using System.Text;

class GFG
{

    static void printReverse(String str)
    {
        // Print first word
        int i = 0;
        for (i = 0; i < str.Length && str[i] != ' '; i++)
            Console.Write(str[i]) ;

        // Print middle words
        String word = "";

        for (; i < str.Length; i++)
        {

            if (str[i] != ' ')
                word += str[i];

            else
            {
                word = reverse(word);
                    Console.Write(new StringBuilder(word).ToString() + " ");
                    word = "";
            }
        }

        // Print last word
        Console.Write(word + " ");
    }
    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver code
    public static void Main(String []args)
    {
        String str = "Hi how are you geeks";
        printReverse(str);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print reverse of all
// words except the corner words.
function printReverse($str)
{
    // Print first word
    $i = 0;
    for ($i = 0; $i < strlen($str) &&
                 $str[$i] != ' '; $i++)
        echo $str[$i];

    // Print middle words
    $word = "";
    for (; $i < strlen($str); $i++)
    {

        if ($str[$i] != ' ')
            $word = $word.$str[$i];
        else
        {
            $word = strrev($word);
            echo $word . " ";
            $word = "";
        }
    }

    // Print last word
    echo $word . " ";
}

// Driver Code
$str = "Hi how are you geeks";
printReverse($str);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to print reverse of
// all words except the corner words.
function printReverse(str)
{

    // Print first word
    var i = 0;
    for(i = 0;
        i < str.length && str[i] != " ";
        i++)
        document.write(str[i]);

    // Print middle words
    var word = "";
    for(; i < str.length; i++)
    {
        if (str[i] != " ")
            word += str[i];
        else
        {
            var temp = word.split("").reverse().join("");
            document.write(temp + " ");
            word = "";
        }
    }

    // Print last word
    document.write(word + " ");
}

// Driver code
var str = "Hi how are you geeks";
printReverse(str);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
Hi woh era uoy geeks
```

**时间复杂度:**O(n)
T3】辅助空间: O(L)其中 L 是字符串中最长单词的长度。