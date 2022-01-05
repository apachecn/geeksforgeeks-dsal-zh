# 字符串中的第一个大写字母(迭代和递归)

> 原文:[https://www . geeksforgeeks . org/首字母大写字符串迭代递归/](https://www.geeksforgeeks.org/first-uppercase-letter-in-a-string-iterative-and-recursive/)

给定一个字符串，找到它的第一个大写字母
**示例:**

```
Input : geeksforgeeKs
Output : K

Input  : geekS
Output : S
```

**方法 1:线性搜索**
使用线性搜索，找到第一个字符，即大写

## C++

```
// C++ program to find the first
// uppercase letter using linear search
#include <bits/stdc++.h>
using namespace std;

// Function to find string which has
// first character of each word.
char first(string str)
{
    for (int i = 0; i < str.length(); i++)
        if (isupper(str[i]))
            return str[i];
    return 0;
}

// Driver code
int main()
{
    string str = "geeksforGeeKS";
    char res = first(str);
    if (res == 0)
        cout << "No uppercase letter";
    else
        cout << res << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the first
// uppercase letter using linear search
import java.io.*;
import java.util.*;

class GFG {

    // Function to find string which has
    // first character of each word.
    static char first(String str)
    {
        for (int i = 0; i < str.length(); i++)
            if (Character.isUpperCase(str.charAt(i)))
                return str.charAt(i);
        return 0;
    }

    // Driver program
    public static void main(String args[])
    {
        String str = "geeksforGeeKS";
        char res = first(str);
        if (res == 0)
            System.out.println("No uppercase letter");
        else
            System.out.println(res);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to find the first
# uppercase letter using linear search

# Function to find string which has
# first character of each word.
def first(str) :

    for i in range(0, len(str)) :

        if (str[i].istitle()) :
            return str[i]

    return 0

# Driver code
str = "geeksforGeeKS"
res = first(str)

if (res == 0) :
    print("No uppercase letter")

else :
    print(res)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to find the first uppercase
// letter using linear search
using System;

class GFG {

    // Function to find string which has
    // first character of each word.
    static char first(string str)
    {
        for (int i = 0; i < str.Length; i++)
            if (char.IsUpper(str[i]) )
                return str[i];
        return '0';
    }

    // Driver function
    public static void Main()
    {
        string str = "geeksforGeeKS";
        char res = first(str);
        if (res == '0')
            Console.WriteLine("No uppercase"
                               + " letter");
        else
            Console.WriteLine(res);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the first
// uppercase letter using linear search

// Function to find string which has
// first character of each word.
function first($str)
{
    for ($i = 0; $i < strlen($str); $i++)
        if (ctype_upper($str[$i]))
        {
            return $str[$i];

        }
    return 0;
}

    // Driver code
    $str = "geeksforGeeKS";
    $res = first($str);

    if (ord($res) ==ord(0) )
        echo "No uppercase letter";
    else
        echo $res . "\n";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
      // JavaScript program to find the first
      // uppercase letter using linear search

      // Function to find string which has
      // first character of each word.
      function first(str) {
        for (var i = 0; i < str.length; i++)
          if (str[i] === str[i].toUpperCase()) return str[i];
        return 0;
      }

      // Driver code

      var str = "geeksforGeeKS";
      var res = first(str);
      if (res == 0) document.write("No uppercase letter");
      else {
        document.write(res);
        document.write("<br>");
      }

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
G
```

**方法 2(使用递归)**
递归遍历字符串，如果发现任何大写字母，则返回该字符

## C++

```
// C++ program to find the
// first uppercase letter.
#include <bits/stdc++.h>
using namespace std;

// Function to find string which has
// first character of each word.
char first(string str, int i=0)
{
    if (str[i] == '\0')
         return 0;
    if (isupper(str[i]))
            return str[i];
    return first(str, i+1);
}

// Driver code
int main()
{
    string str = "geeksforGeeKS";
    char res = first(str);
    if (res == 0)
        cout << "No uppercase letter";
    else
        cout << res << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// first uppercase letter.
import java.io.*;

class GFG {

    // Function to find string which has
    // first character of each word.
    static char first(String str, int i)
    {
        if (str.charAt(i) == '\0')
            return 0;
        if (Character.isUpperCase(str.charAt(i)))
                return str.charAt(i);
        return first(str, i + 1);
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "geeksforGeeKS";
        char res = first(str,0);
        if (res == 0)
            System.out.println("No uppercase letter");
        else
            System.out.println (res );
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
def capital(N, i, x):
    if i >= x:
        return -1
    elif N[i].isupper():
        return i
    if i < x:
        return capital(N, i + 1, x)

def main():
    N = input()
    N = list(N)
    x = len(N)
    y = (capital(N, 0, x))
    print(y)

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to find the
// first uppercase letter.
using System;

class GFG
{

    // Function to find string
    // which has first character
    // of each word.
    static char first(string str, int i)
    {
        if (str[i] == '\0')
            return '0';
        if (char.IsUpper(str[i]))
                return (str[i]);
        return first(str, i + 1);
    }

    // Driver code
    static public void Main ()
    {
        string str = "geeksforGeeKS";
        char res = first(str, 0);
        if (res == 0)
            Console.WriteLine("No uppercase letter");
        else
            Console.WriteLine(res );
    }
}

// This code is contributed by Anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find the
// first uppercase letter.

// Function to find string
// which has first character
// of each word.

function first($str, $i = 0)
{
    if ($str[$i] == '\0')
        return 0;
    if (ctype_upper($str[$i]))
            return $str[$i];
    return first($str, $i+1);
}

// Driver code
    $str = "geeksforGeeKS";
    $res = first($str);

    if (ord($res) ==ord(0))
        echo "No uppercase letter";
    else
        echo $res , "\n";

// This code is contributed
// by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// first uppercase letter.

// Function to find string which has
// first character of each word.
function first(str,i=0)
{
    if (i == str.length)
         return 0;
    if (str[i] == str[i].toUpperCase())
            return str[i];
    return first(str, i+1);
}

// Driver code
var str = "geeksforGeeKS";
var res = first(str);
if (res == 0)
    document.write( "No uppercase letter");
else
    document.write( res + "<br>");

</script>
```

**输出:**

```
G 
```