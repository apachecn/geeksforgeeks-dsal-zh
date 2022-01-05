# 将一个数字从基数 A 转换为基数 B

> 原文:[https://www . geesforgeks . org/convert-a-number-from-base-a-b/](https://www.geeksforgeeks.org/convert-a-number-from-base-a-to-base-b/)

给定两个正整数 **A** 和 **B** 以及一个大小为 **N 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，其中**表示基数 **A** 中的一个数字，任务是将给定字符串 **S** 从基数 **A** 转换为基数 **B** 。

**示例:**

> **输入:** S = "10B "，A = 16，B = 10
> **输出:** 267
> **说明:** 10B 以十六进制(基数= 16)换算成十进制(基数= 10)时为 267。
> 
> **输入:**S =“10011”，A = 2，B = 8
> **输出:** 23
> **说明:** 10011 在二进制(基数= 2)转换为八进制(基数= 8)时为 23。

**方法:** [数字系统是](https://www.geeksforgeeks.org/number-system-and-base-conversions/)在[计算机系统架构](https://www.geeksforgeeks.org/characteristics-of-computer-system/)中表示数字的技术。计算机体系结构支持以下数字系统:

*   **二进制数系统(基数 2):** 二进制数系统只由两位数组成， **0** s 和 **1** s，这个数系统的基数是 **2** 。
*   **八进制数字系统(基数 8):** 八进制数字系统由 **8** 位数字组成，范围从 **0** 到 **7** 。
*   **十进制数字系统(基数 10):** 十进制数字系统由 **10** 位组成，范围从 **0** 到 **9** 。
*   **十六进制数字系统(基数 16):** 十六进制数字系统由带有 **0** 至 **9** 数字的 **16** 数字和字母 **A** 至 **F** 组成。它也称为字母数字代码，因为它由数字和字母组成。

要将一个数从基数 **A** 转换为基数 **B** ，思路是先[将其转换为十进制表示，然后将十进制数转换为基数 **B**](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/) 。

**从任意基数到十进制的转换:**在基数**“基数”**中数字**“str”**的十进制等效值等于**1 * str[len–1]+基数* str[len–2]+(基数)<sup>2</sup>* str[len–3]+…**

**从十进制到任意基数的转换:**
十进制数**【input num】**可以通过重复将 **inputNum** 除以**基数**转换为基数**【基数】**上的数字，并存储余数。最后[反转得到的字符串](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)得到想要的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return ASCII
// value of a character
int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to convert a number
// from given base to decimal number
int toDeci(string str, int base)
{
    // Stores the length
    // of the string
    int len = str.size();

    // Initialize power of base
    int power = 1;

    // Initialize result
    int num = 0;

    // Decimal equivalent is str[len-1]*1
    // + str[len-2]*base + str[len-3]*(base^2) + ...
    for (int i = len - 1; i >= 0; i--) {

        // A digit in input number must
        // be less than number's base
        if (val(str[i]) >= base) {
            printf("Invalid Number");
            return -1;
        }

        // Update num
        num += val(str[i]) * power;

        // Update power
        power = power * base;
    }

    return num;
}

// Function to return equivalent
// character of a given value
char reVal(int num)
{
    if (num >= 0 && num <= 9)
        return (char)(num + '0');
    else
        return (char)(num - 10 + 'A');
}

// Function to convert a given
// decimal number to a given base
string fromDeci(int base, int inputNum)
{
    // Store the result
    string res = "";

    // Repeatedly divide inputNum
    // by base and take remainder
    while (inputNum > 0) {

        // Update res
        res += reVal(inputNum % base);

        // Update inputNum
        inputNum /= base;
    }

    // Reverse the result
    reverse(res.begin(), res.end());

    return res;
}

// Function to convert a given number
// from a base to another base
void convertBase(string s, int a, int b)
{
    // Convert the number from
    // base A to decimal
    int num = toDeci(s, a);

    // Convert the number from
    // decimal to base B
    string ans = fromDeci(b, num);

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given input
    string s = "10B";
    int a = 16, b = 10;

    // Function Call
    convertBase(s, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return ASCII
// value of a character
static int val(char c)
{
    if (c >= '0' && c <= '9')
        return(int)c - '0';
    else
        return(int)c - 'A' + 10;
}

// Function to convert a number
// from given base to decimal number
static int toDeci(String str, int base)
{

    // Stores the length
    // of the String
    int len = str.length();

    // Initialize power of base
    int power = 1;

    // Initialize result
    int num = 0;

    // Decimal equivalent is str[len-1]*1
    // + str[len-2]*base + str[len-3]*(base^2) + ...
    for(int i = len - 1; i >= 0; i--)
    {

        // A digit in input number must
        // be less than number's base
        if (val(str.charAt(i)) >= base)
        {
            System.out.printf("Invalid Number");
            return -1;
        }

        // Update num
        num += val(str.charAt(i)) * power;

        // Update power
        power = power * base;
    }
    return num;
}

// Function to return equivalent
// character of a given value
static char reVal(int num)
{
    if (num >= 0 && num <= 9)
        return(char)(num + '0');
    else
        return(char)(num - 10 + 'A');
}

// Function to convert a given
// decimal number to a given base
static String fromDeci(int base, int inputNum)
{

    // Store the result
    String res = "";

    // Repeatedly divide inputNum
    // by base and take remainder
    while (inputNum > 0)
    {

        // Update res
        res += reVal(inputNum % base);

        // Update inputNum
        inputNum /= base;
    }

    // Reverse the result
    res = reverse(res);

    return res;
}

// Function to convert a given number
// from a base to another base
static void convertBase(String s, int a, int b)
{

    // Convert the number from
    // base A to decimal
    int num = toDeci(s, a);

    // Convert the number from
    // decimal to base B
    String ans = fromDeci(b, num);

    // Print the result
    System.out.print(ans);
}

static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{

    // Given input
    String s = "10B";
    int a = 16, b = 10;

    // Function Call
    convertBase(s, a, b);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to return ASCII
# value of a character
def val(c):
    if (c >= '0' and c <= '9'):
        return ord(c) - 48
    else:
        return ord(c) - 65  + 10

# Function to convert a number
# from given base to decimal number
def toDeci(strr, base):

    # Stores the length
    # of the string
    lenn = len(strr)

    # Initialize power of base
    power = 1

    # Initialize result
    num = 0

    # Decimal equivalent is strr[len-1]*1
    # + strr[len-2]*base + strr[len-3]*(base^2) + ...
    for i in range(lenn - 1, -1, -1):
        # A digit in input number must
        # be less than number's base
        if (val(strr[i]) >= base):
            print("Invalid Number")
            return -1

        # Update num
        num += val(strr[i]) * power

        # Update power
        power = power * base

    return num

# Function to return equivalent
# character of a given value
def reVal(num):

    if (num >= 0 and num <= 9):
        return chr(num + 48)
    else:
        return chr(num - 10 + 65)

# Function to convert a given
# decimal number to a given base
def fromDeci(base, inputNum):

    # Store the result
    res = ""

    # Repeatedly divide inputNum
    # by base and take remainder
    while (inputNum > 0):

        # Update res
        res += reVal(inputNum % base)

        # Update inputNum
        inputNum //= base

    # Reverse the result
    res = res[::-1]

    return res

# Function to convert a given number
# from a base to another base
def convertBase(s, a, b):

    # Convert the number from
    # base A to decimal
    num = toDeci(s, a)

    # Convert the number from
    # decimal to base B
    ans = fromDeci(b, num)

    # Print the result
    print(ans)

# Driver Code

# Given input
s = "10B"
a = 16
b = 10

# Function Call
convertBase(s, a, b)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

    // Function to return ASCII
    // value of a character
    static int val(char c)
    {
        if (c >= '0' && c <= '9')
            return(int)c - '0';
        else
            return(int)c - 'A' + 10;
    }

    // Function to convert a number
    // from given basse to decimal number
    static int toDeci(string str, int basse)
    {

        // Stores the length
        // of the string
        int len = str.Length;

        // Initialize power of basse
        int power = 1;

        // Initialize result
        int num = 0;

        // Decimal equivalent is str[len-1]*1
        // + str[len-2]*basse + str[len-3]*(basse^2) + ...
        for(int i = len - 1; i >= 0; i--)
        {

            // A digit in input number must
            // be less than number's basse
            if (val(str[i]) >= basse)
            {
                Console.Write("Invalid Number");
                return -1;
            }

            // Update num
            num += val(str[i]) * power;

            // Update power
            power = power * basse;
        }
        return num;
    }

    // Function to return equivalent
    // character of a given value
    static char reVal(int num)
    {
        if (num >= 0 && num <= 9)
            return(char)(num + '0');
        else
            return(char)(num - 10 + 'A');
    }

    // Function to convert a given
    // decimal number to a given basse
    static string fromDeci(int basse, int inputNum)
    {

        // Store the result
        string res = "";

        // Repeatedly divide inputNum
        // by basse and take remainder
        while (inputNum > 0)
        {

            // Update res
            res += reVal(inputNum % basse);

            // Update inputNum
            inputNum /= basse;
        }

        // Reverse the result
        res = reverse(res);

        return res;
    }

    // Function to convert a given number
    // from a basse to another basse
    static void convertbasse(string s, int a, int b)
    {

        // Convert the number from
        // basse A to decimal
        int num = toDeci(s, a);

        // Convert the number from
        // decimal to basse B
        string ans = fromDeci(b, num);

        // Print the result
        Console.Write(ans);
    }

    static string reverse(string input)
    {
        char[] a = input.ToCharArray();
        int l, r = a.Length - 1;
        for(l = 0; l < r; l++, r--)
        {
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return new string(a);
    }

    // Driver Code
    static public void Main (){
        // Given input
        string s = "10B";
        int a = 16, b = 10;

        // Function Call
        convertbasse(s, a, b);
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to return ASCII
// value of a character
function val(c)
{
    if (c >= '0' && c <= '9')
        return c.charCodeAt(0) - 48;
    else
        return c.charCodeAt(0) - 65 + 10;
}

// Function to convert a number
// from given base to decimal number
function toDeci(str, base)
{

    // Stores the length
    // of the var
    var len = str.length;

    // Initialize power of base
    var power = 1;

    // Initialize result
    var num = 0;

    // Decimal equivalent is str[len-1]*1
    // + str[len-2]*base + str[len-3]*(base^2) + ...
    for (var i = len - 1; i >= 0; i--) {

        // A digit in input number must
        // be less than number's base
        if (val(str[i]) >= base) {
            document.write("Invalid Number");
            return -1;
        }

        // Update num
        num += val(str[i]) * power;

        // Update power
        power = power * base;
    }

    return num;
}

// Function to return equivalent
// character of a given valueString.fromCharCode
function reVal(num)
{
    if (num >= 0 && num <= 9)
        return String.fromCharCode(num + 48);
    else
        return String.fromCharCode(num - 10 + 65);
}

// Function to convert a given
// decimal number to a given base
function fromDeci(base, inputNum)
{

    // Store the result
    var res = "";

    // Repeatedly divide inputNum
    // by base and take remainder
    while (inputNum > 0) {

        // Update res
        res += reVal(inputNum % base);

        // Update inputNum
        inputNum = Math.floor(inputNum/base);
    }

    // Reverse the result
    res = res.split("").reverse().join("");

    return res;
}

// Function to convert a given number
// from a base to another base
function convertBase(s, a, b)
{

    // Convert the number from
    // base A to decimal
    var num = toDeci(s, a);

    // Convert the number from
    // decimal to base B
    var ans = fromDeci(b, num);

    // Prvar the result
    document.write(ans);
}

// Driver Code
// Given input
var s = "10B";
var a = 16
var b = 10;

// Function Call
convertBase(s, a, b);

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
267
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)