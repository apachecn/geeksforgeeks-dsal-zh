# 只需更改一个字符

即可将字符串转换为回文字符串

> 原文:[https://www . geesforgeks . org/convert-string-回文-string-changing-one-character/](https://www.geeksforgeeks.org/convert-string-palindrome-string-changing-one-character/)

给定一个字符串。检查是否可以通过仅更改一个字符将字符串转换为回文字符串。
**例:**

```
Input : str = "abccaa"
Output : Yes
We can change the second last character
i.e. 'a' to 'b' to make it palindrome string

Input : str = "abbcca"
Output : No
We can not convert the string into palindrome
string by changing only one character.
```

**方法:**思路很简单，我们用 str[n-i-1]检查字符串[i]。如果有不匹配，我们增加计数。如果不匹配的计数超过 1，我们返回 false。否则我们会回到现实。
以下是以上想法的实现:

## C++

```
// CPP program to Check if it is
// possible to convert the string
// into palindrome string by changing
// only one character.
#include<bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to convert the string into palindrome
bool checkPalindrome(string str){

    int n = str.length();       

    // Counting number of characters
    // that should be changed.
    int count = 0;
    for (int i = 0; i < n/2; ++i)
        if (str[i] != str[n - i - 1])
            ++count;

    // If count of changes is less than
    // or equal to 1
    return (count <= 1);
}

// Driver function.
int main()
{
    string str = "abccaa";   
    if (checkPalindrome(str))
       cout << "Yes" << endl;
    else
       cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if it is
// possible to convert the string
// into palindrome string by changing
// only one character.
import java.io.*;

class GFG {

    // Function to check if it is possible
    // to convert the string into palindrome
    static boolean checkPalindrome(String str){

    int n = str.length();    

    // Counting number of characters
    // that should be changed.
    int count = 0;

    for (int i = 0; i < n/2; ++i)

        if (str.charAt(i) != str.charAt(n - i - 1))
            ++count;

    // If count of changes is less than
    // or equal to 1
    return (count <= 1);
    }

// Driver Function   
public static void main(String[] args) {

    String str = "abccaa";

    if (checkPalindrome(str))

        System.out.println("Yes");
    else
        System.out.println("No");

    }

}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program to Check
# if it is possible to
# convert the string into
# palindrome string by
# changing only one character.

# Function to check if
# it is possible to
# convert the string
# into palindrome
def checkPalindrome(str) :

    n = len(str)

    # Counting number of
    # characters that
    # should be changed.
    count = 0
    for i in range(0, int(n / 2)) :
        if (str[i] != str[n - i - 1]) :
            count = count + 1

    # If count of changes
    # is less than
    # or equal to 1
    if(count <= 1) :
        return True
    else :
        return False

# Driver Code
str = "abccaa"
if (checkPalindrome(str)) :
    print ("Yes")
else :
    print ("No")

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to Check if it is
// possible to convert the string
// into palindrome string by changing
// only one character.
using System;

class GFG {

    // Function to check if it is possible
    // to convert the string into palindrome
    static bool checkPalindrome(string str){

        int n = str.Length;

        // Counting number of characters
        // that should be changed.
        int count = 0;

        for (int i = 0; i < n / 2; ++i)

            if (str[i] != str[n - i - 1])
                ++count;

        // If count of changes is less than
        // or equal to 1
        return (count <= 1);
    }

    // Driver Function
    public static void Main()
    {     
        string str = "abccaa";

        if (checkPalindrome(str))

            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        }

}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Check if it is
// possible to convert the string
// into palindrome string by changing
// only one character.

// Function to check if it is possible
// to convert the string into palindrome
function checkPalindrome($str)
{

    $n = strlen($str);    

    // Counting number of characters
    // that should be changed.
    $count = 0;
    for ($i = 0; $i < $n/2; ++$i)
        if ($str[$i] != $str[$n - $i - 1])
            ++$count;

    // If count of changes
    // is less than
    // or equal to 1
    return ($count <= 1);
}

// Driver Code
{
    $str = "abccaa";
    if (checkPalindrome($str))
        echo "Yes" ;
    else
        echo "No" ;

    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript program to Check if it is
    // possible to convert the string
    // into palindrome string by changing
    // only one character.

    // Function to check if it is possible
    // to convert the string into palindrome
    function checkPalindrome(str){

        let n = str.length;       

        // Counting number of characters
        // that should be changed.
        let count = 0;
        for (let i = 0; i < parseInt(n/2, 10); ++i)
            if (str[i] != str[n - i - 1])
                ++count;

        // If count of changes is less than
        // or equal to 1
        return (count <= 1);
    }

    let str = "abccaa";   
    if (checkPalindrome(str))
       document.write("Yes");
    else
       document.write("No");

  // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
Yes
```