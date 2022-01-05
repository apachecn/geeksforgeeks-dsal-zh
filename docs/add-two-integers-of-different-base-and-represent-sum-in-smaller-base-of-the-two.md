# 将两个不同基数的整数相加，表示两个

较小基数的和

> 原文:[https://www . geeksforgeeks . org/add-两个不同基数的整数并表示两个较小基数的总和/](https://www.geeksforgeeks.org/add-two-integers-of-different-base-and-represent-sum-in-smaller-base-of-the-two/)

给定两个整数 **X** 、 **Y** 分别在基地 **B1** 和 **B2** ，任务是求整数 **X** 和 **Y** 的和，表示( **B1** 和 **B2** 的分钟结果。

**示例:**

> **输入:** X = 123，Y = 234，B1 = 6，B2 = 8
> **输出:** 543
> **说明:**
> 基数为 10 的整数:51 和 156
> 整数之和:207
> 最小基数:6
> 基数为 6 的整数之和= 543
> 
> **输入:** X = 16，Y = 24，B1 = 9，B2 = 7
> **输出:** 45
> **解释:**
> 最小基数:7
> 基数中的整数 7: 21 和 24
> 基数 6 中的整数之和–
> 2 1
> +2 4
> ––—
> 4

**方法 1:** 思路是利用[基数转换](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)将**基数 10** (小数)中的两个整数进行转换，然后求出两个数的**和**。然后使用[基数转换](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)将**和**转换成较小的基数 **B** (最小的 **B1** 和 **B2** )。

下面是上述方法的实现:

## C++

```
// Program to find the
// sum of two integers of
// different bases.
#include <bits/stdc++.h>
using namespace std;

int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

int convert(string num, int base)
{
    int len = (num.size());

    // Initialize power of base
    int power = 1;

    // Initialize result
    int res = 0;
    int i;

    // Decimal equivalent is str[len-1]*1 +
    // str[len-2]*base + str[len-3]*(base^2) + ...
    for(i = len - 1; i >= 0; i--)
    {
        res += val(num[i]) * power;
        power = power * base;
    }
    return res;
}

int dec_to_base(int num, int base)
{

    // Maximum base - 36
    string base_num = "";

    while (num > 0)
    {
        int dig = int(num % base);

        if (dig < 10)
            base_num += to_string(dig);
        else
            base_num += to_string('A' + dig - 10);

        num /= base;
    }

    // To reverse the string
    reverse(base_num.begin(),
            base_num.end());
    return stoi(base_num);
}

// Driver Code
int main()
{
    string a = "123";
    string b = "234";

    int base_a = 6;
    int base_b = 8;

    // Integer in base 10
    int a10 = convert(a, base_a);
    int b10 = convert(b, base_b);

    // Sum of integers
    int summ = a10 + b10;

    // uncomment to check
    // intermediate value
    // of a and b to base 10
    // print(a10, b10)

    // Minimum Base
    int min_base = min(base_a, base_b);

    // Sum of integers in Min Base
    cout << (dec_to_base(summ, min_base));
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// sum of two integers of
// different bases.
import java.util.*;
class GFG {

    static int val(char c)
    {
        if (c >= '0' && c <= '9')
            return (int)c - '0';
        else
            return (int)c - 'A' + 10;
    }

    static int convert(String num, int bases)
    {
        int len = (num.length());

        // Initialize power of base
        int power = 1;

        // Initialize result
        int res = 0;
        int i;

        // Decimal equivalent is str[len-1]*1 +
        // str[len-2]*base + str[len-3]*(base^2) + ...
        for (i = len - 1; i >= 0; i--) {
            res += val(num.charAt(i)) * power;
            power = power * bases;
        }
        return res;
    }

    static void dec_to_base(int num, int bases)
    {

        // Maximum base - 36
        // String base_num = "";
        StringBuilder base_num = new StringBuilder();

        while (num > 0) {
            int dig = (num % bases);
            if (dig < 10)
                base_num.append(String.valueOf(dig));
            else
                base_num.append(
                    String.valueOf(('A' + dig - 10)));
            num /= bases;
        }

        // print ans in reverse order
        for (int i = base_num.length() - 1; i >= 0; i--)
            System.out.print(base_num.charAt(i));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String a = "123";
        String b = "234";

        int base_a = 6;
        int base_b = 8;

        // Integer in base 10
        int a10 = convert(a, base_a);
        int b10 = convert(b, base_b);

        // Sum of integers
        int summ = a10 + b10;

        // uncomment to check
        // intermediate value
        // of a and b to base 10
        // print(a10, b10)

        // Minimum Base
        int min_base = Math.min(base_a, base_b);

        // Sum of integers in Min Base
        dec_to_base(summ, min_base);
    }
}

// This code is contributed by ukasp.
```

## 计算机编程语言

```
# Program to find the
# sum of two integers of
# different bases.

# Base conversion
def dec_to_base(num, base):

    # Maximum base - 36
    base_num = ""
    while num > 0:
        dig = int(num % base)
        if dig < 10:
            base_num += str(dig)
        else:
            # Using uppercase letters
            base_num += chr(ord('A')
                            + dig - 10 ) 
        num //= base
    # To reverse the string
    base_num = base_num[::-1]
    return int(base_num)

# Driver Code 
a = '123'
b = '234'
base_a = 6
base_b = 8

# Integer in base 10
a10 = int(a, base_a)
b10 = int(b, base_b)

# Sum of integers
summ = a10 + b10;

# uncomment to check
# intermediate value
# of a and b to base 10
# print(a10, b10)

# Minimum Base
min_base = min(base_a, base_b)

# Sum of integers in Min Base
print(dec_to_base(summ, min_base))
```

## C#

```
// C# Program to find the
// sum of two integers of
// different bases.
using System.Collections.Generic;
using System;
using System.Linq;
using System.Text;
class GFG
{

static int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

static int convert(string num,int bases)
{                                 
    int len = (num.Length);

    // Initialize power of base
    int power = 1;

    // Initialize result
    int res = 0;
    int i;

    // Decimal equivalent is str[len-1]*1 +
    // str[len-2]*base + str[len-3]*(base^2) + ...
    for(i = len - 1; i >= 0; i--)
    {
        res += val(num[i]) * power;
        power = power * bases;
    }
    return res;
}

static void dec_to_base(int num, int bases)
{

    // Maximum base - 36
    // String base_num = "";
    var base_num     = new StringBuilder();

    while (num > 0)
    {
        int dig = (num % bases);     
        if (dig < 10)
            base_num .Append(dig.ToString());
        else
            base_num .Append( ('A' + dig - 10).ToString());          
        num /= bases;
    }

    // print ans in reverse order
    for(int i = base_num.Length - 1; i >= 0; i--)
          Console.Write(base_num[i]);
}

// Driver Code
public static void Main(String[] args)
{
    String a = "123";
    String b = "234";

    int base_a = 6;
    int base_b = 8;

    // Integer in base 10
    int a10 = convert(a, base_a);
    int b10 = convert(b, base_b);

    // Sum of integers
    int summ = a10 + b10;

    // uncomment to check
    // intermediate value
    // of a and b to base 10
    // print(a10, b10)

    // Minimum Base
    int min_base = Math.Min(base_a, base_b);

    // Sum of integers in Min Base
    dec_to_base(summ, min_base);
}
}

// This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>
// Javascript Program to find the
// sum of two integers of
// different bases.
function val(c)
{
    if (c >= '0' && c <= '9')
            return c.charCodeAt(0) - '0'.charCodeAt(0);
        else
            return c.charCodeAt(0) - 'A'.charCodeAt(0) + 10;
}

function convert(num,bases)
{
    let len = (num.length);

        // Initialize power of base
        let power = 1;

        // Initialize result
        let res = 0;
        let i;

        // Decimal equivalent is str[len-1]*1 +
        // str[len-2]*base + str[len-3]*(base^2) + ...
        for (i = len - 1; i >= 0; i--) {
            res += val(num[i]) * power;
            power = power * bases;
        }
        return res;
}

function dec_to_base(num,bases)
{

    // Maximum base - 36
        // String base_num = "";
        let base_num = [];
        while (num > 0) {
            let dig = (num % bases);
            if (dig < 10)
                base_num.push((dig).toString());
            else
                base_num.append(
                    ('A'.charCodeAt(0) + dig - 10).toString());
            num = Math.floor(num/bases);
        }

        // print ans in reverse order
        for (let i = base_num.length - 1; i >= 0; i--)
            document.write(base_num[i]);
}

    // Driver Code
        let a = "123";
        let b = "234";

        let base_a = 6;
        let base_b = 8;

        // Integer in base 10
        let a10 = convert(a, base_a);
        let b10 = convert(b, base_b);

        // Sum of integers
        let summ = a10 + b10;

        // uncomment to check
        // intermediate value
        // of a and b to base 10
        // print(a10, b10)

        // Minimum Base
        let min_base = Math.min(base_a, base_b);

        // Sum of integers in Min Base
        dec_to_base(summ, min_base);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
543
```

**方法 2:** 我们可以减少之前方法的转换次数。这里我们需要找到基数较小的 **B** (最小的 **B1** 和 **B2** ，然后将基数较大的整数转换成基数较小的 **B** ，并借助于给定基数的两个整数[相加得到整数。](https://www.geeksforgeeks.org/program-to-add-two-integers-of-given-base/)

下面是上述方法的实现:

## 蟒蛇 3

```
# Program to find the
# sum of two integers of
# different bases.

# Base conversion
def dec_to_base(num, base):
    # Maximum base - 36
    base_num = ""
    while num > 0:
        dig = int(num % base)
        if dig < 10:
            base_num += str(dig)
        else:
            # Using uppercase letters
            base_num += chr(ord('A') + dig - 10)
        num //= base
    # To reverse the string
    base_num = base_num[::-1]
    return int(base_num)

# Function to find the sum of
# two integers of base B
def sumBase(a, b, base):
    len_a = len(a)
    len_b = len(b)

    s = ""
    sum = ""

    diff = abs(len_a - len_b)

    # Padding 0 in front of the
    # number to make both numbers equal
    for i in range(1, diff + 1):
        s += "0"

    # Condition to check if the strings
    # have lengths mis-match
    if (len_a < len_b):
        a = s + a
    else:
        b = s + b

    carry = 0

    # Loop to find the find the sum
    # of two integers of base B
    for i in range(max(len_a, len_b) - 1, -1, -1):

        # Current Place value for
        # the resultant sum
        curr = carry + (ord(a[i]) - ord('0'))\
               + (ord(b[i]) - ord('0'))

        # Update carry
        carry = curr // base

        # Find current digit
        curr = curr % base

        # Update sum result
        sum = chr(curr + ord('0')) + sum

    if (carry > 0):
        sum = chr(carry + ord('0')) + sum
    return sum

# Driver Code
a = '123'
b = '234'
base_a = 6
base_b = 8

# Convert the integer with
# large base to smaller base B
if base_a > base_b:
    min_Base = base_b
    a10 = int(a, base_a)
    a = dec_to_base(a10, base_b)
else:
    min_Base = base_a
    b10 = int(b, base_b)
    b = dec_to_base(b10, base_a)

# Sum of Integer in min_Base
sum = sumBase(str(a), str(b), min_Base)
print(sum)
```

**Output:** 

```
543
```