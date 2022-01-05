# 通过去除两个辅音之间的元音来修改字符串

> 原文:[https://www . geesforgeks . org/modify-string-by-remove-two-in-wear-in-two-辅音/](https://www.geeksforgeeks.org/modify-string-by-removing-vowels-in-between-two-consonants/)

给定一个仅由小写英文字母组成的字符串 S，任务是通过从两个辅音之间出现的字符串中删除这些元音来更新字符串。
**例**:

> **输入:** bab
> **输出:** bb
> 这里字母‘a’是一个元音，位于两个直接辅音之间。
> 这样，它就从字符串中删除了，结果字符串变成了“**bb**”
> **输入:** geeksforgeeks
> **输出:**geeks geeks
> 在子字符串“for”中，字母“o”位于两个辅音“f”和“r”之间。
> 因此，它从那里被移除，绳子变成-' **极客极客**

**方法:**初始化一个空的*更新数据环*。下面给出了解决上述问题的步骤。

*   从左向右遍历字符串。
*   如果当前字符是元音，检查它前面的字符和它后面的字符，如果**和**都是辅音，那么当前元音是“夹层元音”，需要从 S 中删除，因此不要将该字符附加到 a 上。
    否则，将当前字符附加到 a 上
*   继续这个过程，直到两个辅音之间的所有元音都从字符串中移除

下面是上述方法的实现:

## C++

```
// C++ program to remove all Vowels
// in between two consonants from the string
#include <bits/stdc++.h>
using namespace std;

// Function to check if the character x is a vowel or not
bool isVowel(char x)
{
    if (x == 'a' || x == 'e' || x == 'i' || x == 'o' || x == 'u')
        return true;
    else
        return false;
}

// Returns the updated string formed after removing all
// the Sandwiched Vowels from the given string
string updateSandwichedVowels(string a)
{
    int n = a.length();

    // string to store the Updated String after
    // removing the Sandwiched Vowels
    string updatedString = "";

    // traverse the string from left to right
    for (int i = 0; i < n; i++) {

        // if the current character is the first or the
        // last character of the string then, this needs
        // to be appended to the updatedString, since the
        // corner alphabet irrespective of it being a vowel
        // or a consonant, is never 'Sandwiched'
        if (!i || i == n - 1) {
            updatedString += a[i];
            continue;
        }
        // Check if the current character of the string is
        // a vowel and both the previous and the next characters
        // are consonants, if so then this is a sandwiched
        // vowel, thus is ignored and not appended
        // to the updated string
        if (isVowel(a[i]) && !isVowel(a[i - 1])
            && !isVowel(a[i + 1])) {
            continue;
        }

        // if this character is not a sandwiched Vowel append
        // it to the updated String
        updatedString += a[i];
    }

    return updatedString;
}

// Driver Code
int main()
{

    string str = "geeksforgeeks";

    // Remove all the Sandwitched Vowels
    string updatedString = updateSandwichedVowels(str);

    cout << updatedString;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove all
// Vowels in between two
// consonants from the string
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{

// Function to check if the
// character x is a vowel or not
static boolean isVowel(char x)
{
    if (x == 'a' || x == 'e' ||
        x == 'i' || x == 'o' ||
        x == 'u')
        return true;
    else
        return false;
}

// Returns the updated string
// formed after removing all
// the Sandwiched Vowels from
// the given string
static String updateSandwichedVowels(String a)
{
    int n = a.length();

    // string to store the Updated
    // String after removing the
    // Sandwiched Vowels
    String updatedString = "";

    // traverse the string
    // from left to right
    for (int i = 0; i < n; i++)
    {

        // if the current character is
        // the first or the last character
        // of the string then, this needs
        // to be appended to the updatedString,
        // since the corner alphabet irrespective
        // of it being a vowel or a consonant,
        // is never 'Sandwiched'
        if (i == 0 || i == n - 1)
        {
            updatedString += a.charAt(i);
            continue;
        }

        // Check if the current character
        // of the string is a vowel and both
        // the previous and the next characters
        // are consonants, if so then this is
        // a sandwiched vowel, thus is ignored
        // and not appended to the updated string
        if (isVowel(a.charAt(i))== true &&
            isVowel(a.charAt(i - 1))== false &&
            isVowel(a.charAt(i + 1))== false)
        {
            continue;
        }

        // if this character is not
        // a sandwiched Vowel append
        // it to the updated String
        updatedString += a.charAt(i);
    }

    return updatedString;
}

// Driver Code
public static void main(String[] args)
{

    String str = "geeksforgeeks";

    // Remove all the Sandwitched Vowels
    String updatedString = updateSandwichedVowels(str);

    System.out.print(updatedString);

}
}
```

## 蟒蛇 3

```
# Python 3 program to remove all Vowels
# in between two consonants from the string

# Function to check if the character
# x is a vowel or not
def isVowel(x):
    if (x == 'a' or x == 'e' or x == 'i' or
                    x == 'o' or x == 'u'):
        return True
    else:
        return False

# Returns the updated string formed after
# removing all the Sandwiched Vowels from
# the given string
def updateSandwichedVowels(a):
    n = len(a)

    # string to store the Updated String after
    # removing the Sandwiched Vowels
    updatedString = ""

    # traverse the string from left to right
    for i in range(0, n, 1):

        # if the current character is the first
        # or the last character of the string
        # then, this needs to be appended to
        # the updatedString, since the corner
        # alphabet irrespective of it being a vowel
        # or a consonant, is never 'Sandwiched'
        if (i == 0 or i == n - 1):
            updatedString += a[i]
            continue

        # Check if the current character of the
        # string is a vowel and both the previous
        # and the next characters are consonants,
        # if so then this is a sandwiched vowel,
        # thus is ignored and not appended to the
        # updated string
        if (isVowel(a[i]) == True and
            isVowel(a[i - 1]) == False and
            isVowel(a[i + 1]) == False):
            continue

        # if this character is not a sandwiched
        # Vowel append it to the updated String
        updatedString += a[i]

    return updatedString

# Driver Code
if __name__ == '__main__':
    str = "geeksforgeeks"

    # Remove all the Sandwitched Vowels
    updatedString = updateSandwichedVowels(str)

    print(updatedString)

# This code is contributed by
# Surendra_Gangwar   
```

## C#

```
// C# program to remove all
// Vowels in between two
// consonants from the string
using System;
class GFG
{

// Function to check if the
// character x is a vowel or not
static bool isVowel(char x)
{
    if (x == 'a' || x == 'e' ||
        x == 'i' || x == 'o' ||
        x == 'u')
        return true;
    else
        return false;
}

// Returns the updated string
// formed after removing all
// the Sandwiched Vowels from
// the given string
static String updateSandwichedVowels(String a)
{
    int n = a.Length;
    // string to store the Updated
    // String after removing the
    // Sandwiched Vowels
    String updatedString = "";

    // traverse the string
    // from left to right
    for (int i = 0; i < n; i++)
    {

        // if the current character is
        // the first or the last character
        // of the string then, this needs
        // to be appended to the updatedString,
        // since the corner alphabet irrespective
        // of it being a vowel or a consonant,
        // is never 'Sandwiched'
        if (i == 0 || i == n - 1)
        {
            updatedString += a[i];
            continue;
        }

        // Check if the current character
        // of the string is a vowel and both
        // the previous and the next characters
        // are consonants, if so then this is
        // a sandwiched vowel, thus is ignored
        // and not appended to the updated string
        if ((isVowel(a[i])) == true &&
            isVowel(a[i - 1]) == false &&
            isVowel(a[i + 1]) == false)
        {
            continue;
        }

        // if this character is not
        // a sandwiched Vowel append
        // it to the updated String
        updatedString += a[i];
    }

    return updatedString;
}

// Driver Code
public static void Main()
{

    String str = "geeksforgeeks";

    // Remove all the Sandwitched Vowels
    String updatedString = updateSandwichedVowels(str);

    Console.WriteLine(updatedString);

}
}// This code is contributed by Mukul Singh.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to remove all Vowels
// in between two consonants from the string

// Function to check if the character
// x is a vowel or not
function isVowel($x)
{
    if ($x == 'a' || $x == 'e' ||
        $x == 'i' || $x == 'o' || $x == 'u')
        return true;
    else
        return false;
}

// Returns the updated string formed
// after removing all the Sandwiched
// Vowels from the given string
function updateSandwichedVowels($a)
{
    $n = strlen($a);

    // string to store the Updated String
    // after removing the Sandwiched Vowels
    $updatedString = "";

    // traverse the string from left to right
    for ( $i = 0; $i < $n; $i++)
    {

        // if the current character is the first
        // or the last character of the string
        // then, this needs to be appended to the
        // updatedString, since the corner alphabet
        // irrespective of it being a vowel or a
        // consonant, is never 'Sandwiched'
        if (!$i || $i == $n - 1)
        {
            $updatedString .= $a[$i];
            continue;
        }

        // Check if the current character of the
        // string is a vowel and both the previous
        // and the next characters are consonants,
        // if so then this is a sandwiched vowel,
        // thus is ignored and not appended to the
        // updated string
        if (isVowel($a[$i]) && !isVowel($a[$i - 1]) &&
                               !isVowel($a[$i + 1]))
        {
            continue;
        }

        // if this character is not a sandwiched
        // Vowel append it to the updated String
        $updatedString .= $a[$i];
    }

    return $updatedString;
}

// Driver Code
$str = "geeksforgeeks";

// Remove all the Sandwitched Vowels
$updatedString = updateSandwichedVowels($str);

echo $updatedString;

// This code is contributed
// by princiraj1992
?>
```

## java 描述语言

```
<script>
      // JavaScript program to remove all
      // Vowels in between two
      // consonants from the string
      // Function to check if the
      // character x is a vowel or not
      function isVowel(x) {
        if (x === "a" || x === "e" || x === "i" || x === "o" || x === "u")
          return true;
        else return false;
      }

      // Returns the updated string
      // formed after removing all
      // the Sandwiched Vowels from
      // the given string
      function updateSandwichedVowels(a) {
        var n = a.length;
        // string to store the Updated
        // String after removing the
        // Sandwiched Vowels
        var updatedString = "";

        // traverse the string
        // from left to right
        for (var i = 0; i < n; i++) {
          // if the current character is
          // the first or the last character
          // of the string then, this needs
          // to be appended to the updatedString,
          // since the corner alphabet irrespective
          // of it being a vowel or a consonant,
          // is never 'Sandwiched'
          if (i === 0 || i === n - 1) {
            updatedString += a[i];
            continue;
          }

          // Check if the current character
          // of the string is a vowel and both
          // the previous and the next characters
          // are consonants, if so then this is
          // a sandwiched vowel, thus is ignored
          // and not appended to the updated string
          if (
            isVowel(a[i]) === true &&
            isVowel(a[i - 1]) === false &&
            isVowel(a[i + 1]) === false
          ) {
            continue;
          }

          // if this character is not
          // a sandwiched Vowel append
          // it to the updated String
          updatedString += a[i];
        }

        return updatedString;
      }

      // Driver Code
      var str = "geeksforgeeks";
      // Remove all the Sandwitched Vowels
      var updatedString = updateSandwichedVowels(str);
      document.write(updatedString);
    </script>
```

**输出:**

```
geeksfrgeeks
```

**时间复杂度:** O(N)，其中 N 为输入字符串的长度。
**辅助空间:** O(N)