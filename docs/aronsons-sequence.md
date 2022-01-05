# 阿伦森序列

> 原文:[https://www.geeksforgeeks.org/aronsons-sequence/](https://www.geeksforgeeks.org/aronsons-sequence/)

给定一个整数![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")，生成[阿伦森序列](https://en.wikipedia.org/wiki/Aronson%27s_sequence)的第一个![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")项。
**阿伦森数列**是从句子中 *T(或 t)* 的索引得到的无穷整数序列:

> “T 是这个句子中的第一、第四、第十一、第十六、…个字母。”

*   第一个出现在句子中的 *T* 是在索引 *1* (基于 1 的索引)，第一个提到的数字是*第一个*，即 *1*
*   同样，句子中第二个出现的 *t* 在索引 *4* 处，第二个提到的数字是*第四个*，即 *4*
*   同样，句子中 *t* 的第三次出现在索引 *11* 处，第三次提到的数字是*第十一*即 *11*
*   同样，系列继续为 1，4，11，16，…

**示例:**

> **输入:**n = 3
> T3】输出: 1，4，11
> 
> **输入:** n = 6
> **输出:** 1，4，11，16，24，29

**方法:**一个简单的想法是存储字符串“T 是 the”来获得序列的前两个项。对于这些术语中的每一个，将其转换为序数形式的单词并附加到字符串中，然后计算下一个更高术语的值。对生成 n-2 次的每个后续较高项重复该过程，以生成阿伦森序列的前 n 个项。

要将数字转换为单词，请参考这里的。

下面是上述方法的实现:

## C++

```
// C++ program to generate the
// first n terms of Aronson's sequence

#include <bits/stdc++.h>
using namespace std;

// Returns the given number in words
string convert_to_words(string num)
{

    // Get number of digits in given number
    int len = num.length();

    // Base cases
    if (len == 0 || len > 4) {
        return "";
    }
    /*
      The following arrays contain
      one digit(both cardinal and ordinal forms),
      two digit(<20, ordinal forms) numbers,
      and multiples(ordinal forms) and powers of 10.

     */
    string single_digits_temp[]
        = { "", "one", "two", "three", "four"
              , "five", "six", "seven", "eight", "nine" };
    string single_digits[]
        = { "", "first", "second", "third", "fourth"
              , "fifth", "sixth", "seventh", "eighth", "ninth" };

    string two_digits[]
        = { "", "tenth", "eleventh", "twelfth", "thirteenth"
              , "fourteenth", "fifteenth", "sixteenth"
              , "seventeenth", "eighteenth", "nineteenth" };

    string tens_multiple[]
        = { "", "tenth", "twentieth", "thirtieth", "fortieth"
              , "fiftieth", "sixtieth", "seventieth"
              , "eightieth", "ninetieth" };

    string tens_power[] = { "hundred", "thousand" };
    string word = "";

    // If single digit number
    if (len == 1) {
        word += single_digits[num[0] - '0'];
        return word;
    }
    int i = 0, ctr = 0;
    string s = " ";
    while (i < len) {

        if (len >= 3) {
            if (num[i] != '0') {
                word
                    += single_digits_temp[num[i] - '0']
                       + " ";

                // here len can be 3 or 4
                word += tens_power[len - 3] + " ";
                ctr++;
            }
            len--;
            num.erase(0, 1);
        }

        // last two digits
        else {
            if (ctr != 0) {
                s = " and ";
                word.erase(word.length() - 1);
            }

            // Handle all powers of 10
            if (num[i + 1] == '0')
                if (num[i] == '0')
                    word = word + "th";
                else
                    word += s + tens_multiple[num[i] - '0'];

            // Handle two digit numbers < 20
            else if (num[i] == '1')
                word += s + two_digits[num[i + 1] - '0' + 1];

            else {
                if (num[i] != '0')
                    word
                        += s + tens_multiple[num[i] - '0']
                               .substr(0, tens_multiple[num[i] - '0']
                                  .length() - 4) + "y ";
                else
                    word += s;
                word += single_digits[num[i + 1] - '0'];
            }
            i += 2;
        }
        if (i == len) {
            if (word[0] == ' ')
                word.erase(0, 1);
        }
    }
    return word;
}

// Function to print the first n terms
// of Aronson's sequence
void Aronsons_sequence(int n)
{
    string str = "T is the ";
    int ind = 0;
    for (int i = 0; i < str.length(); i++) {

        // check if character
        // is alphabet or not
        if (isalpha(str[i])) {
            ind += 1;
        }
        if (str[i] == 't' or str[i] == 'T') {
            n -= 1;

            // convert number to words
            // in ordinal format and append
            str += convert_to_words(to_string(ind)) + ", ";
            cout << ind << ", ";
        }
        if (n == 0)

            break;
    }
}

// Driver code
int main(void)
{
    int n = 6;
    Aronsons_sequence(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate the
// first n terms of Aronson's sequence
import java.util.*;

class GFG
{

// Returns the given number in words
static String convert_to_words(char[] num)
{

    // Get number of digits in given number
    int len = num.length;

    // Base cases
    if (len == 0 || len > 4)
    {
        return "";
    }

    /*
    The following arrays contain
    one digit(both cardinal and ordinal forms),
    two digit(<20, ordinal forms) numbers,
    and multiples(ordinal forms) and powers of 10.

    */
    String single_digits_temp[]
        = { "", "one", "two", "three", "four"
            , "five", "six", "seven", "eight", "nine" };
    String single_digits[]
        = { "", "first", "second", "third", "fourth"
            , "fifth", "sixth", "seventh", "eighth", "ninth" };

    String two_digits[]
        = { "", "tenth", "eleventh", "twelfth", "thirteenth"
            , "fourteenth", "fifteenth", "sixteenth"
            , "seventeenth", "eighteenth", "nineteenth" };

    String tens_multiple[]
        = { "", "tenth", "twentieth", "thirtieth", "fortieth"
            , "fiftieth", "sixtieth", "seventieth"
            , "eightieth", "ninetieth" };

    String tens_power[] = { "hundred", "thousand" };
    String word = "";

    // If single digit number
    if (len == 1)
    {
        word += single_digits[num[0] - '0'];
        return word;
    }

    int i = 0, ctr = 0;
    String s = " ";
    while (i < len)
    {

        if (len >= 3)
        {
            if (num[i] != '0')
            {
                word
                    += single_digits_temp[num[i] - '0']
                    + " ";

                // here len can be 3 or 4
                word += tens_power[len - 3] + " ";
                ctr++;
            }
            len--;
            num=Arrays.copyOfRange(num, 1, num.length);
        }

        // last two digits
        else
        {
            if (ctr != 0)
            {
                s = " and ";
                word = word.substring(0,word.length() - 1);
            }

            // Handle all powers of 10
            if (num[i + 1] == '0')
                if (num[i] == '0')
                    word = word + "th";
                else
                    word += s + tens_multiple[num[i] - '0'];

            // Handle two digit numbers < 20
            else if (num[i] == '1')
                word += s + two_digits[num[i + 1] - '0' + 1];

            else
            {
                if (num[i] != '0')
                    word += s + tens_multiple[num[i] - '0']
                            .substring(0, tens_multiple[num[i] - '0']
                                .length() - 4) + "y ";
                else
                    word += s;
                word += single_digits[num[i + 1] - '0'];
            }
            i += 2;
        }
        if (i == len)
        {
            if (word.charAt(0) == ' ')
                word = word.substring(1,word.length());
        }
    }
    return word;
}

// Function to print the first n terms
// of Aronson's sequence
static void Aronsons_sequence(int n)
{
    String str = "T is the ";
    int ind = 0;
    for (int i = 0; i < str.length(); i++)
    {

        // check if character
        // is alphabet or not
        if (Character.isAlphabetic(str.charAt(i)))
        {
            ind += 1;
        }
        if (str.charAt(i) == 't' || str.charAt(i) == 'T')
        {
            n -= 1;

            // convert number to words
            // in ordinal format and append
            str += convert_to_words(String.valueOf(ind).toCharArray()) + ", ";
            System.out.print(ind+ ", ");
        }
        if (n == 0)
            break;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    Aronsons_sequence(n);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to generate the
// first n terms of Aronson's sequence
using System;

class GFG
{

// Returns the given number in words
static String convert_to_words(char[] num)
{

    // Get number of digits in given number
    int len = num.Length;

    // Base cases
    if (len == 0 || len > 4)
    {
        return "";
    }

    /*
    The following arrays contain
    one digit(both cardinal and ordinal forms),
    two digit(<20, ordinal forms) numbers,
    and multiples(ordinal forms) and powers of 10.

    */
    String []single_digits_temp
        = { "", "one", "two", "three", "four"
            , "five", "six", "seven", "eight", "nine" };
    String []single_digits
        = { "", "first", "second", "third", "fourth"
            , "fifth", "sixth", "seventh", "eighth", "ninth" };

    String []two_digits
        = { "", "tenth", "eleventh", "twelfth", "thirteenth"
            , "fourteenth", "fifteenth", "sixteenth"
            , "seventeenth", "eighteenth", "nineteenth" };

    String []tens_multiple
        = { "", "tenth", "twentieth", "thirtieth", "fortieth"
            , "fiftieth", "sixtieth", "seventieth"
            , "eightieth", "ninetieth" };

    String []tens_power = { "hundred", "thousand" };
    String word = "";

    // If single digit number
    if (len == 1)
    {
        word += single_digits[num[0] - '0'];
        return word;
    }

    int i = 0, ctr = 0;
    String s = " ";
    while (i < len)
    {

        if (len >= 3)
        {
            if (num[i] != '0')
            {
                word
                    += single_digits_temp[num[i] - '0']
                    + " ";

                // here len can be 3 or 4
                word += tens_power[len - 3] + " ";
                ctr++;
            }
            len--;
            Array.Copy(num, 1, num, 0, num.Length - 1);
        }

        // last two digits
        else
        {
            if (ctr != 0)
            {
                s = " and ";
                word = word.Substring(0,word.Length - 1);
            }

            // Handle all powers of 10
            if (num[i + 1] == '0')
                if (num[i] == '0')
                    word = word + "th";
                else
                    word += s + tens_multiple[num[i] - '0'];

            // Handle two digit numbers < 20
            else if (num[i] == '1')
                word += s + two_digits[num[i + 1] - '0' + 1];

            else
            {
                if (num[i] != '0')
                    word += s + tens_multiple[num[i] - '0']
                            .Substring(0, tens_multiple[num[i] - '0']
                                .Length - 4) + "y ";
                else
                    word += s;
                word += single_digits[num[i + 1] - '0'];
            }
            i += 2;
        }
        if (i == len)
        {
            if (word[0] == ' ')
                word = word.Substring(1,word.Length - 1);
        }
    }
    return word;
}

// Function to print the first n terms
// of Aronson's sequence
static void Aronsons_sequence(int n)
{
    String str = "T is the ";
    int ind = 0;
    for (int i = 0; i < str.Length; i++)
    {

        // check if character
        // is alphabet or not
        if (char.IsLetterOrDigit(str[i]))
        {
            ind += 1;
        }
        if (str[i] == 't' || str[i] == 'T')
        {
            n -= 1;

            // convert number to words
            // in ordinal format and append
            str += convert_to_words(String.Join("",ind).ToCharArray()) + ", ";
            Console.Write(ind + ", ");
        }
        if (n == 0)
            break;
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;
    Aronsons_sequence(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to generate the
// first n terms of Aronson's sequence

// Returns the given number in words
function convert_to_words(num)
{

    // Get number of digits in given number
    let len = num.length;

    // Base cases
    if (len == 0 || len > 4)
    {
        return "";
    }

    /*
    The following arrays contain
    one digit(both cardinal and ordinal forms),
    two digit(<20, ordinal forms) numbers,
    and multiples(ordinal forms) and powers of 10.
    */
    let single_digits_temp = [ "", "one", "two",
                               "three", "four",
                               "five", "six",
                               "seven", "eight",
                               "nine" ];
    let single_digits = [ "", "first", "second",
                          "third", "fourth",
                          "fifth", "sixth",
                          "seventh", "eighth",
                          "ninth" ];

    let two_digits = [ "", "tenth", "eleventh",
                       "twelfth", "thirteenth",
                       "fourteenth", "fifteenth",
                       "sixteenth", "seventeenth",
                       "eighteenth", "nineteenth" ];

    let tens_multiple = [ "", "tenth", "twentieth",
                          "thirtieth", "fortieth",
                          "fiftieth", "sixtieth",
                          "seventieth", "eightieth",
                          "ninetieth" ];

    let tens_power = [ "hundred", "thousand" ];
    let word = "";

    // If single digit number
    if (len == 1)
    {
        word += single_digits[num[0].charCodeAt(0) -
                                 '0'.charCodeAt(0)];
        return word;
    }

    let i = 0, ctr = 0;
    let s = " ";

    while (i < len)
    {
        if (len >= 3)
        {
            if (num[i] != '0')
            {
                word += single_digits_temp[
                        num[i].charCodeAt(0) -
                        '0'.charCodeAt(0)] + " ";

                // Here len can be 3 or 4
                word += tens_power[len - 3] + " ";
                ctr++;
            }
            len--;
            num=num.slice(1, num.length);
        }

        // Last two digits
        else
        {
            if (ctr != 0)
            {
                s = " and ";
                word = word.substring(0,word.length - 1);
            }

            // Handle all powers of 10
            if (num[i + 1] == '0')
                if (num[i] == '0')
                    word = word + "th";
                else
                    word += s + tens_multiple[
                            num[i].charCodeAt(0) -
                            '0'.charCodeAt(0)];

            // Handle two digit numbers < 20
            else if (num[i] == '1')
                word += s + two_digits[
                    num[i + 1].charCodeAt(0) -
                           '0'.charCodeAt(0) + 1];
            else
            {
                if (num[i] != '0')
                    word += s + tens_multiple[
                            num[i].charCodeAt(0) -
                               '0'.charCodeAt(0)].substring(
                                0, tens_multiple[
                                num[i].charCodeAt(0) -
                                   '0'.charCodeAt(0)].length - 4) + "y ";
                else
                    word += s;

                word += single_digits[
                    num[i + 1].charCodeAt(0) -
                           '0'.charCodeAt(0)];
            }
            i += 2;
        }
        if (i == len)
        {
            if (word.charAt(0) == ' ')
                word = word.substring(1,word.length);
        }
    }
    return word;
}

// Function to print the first n terms
// of Aronson's sequence
function Aronsons_sequence(n)
{
    let str = "T is the ";
    let ind = 0;
    for(let i = 0; i < str.length; i++)
    {

        // Check if character
        // is alphabet or not
        if (str[i].toLowerCase() != str[i].toUpperCase())
        {
            ind += 1;
        }
        if (str[i] == 't' || str[i] == 'T')
        {
            n -= 1;

            // Convert number to words
            // in ordinal format and append
            str += convert_to_words(
                (ind).toString().split("")) + ", ";
            document.write(ind + ", ");
        }
        if (n == 0)
            break;
    }
}

// Driver code
let n = 6;

Aronsons_sequence(n);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
1, 4, 11, 16, 24, 29,
```