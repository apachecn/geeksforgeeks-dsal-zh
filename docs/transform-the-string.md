# 变换字符串

> 原文:[https://www.geeksforgeeks.org/transform-the-string/](https://www.geeksforgeeks.org/transform-the-string/)

给定一个字符串 s，根据下面提供的规则更改字符串 s:

*   删除字符串中的所有元音。
*   在所有辅音前面插入 **#** 。
*   改变字符串中所有字母的大小写。

**例:**

```
Input : aBAcAba
Output :#b#C#B

Input :SunshinE!!
Output :#s#N#S#H#N!!
```

**方法:**
首先，通过从给定的原始字符串中移除所有元音来创建一个新字符串。现在，改变这个字符串中每个字母的大小写。最后，在字符串中的每个字母前面加上 **#** ，这就是必选字符串。

## C++

```
// CPP code to transform string
#include <bits/stdc++.h>
using namespace std;

// Function to change
// character's case
string change_case(string a)
{
    int l = a.length();

    for(int i = 0 ; i < l ; i++)
    {
        // If character is lowercase
        // change to uppercase
        if(a[i] >= 'a' && a[i] <= 'z')
            a[i] = (char)(65 +
                   (int)(a[i] - 'a'));

        // If character is uppercase
        // change to lowercase
        else if(a[i] >= 'A' && a[i] <= 'Z')
            a[i] = (char)(97 +
                   (int)(a[i] - 'A'));
    }

    return a;

}

// Function to delete vowels
string delete_vowels(string a)
{
    string temp = "";
    int l = a.length();
    for(int i = 0 ; i < l ; i++)
    {
        //If character is consonant
        if(a[i] != 'a' && a[i] != 'e' &&
           a[i] != 'i' && a[i] != 'o' &&
           a[i] != 'u' && a[i] != 'A' &&
           a[i] != 'E' && a[i] != 'O' &&
           a[i] != 'U'&& a[i] != 'I')
            temp += a[i];
    }

    return temp;

}

// Function to insert "#"
string insert_hash(string a)
{
    string temp = "";
    int l = a.length();

    for(int i = 0 ; i < l ; i++)
    {
        // If character is not special
        if((a[i] >= 'a' && a[i] <= 'z') ||
           (a[i] >= 'A' && a[i] <= 'Z'))
            temp = temp + '#' + a[i];
        else
            temp = temp + a[i];
    }

    return temp;

}

// Function to transform string
void transformSting(string a)
{
    string b = delete_vowels(a);
    string c = change_case(b);
    string d = insert_hash(c);

    cout << d;
}

// Driver function
int main()
{
    string a = "SunshinE!!";

    // Calling function
    transformSting(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to transform string
import java.io.*;

class Gfg
{
    // Function to change
    // character's case
    public static String change_case(String a)
    {
        String temp = "";
        int l = a.length();

        for(int i = 0 ; i < l ; i++)
        {
            char ch=a.charAt(i);

            // If character is lowercase
            // change to uppercase
            if(ch >= 'a' &&ch <= 'z')
            ch = (char)(65 + (int)(ch - 'a'));

            // If character is uppercase
            // change to lowercase
            else if(ch >= 'A' &&ch <= 'Z')
            ch = (char)(97 +
                 (int)(ch - 'A'));
            temp += ch;
        }

        return temp;

    }

    // Function to delete vowels
    public static String delete_vowels(String a)
    {
        String temp = "";
        int l = a.length();

        for(int i = 0 ; i < l ; i++)
        {
            char ch = a.charAt(i);

            // If character is consonant
            if(ch != 'a' && ch != 'e' &&
               ch != 'i' && ch != 'o' &&
               ch != 'u' && ch != 'A' &&
               ch != 'E' && ch != 'O' &&
               ch != 'U'&&ch != 'I')

                temp += ch;
        }

        return temp;

    }

    // Function to insert "#"
    public static String insert_hash(String a)
    {
        String temp = "";
        int l = a.length();
        char hash = '#';

        for(int i = 0 ; i < l ; i++)
        {
            char ch=a.charAt(i);

            // If character is not
            // special character
            if((ch >= 'a' && ch <= 'z') ||
               (ch >= 'A' && ch <= 'Z'))
                temp = temp + hash + ch;
            else
                temp = temp + ch;
        }

        return temp;

    }

    // Function to transform string
    public static void transformString(String a)
    {
        String b = delete_vowels(a);
        String c = change_case(b);
        String d = insert_hash(c);

        System.out.println(d);
    }

    // Driver function
    public static void main (String args[])
    {
        String a = "SunshinE!!";

        // Calling function
        transformString(a);
    }
}
```

## 蟒蛇 3

```
# Python code to
# transform string

# def to change
# character's case
def change_case(s) :

    a = list(s)
    l = len(s)

    for i in range(0, l) :

        # If character is
        # lowercase change
        # to uppercase
        if(a[i] >= 'a' and
           a[i] <= 'z') :
            a[i] = s[i].upper()

        # If character is uppercase
        # change to lowercase
        elif(a[i] >= 'A' and
             a[i] <= 'Z') :
            a[i] = s[i].lower()

    return a

# def to delete vowels
def delete_vowels(s) :

    temp = ""
    a = list(s)
    l = len(s)
    for i in range(0, l) :

        # If character
        # is consonant
        if(a[i] != 'a' and a[i] != 'e' and
           a[i] != 'i' and a[i] != 'o' and
           a[i] != 'u' and a[i] != 'A' and
           a[i] != 'E' and a[i] != 'O' and
           a[i] != 'U' and a[i] != 'I') :
            temp = temp + a[i]

    return temp

# def to insert "#"
def insert_hash(s) :

    temp = ""
    a = list(s)
    l = len(s)

    for i in range(0, l) :

        # If character is
        # not special
        if((a[i] >= 'a' and
            a[i] <= 'z') or
        (a[i] >= 'A' and
            a[i] <= 'Z')) :
            temp = temp + '#' + a[i]
        else :
            temp = temp + a[i]

    return temp

# def to
# transform string
def transformSting(a) :

    b = delete_vowels(a)
    c = change_case(b)
    d = insert_hash(c)

    print (d)

# Driver Code
a = "SunshinE!!"

# Calling def
transformSting(a)

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# code to transform string
using System;

class Gfg
{
    // Function to change
    // character's case
    public static String change_case(string a)
    {
        string temp = "";
        int l = a.Length;

        for(int i = 0 ; i < l ; i++)
        {
            char ch=a[i];

            // If character is lowercase
            // change to uppercase
            if(ch >= 'a' &&ch <= 'z')
            ch = (char)(65 + (int)(ch - 'a'));

            // If character is uppercase
            // change to lowercase
            else if(ch >= 'A' &&ch <= 'Z')
            ch = (char)(97 +
                (int)(ch - 'A'));
            temp += ch;
        }

        return temp;

    }

    // Function to delete vowels
    public static String delete_vowels(String a)
    {
        String temp = "";
        int l = a.Length;

        for(int i = 0 ; i < l ; i++)
        {
            char ch = a[i];

            // If character is consonant
            if(ch != 'a' && ch != 'e' &&
            ch != 'i' && ch != 'o' &&
            ch != 'u' && ch != 'A' &&
            ch != 'E' && ch != 'O' &&
            ch != 'U'&&ch != 'I')

                temp += ch;
        }

        return temp;

    }

    // Function to insert "#"
    public static String insert_hash(String a)
    {
        String temp = "";
        int l = a.Length;
        char hash = '#';

        for(int i = 0 ; i < l ; i++)
        {
            char ch=a[i];

            // If character is not
            // special character
            if((ch >= 'a' && ch <= 'z') ||
            (ch >= 'A' && ch <= 'Z'))
                temp = temp + hash + ch;
            else
                temp = temp + ch;
        }

        return temp;

    }

    // Function to transform string
    public static void transformString(string a)
    {
        string b = delete_vowels(a);
        string c = change_case(b);
        string d = insert_hash(c);

        Console.WriteLine(d);
    }

    // Driver function
    public static void Main ()
    {
        string a = "SunshinE!!";

        // Calling function
        transformString(a);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to transform string

// Function to change
// character's case
function change_case($a)
{
    $l = strlen($a);

    for($i = 0 ; $i < $l ; $i++)
    {
        // If character is lowercase
        // change to uppercase
        if($a[$i] >= 'a' &&
           $a[$i] <= 'z')
            $a[$i] = chr(65 +
                        (ord($a[$i]) -
                         ord('a')));

        // If character is uppercase
        // change to lowercase
        else if($a[$i] >= 'A' &&
                $a[$i] <= 'Z')
            $a[$i] = chr(97 +
                (ord($a[$i]) -
                 ord('a')));
    }
    return $a;
}

// Function to delete vowels
function delete_vowels($a)
{
    $temp = "";
    $l = strlen($a);
    for($i = 0 ; $i < $l ; $i++)
    {
        // If character
        // is consonant
        if($a[$i] != 'a' && $a[$i] != 'e' &&
           $a[$i] != 'i' && $a[$i] != 'o' &&
           $a[$i] != 'u' && $a[$i] != 'A' &&
           $a[$i] != 'E' && $a[$i] != 'O' &&
           $a[$i] != 'U' && $a[$i] != 'I')
            $temp = $temp.$a[$i];
    }    
    return $temp;    
}

// Function to insert "#"
function insert_hash($a)
{
    $temp = "";
    $l = strlen($a);

    for($i = 0 ; $i < $l ; $i++)
    {
        // If character is
        // not special
        if(($a[$i] >= 'a' &&
            $a[$i] <= 'z') ||
           ($a[$i] >= 'A' &&
            $a[$i] <= 'Z'))
            $temp = $temp . '#' .
                    $a[$i];
        else
            $temp = $temp.$a[$i];
    }    
    return $temp;    
}

// Function to
// transform string
function transformSting($a)
{
    $b = delete_vowels($a);
    $c = change_case($b);
    $d = insert_hash($c);

    echo ($d);
}

// Driver Code
$a = "SunshinE!!";

// Calling function
transformSting($a);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

**输出:**

```
#s#N#S#H#N!!
```