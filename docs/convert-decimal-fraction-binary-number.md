# 将十进制分数转换为二进制数

> 原文:[https://www . geesforgeks . org/convert-十进制-分数-二进制-数字/](https://www.geeksforgeeks.org/convert-decimal-fraction-binary-number/)

给定分数十进制数 n 和整数 k，将十进制数 n 转换为小数点后精度高达 k 的等价二进制数。
**例:**

```
Input: n = 2.47, k = 5
Output: 10.01111

Input: n = 6.986 k = 8
Output: 110.11111100
```

We strongly recommend that you click here and practice it, before moving on to the solution.

**A)将十进制的整数部分转换为二进制等价形式**

1.  将十进制数除以 2，并将余数存储在数组中。
2.  将商除以 2。
3.  重复步骤 2，直到商等于零。
4.  等效的二进制数将与步骤 1 的所有余数相反。

**B)将十进制的小数部分转换为二进制等价形式**

1.  小数乘以 2。
2.  所得十进制数的整数部分将是分数二进制数的第一位。
3.  仅使用小数的小数部分重复步骤 1，然后重复步骤 2。

**C)结合二进制数的整数部分和小数部分。**
**插图**

```
Let's take an example for n = 4.47 k = 3

Step 1: Conversion of 4 to binary
1\. 4/2 : Remainder = 0 : Quotient = 2
2\. 2/2 : Remainder = 0 : Quotient = 1
3\. 1/2 : Remainder = 1 : Quotient = 0

*So equivalent binary of integral part of decimal is 100.*

Step 2: Conversion of .47 to binary
1\. 0.47 * 2 = 0.94, Integral part: 0
2\. 0.94 * 2 = 1.88, Integral part: 1
3\. 0.88 * 2 = 1.76, Integral part: 1

*So equivalent binary of fractional part of decimal is .011*

Step 3: Combined the result of step 1 and 2.

Final answer can be written as:
100 + .011 = 100.011
```

程序演示上述步骤:

## C++

```
// C++ program to convert fractional decimal
// to binary number
#include<bits/stdc++.h>
using namespace std;

// Function to convert decimal to binary upto
// k-precision after decimal point
string decimalToBinary(double num, int k_prec)
{
    string binary = "";

    // Fetch the integral part of decimal number
    int Integral = num;

    // Fetch the fractional part decimal number
    double fractional = num - Integral;

    // Conversion of integral part to
    // binary equivalent
    while (Integral)
    {
        int rem = Integral % 2;

        // Append 0 in binary
        binary.push_back(rem +'0');

        Integral /= 2;
    }

    // Reverse string to get original binary
    // equivalent
    reverse(binary.begin(),binary.end());

    // Append point before conversion of
    // fractional part
    binary.push_back('.');

    // Conversion of fractional part to
    // binary equivalent
    while (k_prec--)
    {
        // Find next bit in fraction
        fractional *= 2;
        int fract_bit = fractional;

        if (fract_bit == 1)
        {
            fractional -= fract_bit;
            binary.push_back(1 + '0');
        }
        else
            binary.push_back(0 + '0');
    }

    return binary;
}

// Driver code
int main()
{

    double n = 4.47;
    int k = 3;
    cout << decimalToBinary(n, k) << "\n";

    n = 6.986 , k = 5;
    cout << decimalToBinary(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert fractional decimal
// to binary number
import java.util.*;

class GFG
{

    // Function to convert decimal to binary upto
    // k-precision after decimal point
    static String decimalToBinary(double num, int k_prec)
    {
        String binary = "";

        // Fetch the integral part of decimal number
        int Integral = (int) num;

        // Fetch the fractional part decimal number
        double fractional = num - Integral;

        // Conversion of integral part to
        // binary equivalent
        while (Integral > 0)
        {
            int rem = Integral % 2;

            // Append 0 in binary
            binary += ((char)(rem + '0'));

            Integral /= 2;
        }

        // Reverse string to get original binary
        // equivalent
        binary = reverse(binary);

        // Append point before conversion of
        // fractional part
        binary += ('.');

        // Conversion of fractional part to
        // binary equivalent
        while (k_prec-- > 0)
        {
            // Find next bit in fraction
            fractional *= 2;
            int fract_bit = (int) fractional;

            if (fract_bit == 1)
            {
                fractional -= fract_bit;
                binary += (char)(1 + '0');
            }
            else
            {
                binary += (char)(0 + '0');
            }
        }

        return binary;
    }

    static String reverse(String input)
    {
        char[] temparray = input.toCharArray();
        int left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.valueOf(temparray);
    }

    // Driver code
    public static void main(String[] args)
    {
        double n = 4.47;
        int k = 3;
        System.out.println(decimalToBinary(n, k));

        n = 6.986;
        k = 5;
        System.out.println(decimalToBinary(n, k));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to convert fractional
# decimal to binary number

# Function to convert decimal to binary
# upto k-precision after decimal point
def decimalToBinary(num, k_prec) :

    binary = ""

    # Fetch the integral part of
    # decimal number
    Integral = int(num)

    # Fetch the fractional part
    # decimal number
    fractional = num - Integral

    # Conversion of integral part to
    # binary equivalent
    while (Integral) :

        rem = Integral % 2

        # Append 0 in binary
        binary += str(rem);

        Integral //= 2

    # Reverse string to get original
    # binary equivalent
    binary = binary[ : : -1]

    # Append point before conversion
    # of fractional part
    binary += '.'

    # Conversion of fractional part
    # to binary equivalent
    while (k_prec) :

        # Find next bit in fraction
        fractional *= 2
        fract_bit = int(fractional)

        if (fract_bit == 1) :

            fractional -= fract_bit
            binary += '1'

        else :
            binary += '0'

        k_prec -= 1

    return binary

# Driver code
if __name__ == "__main__" :

    n = 4.47
    k = 3
    print(decimalToBinary(n, k))

    n = 6.986
    k = 5
    print(decimalToBinary(n, k))

# This code is contributed by Ryuga
```

## C#

```
// C# program to convert fractional decimal
// to binary number
using System;

class GFG
{

    // Function to convert decimal to binary upto
    // k-precision after decimal point
    static String decimalToBinary(double num, int k_prec)
    {
        String binary = "";

        // Fetch the integral part of decimal number
        int Integral = (int) num;

        // Fetch the fractional part decimal number
        double fractional = num - Integral;

        // Conversion of integral part to
        // binary equivalent
        while (Integral > 0)
        {
            int rem = Integral % 2;

            // Append 0 in binary
            binary += ((char)(rem + '0'));

            Integral /= 2;
        }

        // Reverse string to get original binary
        // equivalent
        binary = reverse(binary);

        // Append point before conversion of
        // fractional part
        binary += ('.');

        // Conversion of fractional part to
        // binary equivalent
        while (k_prec-- > 0)
        {
            // Find next bit in fraction
            fractional *= 2;
            int fract_bit = (int) fractional;

            if (fract_bit == 1)
            {
                fractional -= fract_bit;
                binary += (char)(1 + '0');
            }
            else
            {
                binary += (char)(0 + '0');
            }
        }

        return binary;
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver code
    public static void Main(String[] args)
    {
        double n = 4.47;
        int k = 3;
        Console.WriteLine(decimalToBinary(n, k));

        n = 6.986;
        k = 5;
        Console.WriteLine(decimalToBinary(n, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert fractional decimal
// to binary number

// Function to convert decimal to binary upto
// k-precision after decimal point
function decimalToBinary($num, $k_prec)
{
    $binary = "";

    // Fetch the integral part of decimal number
    $Integral = (int)($num);

    // Fetch the fractional part decimal number
    $fractional = $num - $Integral;

    // Conversion of integral part to
    // binary equivalent
    while ($Integral)
    {
        $rem = $Integral % 2;

        // Append 0 in binary
        $binary.=chr($rem + 48 );

        $Integral = (int)($Integral/2);
    }

    // Reverse string to get original binary
    // equivalent
    $binary=strrev($binary);

    // Append point before conversion of
    // fractional part
    $binary.='.';

    // Conversion of fractional part to
    // binary equivalent
    while ($k_prec--)
    {
        // Find next bit in fraction
        $fractional *= 2;
        $fract_bit = (int)$fractional;

        if ($fract_bit == 1)
        {
            $fractional -= $fract_bit;
            $binary.=chr(1 + 48 );
        }
        else
            $binary.=chr(0 + 48 );
    }

    return $binary;
}

// Driver code

    $n = 4.47;
    $k = 3;
    echo decimalToBinary($n, $k)."\n";

    $n = 6.986;
    $k = 5;
    echo decimalToBinary($n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript program to convert fractional
    // decimal to binary number

    // Function to convert decimal to binary upto
    // k-precision after decimal point
    function decimalToBinary(num, k_prec)
    {
        let binary = "";

        // Fetch the integral part of decimal number
        let Integral = parseInt(num, 10);

        // Fetch the fractional part decimal number
        let fractional = num - Integral;

        // Conversion of integral part to
        // binary equivalent
        while (Integral > 0)
        {
            let rem = Integral % 2;

            // Append 0 in binary
            binary +=
            (String.fromCharCode(rem + '0'.charCodeAt()));

            Integral = parseInt(Integral / 2, 10);
        }

        // Reverse string to get original binary
        // equivalent
        binary = reverse(binary);

        // Append point before conversion of
        // fractional part
        binary += ('.');

        // Conversion of fractional part to
        // binary equivalent
        while (k_prec-- > 0)
        {
            // Find next bit in fraction
            fractional *= 2;
            let fract_bit = parseInt(fractional, 10);

            if (fract_bit == 1)
            {
                fractional -= fract_bit;
                binary +=
                String.fromCharCode(1 + '0'.charCodeAt());
            }
            else
            {
                binary +=
                String.fromCharCode(0 + '0'.charCodeAt());
            }
        }

        return binary;
    }

    function reverse(input)
    {
        let temparray = input.split('');
        let left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            let temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return temparray.join("");
    }

    let n = 4.47;
    let k = 3;
    document.write(decimalToBinary(n, k) + "</br>");

    n = 6.986;
    k = 5;
    document.write(decimalToBinary(n, k));

</script>
```

**输出:**

```
100.011
110.11111
```

**时间复杂度:** O(len(n))
**辅助空间:** O(len(n))
其中 len()是数字 n 中包含的总位数。
[将二进制分数转换为十进制](https://www.geeksforgeeks.org/convert-binary-fraction-decimal/)
**参考:**
[http://cs . Furman . edu/digital domain/more/ch6/dec _ frac _ to _ bin . htm](http://cs.furman.edu/digitaldomain/more/ch6/dec_frac_to_bin.htm)
[http://www .如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](http://www.cquestions.com/2011/07/c-program-for-fractional-decimal-to.html)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。