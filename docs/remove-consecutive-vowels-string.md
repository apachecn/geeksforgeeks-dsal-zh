# 去除字符串中的连续元音

> 原文:[https://www . geesforgeks . org/remove-continuous-元音-string/](https://www.geeksforgeeks.org/remove-consecutive-vowels-string/)

给定一串小写字母 s，我们需要从字符串中删除连续的元音

**注意:**句子不能包含两个连续的元音( **a、e、I、o、u** )。

****例:****

```
Input: geeks for geeks
Output: geks for geks

Input : your article is in queue 
Output : yor article is in qu

```

**方法:**使用循环迭代字符串，检查给定句子中元音的重复性，如果发现连续元音，则删除元音，直到出现下一个辅音，并打印更新的字符串。

## C++

```
// C++ program for printing sentence
// without repetitive vowels
#include <bits/stdc++.h>
using namespace std;

// function which returns True or False
// for occurrence of a vowel
bool is_vow(char c)
{
    // this compares vowel with 
    // character 'c'
    return (c == 'a') || (c == 'e') || 
           (c == 'i') || (c == 'o') || 
           (c == 'u');
}

// function to print resultant string
void removeVowels(string str)
{
    // print 1st character
    printf("%c", str[0]);

    // loop to check for each character
    for (int i = 1; str[i]; i++)

        // comparison of consecutive characters
        if ((!is_vow(str[i - 1])) || 
            (!is_vow(str[i])))
            printf("%c", str[i]);
}

// Driver Code
int main()
{
    char str[] = " geeks for geeks";
    removeVowels(str);
}

// This code is contributed by Abhinav96
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing sentence
// without repetitive vowels
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{ 
    // function which returns
    // True or False for
    // occurrence of a vowel
    static boolean is_vow(char c)
    {
        // this compares vowel 
        // with character 'c'
        return (c == 'a') || (c == 'e') || 
               (c == 'i') || (c == 'o') || 
               (c == 'u');
    }

    // function to print
    // resultant string
    static void removeVowels(String str)
    {
        // print 1st character
        System.out.print(str.charAt(0));

        // loop to check for 
        // each character
        for (int i = 1; 
                 i < str.length(); i++)

            // comparison of 
            // consecutive characters
            if ((!is_vow(str.charAt(i - 1))) || 
                (!is_vow(str.charAt(i))))
                System.out.print(str.charAt(i));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "geeks for geeks";
        removeVowels(str);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation for printing 
# sentence without repetitive vowels

# function which returns True or False
# for occurrence of a vowel
def is_vow(c):

    # this compares vowel with 
    # character 'c'
    return ((c == 'a') or (c == 'e') or 
            (c == 'i') or (c == 'o') or 
            (c == 'u'));

# function to print resultant string
def removeVowels(str):

    # print 1st character
    print(str[0], end = "");

    # loop to check for each character
    for i in range(1,len(str)):

        # comparison of consecutive
        # characters
        if ((is_vow(str[i - 1]) != True) or 
            (is_vow(str[i]) != True)):

            print(str[i], end = "");

# Driver code
str= " geeks for geeks";
removeVowels(str);

# This code is contributed by mits 
```

## C#

```
// C# program for printing sentence
// without repetitive vowels
using System;

class GFG
{ 
    // function which returns
    // True or False for
    // occurrence of a vowel
    static bool is_vow(char c)
    {
        // this compares vowel 
        // with character 'c'
        return (c == 'a') || (c == 'e') || 
               (c == 'i') || (c == 'o') || 
               (c == 'u');
    }

    // function to print
    // resultant string
    static void removeVowels(string str)
    {
        // print 1st character
        Console.Write(str[0]);

        // loop to check for 
        // each character
        for (int i = 1; i < str.Length; i++)

            // comparison of 
            // consecutive characters
            if ((!is_vow(str[i - 1])) || 
                (!is_vow(str[i])))
                Console.Write(str[i]);
    }

    // Driver Code
    static void Main()
    {
        string str = "geeks for geeks";
        removeVowels(str);
    }
}

// This code is contributed 
// by Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation for printing 
// sentence without repetitive vowels

// function which returns True or False
// for occurrence of a vowel
function is_vow($c)
{
    // this compares vowel with 
    // character 'c'
    return ($c == 'a') || ($c == 'e') || 
           ($c == 'i') || ($c == 'o') || 
           ($c == 'u');
}

// function to print resultant string
function removeVowels($str)
{
    // print 1st character
    printf($str[0]);

    // loop to check for each character
    for ($i = 1; $i < strlen($str); $i++)

        // comparison of consecutive
        // characters
        if ((!is_vow($str[$i - 1])) || 
            (!is_vow($str[$i])))

            printf($str[$i]);
}

// Driver code
$str= " geeks for geeks";
removeVowels($str);

// This code is contributed by mits 
?>
```

****Output :****

```
geks for geks

```