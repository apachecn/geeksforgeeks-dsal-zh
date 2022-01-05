# 检查给定字符串是否为有效数字(整数或浮点)| SET 1(基本方法)

> 原文:[https://www . geesforgeks . org/check-given-string-valid-number-integer-floating-point/](https://www.geeksforgeeks.org/check-given-string-valid-number-integer-floating-point/)

验证给定字符串是否为数字。

**示例:**

```
Input : str = "11.5"
Output : true

Input : str = "abc"
Output : false

Input : str = "2e10"
Output : true

Input : 10e5.4
Output : false

```

下列情况需要在代码中处理。

1.  忽略前导和尾随空格。
2.  忽略“+”、“-”和“.”开始的时候。
3.  确保字符串中的字符属于{+，-，。，e，[0-9]}
4.  请确保没有“.”在“e”之后。
5.  点字符“.”后面应该跟一个数字。
6.  字符“e”后面应该跟有“+”、“-”或一个数字。

下面是上述步骤的实现。

## C++

```
// C++ program to check if input number
// is a valid number
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

int valid_number(string str)
{
    int i = 0, j = str.length() - 1;

    // Handling whitespaces
    while (i < str.length() && str[i] == ' ')
        i++;
    while (j >= 0 && str[j] == ' ')
        j--;

    if (i > j)
        return 0;

    // if string is of length 1 and the only
    // character is not a digit
    if (i == j && !(str[i] >= '0' && str[i] <= '9'))
        return 0;

    // If the 1st char is not '+', '-', '.' or digit
    if (str[i] != '.' && str[i] != '+'
        && str[i] != '-' && !(str[i] >= '0' && str[i] <= '9'))
        return 0;

    // To check if a '.' or 'e' is found in given
    // string. We use this flag to make sure that
    // either of them appear only once.
    bool flagDotOrE = false;

    for (i; i <= j; i++) {
        // If any of the char does not belong to
        // {digit, +, -, ., e}
        if (str[i] != 'e' && str[i] != '.'
            && str[i] != '+' && str[i] != '-'
            && !(str[i] >= '0' && str[i] <= '9'))
            return 0;

        if (str[i] == '.') {
            // checks if the char 'e' has already
            // occurred before '.' If yes, return 0.
            if (flagDotOrE == true)
                return 0;

            // If '.' is the last character.
            if (i + 1 > str.length())
                return 0;

            // if '.' is not followed by a digit.
            if (!(str[i + 1] >= '0' && str[i + 1] <= '9'))
                return 0;
        }

        else if (str[i] == 'e') {
            // set flagDotOrE = 1 when e is encountered.
            flagDotOrE = true;

            // if there is no digit before 'e'.
            if (!(str[i - 1] >= '0' && str[i - 1] <= '9'))
                return 0;

            // If 'e' is the last Character
            if (i + 1 > str.length())
                return 0;

            // if e is not followed either by
            // '+', '-' or a digit
            if (str[i + 1] != '+' && str[i + 1] != '-'
                && (str[i + 1] >= '0' && str[i] <= '9'))
                return 0;
        }
    }

    /* If the string skips all above cases, then 
    it is numeric*/
    return 1;
}

// Driver code
int main()
{
    char str[] = "0.1e10";
    if (valid_number(str))
        cout << "true";
    else
        cout << "false";
    return 0;
}

// This code is contributed by rahulkumawat2107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if input number
// is a valid number
import java.io.*;
import java.util.*;

class GFG {
    public boolean isValidNumeric(String str)
    {
        str = str.trim(); // trims the white spaces.

        if (str.length() == 0)
            return false;

        // if string is of length 1 and the only
        // character is not a digit
        if (str.length() == 1 && !Character.isDigit(str.charAt(0)))
            return false;

        // If the 1st char is not '+', '-', '.' or digit
        if (str.charAt(0) != '+' && str.charAt(0) != '-'
            && !Character.isDigit(str.charAt(0))
            && str.charAt(0) != '.')
            return false;

        // To check if a '.' or 'e' is found in given
        // string. We use this flag to make sure that
        // either of them appear only once.
        boolean flagDotOrE = false;

        for (int i = 1; i < str.length(); i++) {
            // If any of the char does not belong to
            // {digit, +, -, ., e}
            if (!Character.isDigit(str.charAt(i))
                && str.charAt(i) != 'e' && str.charAt(i) != '.'
                && str.charAt(i) != '+' && str.charAt(i) != '-')
                return false;

            if (str.charAt(i) == '.') {
                // checks if the char 'e' has already
                // occurred before '.' If yes, return 0.
                if (flagDotOrE == true)
                    return false;

                // If '.' is the last character.
                if (i + 1 >= str.length())
                    return false;

                // if '.' is not followed by a digit.
                if (!Character.isDigit(str.charAt(i + 1)))
                    return false;
            }

            else if (str.charAt(i) == 'e') {
                // set flagDotOrE = 1 when e is encountered.
                flagDotOrE = true;

                // if there is no digit before 'e'.
                if (!Character.isDigit(str.charAt(i - 1)))
                    return false;

                // If 'e' is the last Character
                if (i + 1 >= str.length())
                    return false;

                // if e is not followed either by
                // '+', '-' or a digit
                if (!Character.isDigit(str.charAt(i + 1))
                    && str.charAt(i + 1) != '+'
                    && str.charAt(i + 1) != '-')
                    return false;
            }
        }

        /* If the string skips all above cases, then
           it is numeric*/
        return true;
    }

    /* Driver Function to test isValidNumeric function */
    public static void main(String[] args)
    {
        String input = "0.1e10";
        GFG gfg = new GFG();
        System.out.println(gfg.isValidNumeric(input));
    }
}
```

[/sourcecode]

## 蟒蛇 3

```
# Python3 program to check if input number
# is a valid number
def valid_number(str):
    i = 0
    j = len(str) - 1

    # Handling whitespaces
    while i<len(str) and str[i] == ' ':
        i += 1
    while j >= 0 and str[j] == ' ':
        j -= 1

    if i > j:
        return False

    # if string is of length 1 and the only
    # character is not a digit
    if (i == j and not(str[i] >= '0' and 
                       str[i] <= '9')):
        return False

    # If the 1st char is not '+', '-', '.' or digit
    if (str[i] != '.' and str[i] != '+' and 
        str[i] != '-' and not(str[i] >= '0' and 
        str[i] <= '9')):
        return False

    # To check if a '.' or 'e' is found in given
    # string.We use this flag to make sure that
    # either of them appear only once.
    flagDotOrE = False

    for i in range(j + 1):

        # If any of the char does not belong to
        # {digit, +, -,., e}
        if (str[i] != 'e' and str[i] != '.' and 
            str[i] != '+' and str[i] != '-' and not
           (str[i] >= '0' and str[i] <= '9')):
            return False

        if str[i] == '.':

            # check if the char e has already
            # occured before '.' If yes, return 0
            if flagDotOrE:
                return False
            if i + 1 > len(str):
                return False
            if (not(str[i + 1] >= '0' and 
                    str[i + 1] <= '9')):
                return False
        elif str[i] == 'e':

            # set flagDotOrE = 1 when e is encountered.
            flagDotOrE = True

            # if there is no digit before e
            if (not(str[i - 1] >= '0' and 
                    str[i - 1] <= '9')):
                return False

            # if e is the last character
            if i + 1 > len(str):
                return False

            # if e is not followed by
            # '+', '-' or a digit
            if (str[i + 1] != '+' and str[i + 1] != '-' and 
               (str[i + 1] >= '0' and str[i] <= '9')):
                return False

    # If the string skips all the
    # above cases, it must be a numeric string
    return True

# Driver Code
if __name__ == '__main__':
    str = "0.1e10"
    if valid_number(str):
        print('true')
    else:
        print('false')

# This code is contributed by
# chaudhary_19 (Mayank Chaudhary)
```

## C#

// C#程序使用 System 检查输入数字
//是否为有效数字
；

GFG 类{
public Boolean is valid numeric(String str)
{
str = str。trim()；//修剪空白。

if (str。Length == 0)
返回 false

//如果字符串长度为 1，并且唯一的
//字符不是数字
if (str。长度== 1 & &！查尔。IsDigit(str[0])
返回 false

//如果第一个字符不是“+”、“-”、“.”或者数字
if (str[0]！= '+'&' T4】str[0]！= '-'
& &！查尔。IsDigit(str[0]) & & str[0]！= '.')
归假；

//检查是否有“.”或者在给定的
//字符串中找到“e”。我们用这个标志来确保
//它们中的任何一个只出现一次。
布尔 flagDotOrE = false

for(int I = 1；i < str.Length; i++) { // If any of the char does not belong to // {digit, +, -, ., e} if (!char.IsDigit(str[i]) && str[i] != 'e' && str[i] != '.' && str[i] != '+' && str[i] != '-') return false; if (str[i] == '.') { // checks if the char 'e' has already // occurred before '.' If yes, return 0. if (flagDotOrE == true) return false; // If '.' is the last character. if (i + 1 > = str。长度)
返回 false

// if .“”后面没有数字。
如果(！查尔。IsDigit(str[I+1])
返回 false

else if (str[i] == 'e') {
//遇到 e 时设置 flagDotOrE = 1。
flag dotore = true；

//如果“e”前没有数字。
如果(！查尔。IsDigit(str[I–1])
返回 false

//If‘e’是最后一个字符
if (i + 1 > = str。长度)
返回 false

//如果 e 后面没有跟
//“+”、“-”或者一个数字
如果(！查尔。IsDigit(str[I+1])&&str[I+1]！= '+'
& & str[i + 1]！= '-')
返回 false
}

/*如果字符串跳过以上所有情况，
则为数值*/
返回 true

//驱动程序代码
公共静态 void Main(String[]args)
{
String input =“0.1e 10”；
GFG gfg =新 GFG()；
控制台。WriteLine(gfg.isValidNumeric(输入))；
}

//本代码由拉杰普特-吉供稿

**Output:**

```
true

```

**时间复杂度:** O(n)

本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。