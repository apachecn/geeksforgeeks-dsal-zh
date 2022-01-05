# 串中元音、辅音、数字、特殊字符计数程序。

> 原文:[https://www . geesforgeks . org/program-count-元音-辅音-数字-特殊字符-string/](https://www.geeksforgeeks.org/program-count-vowels-consonant-digits-special-characters-string/)

给定一个字符串，任务是统计字符串中的元音、辅音、数字和特殊字符。特殊字符也包含空格。
示例:

```
Input : str = "geeks for geeks121"
Output : Vowels: 5
         Consonant: 8
         Digit: 3
         Special Character: 2

Input : str = " A1 B@ d  adc"
Output : Vowels: 2
         Consonant: 4
         Digit: 1
         Special Character: 6
```

## C++

```
// Program to count vowels, consonant, digits and
// special character in a given string.
#include <bits/stdc++.h>
using namespace std;

// Function to count number of vowels, consonant, 
// digitsand special character in a string.
void countCharacterType(string str)
{
    // Declare the variable vowels, consonant, digit
    // and special characters
    int vowels = 0, consonant = 0, specialChar = 0,
        digit = 0;

    // str.length() function to count number of
    // character in given string.
    for (int i = 0; i < str.length(); i++) {

        char ch = str[i];

        if ( (ch >= 'a' && ch <= 'z') ||
              (ch >= 'A' && ch <= 'Z') ) {

            // To handle upper case letters
            ch = tolower(ch);

            if (ch == 'a' || ch == 'e' || ch == 'i' ||
                ch == 'o' || ch == 'u')
                vowels++;
            else
                consonant++;
        }
        else if (ch >= '0' && ch <= '9')
            digit++;
        else
            specialChar++;
    }
    cout << "Vowels: " << vowels << endl;
    cout << "Consonant: " << consonant << endl;
    cout << "Digit: " << digit << endl;
    cout << "Special Character: " << specialChar << endl;
}

// Driver function.
int main()
{
    string str = "geeks for geeks121";
    countCharacterType(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count vowels, consonant, digits and
// special character in a given string
import java.io.*;

public class GFG {

    // Function to count number of vowels, consonant,
    // digitsand special character in a string.
    static void countCharacterType(String str)
    {
        // Declare the variable vowels, consonant, digit
        // and special characters
        int vowels = 0, consonant = 0, specialChar = 0,
            digit = 0;

        // str.length() function to count number of
        // character in given string.
        for (int i = 0; i < str.length(); i++) {

            char ch = str.charAt(i);

            if ( (ch >= 'a' && ch <= 'z') ||
                (ch >= 'A' && ch <= 'Z') ) {

                // To handle upper case letters
                ch = Character.toLowerCase(ch);;

                if (ch == 'a' || ch == 'e' || ch == 'i' ||
                    ch == 'o' || ch == 'u')
                    vowels++;
                else
                    consonant++;
            }
            else if (ch >= '0' && ch <= '9')
                digit++;
            else
                specialChar++;
        }

        System.out.println("Vowels: " + vowels);
        System.out.println("Consonant: " + consonant);
        System.out.println("Digit: " + digit);
        System.out.println("Special Character: " + specialChar);
    }

    // Driver function.
    static public void main (String[] args)
    {
        String str = "geeks for geeks121";

        countCharacterType(str);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 Program to count vowels,
# consonant, digits and special
# character in a given string.

# Function to count number of vowels,
# consonant, digits and special
# character in a string.
def countCharacterType(str):

    # Declare the variable vowels,
    # consonant, digit and special
    # characters
    vowels = 0
    consonant = 0
    specialChar = 0
    digit = 0

    # str.length() function to count
    # number of character in given string.
    for i in range(0, len(str)):

        ch = str[i]

        if ( (ch >= 'a' and ch <= 'z') or
             (ch >= 'A' and ch <= 'Z') ):

            # To handle upper case letters
            ch = ch.lower()

            if (ch == 'a' or ch == 'e' or ch == 'i'
                        or ch == 'o' or ch == 'u'):
                vowels += 1
            else:
                consonant += 1

        elif (ch >= '0' and ch <= '9'):
            digit += 1
        else:
            specialChar += 1

    print("Vowels:", vowels)
    print("Consonant:", consonant)
    print("Digit:", digit)
    print("Special Character:", specialChar)

# Driver function.
str = "geeks for geeks121"
countCharacterType(str)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// Program to count vowels, consonant,
// digits and special character in
// a given string
using System;
using System.Globalization;

class GFG {

    // Function to count number of
    // vowels, consonant, digitsand
    // special character in a string.
    static void countCharacterType(string str)
    {
        // Declare the variable vowels, consonant,
        // digit and special characters
        int vowels = 0, consonant = 0,
        specialChar = 0, digit = 0;

        // str.length() function to count number of
        // character in given string.
        for (int i = 0; i < str.Length; i++) {

            char ch = str[i];

            if ((ch >= 'a' && ch <= 'z') ||
                (ch >= 'A' && ch <= 'Z')) {

                // To handle upper case letters
                ch = char.ToLower(ch);

                if (ch == 'a' || ch == 'e' || ch == 'i' ||
                    ch == 'o' || ch == 'u')
                    vowels++;
                else
                    consonant++;
            }
            else if (ch >= '0' && ch <= '9')
                digit++;
            else
                specialChar++;
        }
        Console.WriteLine("Vowels: " + vowels);
        Console.WriteLine("Consonant: " + consonant);
        Console.WriteLine("Digit: " + digit);
        Console.WriteLine("Special Character: " + specialChar);
    }

    // Driver function.
    static public void Main()
    {
        string str = "geeks for geeks121";
        countCharacterType(str);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

      // Program to count vowels, consonant,
      // digits and
      // special character in a given string.

      // Function to count number of vowels, consonant,
      // digitsand special character in a string.
      function countCharacterType(str) {
        // Declare the variable vowels,
        // consonant, digit
        // and special characters
        var vowels = 0,
          consonant = 0,
          specialChar = 0,
          digit = 0;

        // str.length() function to count number of
        // character in given string.
        for (var i = 0; i < str.length; i++) {
          var ch = str[i];

          if ((ch >= "a" && ch <= "z") ||
          (ch >= "A" && ch <= "Z")) {
            // To handle upper case letters
            ch = ch.toLowerCase();

            if (ch == "a" || ch == "e" || ch == "i" ||
            ch == "o" || ch == "u")
              vowels++;
            else consonant++;
          } else if (ch >= "0" && ch <= "9") digit++;
          else specialChar++;
        }
        document.write("Vowels: " + vowels + "<br>");
        document.write("Consonant: " + consonant + "<br>");
        document.write("Digit: " + digit + "<br>");
        document.write("Special Character: " + specialChar + "<br>");
      }

      // Driver function.
      var str = "geeks for geeks121";
      countCharacterType(str);

</script>
```

**输出:**

```
Vowels: 5
Consonant: 8
Digit: 3
Special Character: 2
```