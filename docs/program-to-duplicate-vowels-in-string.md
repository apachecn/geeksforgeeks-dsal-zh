# 在字符串中复制元音的程序

> 原文:[https://www . geeksforgeeks . org/program-to-replicate-in-string 元音/](https://www.geeksforgeeks.org/program-to-duplicate-vowels-in-string/)

给定一个字符串“str”，任务是复制这个字符串中的元音。

**示例:**

```
Input: str = "geeks"
Output: geeeeks

Input: str = "java"
Output: jaavaa
```

**方法:**使用循环迭代字符串。检查字符是否是元音并复制它。返回
然后打印结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for printing string
// with duplicate vowels

#include <bits/stdc++.h>
using namespace std;

// Function to check for the Vowel
bool isVowel(char ch)
{
    ch = toupper(ch);
    return (ch == 'A' || ch == 'E'
            || ch == 'I' || ch == 'O'
            || ch == 'U');
}

// Function to get the resultant string
// with vowels duplicated
string duplicateVowels(string str)
{
    int t = str.length();

    // Another string to store
    // the resultant string
    string res = "";

    // Loop to check for each character
    for (int i = 0; i < t; i++) {
        if (isVowel(str[i])) {
            res += str[i];
        }
        res += str[i];
    }

    return res;
}

// Driver Code
int main()
{
    string str = "helloworld";

    // Print the original string
    cout << "Original String: "
         << str << endl;

    string res = duplicateVowels(str);

    // Print the resultant string
    cout << "String with Vowels duplicated: "
         << res << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing string
// with duplicate vowels
import java.util.*;

class GFG
{

    // Function to check for the Vowel
    static boolean isVowel(char ch)
    {
        ch = Character.toUpperCase(ch);
        return (ch == 'A' || ch == 'E' ||
                ch == 'I' || ch == 'O' || ch == 'U');
    }

    // Function to get the resultant string
    // with vowels duplicated
    static String duplicateVowels(String str)
    {
        int t = str.length();

        // Another string to store
        // the resultant string
        String res = "";

        // Loop to check for each character
        for (int i = 0; i < t; i++)
        {
            if (isVowel(str.charAt(i)))
                res += str.charAt(i);
            res += str.charAt(i);
        }
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "helloworld";

        // Print the original string
        System.out.println("Original String: " + str);
        String res = duplicateVowels(str);

        // Print the resultant string
        System.out.println("String with Vowels duplicated: " + res);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for printing String
# with duplicate vowels

# Function to check for the Vowel
def isVowel(ch):
    ch = ch.upper()
    if (ch == 'A' or ch == 'E' or
        ch == 'I' or ch == 'O' or
        ch == 'U'):
        return True
    else:
        return False

# Function to get the resultant String
# with vowels duplicated
def duplicateVowels(S):
    t = len(S)

    # Another to store
    # the resultant String
    res = ""

    # Loop to check for each character
    for i in range(t):
        if (isVowel(S[i])):
            res += S[i]
        res += S[i]

    return res

# Driver Code
S = "helloworld"

# Print the original String
print("Original String: ", S)

res = duplicateVowels(S)

# Print the resultant String
print("String with Vowels duplicated: ", res)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for printing string
// with duplicate vowels
using System;

class GFG
{

    // Function to check for the Vowel
    static bool isVowel(char ch)
    {
        ch = char.ToUpper(ch);
        return (ch == 'A' || ch == 'E' ||
                ch == 'I' || ch == 'O' || ch == 'U');
    }

    // Function to get the resultant string
    // with vowels duplicated
    static String duplicateVowels(String str)
    {
        int t = str.Length;

        // Another string to store
        // the resultant string
        String res = "";

        // Loop to check for each character
        for (int i = 0; i < t; i++)
        {
            if (isVowel(str[i]))
                res += str[i];
            res += str[i];
        }
        return res;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "helloworld";

        // Print the original string
        Console.WriteLine("Original String: " + str);
        String res = duplicateVowels(str);

        // Print the resultant string
        Console.WriteLine("String with Vowels duplicated: " + res);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for printing string
// with duplicate vowels

// Function to check for the Vowel
function isVowel(ch)
{
    ch = ch.toUpperCase();
    return(ch == 'A' || ch == 'E' ||
           ch == 'I' || ch == 'O' ||
           ch == 'U');
}

// Function to get the resultant string
// with vowels duplicated
function duplicateVowels(str)
{
    let t = str.length;

    // Another string to store
    // the resultant string
    let res = "";

    // Loop to check for each character
    for(let i = 0; i < t; i++)
    {
        if (isVowel(str[i]))
            res += str[i];

        res += str[i];
    }
    return res;
}

// Driver Code
let str = "helloworld";

// Print the original string
document.write("Original String: " + str + "<br>");
let res = duplicateVowels(str);

// Print the resultant string
document.write("String with Vowels duplicated: " +
               res + "<br>");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Original String: helloworld
String with Vowels duplicated: heelloowoorld
```