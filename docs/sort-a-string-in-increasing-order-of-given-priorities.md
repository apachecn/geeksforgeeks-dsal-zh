# 按照给定优先级的递增顺序对字符串进行排序

> 原文:[https://www . geesforgeks . org/sort-a-string-in-递增顺序-给定优先级/](https://www.geeksforgeeks.org/sort-a-string-in-increasing-order-of-given-priorities/)

给定一个长度为 **N** 的字母数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是[根据以下条件按优先级的升序对字符串](https://www.geeksforgeeks.org/sort-string-characters/)进行排序:

*   ASCII 值为偶数的字符比 ASCII 值为奇数的字符具有更高的优先级。
*   偶数比奇数有更高的优先级。
*   数字的*优先级高于字符的*。
*   对于具有相同奇偶校验的字符或数字，优先级按照其 ASCII 值的升序排列。

**示例:**

> **输入:** S = "abcd1234"
> **输出:** 1324bdac
> **说明:**
> a 的 ASCII 值为 97。
> ASCII 值“b”为 98。
> ASCII 值“c”为 99。
> ASCII 值“d”为 100。
> 由于 ASCII 值均匀的字符优先级较高，“b”和“d”放在第一位，后面是“a”和“c”。
> 同样，偶数比奇数优先级高。因此，它们被放在第一位。
> 由于数字的优先级高于字符，因此排序后的字符串为“1324bdac”
> 
> **输入:**S = " ADB 123 "
> T3】输出: bda132

**做法:**思路是将 ASCII 值为奇数和偶数的字符以及奇偶校验位的数字分开。然后，按照优先级的顺序连接这些子字符串。按照以下步骤解决问题:

1.  初始化两个变量，比如**数字**和**字符**，分别存储字符和数字。
2.  根据 ASCII 表对字符串**数字**和**字符**进行排序。
3.  现在，遍历字符中的所有字符，并将每个具有奇数奇偶校验的字符附加到一个变量上，比如说**奇数字符**，将每个具有偶数奇偶校验的字符附加到另一个变量上，比如说**偶数字符**。
4.  同样，对于字符串数字，将奇偶校验位分开，比如**奇数位**和**偶数位**。
5.  最后，[将字符串连接为**奇数字符+偶数字符+奇数字符+偶数字符**。](https://www.geeksforgeeks.org/python-string-concatenation/)

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the string s
// based on the given conditions
string sortString(string s)
{
    // Stores digits of given string
    string digits = "";

    // Stores characters of given string
    string character = "";

    // Iterate over characters of the string
    for (int i = 0; i < s.size(); ++i) {
        if (s[i] >= '0' && s[i] <= '9')
 {
     digits += s[i];
 }
 else
 {
     character += s[i];
 }
 }

 // Sort the string of digits
 sort(digits.begin(), digits.end());

 // Sort the string of characters
 sort(character.begin(), character.end());

 // Stores odd and even characters
 string OddChar = "", EvenChar = "";

 // Separate odd and even digits
 for (int i = 0; i < digits.length(); ++i) {
     if ((digits[i] - '0') % 2 == 1) {
         OddChar += digits[i];
     }
     else {
         EvenChar += digits[i];
     }
 }

 // Concatenate strings in the order
 // odd characters followed by even
 OddChar += EvenChar;

 EvenChar = "";

 // Separate the odd and even chars
 for (int i = 0; i < character.length();
      ++i) {

     if ((character[i] - 'a') % 2 == 1) {
         OddChar += character[i];
     }
     else {
         EvenChar += character[i];
     }
 }

 // Final string
 OddChar += EvenChar;

 // Return the final string
 return OddChar;
 }

 // Driver Code
 int main()
 {
     // Given string
     string s = "abcd1234";

     // Returns the sorted string
     cout << sortString(s);

     return 0;
 }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

    // Function to sort the String s
    // based on the given conditions
    static String sortString(String s)
    {

        // Stores digits of given String
        String digits = "";

        // Stores characters of given String
        String character = "";

        // Iterate over characters of the String
        for (int i = 0; i < s.length(); ++i) {
            if (s.charAt(i) >= '0' && s.charAt(i) <= '9') {
                digits += s.charAt(i);
            } else {
                character += s.charAt(i);
            }
        }

        // Sort the String of digits
        digits = sort(digits);
        // Sort the String of characters
        character = sort(character);

        // Stores odd and even characters
        String OddChar = "", EvenChar = "";

        // Separate odd and even digits
        for (int i = 0; i < digits.length(); ++i) {
            if ((digits.charAt(i) - '0') % 2 == 1) {
                OddChar += digits.charAt(i);
            } else {
                EvenChar += digits.charAt(i);
            }
        }

        // Concatenate Strings in the order
        // odd characters followed by even
        OddChar += EvenChar;
        EvenChar = "";

        // Separate the odd and even chars
        for (int i = 0; i < character.length(); ++i) {

            if ((character.charAt(i) - 'a') % 2 == 1) {
                OddChar += character.charAt(i);
            } else {
                EvenChar += character.charAt(i);
            }
        }

        // Final String
        OddChar += EvenChar;

        // Return the final String
        return OddChar;
    }

    static String sort(String inputString)
    {

        // convert input string to char array
        char tempArray[] = inputString.toCharArray();

        // sort tempArray
        Arrays.sort(tempArray);

        // return new sorted string
        return new String(tempArray);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given String
        String s = "abcd1234";

        // Returns the sorted String
        System.out.print(sortString(s));

    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to sort the string s
# based on the given conditions
def sortString(s):

    # Stores digits of given string
    digits = ""

    # Stores characters of given string
    character = ""

    # Iterate over characters of the string
    for i in range(len(s)):
        if (s[i] >= '0' and s[i] <= '9'):
            digits += s[i]
        else:
            character += s[i]

    # Sort the string of digits
    Digits = list(digits)
    Digits.sort()

    # Sort the string of characters
    Character = list(character)
    Character.sort()

    # Stores odd and even characters
    OddChar, EvenChar = "", ""

    # Separate odd and even digits
    for i in range(len(Digits)):
        if ((ord(digits[i]) - ord('0')) % 2 == 1):
            OddChar += Digits[i]
        else:
            EvenChar += Digits[i]

    # Concatenate strings in the order
    # odd characters followed by even
    OddChar += EvenChar
    EvenChar = ""

    # Separate the odd and even chars
    for i in range(len(Character)):
        if ((ord(Character[i]) - ord('a')) % 2 == 1):
            OddChar += Character[i]
        else:
            EvenChar += Character[i]

    # Final string
    OddChar += EvenChar

    # Return the final string
    return OddChar

# Driver Code

# Given string
s = "abcd1234"

# Returns the sorted string
print(sortString(list(s)))

# This code is contributed by divyesh072019
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to sort the string s
  // based on the given conditions
  static string sortString(char[] s)
  {

    // Stores digits of given string
    string digits = "";

    // Stores characters of given string
    string character = "";

    // Iterate over characters of the string
    for (int i = 0; i < s.Length; ++i)
    {
      if (s[i] >= '0' && s[i] <= '9')
      {
        digits += s[i];
      }
      else
      {
        character += s[i];
      }
    }

    // Sort the string of digits
    char[] Digits = digits.ToCharArray();
    Array.Sort(Digits);

    // Sort the string of characters
    char[] Character = character.ToCharArray();
    Array.Sort(Character);

    // Stores odd and even characters
    string OddChar = "", EvenChar = "";

    // Separate odd and even digits
    for (int i = 0; i < Digits.Length; ++i)
    {
      if ((digits[i] - '0') % 2 == 1)
      {
        OddChar += Digits[i];
      }
      else
      {
        EvenChar += Digits[i];
      }
    }

    // Concatenate strings in the order
    // odd characters followed by even
    OddChar += EvenChar;
    EvenChar = "";

    // Separate the odd and even chars
    for (int i = 0; i < Character.Length; ++i)
    {

      if ((Character[i] - 'a') % 2 == 1)
      {
        OddChar += Character[i];
      }
      else
      {
        EvenChar += Character[i];
      }
    }

    // Final string
    OddChar += EvenChar;

    // Return the final string
    return OddChar;
  }

  // Driver code
  static void Main()
  {

    // Given string
    string s = "abcd1234";

    // Returns the sorted string
    Console.WriteLine(sortString(s.ToCharArray()));
  }
}

// This code is contributed by divyehrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to sort the string s
    // based on the given conditions
    function sortString(s)
    {

      // Stores digits of given string
      let digits = "";

      // Stores characters of given string
      let character = "";

      // Iterate over characters of the string
      for (let i = 0; i < s.length; ++i)
      {
        if (s[i].charCodeAt() >= '0'.charCodeAt() && s[i].charCodeAt() <= '9'.charCodeAt())
        {
          digits += s[i];
        }
        else
        {
          character += s[i];
        }
      }

      // Sort the string of digits
      let Digits = digits.split('');
      Digits.sort();

      // Sort the string of characters
      let Character = character.split('');
      Character.sort();

      // Stores odd and even characters
      let OddChar = "", EvenChar = "";

      // Separate odd and even digits
      for (let i = 0; i < Digits.length; ++i)
      {
        if ((digits[i].charCodeAt() - '0'.charCodeAt()) % 2 == 1)
        {
          OddChar += Digits[i];
        }
        else
        {
          EvenChar += Digits[i];
        }
      }

      // Concatenate strings in the order
      // odd characters followed by even
      OddChar += EvenChar;
      EvenChar = "";

      // Separate the odd and even chars
      for (let i = 0; i < Character.length; ++i)
      {

        if ((Character[i].charCodeAt() - 'a'.charCodeAt()) % 2 == 1)
        {
          OddChar += Character[i];
        }
        else
        {
          EvenChar += Character[i];
        }
      }

      // Final string
      OddChar += EvenChar;

      // Return the final string
      return OddChar;
    }

    // Given string
    let s = "abcd1234";

    // Returns the sorted string
    document.write(sortString(s.split('')));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
1324bdac
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)