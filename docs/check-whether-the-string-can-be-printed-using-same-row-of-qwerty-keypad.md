# 检查字符串是否可以使用同一行 qwerty 键盘打印

> 原文:[https://www . geesforgeks . org/check-字符串是否可以使用同一行 qwerty 键盘打印/](https://www.geeksforgeeks.org/check-whether-the-string-can-be-printed-using-same-row-of-qwerty-keypad/)

给定一个字符串 **S** ，任务是检查该字符串是否可以仅使用 qwerty 键盘的一行来键入。

![](img/e05b4960a554c7949a6ba6d5ea483314.png)

**示例:**

> **输入:** S = "爸爸"
> **输出:**是
> **说明:**
> 字符“D”和“a”出现在 qwerty 小键盘的同一行。那是第二排。
> **输入:** S = "Mom"
> **输出:**否
> **说明:**
> qwerty 小键盘同一行不存在字符“M”和“o”。

**方法:**想法是将 qwerty 键盘同一行的字符存储到不同的[哈希映射](https://www.geeksforgeeks.org/hashing-data-structure/)中，以检查字符串的所有字符是否来自同一行。
以下是上述方法的实施:

## C++

```
// C++ Program to check whether
// the string can be printed
// using same row of qwerty keypad

#include <bits/stdc++.h>
using namespace std;

// Function to find the row of the
// character in the qwerty keypad
int checkQwertyRow(char x)
{
    // Sets to include the characters
    // from the same row of the qwerty keypad
    set<char> first_row
        = { '1', '2', '3', '4',
            '5', '6', '7', '8',
            '9', '0', '-', '=' };
    set<char> second_row
        = { 'Q', 'W', 'E', 'R', 'T',
            'Y', 'U', 'I', 'O', 'P',
            '[', ']', 'q', 'w', 'e',
            'r', 't', 'y', 'u', 'i',
            'o', 'p' };
    set<char> third_row
        = { 'A', 'S', 'D', 'F', 'G',
            'H', 'J', 'K', 'L', ';',
            ':', 'a', 's', 'd', 'f',
            'g', 'h', 'j', 'k', 'l' };
    set<char> fourth_row
        = { 'Z', 'X', 'C', 'V', 'B',
            'N', 'M', ',', '.',
            '/', 'z', 'x', 'c', 'v',
            'b', 'n', 'm' };

    // Condition to check the row of the
    // current character of the string
    if (first_row.count(x) > 0) {
        return 1;
    }
    else if (second_row.count(x) > 0) {
        return 2;
    }
    else if (third_row.count(x) > 0) {
        return 3;
    }
    else if (fourth_row.count(x) > 0) {
        return 4;
    }

    return 0;
}

// Function to check the characters are
// from the same row of the qwerty keypad
bool checkValidity(string str)
{
    char x = str[0];
    int row = checkQwertyRow(x);
    for (int i = 0; i < str.length(); i++) {
        x = str[i];
        if (row != checkQwertyRow(x)) {
            return false;
        }
    }
    return true;
}

// Driver Code
int main()
{
    string str = "GeeksforGeeks";

    if (checkValidity(str))
        cout << "Yes";
    else
        cout << "No";

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether
// the string can be printed
// using same row of qwerty keypad
import java.util.*;

class GFG{

// Function to find the row of the
// character in the qwerty keypad
static int checkQwertyRow(char x)
{

    // Sets to include the characters
    // from the same row of the qwerty keypad
    Character[] first_row1 = { '1', '2', '3', '4',
                               '5', '6', '7', '8',
                               '9', '0', '-', '=' };
    Set<Character> first_row = new HashSet<>(
     Arrays.asList(first_row1));

    Character[] second_row1 = { 'Q', 'W', 'E', 'R', 'T',
                                'Y', 'U', 'I', 'O', 'P',
                                '[', ']', 'q', 'w', 'e',
                                'r', 't', 'y', 'u', 'i',
                                'o', 'p' };
    Set<Character> second_row = new HashSet<>(
     Arrays.asList(second_row1));

    Character[] third_row1 = { 'A', 'S', 'D', 'F', 'G',
                               'H', 'J', 'K', 'L', ';',
                               ':', 'a', 's', 'd', 'f',
                               'g', 'h', 'j', 'k', 'l' };
    Set<Character> third_row = new HashSet<>(
     Arrays.asList(third_row1));

    Character[] fourth_row1 = { 'Z', 'X', 'C', 'V', 'B',
                                'N', 'M', ',', '.',
                                '/', 'z', 'x', 'c', 'v',
                                'b', 'n', 'm' };
    Set<Character> fourth_row = new HashSet<>(
     Arrays.asList(fourth_row1));

    // Condition to check the row of the
    // current character of the string
    if (first_row.contains(x))
    {
        return 1;
    }
    else if (second_row.contains(x))
    {
        return 2;
    }
    else if (third_row.contains(x))
    {
        return 3;
    }
    else if (fourth_row.contains(x))
    {
        return 4;
    }
    return 0;
}

// Function to check the characters are
// from the same row of the qwerty keypad
static boolean checkValidity(String str)
{
    char x = str.charAt(0);
    int row = checkQwertyRow(x);

    for(int i = 0; i < str.length(); i++)
    {
        x = str.charAt(i);
        if (row != checkQwertyRow(x))
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "GeeksforGeeks";

    if (checkValidity(str))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to check whether
# the string can be printed
# using same row of qwerty keypad

# Function to find the row of the
# character in the qwerty keypad
def checkQwertyRow(x):

    # Sets to include the
    # characters from the
    # same row of the qwerty keypad
    first_row = ['1', '2', '3', '4',
                 '5', '6', '7', '8',
                 '9', '0', '-', '=']

    second_row = ['Q', 'W', 'E', 'R',
                  'T', 'Y', 'U', 'I',
                  'O', 'P', '[', ']',
                  'q', 'w', 'e', 'r',
                  't', 'y', 'u', 'i',
                  'o', 'p']
    third_row = ['A', 'S', 'D', 'F',
                 'G', 'H', 'J', 'K',
                 'L', ';', ':', 'a',
                 's', 'd', 'f', 'g',
                 'h', 'j', 'k', 'l']
    fourth_row = ['Z', 'X', 'C', 'V',
                  'B', 'N', 'M', ',',
                  '.', '/', 'z', 'x',
                  'c', 'v', 'b', 'n', 'm']

    # Condition to check the
    # row of the current character
    # of the string
    if(first_row.count(x) > 0):
        return 1
    elif(second_row.count(x) > 0):
        return 2
    elif(third_row.count(x) > 0):
        return 3
    elif(fourth_row.count(x) > 0):
        return 4
    return 0

# Function to check the 
# characters are from the
# same row of the qwerty keypad
def checkValidity(str):

    x = str[0]
    row = checkQwertyRow(x)

    for i in range(len(str)):
        x = str[i]
        if(row != checkQwertyRow(x)):
            return False
    return True

# Driver Code
str = "GeeksforGeeks"

if(checkValidity(str)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to check whether
// the string can be printed
// using same row of qwerty keypad
using System;
using System.Collections.Generic;

class GFG{

// Function to find the row of the
// character in the qwerty keypad
static int checkQwertyRow(char x)
{

    // Sets to include the characters
    // from the same row of the qwerty keypad
    char[] first_row1 = { '1', '2', '3', '4',
                          '5', '6', '7', '8',
                          '9', '0', '-', '=' };
    HashSet<char> first_row = new HashSet<char>(
                              first_row1);

    char[] second_row1 = { 'Q', 'W', 'E', 'R', 'T',
                           'Y', 'U', 'I', 'O', 'P',
                           '[', ']', 'q', 'w', 'e',
                           'r', 't', 'y', 'u', 'i',
                           'o', 'p' };
    HashSet<char> second_row = new HashSet<char>(
                               second_row1);

    char[] third_row1 = { 'A', 'S', 'D', 'F', 'G',
                          'H', 'J', 'K', 'L', ';',
                          ':', 'a', 's', 'd', 'f',
                          'g', 'h', 'j', 'k', 'l' };
    HashSet<char> third_row = new HashSet<char>(
                              third_row1);

    char[] fourth_row1 = { 'Z', 'X', 'C', 'V', 'B',
                           'N', 'M', ',', '.', '/',
                           'z', 'x', 'c', 'v', 'b',
                           'n', 'm' };
    HashSet<char> fourth_row = new HashSet<char>(
                               fourth_row1);

    // Condition to check the row of the
    // current character of the string
    if (first_row.Contains(x))
    {
        return 1;
    }
    else if (second_row.Contains(x))
    {
        return 2;
    }
    else if (third_row.Contains(x))
    {
        return 3;
    }
    else if (fourth_row.Contains(x))
    {
        return 4;
    }
    return 0;
}

// Function to check the characters are
// from the same row of the qwerty keypad
static bool checkValidity(String str)
{
    char x = str[0];
    int row = checkQwertyRow(x);

    for(int i = 0; i < str.Length; i++)
    {
        x = str[i];
        if (row != checkQwertyRow(x))
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    String str = "GeeksforGeeks";

    if (checkValidity(str))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

      // JavaScript program to check whether
      // the string can be printed
      // using same row of qwerty keypad

      // Function to find the row of the
      // character in the qwerty keypad
      function checkQwertyRow(x) {
        // Sets to include the characters
        // from the same row of the qwerty keypad
        var first_row = [
          "1",
          "2",
          "3",
          "4",
          "5",
          "6",
          "7",
          "8",
          "9",
          "0",
          "-",
          "=",
        ];

        var second_row = [
          "Q",
          "W",
          "E",
          "R",
          "T",
          "Y",
          "U",
          "I",
          "O",
          "P",
          "[",
          "]",
          "q",
          "w",
          "e",
          "r",
          "t",
          "y",
          "u",
          "i",
          "o",
          "p",
        ];
        var third_row = [
          "A",
          "S",
          "D",
          "F",
          "G",
          "H",
          "J",
          "K",
          "L",
          ";",
          ":",
          "a",
          "s",
          "d",
          "f",
          "g",
          "h",
          "j",
          "k",
          "l",
        ];
        var fourth_row = [
          "Z",
          "X",
          "C",
          "V",
          "B",
          "N",
          "M",
          ",",
          ".",
          "/",
          "z",
          "x",
          "c",
          "v",
          "b",
          "n",
          "m",
        ];

        // Condition to check the row of the
        // current character of the string
        if (first_row.includes(x)) {
          return 1;
        } else if (second_row.includes(x)) {
          return 2;
        } else if (third_row.includes(x)) {
          return 3;
        } else if (fourth_row.includes(x)) {
          return 4;
        }
        return 0;
      }

      // Function to check the characters are
      // from the same row of the qwerty keypad
      function checkValidity(str) {
        var x = str[0];
        var row = checkQwertyRow(x);

        for (var i = 0; i < str.length; i++) {
          x = str[i];
          if (row !== checkQwertyRow(x)) {
            return false;
          }
        }
        return true;
      }

      // Driver code
      var str = "GeeksforGeeks";

      if (checkValidity(str)) document.write("Yes");
      else document.write("No");

</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(N)*