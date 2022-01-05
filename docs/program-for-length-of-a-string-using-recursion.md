# 使用递归计算字符串长度的程序

> 原文:[https://www . geesforgeks . org/program-for-length-of-string-use-recursion/](https://www.geeksforgeeks.org/program-for-length-of-a-string-using-recursion/)

给定一个字符串，使用递归计算字符串的长度。
**例:**

```
Input : str = "abcd"
Output :4

Input : str = "GEEKSFORGEEKS"
Output :13
```

我们已经讨论了 [5 种不同的方法在 C++中求字符串的长度](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)
[如何在 C 中求没有 string.h 和 loop 的字符串的长度？](https://www.geeksforgeeks.org/find-length-string-without-strlen-loop/)
**算法**

```
recLen(str)
{
   If str is NULL 
       return 0
   Else 
      return 1 + recLen(str + 1)
}
```

## C++

```
// CPP program to calculate length of
// a string using recursion
#include <bits/stdc++.h>
using namespace std;

/* Function to calculate length */
int recLen(char* str)   
{
    // if we reach at the end of the string
    if (*str == '\0')
        return 0;
    else
        return 1 + recLen(str + 1);
}

/* Driver program to test above function */
int main()
{
    char str[] = "GeeksforGeeks";
    cout << recLen(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to calculate length of
// a string using recursion
import java.util.*;

public class GFG{

    /* Function to calculate length */
    private static int recLen(String str)
    {

        // if we reach at the end of the string
        if (str.equals(""))
            return 0;
        else
            return recLen(str.substring(1)) + 1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

        String str ="GeeksforGeeks";
        System.out.println(recLen(str));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python program to calculate
# length of a string using
# recursion
str = "GeeksforGeeks"

# Function to
# calculate length
def string_length(str) :

    # if we reach at the
    # end of the string
    if str == '':
        return 0
    else :
        return 1 + string_length(str[1:])

# Driver Code
print (string_length(str))

# This code is contributed by
# Prabhjeet
```

## C#

```
// C# program to calculate length of
// a string using recursion
using System;

public class GFG{

    /* Function to calculate length */
    private static int recLen(string str)
    {

        // if we reach at the end of the string
        if (str.Equals(""))
            return 0;
        else
            return recLen(str.Substring(1)) + 1;
    }

    /* Driver program to test above function */
    public static void Main()
    {

        string str ="GeeksforGeeks";
        Console.WriteLine(recLen(str));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// length of a string using
// recursion

// Function to
// calculate length
function recLen(&$str, $i)   
{
    // if we reach at the
    // end of the string
    if ($i == strlen($str))
        return 0;
    else
        return 1 +
               recLen($str,
                      $i + 1);
}

// Driver Code
$str = "GeeksforGeeks";
echo (recLen($str, 0));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program to calculate length of
// a string using recursion

/* Function to calculate length */
    function recLen(str)
    {

        // if we reach at the end of the string
        if (str == "")
            return 0;
        else
            return recLen(str.substring(1)) + 1;
    }

// Driver code

        let str ="GeeksforGeeks";
        document.write(recLen(str));

</script>
```

**输出:**

```
13
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)为递归调用栈。

由于该解决方案需要额外的空间和函数调用开销，因此不建议在实践中使用。