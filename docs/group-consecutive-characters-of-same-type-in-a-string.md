# 将同一类型的连续字符组合成一个字符串

> 原文:[https://www . geesforgeks . org/group-同类型字符串中的连续字符/](https://www.geeksforgeeks.org/group-consecutive-characters-of-same-type-in-a-string/)

给定一个由大写字母、数字和算术运算符组成的字符串 **str** ，任务是将它们分组为相同类型的连续子字符串。
**例:**

> **输入:** str = "G E E K S 1 2 3 4 5"
> **输出:** GEEKS 12345
> 所有连续的大写字符可以组合在一起
> 所有的数字字符可以组合在一个单独的组中。
> **输入:** str = "DEGFT +- * 5 6 7"
> **输出:** DEGFT +-* 567

**方法:**删除字符串中的所有空格。删除所有空格后，逐个遍历字符串，并根据字符的 ASCII 值对其进行分组。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the modified string
string groupCharacters(string s, int len)
{

    // Store original string
    string temp = "";

    // Remove all white spaces
    for (int i = 0; i < len; i++)
        if (s[i] != ' ')
            temp = temp + s[i];

    len = temp.length();

    // To store the resultant string
    string ans = "";
    int i = 0;

    // Traverse the string
    while (i < len) {

        // Group upper case characters
        if (int(temp[i]) >= int('A')
            && int(temp[i]) <= int('Z')) {
            while (i < len && int(temp[i]) >= int('A')
                   && int(temp[i]) <= int('Z')) {
                ans = ans + temp[i];
                i++;
            }
            ans = ans + " ";
        }

        // Group numeric characters
        else if (int(temp[i]) >= int('0')
                 && int(temp[i]) <= int('9')) {
            while (i < len && int(temp[i]) >= int('0')
                   && int(temp[i]) <= int('9')) {
                ans = ans + temp[i];
                i++;
            }
            ans = ans + " ";
        }

        // Group arithmetic operators
        else {
            while (i < len && int(temp[i]) >= int('*')
                   && int(temp[i]) <= int('/')) {
                ans = ans + temp[i];
                i++;
            }
            ans = ans + " ";
        }
    }

    // Return the resultant string
    return ans;
}

// Driver code
int main()
{
    string s = "34FTG234+ +- *";
    int len = s.length();
    cout << groupCharacters(s, len);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

// Function to return the modified String
static String groupCharacters(char []s, int len)
{

    // Store original String
    String temp = "";

    // Remove all white spaces
    for (int i = 0; i < len; i++)
        if (s[i] != ' ')
            temp = temp + s[i];

    len = temp.length();

    // To store the resultant String
    String ans = "";
    int i = 0;

    // Traverse the String
    while (i < len) {

        // Group upper case characters
        if (temp.charAt(i) >= ('A')
            && temp.charAt(i) <= ('Z')) {
            while (i < len && temp.charAt(i) >= ('A')
                   && temp.charAt(i) <= ('Z')) {
                ans = ans + temp.charAt(i);
                i++;
            }
            ans = ans + " ";
        }

        // Group numeric characters
        else if (temp.charAt(i) >= ('0')
                 && temp.charAt(i) <= ('9')) {
            while (i < len && temp.charAt(i) >= ('0')
                   && temp.charAt(i) <= ('9')) {
                ans = ans + temp.charAt(i);
                i++;
            }
            ans = ans + " ";
        }

        // Group arithmetic operators
        else {
            while (i < len && temp.charAt(i) >= ('*')
                   && temp.charAt(i) <= ('/')) {
                ans = ans + temp.charAt(i);
                i++;
            }
            ans = ans + " ";
        }
    }

    // Return the resultant String
    return ans;
}

// Driver code
public static void main(String[] args) {
   String s = "34FTG234+ +- *";
    int len = s.length();
    System.out.print(groupCharacters(s.toCharArray(), len));
    }
}
// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the modified string
def groupCharacters(s, l):

    # Store original string
    temp = ""

    # Remove all white spaces
    for i in range(l):
        if (s[i] != ' '):
            temp = temp + s[i]

    l = len(temp)

    # To store the resultant string
    ans = ""
    i = 0

    # Traverse the string
    while (i < l):

        # Group upper case characters
        if (ord(temp[i]) >= ord('A')
            and ord(temp[i]) <= ord('Z')):
            while (i < l and ord(temp[i]) >= ord('A')
                and ord(temp[i]) <= ord('Z')) :
                ans = ans + temp[i]
                i += 1

            ans = ans + " "

        # Group numeric characters
        elif (ord(temp[i]) >= ord('0')
                and ord(temp[i]) <= ord('9')):
            while (i < l and ord(temp[i]) >= ord('0')
                and ord(temp[i]) <= ord('9')):
                ans = ans + temp[i]
                i += 1
            ans = ans + " "

        # Group arithmetic operators
        else :
            while (i < l and ord(temp[i]) >= ord('*')
                and ord(temp[i]) <= ord('/')):
                ans = ans + temp[i]
                i += 1
            ans = ans + " "

    # Return the resultant string
    return ans

# Driver code
if __name__ == "__main__":

    s = "34FTG234+ +- *"
    l = len(s)
    print(groupCharacters(s, l))

# This code is contributed by Ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the modified String
    static String groupCharacters(char []s, int len)
    {

        // Store original String
        string temp = "";

        // Remove all white spaces
        for (int j = 0; j < len; j++)
            if (s[j] != ' ')
                temp = temp + s[j];

        len = temp.Length;

        // To store the resultant String
        string ans = "";
        int i = 0;

        // Traverse the String
        while (i < len)
        {

            // Group upper case characters
            if (temp[i] >= ('A')
                && temp[i] <= ('Z'))
            {
                while (i < len && temp[i] >= ('A')
                    && temp[i] <= ('Z'))
                {
                    ans = ans + temp[i];
                    i++;
                }
                ans = ans + " ";
            }

            // Group numeric characters
            else if (temp[i] >= ('0')
                    && temp[i] <= ('9'))
            {
                while (i < len && temp[i] >= ('0')
                    && temp[i] <= ('9'))
                {
                    ans = ans + temp[i];
                    i++;
                }
                ans = ans + " ";
            }

            // Group arithmetic operators
            else
            {
                while (i < len && temp[i] >= ('*')
                    && temp[i] <= ('/'))
                {
                    ans = ans + temp[i];
                    i++;
                }
                ans = ans + " ";
            }
        }

        // Return the resultant String
        return ans;
    }

    // Driver code
    public static void Main()
    {
        string s = "34FTG234+ +- *";
        int len = s.Length;
        Console.WriteLine(groupCharacters(s.ToCharArray(), len));
    }
}

// This code contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the modified string
function groupCharacters($s, $len)
{

    // Store original string
    $temp = "";

    // Remove all white spaces
    for ($i = 0; $i < $len; $i++)
        if ($s[$i] != ' ')
            $temp = $temp.$s[$i];

    $len = strlen($temp);

    // To store the resultant string
    $ans = "";
    $i = 0;

    // Traverse the string
    while ($i < $len)
    {

        // Group upper case characters
        if (ord($temp[$i]) >= ord('A') &&
            ord($temp[$i]) <= ord('Z'))
        {
            while ($i < $len && ord($temp[$i]) >= ord('A') &&
                                ord($temp[$i]) <= ord('Z'))
            {
                $ans = $ans.$temp[$i];
                $i++;
            }
            $ans = $ans . " ";
        }

        // Group numeric characters
        else if (ord($temp[$i]) >= ord('0') &&
                 ord($temp[$i]) <= ord('9'))
        {
            while ($i < $len && ord($temp[$i]) >= ord('0') &&
                                ord($temp[$i]) <= ord('9'))
            {
                $ans = $ans.$temp[$i];
                $i++;
            }
            $ans = $ans . " ";
        }

        // Group arithmetic operators
        else
        {
            while ($i < $len && ord($temp[$i]) >= ord('*') &&
                                ord($temp[$i]) <= ord('/'))
            {
                $ans = $ans.$temp[$i];
                $i++;
            }
            $ans = $ans . " ";
        }
    }

    // Return the resultant string
    return $ans;
}

// Driver code
$s = "34FTG234+ +- *";
$len = strlen($s);
print(groupCharacters($s, $len));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the modified String
function groupCharacters(s,len)
{
    // Store original String
    let temp = "";

    // Remove all white spaces
    for (let i = 0; i < len; i++)
        if (s[i] != ' ')
            temp = temp + s[i];

    len = temp.length;

    // To store the resultant String
    let ans = "";
    let i = 0;

    // Traverse the String
    while (i < len) {

        // Group upper case characters
        if (temp[i] >= ('A')
            && temp[i] <= ('Z')) {
            while (i < len && temp[i] >= ('A')
                   && temp[i] <= ('Z')) {
                ans = ans + temp[i];
                i++;
            }
            ans = ans + " ";
        }

        // Group numeric characters
        else if (temp[i] >= ('0')
                 && temp[i] <= ('9')) {
            while (i < len && temp[i] >= ('0')
                   && temp[i] <= ('9')) {
                ans = ans + temp[i];
                i++;
            }
            ans = ans + " ";
        }

        // Group arithmetic operators
        else {
            while (i < len && temp[i] >= ('*')
                   && temp[i] <= ('/')) {
                ans = ans + temp[i];
                i++;
            }
            ans = ans + " ";
        }
    }

    // Return the resultant String
    return ans;
}

// Driver code
let s = "34FTG234+ +- *";
let len = s.length;
document.write(groupCharacters(s.split(""), len));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
34 FTG 234 ++-*
```