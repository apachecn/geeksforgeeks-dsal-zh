# 检查两个字符串是否相同，忽略它们的情况

> 原文:[https://www . geesforgeks . org/check-如果两个字符串相同-忽略它们的大小写/](https://www.geeksforgeeks.org/check-if-two-strings-are-same-ignoring-their-cases/)

给定两个字符串 str1 和 str2。任务是检查如果遵循不区分大小写的比较，即在 Java 中忽略字符串的大小写，两个给定的字符串是否相同。
**例:**

```
Input: str1 = "Geeks", str2 = "geeks"
Output: Same

Input: str1 = "Geek", str2 = "geeksforgeeks"
Output: Not Same
```

**方法 1:天真的方法**

*   将第一个字符串的每个字符与第二个字符串的相应字符进行比较。
*   如果匹配，比较下一个字符。
*   如果不匹配，通过忽略它们的案例来检查是否匹配。
*   如果匹配，比较下一个字符。
*   如果所有字符都匹配，则返回 true
*   如果任何字符不匹配，则返回 false。

实现如下。

## C++

```
#include <iostream>
using namespace std;

// Function to compare two strings
// ignoring their cases
bool equalIgnoreCase(string str1, string str2)
{
    int i = 0;

    // length of first string
    int len1 = str1.size();

    // length of second string
    int len2 = str2.size();

    // if length is not same
    // simply return false since both string
    // can not be same if length is not equal
    if (len1 != len2)
        return false;

    // loop to match one by one
    // all characters of both string
    while (i < len1) {

        // if current characters of both string are same,
        // increase value of i to compare next character
        if (str1[i] == str2[i]) {
            i++;
        }

        // if any character of first string
        // is some special character
        // or numeric character and
        // not same as corresponding character
        // of second string then return false
        else if (!((str1[i] >= 'a' && str1[i] <= 'z')
                   || (str1[i] >= 'A' && str1[i] <= 'Z'))) {
            return false;
        }

        // do the same for second string
        else if (!((str2[i] >= 'a' && str2[i] <= 'z')
                   || (str2[i] >= 'A' && str2[i] <= 'Z'))) {
            return false;
        }

        // this block of code will be executed
        // if characters of both strings
        // are of different cases
        else {
            // compare characters by ASCII value
            if (str1[i] >= 'a' && str1[i] <= 'z') {
                if (str1[i] - 32 != str2[i])
                    return false;
            }

            else if (str1[i] >= 'A' && str1[i] <= 'Z') {
                if (str1[i] + 32 != str2[i])
                    return false;
            }

            // if characters matched,
            // increase the value of i to compare next char
            i++;

        } // end of outer else block

    } // end of while loop

    // if all characters of the first string
    // are matched with corresponding
    // characters of the second string,
    // then return true
    return true;

} // end of equalIgnoreCase function

// Function to print the same or not same
// if strings are equal or not equal
void equalIgnoreCaseUtil(string str1, string str2)
{
    bool res = equalIgnoreCase(str1, str2);

    if (res == true)
        cout << "Same" << endl;

    else
        cout << "Not Same" << endl;
}

// Driver Code
int main()
{
    string str1, str2;

    str1 = "Geeks";
    str2 = "geeks";
    equalIgnoreCaseUtil(str1, str2);

    str1 = "Geek";
    str2 = "geeksforgeeks";
    equalIgnoreCaseUtil(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
// Function to compare two strings
// ignoring their cases
static boolean equalIgnoreCase(String str1, String str2)
{
    int i = 0;

    // length of first string
    int len1 = str1.length();

    // length of second string
    int len2 = str2.length();

    // if length is not same
    // simply return false since both string
    // can not be same if length is not equal
    if (len1 != len2)
        return false;

    // loop to match one by one
    // all characters of both string
    while (i < len1)
    {

        // if current characters of both string are same,
        // increase value of i to compare next character
        if (str1.charAt(i) == str2.charAt(i))
        {
            i++;
        }

        // if any character of first string
        // is some special character
        // or numeric character and
        // not same as corresponding character
        // of second string then return false
        else if (!((str1.charAt(i) >= 'a' && str1.charAt(i) <= 'z')
                || (str1.charAt(i) >= 'A' && str1.charAt(i) <= 'Z')))
        {
            return false;
        }

        // do the same for second string
        else if (!((str2.charAt(i) >= 'a' && str2.charAt(i) <= 'z')
                || (str2.charAt(i) >= 'A' && str2.charAt(i) <= 'Z')))
        {
            return false;
        }

        // this block of code will be executed
        // if characters of both strings
        // are of different cases
        else
        {
            // compare characters by ASCII value
            if (str1.charAt(i) >= 'a' && str1.charAt(i) <= 'z')
            {
                if (str1.charAt(i) - 32 != str2.charAt(i))
                    return false;
            }

            else if (str1.charAt(i) >= 'A' && str1.charAt(i) <= 'Z')
            {
                if (str1.charAt(i) + 32 != str2.charAt(i))
                    return false;
            }

            // if characters matched,
            // increase the value of i to compare next char
            i++;

        } // end of outer else block

    } // end of while loop

    // if all characters of the first string
    // are matched with corresponding
    // characters of the second string,
    // then return true
    return true;

} // end of equalIgnoreCase function

// Function to print the same or not same
// if strings are equal or not equal
static void equalIgnoreCaseUtil(String str1, String str2)
{
    boolean res = equalIgnoreCase(str1, str2);

    if (res == true)
        System.out.println( "Same" );

    else
        System.out.println( "Not Same" );
}

// Driver Code
public static void main(String args[])
{
    String str1, str2;

    str1 = "Geeks";
    str2 = "geeks";
    equalIgnoreCaseUtil(str1, str2);

    str1 = "Geek";
    str2 = "geeksforgeeks";
    equalIgnoreCaseUtil(str1, str2);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Function to compare two strings
# ignoring their cases
def equalIgnoreCase(str1, str2):
    i = 0

    # length of first string
    len1 = len(str1)

    # length of second string
    len2 = len(str2)

    # if length is not same
    # simply return false since both string
    # can not be same if length is not equal
    if (len1 != len2):
        return False

    # loop to match one by one
    # all characters of both string
    while (i < len1):

        # if current characters of both string are same,
        # increase value of i to compare next character
        if (str1[i] == str2[i]):
            i += 1

        # if any character of first string
        # is some special character
        # or numeric character and
        # not same as corresponding character
        # of second string then return false
        elif (((str1[i] >= 'a' and str1[i] <= 'z') or
               (str1[i] >= 'A' and str1[i] <= 'Z')) == False):
            return False

        # do the same for second string
        elif (((str2[i] >= 'a' and str2[i] <= 'z') or
               (str2[i] >= 'A' and str2[i] <= 'Z')) == False):
            return False

        # this block of code will be executed
        # if characters of both strings
        # are of different cases
        else:

            # compare characters by ASCII value
            if (str1[i] >= 'a' and str1[i] <= 'z'):
                if (ord(str1[i]) - 32 != ord(str2[i])):
                    return False

            elif (str1[i] >= 'A' and str1[i] <= 'Z'):
                if (ord(str1[i]) + 32 != ord(str2[i])):
                    return False

            # if characters matched,
            # increase the value of i
            # to compare next char
            i += 1

        # end of outer else block

    # end of while loop

    # if all characters of the first string
    # are matched with corresponding
    # characters of the second string,
    # then return true
    return True

# end of equalIgnoreCase function

# Function to print the same or not same
# if strings are equal or not equal
def equalIgnoreCaseUtil(str1, str2):
    res = equalIgnoreCase(str1, str2)

    if (res == True):
        print("Same")

    else:
        print("Not Same")

# Driver Code
if __name__ == '__main__':
    str1 = "Geeks"
    str2 = "geeks"
    equalIgnoreCaseUtil(str1, str2)

    str1 = "Geek"
    str2 = "geeksforgeeks"
    equalIgnoreCaseUtil(str1, str2)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
using System;
class GFG
{
// Function to compare two strings
// ignoring their cases
static bool equalIgnoreCase(string str1, string str2)
{
    int i = 0;

    // length of first string
    int len1 = str1.Length;

    // length of second string
    int len2 = str2.Length;

    // if length is not same
    // simply return false since both string
    // can not be same if length is not equal
    if (len1 != len2)
        return false;

    // loop to match one by one
    // all characters of both string
    while (i < len1)
    {

        // if current characters of both string are same,
        // increase value of i to compare next character
        if (str1[i] == str2[i])
        {
            i++;
        }

        // if any character of first string
        // is some special character
        // or numeric character and
        // not same as corresponding character
        // of second string then return false
        else if (!((str1[i] >= 'a' && str1[i] <= 'z')
                || (str1[i] >= 'A' && str1[i] <= 'Z')))
        {
            return false;
        }

        // do the same for second string
        else if (!((str2[i] >= 'a' && str2[i] <= 'z')
                || (str2[i] >= 'A' && str2[i] <= 'Z')))
        {
            return false;
        }

        // this block of code will be executed
        // if characters of both strings
        // are of different cases
        else
        {
            // compare characters by ASCII value
            if (str1[i] >= 'a' && str1[i] <= 'z')
            {
                if (str1[i] - 32 != str2[i])
                    return false;
            }

            else if (str1[i] >= 'A' && str1[i] <= 'Z')
            {
                if (str1[i] + 32 != str2[i])
                    return false;
            }

            // if characters matched,
            // increase the value of i to compare next char
            i++;

        } // end of outer else block

    } // end of while loop

    // if all characters of the first string
    // are matched with corresponding
    // characters of the second string,
    // then return true
    return true;

} // end of equalIgnoreCase function

// Function to print the same or not same
// if strings are equal or not equal
static void equalIgnoreCaseUtil(string str1, string str2)
{
    bool res = equalIgnoreCase(str1, str2);

    if (res == true)
        Console.WriteLine( "Same" );

    else
        Console.WriteLine( "Not Same" );
}

// Driver Code
public static void Main()
{
    string str1, str2;

    str1 = "Geeks";
    str2 = "geeks";
    equalIgnoreCaseUtil(str1, str2);

    str1 = "Geek";
    str2 = "geeksforgeeks";
    equalIgnoreCaseUtil(str1, str2);
}
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
    // Function to compare two strings
    // ignoring their cases
    function equalIgnoreCase(str1, str2)
    {
        let i = 0;

        // length of first string
        let len1 = str1.length;

        // length of second string
        let len2 = str2.length;

        // if length is not same
        // simply return false since both string
        // can not be same if length is not equal
        if (len1 != len2)
            return false;

        // loop to match one by one
        // all characters of both string
        while (i < len1)
        {

            // if current characters of both string are same,
            // increase value of i to compare next character
            if (str1[i] == str2[i])
            {
                i++;
            }

            // if any character of first string
            // is some special character
            // or numeric character and
            // not same as corresponding character
            // of second string then return false
            else if (!((str1[i].charCodeAt() >= 'a'.charCodeAt() && str1[i].charCodeAt() <= 'z'.charCodeAt())
                    || (str1[i].charCodeAt() >= 'A'.charCodeAt() && str1[i].charCodeAt() <= 'Z'.charCodeAt())))
            {
                return false;
            }

            // do the same for second string
            else if (!((str2[i].charCodeAt() >= 'a'.charCodeAt() && str2[i].charCodeAt() <= 'z'.charCodeAt())
                    || (str2[i].charCodeAt() >= 'A'.charCodeAt() && str2[i].charCodeAt() <= 'Z'.charCodeAt())))
            {
                return false;
            }

            // this block of code will be executed
            // if characters of both strings
            // are of different cases
            else
            {
                // compare characters by ASCII value
                if (str1[i].charCodeAt() >= 'a'.charCodeAt() && str1[i].charCodeAt() <= 'z'.charCodeAt())
                {
                    if (str1[i].charCodeAt() - 32 != str2[i].charCodeAt())
                        return false;
                }

                else if (str1[i].charCodeAt() >= 'A'.charCodeAt() && str1[i].charCodeAt() <= 'Z'.charCodeAt())
                {
                    if (str1[i].charCodeAt() + 32 != str2[i].charCodeAt())
                        return false;
                }

                // if characters matched,
                // increase the value of i to compare next char
                i++;

            } // end of outer else block

        } // end of while loop

        // if all characters of the first string
        // are matched with corresponding
        // characters of the second string,
        // then return true
        return true;

    } // end of equalIgnoreCase function

    // Function to print the same or not same
    // if strings are equal or not equal
    function equalIgnoreCaseUtil(str1, str2)
    {
        let res = equalIgnoreCase(str1, str2);

        if (res == true)
            document.write( "Same" + "</br>");

        else
            document.write( "Not Same"  + "</br>");
    }

    let str1, str2;

    str1 = "Geeks";
    str2 = "geeks";
    equalIgnoreCaseUtil(str1, str2);

    str1 = "Geek";
    str2 = "geeksforgeeks";
    equalIgnoreCaseUtil(str1, str2);

    // This code is contributed by diveshrabadiya07.
</script>
```

**Output:** 

```
Same
Not Same
```