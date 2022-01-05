# 检查给定字符串中字母数和数字数是否相等

> 原文:[https://www . geesforgeks . org/check-如果给定字符串中的字母数和数字数相等/](https://www.geeksforgeeks.org/check-if-count-of-alphabets-and-count-of-numbers-are-equal-in-the-given-string/)

给定字母数字字符串 **str** ，任务是检查字母计数和数字计数是否相等。

**示例:**

> **输入:**str = " geeks 01234 "
> T3】输出:是
> T6】说明:T8】字母和数字的个数等于 5。
> 
> **输入:** str = "Gfg01234"
> **输出:**否
> **说明:**
> 字母表的计数是 3，而数字的计数是 5。

**方法:**想法是使用字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)来区分数字和字母表。区分字符后，保留两个计数器，分别计数字母和数字的数量。最后，检查两个计数器是否相等。
字符的 ASCII 范围如下:

*   小写字符:97 到 122
*   大写字符:65 到 90
*   数字:48 到 57

下面是上述方法的实现:

## C++

```
// C++ program to check if the count of
// alphabets and numbers in a string
// are equal or not.

#include <iostream>
using namespace std;

// Function to count the
// number of alphabets
int countOfLetters(string str)
{
    // Counter to store the number
    // of alphabets in the string
    int letter = 0;

    // Every character in the string
    // is iterated
    for (int i = 0; i < str.length(); i++) {

        // To check if the character is
        // an alphabet or not
        if ((str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= 'a' && str[i] <= 'z'))
            letter++;
    }

    return letter;
}

// Function to count the number of numbers
int countOfNumbers(string str)
{
    // Counter to store the number
    // of alphabets in the string
    int number = 0;

    // Every character in the string is iterated
    for (int i = 0; i < str.length(); i++) {

        // To check if the character is
        // a digit or not
        if (str[i] >= '0' && str[i] <= '9')
            number++;
    }

    return number;
}

// Function to check if the
// count of alphabets is equal to
// the count of numbers or not
void check(string str)
{
    if (countOfLetters(str)
        == countOfNumbers(str))
        cout << "Yes\n";
    else
        cout << "No\n";
}

// Driver code
int main()
{
    string str = "GeeKs01324";
    check(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the count of
// alphabets and numbers in a String
// are equal or not.
class GFG
{

// Function to count the
// number of alphabets
static int countOfLetters(String str)
{
    // Counter to store the number
    // of alphabets in the String
    int letter = 0;

    // Every character in the String
    // is iterated
    for (int i = 0; i < str.length(); i++)
    {

        // To check if the character is
        // an alphabet or not
        if ((str.charAt(i) >= 'A' && str.charAt(i) <= 'Z')
            || (str.charAt(i) >= 'a' && str.charAt(i) <= 'z'))
            letter++;
    }

    return letter;
}

// Function to count the number of numbers
static int countOfNumbers(String str)
{
    // Counter to store the number
    // of alphabets in the String
    int number = 0;

    // Every character in the String is iterated
    for (int i = 0; i < str.length(); i++)
    {

        // To check if the character is
        // a digit or not
        if (str.charAt(i) >= '0' && str.charAt(i) <= '9')
            number++;
    }

    return number;
}

// Function to check if the
// count of alphabets is equal to
// the count of numbers or not
static void check(String str)
{
    if (countOfLetters(str)
        == countOfNumbers(str))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}

// Driver code
public static void main(String[] args)
{
    String str = "GeeKs01324";
    check(str);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if the count of
# alphabets and numbers in a string
# are equal or not.

# Function to count the
# number of alphabets
def countOfLetters(string ) :

    # Counter to store the number
    # of alphabets in the string
    letter = 0;

    # Every character in the string
    # is iterated
    for i in range(len(string)) :

        # To check if the character is
        # an alphabet or not
        if ((string[i] >= 'A' and string[i] <= 'Z')
            or (string[i] >= 'a' and string[i] <= 'z')) :
            letter += 1;

    return letter;

# Function to count the number of numbers
def countOfNumbers(string ) :

    # Counter to store the number
    # of alphabets in the string
    number = 0;

    # Every character in the string is iterated
    for i in range(len(string)) :

        # To check if the character is
        # a digit or not
        if (string[i] >= '0' and string[i] <= '9') :
            number += 1;

    return number;

# Function to check if the
# count of alphabets is equal to
# the count of numbers or not
def check(string) :

    if (countOfLetters(string) == countOfNumbers(string)) :
        print("Yes");
    else :
        print("No");

# Driver code
if __name__ == "__main__" :

    string = "GeeKs01324";
    check(string);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to check if the count of
// alphabets and numbers in a String
// are equal or not.
using System;

class GFG
{

// Function to count the
// number of alphabets
static int countOfLetters(String str)
{
    // Counter to store the number
    // of alphabets in the String
    int letter = 0;

    // Every character in the String
    // is iterated
    for (int i = 0; i < str.Length; i++)
    {

        // To check if the character is
        // an alphabet or not
        if ((str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= 'a' && str[i] <= 'z'))
            letter++;
    }

    return letter;
}

// Function to count the number of numbers
static int countOfNumbers(String str)
{
    // Counter to store the number
    // of alphabets in the String
    int number = 0;

    // Every character in the String is iterated
    for (int i = 0; i < str.Length; i++)
    {

        // To check if the character is
        // a digit or not
        if (str[i] >= '0' && str[i] <= '9')
            number++;
    }

    return number;
}

// Function to check if the
// count of alphabets is equal to
// the count of numbers or not
static void check(String str)
{
    if (countOfLetters(str)
        == countOfNumbers(str))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}

// Driver code
public static void Main(String[] args)
{
    String str = "GeeKs01324";
    check(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to check if the count of
// alphabets and numbers in a string
// are equal or not.

// Function to count the
// number of alphabets
function countOfLetters( str)
{
    // Counter to store the number
    // of alphabets in the string
    var letter = 0;

    // Every character in the string
    // is iterated
    for (var i = 0; i < str.length; i++) {

        // To check if the character is
        // an alphabet or not
        if ((str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= 'a' && str[i] <= 'z'))
            letter++;
    }

    return letter;
}

// Function to count the number of numbers
function countOfNumbers( str)
{
    // Counter to store the number
    // of alphabets in the string
    var number = 0;

    // Every character in the string is iterated
    for (var i = 0; i < str.length; i++) {

        // To check if the character is
        // a digit or not
        if (str[i] >= '0' && str[i] <= '9')
            number++;
    }

    return number;
}

// Function to check if the
// count of alphabets is equal to
// the count of numbers or not
function check( str)
{
    if (countOfLetters(str) == countOfNumbers(str))
       document.write( "Yes<br>");
    else
       document.write( "No<br>");
}

var str = "GeeKs01324";
check(str);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```