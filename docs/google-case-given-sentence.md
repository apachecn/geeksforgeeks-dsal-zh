# 给定句子的 Google CaSe

> 原文:[https://www.geeksforgeeks.org/google-case-given-sentence/](https://www.geeksforgeeks.org/google-case-given-sentence/)

给定一个句子，任务是在谷歌案例中重写。这是一种写作风格，我们将所有小写字母替换为大写字母，留下所有单词的首字母。

**例:**

```
Input : gEEks fOr GeeKs
Output : gEEKS fOR gEEKS 

Input : I got intern at geeksforgeeks
Output : i gOT iNTERN aT gEEKSFORGEEKS 
```

一个**简单的解决方案**就是把整个字符串转换成一个大写字母，然后遍历给定的字符串，同时遍历我们用小替换所有单词的首字母。

## c++

```
// C++ program to convert a
// sentence to gOOGLE cASE.
#include <bits/stdc++.h>
using namespace std;

string convert(string str)
{

    // Empty strings
    string w = "", z = "";

    // Convert input string to upper case
    transform(str.begin(), str.end(),
              str.begin(), ::toupper);
    str += " ";
    for(int i = 0; i < str.length(); i++)
    {

       // Check if character is not a space
       // and adding it to string w
       char ch = str[i];
       if (ch != ' ')
       {
           w = w + ch;
       }
       else
       {

           // Converting first character
           // to lower case and subsequent
           // initial letter of another
           // word to lower case
           z = z + char(tolower(w[0])) +
                           w.substr(1) + " ";
           w = "";
       }
    }
    return z;
}

// Driver code
int main()
{
    string str = "I got intern at geeksforgeeks";

    cout << convert(str) << endl;
    return 0;
}

// This code is contributed by rutvik_56
```

## Java

```
// Java program to convert a
// sentence to gOOGLE cASE.

class GFG
{
    static String convert(String str)
    {
        // empty strings
        String w = "", z = "";

        // convert input string to upper case
        str = str.toUpperCase() + " ";

        for (int i = 0; i < str.length(); i++)
        {

            // checki if character is not a space
            // and adding it to string w
            char ch = str.charAt(i);
            if (ch != ' ')
                w = w + ch;
            else {

                // converting first character to lower
                // case and subsequent initial
                // letter of another word to lower case
                z = z + (Character.toLowerCase(w.charAt(0))) +
                         w.substring(1) + " ";
                w = "";
            }
        }

        return z;
    }

    // Driver code
    public static void main(String[] args)
    {

        String str = "I got intern at geeksforgeeks";
        System.out.println(convert(str));
    }
}
```

## python 3

```
# Python3 program to convert a
# sentence to gOOGLE cASE.
def convert(str):

    # empty strings
    w = ""
    z = "";

    # convert input string
    # to upper case
    str = str.upper() + " ";

    for i in range(len(str)):

        # checki if character is not
        # a space and adding it to
        # string w
        ch = str[i];
        if (ch != ' '):
            w = w + ch;
        else:

            # converting first character
            # to lower case and subsequent
            # initial letter of another
            # word to lower case
            z = (z + (w[0]).lower() +
                 w[1:len(w)] + " ");
            w = "";

    return z;

# Driver code
if __name__ == '__main__':

    str = "I got intern at geeksforgeeks";
    print(convert(str));

# This code is contributed by 29AjayKumar
```

## c#

```
// C# program to convert a
// sentence to gOOGLE cASE.
using System;

class GFG
{
    static string convert(string str)
    {
        // empty strings
        string w = "", z = "";

        // convert input string
        // to upper case
        str = str.ToUpper() + " ";

        for (int i = 0;
                 i < str.Length; i++)
        {

            // checki if character is
            // not a space and adding
            // it to string w
            char ch = str[i];
            if (ch != ' ')
                w = w + ch;
            else
            {

                // converting first character
                // to lower case and subsequent
                // initial letter of another
                // word to lower case
                z = z + (Char.ToLower(w[0])) +
                         w.Substring(1) + " ";
                w = "";
            }
        }
        return z;
    }

    // Driver code
    static void Main()
    {
        string str = "I got intern at geeksforgeeks";
        Console.WriteLine(convert(str));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## PHP

```
<?php
// PHP program to convert a
// sentence to gOOGLE cASE.

function convert($str)
{
    // empty strings
    $w = ""; $z = "";

    // convert input
    // to upper case
    $str = strtoupper($str) . " ";

    for ($i = 0;
         $i < strlen($str); $i++)
    {

        // checki if character
        // is not a space
        // and adding it to $w
        $ch = $str[$i];
        if ($ch != ' ')
            $w = $w . $ch;
        else
        {

            // converting first character
            // to lower case and subsequent
            // initial letter of another
            // word to lower case
            $z = $z . strtolower($w[0]) .
                          substr($w, 1) . " ";
            $w = "";
        }
    }
    return $z;
}

// Driver code
$str = "I got intern at geeksforgeeks";
echo (convert($str));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## Javascript

T33】

**输出:**

```
i gOT iNTERN aT gEEKSFORGEEKS 
```

上述解决方案需要两次字符串遍历。一个有效的解决方案是在一次遍历中完成。这个想法是跟踪空间。在每个空格后，将字符打印到下方，否则打印到上方。

## c++

```
// CPP program to convert given
// sentence to camel case.
#include <bits/stdc++.h>
using namespace std;

// Function to remove spaces and
// convert into camel case
string convert(string s)
{
    int n = s.length();
    s[0] = tolower(s[0]);

    for (int i = 1; i < n; i++)
    {

        // check for spaces in the sentence
        if (s[i] == ' ' && i < n)
        {

            // conversion into upper case
            s[i + 1] = tolower(s[i + 1]);
            i++;
        }

        // If not space, copy character
        else
            s[i] = toupper(s[i]);
    }

    // return string to main
    return s;
}

// Driver Code
int main()
{
    string str = "I get intern at geeksforgeeks";
    cout << convert(str);
    return 0;
}
```

## Java

```
// Java program to convert given
// sentence to camel case.
import java.io.*;

class GFG
{
    // Function to remove spaces
    // and convert into camel case
    static String convert(String s)
    {
        int n = s.length();
        String s1 = "";
        s1 = s1 + Character.toLowerCase(s.charAt(0));

        for (int i = 1; i < n; i++)
        {
            // check for spaces in the sentence
            if (s.charAt(i) == ' ' && i < n)
            {
                // conversion into upper case
                s1 = s1 + " " + Character.toLowerCase
                                (s.charAt(i + 1));
                i++;

            }

            // If not space, copy character
            else
            s1= s1 + Character.toUpperCase(s.charAt(i));

        }

        // return string to main
        return s1;

    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "I get intern at geeksforgeeks";
        System.out.println(convert(str));
    }
}

// This code is contributed by Gitanjali.
```

## python 3

```
# Python program to convert given
# sentence to camel case.
import math

# Function to remove spaces
# and convert into camel case
def convert( s):

        n = len(s)
        s1 = ""
        s1 = s1 + s[0].lower()
        i = 1
        while i < n:
            # check for spaces in the sentence
            if (s[i] == ' ' and i <= n):

                # conversion into upper case
                s1 = s1 + " " + (s[i + 1]).lower()
                i = i + 1

            # If not space, copy character
            else:
                s1 = s1 + (s[i]).upper()

            # increase index of string by s1
            i = i + 1

        # return string to main
        return s1

# Driver code
str = "I get intern at geeksforgeeks"
print(convert(str))

# This code is contributed by Gitanjali.
```

## c#

```
// C# program to convert given
// sentence to camel case.
using System;

class GFG
{
    // Function to remove spaces
    // and convert into camel case
    static String convert(String s)
    {
        int n = s.Length;
        String s1 = "";
        s1 = s1 + Char.ToLower(s[0]);

        for (int i = 1; i < n; i++)
        {
            // check for spaces in the sentence
            if (s[i] == ' ' && i < n)
            {
                // conversion into upper case
                s1 = s1 + " " + Char.ToLower
                                (s[i + 1]);
                i++;

            }

            // If not space, copy character
            else
            s1= s1 + Char.ToUpper(s[i]);

        }

        // return string to main
        return s1;

    }

    // Driver code
    public static void Main ()
    {
        String str = "I get intern at geeksforgeeks";
        Console.Write(convert(str));
    }
}

// This code is contributed by nitin mittal
```

## PHP

```
<?php
// PHP program to convert given
// sentence to camel case.

// Function to remove spaces and
// convert into camel case
function convert($s)
{
    $n = strlen($s);
    $s[0] = strtolower($s[0]);

    for ($i = 1; $i < $n; $i++)
    {

        // check for spaces
        // in the sentence
        if ($s[$i] == ' ' && $i < $n)
        {

            // conversion into
            // upper case
            $s[$i + 1] = strtolower($s[$i + 1]);
            $i++;
        }

        // If not space,
        // copy character
        else
            $s[$i] = strtoupper($s[$i]);
    }

    // return string to main
    return $s;
}

// Driver Code
$str = "I get intern at geeksforgeeks";
echo (convert($str));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## Javascript

T33】

**输出:**

```
i gET iNTERN aT gEEKSFORGEEKS 
```