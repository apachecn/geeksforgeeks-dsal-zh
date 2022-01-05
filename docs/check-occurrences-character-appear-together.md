# 检查一个字符的所有出现是否一起出现

> 原文:[https://www . geesforgeks . org/check-occurs-characters-appearance-together/](https://www.geeksforgeeks.org/check-occurrences-character-appear-together/)

给定一个字符串 **s** 和一个字符 **c** ，查找所有出现的 **c** 是否一起出现在 **s** 中。如果字符串中根本没有出现字符 **c** ，则答案为真。

**示例**

```
Input: s = "1110000323", c = '1'
Output: Yes
All occurrences of '1' appear together in
"1110000323"

Input: s  = "3231131", c = '1'
Output: No
All occurrences of 1 are not together

Input: s  = "abcabc", c = 'c'
Output: No
All occurrences of 'c' are not together

Input: s  = "ababcc", c = 'c'
Output: Yes
All occurrences of 'c' are together
```

我们的想法是遍历给定的字符串，一旦我们发现 c 的出现，我们就继续遍历，直到找到一个不是 c 的字符。我们还设置了一个标志来指示可以看到 c 的更多出现。如果我们再次看到 c 并且标志被设置，那么我们返回 false。

## C++

```
// C++ program to find if all occurrences
// of a character appear together in a string.
#include <iostream>
#include <string>
using namespace std;

bool checkIfAllTogether(string s, char c)
{
    // To indicate if one or more occurrences
    // of 'c' are seen or not.
    bool oneSeen = false;

    // Traverse given string
    int i = 0, n = s.length();
    while (i < n) {

        // If current character is same as c,
        // we first check if c is already seen.        
        if (s[i] == c) {
            if (oneSeen == true)
                return false;

            // If this is very first appearance of c,
            // we traverse all consecutive occurrences.
            while (i < n && s[i] == c)
                i++;

            // To indicate that character is seen  once.
            oneSeen = true;
        }

        else
            i++;
    }
    return true;
}

// Driver program
int main()
{
    string s = "110029";
    if (checkIfAllTogether(s, '1'))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if all
// occurrences of a character
// appear together in a string.
import java.io.*;

class GFG {

static boolean checkIfAllTogether(String s,
                                    char c)
    {

        // To indicate if one or more
        // occurrences of 'c' are seen
        // or not.
        boolean oneSeen = false;

        // Traverse given string
        int i = 0, n = s.length();
        while (i < n)
        {

            // If current character is
            // same as c, we first check
            // if c is already seen.        
            if (s.charAt(i) == c)
            {
                if (oneSeen == true)
                    return false;

                // If this is very first
                // appearance of c, we
                // traverse all consecutive
                // occurrences.
                while (i < n && s.charAt(i) == c)
                    i++;

                // To indicate that character
                // is seen once.
                oneSeen = true;
            }

            else
                i++;
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {

        String s = "110029";

        if (checkIfAllTogether(s, '1'))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python program to find
# if all occurrences
# of a character appear
# together in a string.

# function to find
# if all occurrences
# of a character appear
# together in a string.
def checkIfAllTogether(s, c) :

    # To indicate if one or
    # more occurrences of
    # 'c' are seen or not.
    oneSeen = False

    # Traverse given string
    i = 0
    n = len(s)
    while (i < n) :
        # If current character
        # is same as c,
        # we first check
        # if c is already seen.    
        if (s[i] == c) :    
            if (oneSeen == True) :
                return False
            # If this is very first
            # appearance of c,
            # we traverse all
            # consecutive occurrences.
            while (i < n and s[i] == c) :
                i = i + 1
            # To indicate that character
            # is seen once.
            oneSeen = True

        else :
            i = i + 1

    return True

# Driver Code
s = "110029";
if (checkIfAllTogether(s, '1')) :
    print ("Yes\n")
else :
    print ("No\n")

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# program to find if all occurrences
// of a character appear together in a
// string.
using System;

public class GFG {

    static bool checkIfAllTogether(string s,
                                     char c)
    {

        // To indicate if one or more
        // occurrences of 'c' are seen
        // or not.
        bool oneSeen = false;

        // Traverse given string
        int i = 0, n = s.Length;
        while (i < n) {

            // If current character is
            // same as c, we first check
            // if c is already seen.        
            if (s[i] == c) {
                if (oneSeen == true)
                    return false;

                // If this is very first
                // appearance of c, we
                // traverse all consecutive
                // occurrences.
                while (i < n && s[i] == c)
                    i++;

                // To indicate that character
                // is seen once.
                oneSeen = true;
            }

            else
                i++;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        string s = "110029";

        if (checkIfAllTogether(s, '1'))
            Console.Write( "Yes" );
        else
            Console.Write( "No" );
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// if all occurrences
// of a character appear
// together in a string.

// function to find
// if all occurrences
// of a character appear
// together in a string.
function checkIfAllTogether($s, $c)
{

    // To indicate if one or
    // more occurrences of
    // 'c' are seen or not.
    $oneSeen = false;

    // Traverse given string
    $i = 0; $n = strlen($s);
    while ($i < $n)
    {

        // If current character
        // is same as c,
        // we first check
        // if c is already seen.    
        if ($s[$i] == $c)
        {
            if ($oneSeen == true)
                return false;

            // If this is very first
            // appearance of c,
            // we traverse all
            // consecutive occurrences.
            while ($i < $n && $s[$i] == $c)
                $i++;

            // To indicate that character
            // is seen once.
            $oneSeen = true;
        }

        else
            $i++;
    }
    return true;
}

// Driver Code
$s = "110029";
if (checkIfAllTogether($s, '1'))
    echo("Yes\n");
else
    echo("No\n");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find if all
// occurrences of a character appear
// together in a string.
function checkIfAllTogether(s, c)
{

    // To indicate if one or more
    // occurrences of 'c' are seen
    // or not.
    let oneSeen = false;

    // Traverse given string
    let i = 0, n = s.length;

    while (i < n)
    {

        // If current character is
        // same as c, we first check
        // if c is already seen.        
        if (s[i] == c)
        {
            if (oneSeen == true)
                return false;

            // If this is very first
            // appearance of c, we
            // traverse all consecutive
            // occurrences.
            while (i < n && s[i] == c)
                i++;

            // To indicate that character
            // is seen once.
            oneSeen = true;
        }
        else
            i++;
    }
    return true;
}

// Driver code
let s = "110029";

if (checkIfAllTogether(s, '1'))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by mukesh07

</script>
```

**输出:**

```
Yes
```

上述程序的复杂度为 O(n)。