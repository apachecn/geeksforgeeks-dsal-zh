# 使用加密字符串的程序！和@

> 原文:[https://www . geesforgeks . org/program-to-encrypt-a-string-use-and/](https://www.geeksforgeeks.org/program-to-encrypt-a-string-using-and/)

给定一个字符串，任务是使用**加密这个字符串！**和 **@** 符号交替出现。加密邮件时，加密格式必须按照字母顺序重复符号和字母位置。
**例:**

```
Input: string = "Ab" 
Output: !@@
Explanation:
Position of 'A' in alphabetical order is 1
and in String is odd position 
so encrypted message will have 1 '!'

Position of 'b' in alphabetical order is 2
and in String is even position 
so encrypted message will have 2 '@'

Therefore, the output "!@@"

Input: string = "CDE"
Output: !!!@@@@!!!!!
```

**方法:**这是一种非常基本和简单的加密技术，可以通过以下方式完成:

*   从字符串中逐个获取字符
*   对于每个字符，获取该字符的 ASCII 值与“A”(如果该字符是大写字母)或“A”(如果该字母是小写字母)之间的差值。这将是加密字符被重复的次数。
*   对于字符串的第 I 个字符，如果 I 是奇数，加密字符将是'！'如果我是偶数，加密字符将是‘@’。

下面是上面代码的实现:

## C++

```
// C++ program to Encrypt the String
// using ! and @
#include <bits/stdc++.h>
using namespace std;

// Function to encrypt the string
void encrypt(char input[100])
{

    // evenPos is for storing encrypting
    // char at evenPosition
    // oddPos is for storing encrypting
    // char at oddPosition
    char evenPos = '@', oddPos = '!';

    int repeat, ascii;

    for (int i = 0; i <= strlen(input); i++)
    {

        // Get the number of times the character
        // is to be repeated
        ascii = input[i];
        repeat = ascii >= 97 ? ascii - 96 : ascii - 64;

        for (int j = 0; j < repeat; j++)
        {

            // if i is odd, print '!'
            // else print '@'
            if (i % 2 == 0)
                cout << oddPos;
            else
                cout << evenPos;
        }
    }
}

// Driver code
int main()
{
    char input[100] = { 'A', 'b', 'C', 'd' };

    // Encrypt the String
    encrypt(input);
    return 0;
}

// This code is contributed by
// shubhamsingh10
```

## C

```
// C program to Encrypt the String
// using ! and @

#include <stdio.h>
#include <string.h>

// Function to encrypt the string
void encrypt(char input[100])
{

    // evenPos is for storing encrypting
    // char at evenPosition
    // oddPos is for storing encrypting
    // char at oddPosition
    char evenPos = '@', oddPos = '!';

    int repeat, ascii;

    for (int i = 0; i <= strlen(input); i++) {

        // Get the number of times the character
        // is to be repeated
        ascii = input[i];
        repeat = ascii >= 97 ? ascii - 96 : ascii - 64;

        for (int j = 0; j < repeat; j++) {
            // if i is odd, print '!'
            // else print '@'
            if (i % 2 == 0)
                printf("%c", oddPos);
            else
                printf("%c", evenPos);
        }
    }
}

// Driver code
void main()
{
    char input[100] = { 'A', 'b', 'C', 'd' };

    // Encrypt the String
    encrypt(input);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Encrypt the String
// using ! and @
class GFG
{

// Function to encrypt the string
static void encrypt(char input[])
{

    // evenPos is for storing encrypting
    // char at evenPosition
    // oddPos is for storing encrypting
    // char at oddPosition
    char evenPos = '@', oddPos = '!';

    int repeat, ascii;

    for (int i = 0; i < input.length; i++)
    {

        // Get the number of times the character
        // is to be repeated
        ascii = input[i];
        repeat = ascii >= 97 ?
                  ascii - 96 : ascii - 64;

        for (int j = 0; j < repeat; j++)
        {
            // if i is odd, print '!'
            // else print '@'
            if (i % 2 == 0)
                System.out.printf("%c", oddPos);
            else
                System.out.printf("%c", evenPos);
        }
    }
}

// Driver code
public static void main(String[] args)
{
    char input[] = { 'A', 'b', 'C', 'd' };

    // Encrypt the String
    encrypt(input);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to Encrypt the String
# using ! and @

# Function to encrypt the string
def encrypt(input_arr) :

    # evenPos is for storing encrypting
    # char at evenPosition
    # oddPos is for storing encrypting
    # char at oddPosition
    evenPos = '@'; oddPos = '!';

    for i in range(len(input_arr)) :

        # Get the number of times the character
        # is to be repeated
        ascii = ord(input_arr[i]);
        repeat = (ascii - 96 ) if ascii >= 97 \
                               else (ascii - 64);

        for j in range(repeat) :

            # if i is odd, print '!'
            # else print '@'
            if (i % 2 == 0) :
                print(oddPos, end = "");
            else :
                print(evenPos, end = "");

# Driver code
if __name__ == "__main__" :

    input_arr = [ 'A', 'b', 'C', 'd' ];

    # Encrypt the String
    encrypt(input_arr);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to Encrypt the String
// using ! and @
using System;
using System.Collections.Generic;

class GFG
{

// Function to encrypt the string
static void encrypt(char []input)
{

    // evenPos is for storing encrypting
    // char at evenPosition
    // oddPos is for storing encrypting
    // char at oddPosition
    char evenPos = '@', oddPos = '!';

    int repeat, ascii;

    for (int i = 0; i < input.Length; i++)
    {

        // Get the number of times the character
        // is to be repeated
        ascii = input[i];
        repeat = ascii >= 97 ?
                ascii - 96 : ascii - 64;

        for (int j = 0; j < repeat; j++)
        {
            // if i is odd, print '!'
            // else print '@'
            if (i % 2 == 0)
                Console.Write("{0}", oddPos);
            else
                Console.Write("{0}", evenPos);
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    char []input = { 'A', 'b', 'C', 'd' };

    // Encrypt the String
    encrypt(input);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to Encrypt the
    // String using ! and @

    // Function to encrypt the string
    function encrypt(input)
    {

        // evenPos is for storing encrypting
        // char at evenPosition
        // oddPos is for storing encrypting
        // char at oddPosition
        let evenPos = '@', oddPos = '!';

        let repeat, ascii;

        for (let i = 0; i < input.length; i++)
        {

            // Get the number of times the character
            // is to be repeated
            ascii = input[i].charCodeAt();
            repeat = ascii >= 97 ?
                    ascii - 96 : ascii - 64;

            for (let j = 0; j < repeat; j++)
            {
                // if i is odd, print '!'
                // else print '@'
                if (i % 2 == 0)
                    document.write(oddPos);
                else
                    document.write(evenPos);
            }
        }
    }

    let input = [ 'A', 'b', 'C', 'd' ];

    // Encrypt the String
    encrypt(input);

</script>
```

**Output:** 

```
!@@!!!@@@@
```