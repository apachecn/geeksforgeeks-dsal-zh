# 检查字符串的第一个和最后一个字符是否相等的程序

> 原文:[https://www . geesforgeks . org/program-to-check 字符串的第一个和最后一个字符是否相等/](https://www.geeksforgeeks.org/program-to-check-if-first-and-the-last-characters-of-string-are-equal/)

给我们一个字符串，我们需要检查字符串的第一个和最后一个字符是否相等。应考虑区分大小写。
**例:**

```
Input  : university 
Output : Not Equal
Explanation: In the string "university", the first character is 'u' 
and the last character is 'y', as they are not equal, "Not Equal" is the output.

Input  : racecar
Output : Equal
Explanation: In the string "racecar", the first character is 'r' 
and the last character is 'r', as they are equal, "Equal" is the output.
```

## C++

```
// C++ program to check if the first
// and the last characters of a string
// are equal or not.
#include<iostream>

using namespace std;

// Function to check if the first
// and the last haracters of a
// string are equal or not.
int areCornerEqual(string s)
    {
        int n = s.length();
        if (n < 2)
        return -1;
        if (s[0] == s[n - 1])
        return 1;
        else
        return 0;
    }

// Driver code
int main()
    {
        string s = "GfG";
        int res = areCornerEqual(s);
        if (res == -1)
            cout<<"Invalid Input";
        else if (res == 1)
            cout<<"Equal";
        else
            cout<<"Not Equal";
    }

// This code is contributed by
// Smitha Dinesh Semwal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the first and the last
// characters of a string are equal or not.
class GFG {
    public static int areCornerEqual(String s)
    {
        int n = s.length();
        if (n < 2)
           return -1;
        if (s.charAt(0) == s.charAt(n-1))
           return 1;
        else
           return 0;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "GfG";
        int res = areCornerEqual(s);
        if (res == -1)
            System.out.println("Invalid Input");
        else if (res == 1)
            System.out.println("Equal");
        else
            System.out.println("Not Equal");
    }
}
```

## 蟒蛇 3

```
# Python program to check
# if the first and the
# last characters of a
# string are equal or not.

st = "GfG"
if(st[0] == st[-1]):

    # print output
    # if condition
    # is satisfied
    print("Equal")
else:

    # print output
    # if condition is
    # not satisfied
    print("Not Equal")

# This code is contributed by
# shivi Aggarwal
```

## C#

```
// Java program to check if the first and the last
// characters of a string are equal or not.
using System;

class GFG
{

    public static int areCornerEqual(String s)
    {
        int n = s.Length;
        if (n < 2)
            return -1;
        if (s[0] == s[n - 1])
            return 1;
        else
            return 0;
    }

    // Driver code
    static public void Main ()
    {
        String s = "GfG";
        int res = areCornerEqual(s);

        if (res == -1)
            Console.WriteLine("Invalid Input");
        else if (res == 1)
            Console.WriteLine("Equal");
        else
            Console.WriteLine("Not Equal");
    }
}

// This code is contributed by Ajit.
.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// the first and the last
// characters of a $are
// equal or not.

function areCornerEqual($s)
{
    $n = strlen($s);
    if ($n < 2)
        return -1;
    if ($s[0] == $s[$n - 1])
        return 1;
    else
        return 0;
}

// Driver code
$s = "GfG";
$res = areCornerEqual($s);

if ($res == -1)
    echo ("Invalid Input");
else if ($res == 1)
    echo ("Equal");
else
    echo ("Not Equal");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

    // Javascript program to check
    // if the first and the last
    // characters of a string are equal or not.

    function areCornerEqual(s)
    {
        let n = s.length;
        if (n < 2)
            return -1;
        if (s[0] == s[n - 1])
            return 1;
        else
            return 0;
    }

    let s = "GfG";
    let res = areCornerEqual(s);

    if (res == -1)
      document.write("Invalid Input");
    else if (res == 1)
      document.write("Equal");
    else
      document.write("Not Equal");

</script>
```

**输出:**

```
Equal
```