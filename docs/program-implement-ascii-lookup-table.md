# 实现 ASCII 查找表的程序

> 原文:[https://www . geesforgeks . org/program-implement-ascii-lookup-table/](https://www.geeksforgeeks.org/program-implement-ascii-lookup-table/)

ASCII 代表美国信息交换标准代码。计算机只能理解数字，因此 ASCII 码是字符的数字表示，如“a”或“@”或某种动作。
[ASCII 查找表](http://www.asciitable.com/)是与字符相关的相应值的表格表示，即我们可以查找字符的相应八进制、十进制、十六进制或 HTML ASCII。
这里，我们实现了一个 ASCII 查找表，它以一个字符作为输入，返回该字符的等效八进制、十进制、十六进制和 HTML ASCII 值。这个 ASCII 查找表适用于字母、数字、运算符、分隔符和特殊符号。
例:

```
Input character = @ 
Output : 
Octal value: 100         
Decimal value: 64
Hexadecimal value: 40
HTML value: &#064;

```

**第一步:**将给定字符转换成它的等效十进制 ASCII。这可以通过隐式地将字符类型转换为整数值(或通过空值减去)来实现。
**第 2 步:**第 1 步计算的值成为字符的十进制表示。将十进制值转换为八进制和十六进制形式，以获得给定格式的输入字符的 ASCII 码。
**第三步:**添加字符& #作为前缀和；作为十进制 ASCII 的后缀，获得的表达式成为给定字符的 HTML ASCII。
这样我们就可以轻松实现 ASCII 查找表。按照下面的代码查看实现。

## C++

```
// C++ implementation of ASCII lookup table
#include <iostream>
#include <string>
using namespace std;

// Function to convert decimal value to
// equivalent octal value
int Octal(int decimal)
{
    int octal = 0;
    string temp = "";
    while (decimal > 0) {
        int remainder = decimal % 8;
        temp = to_string(remainder) + temp;
        decimal /= 8;
    }

    for (int i = 0; i < temp.length(); i++) 
        octal = (octal * 10) + (temp[i] - '0');

    return octal;
}

// Function to convert decimal value to
// equivalent hexadecimal value
string Hexadecimal(int decimal)
{
    string hex = "";
    while (decimal > 0) {

        int remainder = decimal % 16;
        if (remainder >= 0 && remainder <= 9)
            hex = to_string(remainder) + hex;
        else
            hex = (char)('A' + remainder % 10) + hex;
        decimal /= 16;
    }
    return hex;
}

// Function to convert decimal value to
// equivalent HTML value
string HTML(int decimal)
{
    string html = to_string(decimal);
    html = ""&#" + html + ";";
    return html;
}

// ASCII lookup table
void ASCIIlookuptable(char ch)
{
    // Implicit typecasting converts the
    // character into it's equivalent ASCII
    int decimal = ch;

    cout << "Octal value: " << Octal(decimal) << endl;
    cout << "Decimal value: " << decimal << endl;
    cout << "Hexadecimal value: " << Hexadecimal(decimal) << endl;
    cout << "HTML value: " << HTML(decimal);
}

// Driver function
int main()
{
    char ch = '@';
    ASCIIlookuptable(ch);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for ASCII table lookup
import java.util.*;
import java.lang.*;

class GeeksforGeeks {

    // Function to convert decimal value to
    // equivalent octal value
    static int Octal(int decimal)
    {
        int octal = 0;
        String temp = "";
        while (decimal > 0) {
            int remainder = decimal % 8;
            temp = remainder + temp;
            decimal /= 8;
        }

        for (int i = 0; i < temp.length(); i++) 
            octal = (octal * 10) + (temp.charAt(i) - '0');

        return octal;
    }

    // Function to convert decimal value to
    // equivalent hexadecimal value
    static String Hexadecimal(int decimal)
    {
        String hex = "";
        while (decimal > 0) {

            int remainder = decimal % 16;
            if (remainder >= 0 && remainder <= 9)
                hex = remainder + hex;
            else
                hex = (char)('A' + remainder % 10) + hex;
            decimal /= 16;
        }
        return hex;
    }

    // Function to convert decimal value to
    // equivalent HTML value
    static String HTML(int decimal)
    {
        String html = "";
        html = html + decimal;
        html = ""&#" + html + ";";
        return html;
    }

    // ASCII lookup table
    static void ASCIIlookuptable(char ch)
    {
        // Implicit typecasting converts the
        // character into it's equivalent ASCII
        int decimal = ch;

        System.out.println("Octal value: " + Octal(decimal));
        System.out.println("Decimal value: " + decimal);
        System.out.println("Hexadecimal value: " + Hexadecimal(decimal));
        System.out.println("HTML value: " + HTML(decimal));
    }

    // driver function
    public static void main(String args[])
    {
        char ch = '@';
        ASCIIlookuptable(ch);
    }
}
```

## C#

```
// C# implementation for ASCII 
// table lookup
using System;

class GeeksforGeeks {

    // Function to convert decimal value to
    // equivalent octal value
    static int Octal(int decima)
    {
        int octal = 0;
        String temp = "";
        while (decima > 0)
        {
            int remainder = decima % 8;
            temp = remainder + temp;
            decima /= 8;
        }

        for (int i = 0; i < temp.Length; i++) 
            octal = (octal * 10) + 
                    (temp[i] - '0');

        return octal;
    }

    // Function to convert decimal value
    //  to equivalent hexadecimal value
    static String Hexadecimal(int decima)
    {
        String hex = "";
        while (decima > 0) 
        {

            int remainder = decima % 16;
            if (remainder >= 0 && 
                remainder <= 9)
                hex = remainder + hex;
            else
                hex = (char)('A' + remainder % 
                                    10) + hex;
            decima /= 16;
        }
        return hex;
    }

    // Function to convert decimal 
    // value to equivalent HTML value
    static String HTML(int decima)
    {
        String html = "";
        html = html + decima;
        html = ""&#" + html + ";";
        return html;
    }

    // ASCII lookup table
    static void ASCIIlookuptable(char ch)
    {

        // Implicit typecasting converts the
        // character into it's equivalent ASCII
        int decima = ch;

        Console.WriteLine("Octal value: " +
                           Octal(decima));
        Console.WriteLine("Decimal value: " + 
                           decima);
        Console.WriteLine("Hexadecimal value: " +
                           Hexadecimal(decima));
        Console.Write("HTML value: " + 
                       HTML(decima));
    }

    // Driver Code
    public static void Main()
    {
        char ch = '@';
        ASCIIlookuptable(ch);
    }
}

// This code is contributed by nitin mittal.
```

Output:

```
Octal value: 100
Decimal value: 64
Hexadecimal value: 40
HTML value: &#064;

```