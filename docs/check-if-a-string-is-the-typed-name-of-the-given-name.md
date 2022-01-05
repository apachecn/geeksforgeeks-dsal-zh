# 检查字符串是否是给定名称的输入名称

> 原文:[https://www . geesforgeks . org/check-if-a-string-is-type-name-of-the-name/](https://www.geeksforgeeks.org/check-if-a-string-is-the-typed-name-of-the-given-name/)

给定一个人的名字和键入的名字。有时，在输入元音**【aeiou】**时，按键可能被长按，字符将被输入 1 次或更多次。任务是检查键入的名称，并判断键入的名称是否可能是人名，某些字符(可能没有)被长按。返回“**真**”如果是，则返回“**假**”。

**注意:**姓名和打字姓名之间用空格隔开，个人姓名之间没有**空格。名字的每个字符都是**独有的**。**

**示例:**

> **输入:** str = "geeks "，type = " geeeks "
> **输出:** True
> 元音“e”在键入时重复更多次，所有其他字符都匹配。
> 
> **输入:** str = "alice "，type = " a licce "
> **输出:** False
> 这里的‘l’和‘c’是重复的，不是元音。
> 因此名字和键入的名字代表不同的名字。
> 
> **输入:** str = "alex "，type = " aalaeex "
> **输出:** False
> 在键入时多了一个元音‘A’。

**方法:**思路基于[游程编码](https://www.geeksforgeeks.org/run-length-encoding/)。我们只考虑元音，并计算它们在 str 和 typed 中的连续出现次数。字符串中出现的次数必须少于。

下面是上述方法的实现。

## C++

```
// CPP program to implement run length encoding
#include <bits/stdc++.h>
using namespace std;

// Check if the character is vowel or not
bool isVowel(char c)
{
    string vowel = "aeiou";
    for (int i = 0; i < vowel.length(); ++i)
        if (vowel[i] == c)
            return true;
    return false;
}

// Returns true if 'typed' is a typed name
// given str
bool printRLE(string str, string typed)
{
    int n = str.length(), m = typed.length();

    // Traverse through all characters of str.
    int j = 0;
    for (int i = 0; i < n; i++) {

        // If current characters do not match
        if (str[i] != typed[j])
            return false;

        // If not vowel, simply move ahead in both
        if (isVowel(str[i]) == false) {
            j++;
            continue;
        }

        // Count occurrences of current vowel in str
        int count1 = 1;
        while (i < n - 1 && str[i] == str[i + 1]) {
            count1++;
            i++;
        }

        // Count occurrences of current vowel in
        // typed.
        int count2 = 1;
        while (j < m - 1 && typed[j] == str[i]) {
            count2++;
            j++;
        }

        if (count1 > count2)
            return false;
    }

    return true;
}

int main()
{
    string name = "alex", typed = "aaalaeex";
    if (printRLE(name, typed))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement run length encoding

public class Improve {

    // Check if the character is vowel or not
    static boolean isVowel(char c)
    {
        String vowel = "aeiou";
        for (int i = 0; i < vowel.length(); ++i)
            if (vowel.charAt(i) == c)
                return true;
        return false;
    }

    // Returns true if 'typed' is a typed name
    // given str
    static boolean printRLE(String str, String typed)
    {
        int n = str.length(), m = typed.length();

        // Traverse through all characters of str.
        int j = 0;
        for (int i = 0; i < n; i++) {

            // If current characters do not match
            if (str.charAt(i) != typed.charAt(j))
                return false;

            // If not vowel, simply move ahead in both
            if (isVowel(str.charAt(i)) == false) {
                j++;
                continue;
            }

            // Count occurrences of current vowel in str
            int count1 = 1;
            while (i < n - 1 && str.charAt(i) == str.charAt(i+1)) {
                count1++;
                i++;
            }

            // Count occurrences of current vowel in
            // typed.
            int count2 = 1;
            while (j < m - 1 && typed.charAt(j) == str.charAt(i)) {
                count2++;
                j++;
            }

            if (count1 > count2)
                return false;
        }

        return true;
    }

    public static void main(String args[])
    {

           String name = "alex", typed = "aaalaeex";
            if (printRLE(name, typed))
                System.out.println("Yes");
            else
                System.out.println("No");

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to implement run
# length encoding

# Check if the character is
# vowel or not
def isVowel(c):

    vowel = "aeiou"
    for i in range(len(vowel)):
        if(vowel[i] == c):
            return True
    return False

# Returns true if 'typed' is a
# typed name given str
def printRLE(str, typed):

    n = len(str)
    m = len(typed)

    # Traverse through all
    # characters of str
    j = 0
    for i in range(n):

        # If current characters do
        # not match
        if str[i] != typed[j]:
            return False

        # If not vowel, simply move
        # ahead in both
        if isVowel(str[i]) == False:
            j = j + 1
            continue

        # Count occurrences of current
        # vowel in str
        count1 = 1
        while (i < n - 1 and (str[i] == str[i + 1])):
            count1 = count1 + 1
            i = i + 1

        # Count occurrence of current
        # vowel in typed
        count2 = 1
        while(j < m - 1 and typed[j] == str[i]):
            count2 = count2 + 1
            j = j + 1

        if count1 > count2:
            return False

    return True

# Driver code
name = "alex"
typed = "aaalaeex"
if (printRLE(name, typed)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Shashank_Sharma    
```

## C#

```
// C# program to implement run
// length encoding
using System;

class GFG
{

// Check if the character is
// vowel or not
public static bool isVowel(char c)
{
    string vowel = "aeiou";
    for (int i = 0;
             i < vowel.Length; ++i)
    {
        if (vowel[i] == c)
        {
            return true;
        }
    }
    return false;
}

// Returns true if 'typed' is
//  a typed name given str
public static bool printRLE(string str,
                            string typed)
{
    int n = str.Length, m = typed.Length;

    // Traverse through all
    // characters of str.
    int j = 0;
    for (int i = 0; i < n; i++)
    {

        // If current characters
        // do not match
        if (str[i] != typed[j])
        {
            return false;
        }

        // If not vowel, simply move
        // ahead in both
        if (isVowel(str[i]) == false)
        {
            j++;
            continue;
        }

        // Count occurrences of current
        // vowel in str
        int count1 = 1;
        while (i < n - 1 &&
               str[i] == str[i + 1])
        {
            count1++;
            i++;
        }

        // Count occurrences of current
        // vowel in typed
        int count2 = 1;
        while (j < m - 1 &&
               typed[j] == str[i])
        {
            count2++;
            j++;
        }

        if (count1 > count2)
        {
            return false;
        }
    }

    return true;
}

// Driver Code
public static void Main(string[] args)
{
    string name = "alex",
           typed = "aaalaeex";
    if (printRLE(name, typed))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// run length encoding

// Check if the character is vowel or not
function isVowel($c)
{
    $vowel = "aeiou";
    for ($i = 0; $i < strlen($vowel); ++$i)
        if ($vowel[$i] == $c)
            return true;
    return false;
}

// Returns true if 'typed'
// is a typed name
// given str
function printRLE($str, $typed)
{
    $n = strlen($str);
    $m = strlen($typed);

    // Traverse through all
    // characters of str.
    $j = 0;
    for ($i = 0; $i < $n; $i++) {

        // If current characters
        // do not match
        if ($str[$i] != $typed[$j])
            return false;

        // If not vowel, simply
        // move ahead in both
        if (isVowel($str[$i]) == false) {
            $j++;
            continue;
        }

        // Count occurrences of
        // current vowel in str
        $count1 = 1;
        while ($i < $n - 1 && $str[$i] == $str[$i + 1]) {
            $count1++;
            $i++;
        }

        // Count occurrences of
        // current vowel in typed.
        $count2 = 1;
        while ($j < $m - 1 && $typed[$j] == $str[$i]) {
            $count2++;
            $j++;
        }

        if ($count1 > $count2)
            return false;
    }

    return true;
}

// Driver code
$name = "alex";
$typed = "aaalaeex";
if (printRLE($name, $typed))
        echo "Yes";
else
        echo "No";

// This code is contributed
// by Shivi_Aggarwal    
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// run length encoding

// Check if the character is vowel or not
function isVowel(c)
{
    let vowel = "aeiou";
    for(let i = 0; i < vowel.length; ++i)
    {
        if (vowel[i] == c)
        {
            return true;
        }
    }
    return false;
}

// Returns true if 'typed' is
//  a typed name given str
function printRLE(str, typed)
{
    let n = str.length, m = typed.length;

    // Traverse through all
    // characters of str.
    let j = 0;
    for(let i = 0; i < n; i++)
    {

        // If current characters
        // do not match
        if (str[i] != typed[j])
        {
            return false;
        }

        // If not vowel, simply move
        // ahead in both
        if (isVowel(str[i]) == false)
        {
            j++;
            continue;
        }

        // Count occurrences of current
        // vowel in str
        let count1 = 1;
        while (i < n - 1 &&
               str[i] == str[i + 1])
        {
            count1++;
            i++;
        }

        // Count occurrences of current
        // vowel in typed
        let count2 = 1;
        while (j < m - 1 &&
               typed[j] == str[i])
        {
            count2++;
            j++;
        }
        if (count1 > count2)
        {
            return false;
        }
    }
    return true;
}

// Driver code
let name = "alex", typed = "aaalaeex";
if (printRLE(name, typed))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by decode2207

</script>
```

**Output:** 

```
No
```

**时间复杂度:**O(m+n)
T3】辅助空间: O(1)