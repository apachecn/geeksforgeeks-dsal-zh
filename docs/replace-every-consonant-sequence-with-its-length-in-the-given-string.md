# 用给定字符串中的长度替换每个辅音序列

> 原文:[https://www . geesforgeks . org/用给定字符串中的长度替换每个辅音序列/](https://www.geeksforgeeks.org/replace-every-consonant-sequence-with-its-length-in-the-given-string/)

给定一个由小写字符组成的字符串**字符串**。任务是用辅音的长度替换连续的辅音序列。
**例:**

> **输入:**str = " abcdieop "
> **输出:** a3eio1
> 给定字符串包含长度为 3 和 1 的两个辅音序列“bcd”和“p”。
> **输入:** str = "abecidofu"
> **输出:**a1e 111u

**方法:**制作一个没有辅音的新字符串。为此，我们必须迭代给定的字符串。如果我们找到元音，它将按原样添加到新字符串中。如果我们找到辅音，那么我们必须找到完整辅音序列的长度，然后把它的长度加到新的字符串中。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the converted string
// after replacing every consonant sequence
// with its length
string replaceConsonants(string str)
{

    // To store the resultant string
    string res = "";
    int i = 0, count = 0;

    // Checking each character
    // for consonant sequence
    while (i < str.length()) {

        // Count the length of consonants sequence
        if (str[i] != 'a'
            && str[i] != 'e'
            && str[i] != 'i'
            && str[i] != 'o'
            && str[i] != 'u') {
            i++;
            count++;
        }
        else {

            // Add the length in the string
            if (count > 0)
                res += to_string(count);

            // Add the vowel
            res += str[i];

            i++;
            count = 0;
        }
    }

    // Check for the last consonant sequence
    // in the string
    if (count > 0)
        res += to_string(count);

    // Return the resultant string
    return res;
}

// Driver code
int main()
{
    string str = "abcdeiop";
    cout << replaceConsonants(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to return the converted string
    // after replacing every consonant sequence
    // with its length
    static String replaceConsonants(String str)
    {

        // To store the resultant string
        String res = "";
        int i = 0, count = 0;

        // Checking each character
        // for consonant sequence
        while (i < str.length()) {

            // Count the length of consonants sequence
            if (str.charAt(i) != 'a'
                && str.charAt(i) != 'e'
                && str.charAt(i) != 'i'
                && str.charAt(i) != 'o'
                && str.charAt(i) != 'u') {
                i++;
                count++;
            }
            else {

                // Add the length in the string
                if (count > 0)
                    res += count;

                // Add the vowel
                res += str.charAt(i);

                i++;
                count = 0;
            }
        }

        // Check for the last consonant sequence
        // in the string
        if (count > 0)
            res += count;

        // Return the resultant string
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abcdeiop";
        System.out.println(replaceConsonants(str));
    }
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the converted string
# after replacing every consonant sequence
# with its length
def replaceConsonants(string) :

    # To store the resultant string
    res = "";
    i = 0; count = 0;

    # Checking each character
    # for consonant sequence
    while (i < len(string)) :

        # Count the length of consonants sequence
        if (string[i] != 'a'
            and string[i] != 'e'
            and string[i] != 'i'
            and string[i] != 'o'
            and string[i] != 'u') :
            i += 1;
            count += 1;

        else :

            # Add the length in the string
            if (count > 0) :
                res += str(count);

            # Add the vowel
            res += string[i];

            i += 1
            count = 0;

    # Check for the last consonant
    # sequence in the string
    if (count > 0) :
        res += str(count);

    # Return the resultant string
    return res;

# Driver code
if __name__ == "__main__" :

    string = "abcdeiop";
    print(replaceConsonants(string));

# This code is contributed by Ryuga
```

## C#

```
using System;

// c# implementation of the approach

public class GFG {

    // Function to return the converted string
    // after replacing every consonant sequence
    // with its length
    public static string replaceConsonants(string str)
    {

        // To store the resultant string
        string res = "";
        int i = 0, count = 0;

        // Checking each character
        // for consonant sequence
        while (i < str.Length) {

            // Count the length of consonants sequence
            if (str[i] != 'a'
                && str[i] != 'e'
                && str[i] != 'i'
                && str[i] != 'o'
                && str[i] != 'u') {
                i++;
                count++;
            }
            else {

                // Add the length in the string
                if (count > 0) {
                    res += count;
                }

                // Add the vowel
                res += str[i];

                i++;
                count = 0;
            }
        }

        // Check for the last consonant sequence
        // in the string
        if (count > 0) {
            res += count;
        }

        // Return the resultant string
        return res;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string str = "abcdeiop";
        Console.WriteLine(replaceConsonants(str));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach

      // Function to return the converted string
      // after replacing every consonant sequence
      // with its length
      function replaceConsonants(str) {
        // To store the resultant string
        var res = "";
        var i = 0,
          count = 0;

        // Checking each character
        // for consonant sequence
        while (i < str.length) {
          // Count the length of consonants sequence
          if (
            str[i] !== "a" &&
            str[i] !== "e" &&
            str[i] !== "i" &&
            str[i] !== "o" &&
            str[i] !== "u"
          ) {
            i++;
            count++;
          } else {
            // Add the length in the string
            if (count > 0) res += count.toString();

            // Add the vowel
            res += str[i];

            i++;
            count = 0;
          }
        }

        // Check for the last consonant sequence
        // in the string
        if (count > 0) res += count.toString();

        // Return the resultant string
        return res;
      }

      // Driver code
      var str = "abcdeiop";
      document.write(replaceConsonants(str));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
a3eio1
```