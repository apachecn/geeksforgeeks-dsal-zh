# 使用递归打印字符串的反串

> 原文:[https://www . geesforgeks . org/reverse-a-string-use-recursive/](https://www.geeksforgeeks.org/reverse-a-string-using-recursion/)

写一个递归函数来打印给定字符串的反串。
**程序:**

## C++

```
// C++ program to reverse a string using recursion
#include <bits/stdc++.h>
using namespace std;

/* Function to print reverse of the passed string */
void reverse(string str)
{
    if(str.size() == 0)
    {
        return;
    }
    reverse(str.substr(1));
    cout << str[0];
}

/* Driver program to test above function */
int main()
{
    string a = "Geeks for Geeks";
    reverse(a);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// C program to reverse a string using recursion
# include <stdio.h>

/* Function to print reverse of the passed string */
void reverse(char *str)
{
   if (*str)
   {
       reverse(str+1);
       printf("%c", *str);
   }
}

/* Driver program to test above function */
int main()
{
   char a[] = "Geeks for Geeks";
   reverse(a);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a string using recursion

class StringReverse
{
    /* Function to print reverse of the passed string */
    void reverse(String str)
    {
        if ((str==null)||(str.length() <= 1))
           System.out.println(str);
        else
        {
            System.out.print(str.charAt(str.length()-1));
            reverse(str.substring(0,str.length()-1));
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        String str = "Geeks for Geeks";
        StringReverse obj = new StringReverse();
        obj.reverse(str);
    }   
}
```

## 计算机编程语言

```
# Python program to reverse a string using recursion

# Function to print reverse of the passed string
def reverse(string):
    if len(string) == 0:
        return

    temp = string[0]
    reverse(string[1:])
    print(temp, end='')

# Driver program to test above function
string = "Geeks for Geeks"
reverse(string)

# A single line statement to reverse string in python
# string[::-1]

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to reverse
// a string using recursion
using System;

class GFG
{
    // Function to print reverse
    // of the passed string
    static void reverse(String str)
    {
        if ((str == null) || (str.Length <= 1))
        Console.Write(str);

        else
        {
            Console.Write(str[str.Length-1]);
            reverse(str.Substring(0,(str.Length-1)));
        }
    }

    // Driver Code
    public static void Main()
    {
        String str = "Geeks for Geeks";
        reverse(str);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to reverse
// a string using recursion

// Function to print reverse
// of the passed string
function reverse($str)
{
    if (($str == null) ||
        (strlen($str) <= 1))
    echo ($str);

    else
    {
        echo ($str[strlen($str) - 1]);
        reverse(substr($str, 0,
               (strlen($str) - 1)));
    }
}

// Driver Code
$str = "Geeks for Geeks";
reverse($str);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        /* Function to print reverse of the passed string */
        function reverse(str, len) {
            if (len == str.length) {
                return;
            }
            reverse(str, len + 1);

            document.write(str[len]);

        }

        /* Driver program to test above function */

        let a = "Geeks for Geeks";

        reverse(a, 0);

    // This code is contributed by Potta Lokesh
    </script>
```

**输出:**

```
skeeG rof skeeG
```

**说明:**递归函数(逆向)以字符串指针(str)为输入，用传递指针(str+1)的下一个位置调用自身。当指针到达' \0 '时，递归以这种方式继续，所有函数在堆栈打印字符中的传递位置(str)累积并逐个返回。
**时间复杂度:** O(n^2) as substr()方法的时间复杂度为 O(k)，其中 k 是返回字符串的大小。因此，对于每次递归调用，我们都将字符串的大小减少一，这将导致类似(k-1)+(k-2)+…+1 = k *(k-1)/2 = o(k^2 = o(n^2)这样的序列
有关反转字符串的其他方法，请参见[反转字符串](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。