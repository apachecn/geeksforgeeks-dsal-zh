# 字符串中的泛字符窗口

> 原文:[https://www.geeksforgeeks.org/panalphabetic-window-string/](https://www.geeksforgeeks.org/panalphabetic-window-string/)

给定一根大小为 **n** 的绳子 **S** 。任务是检查给定的字符串是否包含泛字符窗口。一个 [**泛字母窗口**](https://en.wikipedia.org/wiki/Panalphabetic_window) 是一段包含字母表中所有字母的有序文本。
**举例:**

```
Input : S = "abujm zvcd acefc deghf gijkle m n o p pafqrstuvwxyzfap"
Output : YES
Panalphabetic Window is in Bold:
abujm zvcd acefc deghf gijkle m n o p pafqrstuvwxyzfap

Input : S = "geeksforgeeks"
Output : NO
```

这个想法是将一个变量，比如 ch，初始化为“a”。如果我们找到一个等于 ch 的字符，从开始遍历给定的字符串，并将变量 ch 增加 1，否则移动到下一个索引。当字符串结束时，检查 ch 是否等于' z' + 1，如果是，返回 true，否则返回 false。
以下是该方法的实施:

## C++

```
// CPP Program to check whether given string contain
// panalphabetic window or not
#include<bits/stdc++.h>
using namespace std;

// Return if given string contain panalphabetic window.
bool isPanalphabeticWindow(char s[], int n)
{
    char ch = 'a';

    // traversing the string
    for (int i = 0; i < n; i++)
    {
        // if character of string is equal to ch, 
        // increment ch.
        if (s[i] == ch)
            ch++;

        // if all characters are found, return true.
        if (ch == 'z' + 1)
            return true;
    }

    return false;
}
// Driven Program
int main()
{
    char s[] = "abujm zvcd acefc deghf gijkle"
                " m n o p pafqrstuvwxyzfap";
    int n = strlen(s);

    (isPanalphabeticWindow(s, n))?(cout << "YES"):
                                  (cout << "NO");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check whether given
// string contain panalphabetic
// window or not
class GFG
{

    // Return if given string contain
    // panalphabetic window.
    static boolean isPanalphabeticWindow(String s, 
                                            int n)
    {
        char ch = 'a';

        // traversing the string
        for (int i = 0; i < n; i++)
        {
            // if character of string is equal 
            // to ch, increment ch.
            if (s.charAt(i) == ch)
                ch++;

            // if all characters are
            // found, return true.
            if (ch == 'z' + 1)
                return true;
        }

        return false;
}

// Driver code
public static void main (String[] args)
{
    String s = "abujm zvcd acefc deghf"
       + " gijklem n o p pafqrstuvwxyzfap";
    int n = s.length();

    if(isPanalphabeticWindow(s, n))
            System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by
// Anant Agarwal.
```

## 蟒蛇 3

```
# Python Program to check
# whether given string
# contain panalphabetic
# window or not

# Return if given string
# contain panalphabetic window.
def isPanalphabeticWindow(s, n) :

    ch = 'a'

    # traversing the string
    for i in range(0, n) :

        # if character of string
        # is equal to ch, increment ch.
        if (s[i] == ch) :
            ch = chr(ord(ch) + 1)

        # if all characters are
        # found, return true.
        if (ch == 'z') :
            return True

    return False

# Driver Code
s = "abujm zvcd acefc deghf gijkle m n o p pafqrstuvwxyzfap"
n = len(s)

if(isPanalphabeticWindow(s, n)) :
    print ("YES")
else :
    print ("NO")

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program to check whether given
// string contain panalphabetic
// window or not
using System;

class GFG
{

    // Return if given string contain
    // panalphabetic window.
    static bool isPanalphabeticWindow(string s,
                                            int n)
    {
        char ch = 'a';

        // traversing the string
        for (int i = 0; i < n; i++)
        {
            // if character of string is equal
            // to ch, increment ch.
            if (s[i] == ch)
                ch++;

            // if all characters are
            // found, return true.
            if (ch == 'z' + 1)
                return true;
        }

        return false;
}

    // Driver code
    public static void Main ()
    {
        string s = "abujm zvcd acefc deghf"
        + " gijklem n o p pafqrstuvwxyzfap";
        int n = s.Length;

        if(isPanalphabeticWindow(s, n))
                Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by
// Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check whether
// given string contain
// panalphabetic window or not

// Return if given string
// contain panalphabetic window.
function isPanalphabeticWindow($s, $n)
{
    $ch = 'a';

    // traversing the string
    for ($i = 0; $i < $n; $i++)
    {
        // if character of string
        // is equal to ch, increment ch.
        if ($s[$i] == $ch)
            $ch++;

        // if all characters are
        // found, return true.
        if ($ch == 'z')
            return true;
    }    
    return false;
}

// Driver Code
$s = "abujm zvcd acefc deghf gijkle".
         " m n o p pafqrstuvwxyzfap";
$n = strlen($s);

if(isPanalphabeticWindow($s, $n))
    echo ("YES");
else
    echo ("NO");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript Program to check whether given string contain
// panalphabetic window or not

// Return if given string contain panalphabetic window.
function isPanalphabeticWindow(s, n)
{
    var ch = 'a';

    // traversing the string
    for (var i = 0; i < n; i++)
    {
        // if character of string is equal to ch, 
        // increment ch.
        if (s[i] == ch)
            ch = String.fromCharCode(ch.charCodeAt(0) + 1);

        // if all characters are found, return true.
        if (ch == String.fromCharCode('z'.charCodeAt(0) + 1))
            return true;
    }

    return false;
}

// Driven Program
var s = "abujm zvcd acefc deghf"
        + " gijklem n o p pafqrstuvwxyzfap";
var n = (s.length);

(isPanalphabeticWindow(s, n))?(document.write( "YES")):
                              (document.write( "NO"));

// This code is contributed by itsok.
</script>
```

**输出:**

```
YES
```

https://youtu.be/HQY36

-我是 T0