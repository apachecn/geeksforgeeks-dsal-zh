# 将给定二进制转换为其等效 ASCII 字符串的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-给定二进制到其等效 ascii 字符串/](https://www.geeksforgeeks.org/program-to-convert-given-binary-to-its-equivalent-ascii-character-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是找到它的等价 ASCII 字符串。

**示例:**

> **输入:**str = " 0110000101100010 "
> **输出:** ab
> **解释:**将 str 分成一组 8 位，如下所示:
> 
> *   01100001 = 97，ASCII 值 97 为' a '。
> *   01100010 = 98，ASCII 值 98 为' b '。
> 
> 因此，所需的 ASCII 字符串是“ab”。
> 
> **输入:** str = "10000101100"
> **输出:**不可能
> **解释:**给定的二进制字符串不是有效字符串，因为字符数不是 8 的倍数。

**方法:**这个问题是基于实现的问题。按照以下步骤解决给定的问题。

*   首先，检查 s 是否能被 **8** 整除
    *   如果不能被 **8** 整除，打印**“不可能”**
    *   否则，进入下一步
*   声明一个空的[字符串](https://www.geeksforgeeks.org/string-data-structure/)来存储所有的 ASCII 字符串。
*   遍历 **s** 中的一跳 **8** 字符，在每一步中找到当前 8 位组的[十进制等值](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)。
*   将十进制值转换为等效的 [ASCII 字符](https://www.geeksforgeeks.org/program-print-ascii-value-character/)，并将其附加到 **res** 字符串中。
*   返回**静止**弦。

下面是上述方法的实现:

## C++14

```
// C++ implementation for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert binary to decimal
int binaryToDecimal(string n)
{
    string num = n;

    // Stores the decimal value
    int dec_value = 0;

    // Initializing base value to 1
    int base = 1;

    int len = num.length();
    for (int i = len - 1; i >= 0; i--) {

        // If the current bit is 1
        if (num[i] == '1')
            dec_value += base;
        base = base * 2;
    }

    // Return answer
    return dec_value;
}

// Function to convert binary to ASCII
string setStringtoASCII(string str)
{
    // To store size of s
    int N = int(str.size());

    // If given string is not a
    // valid string
    if (N % 8 != 0) {
        return "Not Possible!";
    }

    // To store final answer
    string res = "";

    // Loop to iterate through string
    for (int i = 0; i < N; i += 8) {
        int decimal_value
            = binaryToDecimal((str.substr(i, 8)));

        // Apprend the ASCII character
        // equivalent to current value
        res += char(decimal_value);
    }

    // Return Answer
    return res;
}

// Driver Code
int main()
{
    string s = "0110000101100010";
    cout << setStringtoASCII(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
import java.util.*;

class GFG
{

// Function to convert binary to decimal
static int binaryToDecimal(String n)
{
    String num = n;

    // Stores the decimal value
    int dec_value = 0;

    // Initializing base value to 1
    int base = 1;

    int len = num.length();
    for (int i = len - 1; i >= 0; i--) {

        // If the current bit is 1
        if (num.charAt(i) == '1')
            dec_value += base;
        base = base * 2;
    }

    // Return answer
    return dec_value;
}

// Function to convert binary to ASCII
static String setStringtoASCII(String str)
{

    // To store size of s
    int N = (str.length());

    // If given String is not a
    // valid String
    if (N % 8 != 0) {
        return "Not Possible!";
    }

    // To store final answer
    String res = "";

    // Loop to iterate through String
    for (int i = 0; i < N; i += 8) {
        int decimal_value
            = binaryToDecimal((str.substring(i, 8+i)));

        // Apprend the ASCII character
        // equivalent to current value
        res += (char)(decimal_value);
    }

    // Return Answer
    return res;
}

// Driver Code
public static void main(String[] args)
{
    String s = "0110000101100010";
    System.out.print(setStringtoASCII(s));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python implementation for above approach

# Function to convert binary to decimal
def binaryToDecimal(n):
    num = n

    # Stores the decimal value
    dec_value = 0

    # Initializing base value to 1
    base = 1

    le = len(num)
    for i in range(le - 1, -1, -1):

        # If the current bit is 1
        if (num[i] == '1'):
            dec_value += base
        base = base * 2

    # Return answer
    return dec_value

# Function to convert binary to ASCII
def setStringtoASCII(str):

    # To store size of s
    N = int(len(str))

    # If given string is not a
    # valid string
    if (N % 8 != 0):
        return "Not Possible!"

        # To store final answer
    res = ""

    # Loop to iterate through string
    for i in range(0, N, 8):
        decimal_value = binaryToDecimal(str[i: i + 8])

        # Apprend the ASCII character
        # equivalent to current value
        res += chr(decimal_value)

        # Return Answer
    return res

# Driver Code
if __name__ == "__main__":

    s = "0110000101100010"
    print(setStringtoASCII(s))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for above approach
using System;

class GFG {

    // Function to convert binary to decimal
    static int binaryToDecimal(string n)
    {
        string num = n;

        // Stores the decimal value
        int dec_value = 0;

        // Initializing base value to 1
        int base1 = 1;

        int len = num.Length;
        for (int i = len - 1; i >= 0; i--) {

            // If the current bit is 1
            if (num[i] == '1')
                dec_value += base1;
            base1 = base1 * 2;
        }

        // Return answer
        return dec_value;
    }

    // Function to convert binary to ASCII
    static string setStringtoASCII(string str)
    {

        // To store size of s
        int N = (str.Length);

        // If given String is not a
        // valid String
        if (N % 8 != 0) {
            return "Not Possible!";
        }

        // To store final answer
        string res = "";

        // Loop to iterate through String
        for (int i = 0; i < N; i += 8) {
            int decimal_value
                = binaryToDecimal((str.Substring(i, 8)));

            // Apprend the ASCII character
            // equivalent to current value
            res += (char)(decimal_value);
        }

        // Return Answer
        return res;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string s = "0110000101100010";
        Console.WriteLine(setStringtoASCII(s));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript implementation for above approach

// Function to convert binary to decimal
function binaryToDecimal(n)
{
    let num = n;

    // Stores the decimal value
    let dec_value = 0;

    // Initializing base value to 1
    let base = 1;

    let len = n.length;
    for(let i = len - 1; i >= 0; i--)
    {

        // If the current bit is 1
        if (n[i] == '1')
            dec_value += base;

        base = base * 2;
    }

    // Return answer
    return dec_value;
}

// Function to convert binary to ASCII
function setStringtoASCII(str)
{

    // To store size of s
    let N = str.length;

    // If given string is not a
    // valid string
    if (N % 8 != 0)
    {
        return "Not Possible!";
    }

    // To store final answer
    let res = "";

    // Loop to iterate through string
    for(let i = 0; i < N; i = i + 8)
    {
        let decimal_value = binaryToDecimal(
            (str.slice(i, i + 8)));

        // Apprend the ASCII character
        // equivalent to current value
        res = res + String.fromCharCode(decimal_value);
    }

    // Return Answer
    return res;
}

// Driver Code
let s = "0110000101100010";
document.write(setStringtoASCII(s));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
ab
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)