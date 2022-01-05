# 检查字符串中的元音是否按字母顺序排列

> 原文:[https://www . geesforgeks . org/check-字符串中的元音是否按字母顺序排列/](https://www.geeksforgeeks.org/check-whether-the-vowels-in-a-string-are-in-alphabetical-order-or-not/)

给定一个字符串“str”，任务是找出字符串中的元音是否按字母顺序排列。该字符串只包含小写字母。

**示例:**

```
Input: str = "aabbbddeecc"
Output: Vowels are in alphabetical order
The vowel characters in the string are : a, a, e, e 
which are in sorted order.

Input: str = "aabbbdideecc"
Output: Vowels are not in alphabetical order
```

**进场:**

*   遍历数组，找到元音字符。
*   如果任何元音小于数组中先前出现的元音，则打印元音不是按字母顺序排列的。
*   否则，打印元音字母顺序。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that checks whether the vowel
// characters in a string are
// in alphabetical order or not
bool areVowelsInOrder(string s)
{
    int n = s.length();

    // ASCII Value 64 is less than
    // all the alphabets
    // so using it as a default value
    char c = (char)64;

    // check if the vowels in
    // the string are sorted or not
    for (int i = 0; i < n; i++) {
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i'
            || s[i] == 'o' || s[i] == 'u') {

            // if the vowel is smaller
            // than the previous vowel
            if (s[i] < c)
                return false;
            else {

                // store the vowel
                c = s[i];
            }
        }
    }
    return true;
}

// Driver code
int main()
{
    string s = "aabbbddeecc";

    // check whether the vowel
    // characters in a string are
    // in alphabetical order or not
    if (areVowelsInOrder(s))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.io.*;

class GFG {

    // Function that checks whether the vowel
    // characters in a string are
    // in alphabetical order or not
    static boolean areVowelsInOrder(String s)
    {
        int n = s.length();

        // ASCII Value 64 is less than
        // all the alphabets
        // so using it as a default value
        char c = (char)64;

        // check if the vowels in
        // the string are sorted or not
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == 'a' || s.charAt(i) == 'e'
                || s.charAt(i) == 'i' || s.charAt(i) == 'o'
                || s.charAt(i) == 'u') {

                // if the vowel is smaller than the previous
                // vowel
                if (s.charAt(i) < c)
                    return false;
                else {

                    // store the vowel
                    c = s.charAt(i);
                }
            }
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "aabbbddeecc";

        // check whether the vowel
        // characters in a string are
        // in alphabetical order or not
        if (areVowelsInOrder(s))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This Code is contributed
// by anuj_67....
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function that checks whether the vowel
# characters in a string are
# in alphabetical order or not

def areVowelsInOrder(s):

    n = len(s)

    # ASCII Value 64 is less than
    # all the alphabets
    # so using it as a default value
    c = chr(64)

    # check if the vowels in
    # the string are sorted or not
    for i in range(0, n):

        if (s[i] == 'a' or s[i] == 'e' or s[i] ==
                'i' or s[i] == 'o' or s[i] == 'u'):

            # if the vowel is smaller
            # than the previous vowel
            if s[i] < c:
                return False
            else:

                # store the vowel
                c = s[i]

    return True

# Driver code
if __name__ == "__main__":

    s = "aabbbddeecc"

    # check whether the vowel
    # characters in a string are
    # in alphabetical order or not
    if areVowelsInOrder(s):
        print("Yes")

    else:
        print("No")

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    // Function that checks whether the vowel
    // characters in a string are
    // in alphabetical order or not
    public static bool areVowelsInOrder(string s)
    {
        int n = s.Length;

        // ASCII Value 64 is less than
        // all the alphabets
        // so using it as a default value
        char c = (char)64;

        // check if the vowels in
        // the string are sorted or not
        for (int i = 0; i < n; i++) {
            if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i'
                || s[i] == 'o' || s[i] == 'u') {

                // if the vowel is smaller
                // than the previous vowel
                if (s[i] < c) {
                    return false;
                }
                else {

                    // store the vowel
                    c = s[i];
                }
            }
        }
        return true;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string s = "aabbbddeecc";

        // check whether the vowel
        // characters in a string are
        // in alphabetical order or not
        if (areVowelsInOrder(s)) {
            Console.Write("Yes");
        }

        else {
            Console.Write("No");
        }
    }
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that checks whether the vowel
// characters in a string are
// in alphabetical order or not
function areVowelsInOrder($s)
{
    $n = strlen($s);

    // ASCII Value 64 is less than
    // all the alphabets
    // so using it as a default value
    $c = chr(64);

    // check if the vowels in
    // the string are sorted or not
    for ($i = 0; $i < $n; $i++)
    {
        if ($s[$i] == 'a' || $s[$i] == 'e' ||
            $s[$i] == '$i' || $s[$i] == 'o' ||
            $s[$i] == 'u')
        {

            // if the vowel is smaller
            // than the previous vowel
            if ($s[$i] < $c)
                return false;    
            else {

                // store the vowel
                $c = $s[$i];
            }
        }
    }
    return true;
}

// Driver code
$s = "aabbbddeecc";

// check whether the vowel
// characters in a string are
// in alphabetical order or not
if (areVowelsInOrder($s))
    echo "Yes";
else
    echo "No";

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function that checks whether the vowel
// characters in a string are
// in alphabetical order or not
function areVowelsInOrder(s)
{
    var n = s.length;

    // ASCII Value 64 is less than
    // all the alphabets
    // so using it as a default value
    var c = String.fromCharCode(64);

    // check if the vowels in
    // the string are sorted or not
    for (var i = 0; i < n; i++) {
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i'
            || s[i] == 'o' || s[i] == 'u') {

            // if the vowel is smaller
            // than the previous vowel
            if (s[i] < c)
                return false;
            else {

                // store the vowel
                c = s[i];
            }
        }
    }
    return true;
}

var s = "aabbbddeecc";
// check whether the vowel
// characters in a string are
// in alphabetical order or not
if (areVowelsInOrder(s))
   document.write("Yes");
else
   document.write("No");

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)