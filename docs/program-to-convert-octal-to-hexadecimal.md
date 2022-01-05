# 将八进制转换为十六进制的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-octal-to-十六进制/](https://www.geeksforgeeks.org/program-to-convert-octal-to-hexadecimal/)

给定一个八进制数，任务是将其转换成十六进制数。

**示例:**

```
Input:  47 
Output: 27
Explanation:
Decimal value of 47 is = (7 * 1) + (4 * 8) = 39

Now, convert this number to hexadecimal
39/16 -> quotient = 2, remainder = 7
2/16 ->  quotient = 0, remainder = 2

So, the equivalent hexadecimal number is = 27

Input: 235
Output:  9d
```

**方法:**
一个**八进制数字**或简称 oct 是基数-8 的数字，使用数字 0 到 7。八进制数字可以由二进制数字组成，方法是将连续的二进制数字分成三组(从右边开始)。

一个**十六进制数**是一个以 16 为基数的位置数字系统，使用十六个不同的符号。它可能是字母和数字的组合。它使用从 0 到 9 的数字和从 A 到 f 的字母

**转换步骤:**
最简单的方法就是把八进制数转换成十进制，再把十进制转换成十六进制形式。

1.  在八进制数字旁边从下往上写 8 的幂(1，8，64，512，4096，等等)。
2.  将每个数字乘以它的幂。
3.  把答案加起来。这是十进制解。
4.  十进制数除以 16。
5.  获取下一次迭代的整数商(如果该数不等于 16，则将结果向下舍入到最接近的整数)。
6.  记下余数，余数应该在 0 到 15 之间。
7.  重复步骤 4 中的步骤。直到商等于 0。
8.  从下到上写出所有的余数。
9.  将任何大于 9 的余数转换成十六进制字母。这是十六进制解。

**例如**，如果给定的八进制数是 5123:

<figure class="table">

| 手指 | 力量 | 增加 |
| --- | --- | --- |
| five | Five hundred and twelve | Two thousand five hundred and sixty |
| one | Sixty-four | Sixty-four |
| Two | eight | Sixteen |
| three | one | three |

那么十进制数(2560 + 64 + 16 + 3)就是:2643

<figure class="table">

| 分开 | 商 | 剩余物 |
| --- | --- | --- |
| 2643/16 | One hundred and sixty-five | three |
| 165/16 | Ten | five |
| 10/16 | Zero | 10 (a) |

最后，十六进制数是:a53

下面是上述方法的实现:

## C++

```
// C++ program to convert Octal
// to Hexadecimal
#include<bits/stdc++.h>
using namespace std;

// Function to convert octal to decimal
int octalToDecimal(int n)
{
    int num = n;
    int dec_value = 0;

    // Initializing base value
    // to 1, i.e 8^0
    int base = 1;

    int temp = num;
    while (temp)
    {

        // Extracting last digit
        int last_digit = temp % 10;
        temp = temp / 10;

        // Multiplying last digit with
        // appropriate base value and
        // adding it to dec_value
        dec_value += last_digit * base;

        base = base * 8;
    }
    return dec_value;
}

// Function to convert decimal
// to hexadecimal
string decToHexa(int n)
{

    // char array to store
    // hexadecimal number
    char hexaDeciNum[100];

    // counter for hexadecimal
    // number array
    int i = 0;
    while(n != 0)
    {   

        // Temporary variable to
        // store remainder
        int temp  = 0;

        // Storing remainder in
        // temp variable.
        temp = n % 16;

        // Check if temp < 10
        if (temp < 10)
        {
            hexaDeciNum[i] = temp + 48;
            i++;
        }
        else
        {
            hexaDeciNum[i] = temp + 87;
            i++;
        }
        n = n / 16;
    }

    string ans = "";

    // Printing hexadecimal number array
    // in reverse order
    for(int j = i - 1; j >= 0; j--)
    {
        ans += hexaDeciNum[j];
    }
    return ans;
}

// Driver Code
int main()
{
    string hexnum;
    int decnum, octnum;

    // Taking 5123 as an example of
    // Octal Number.
    octnum = 5123;

    // Convert Octal to Decimal
    decnum = octalToDecimal(octnum);

    // Convert Decimal to Hexadecimal
    hexnum = decToHexa(decnum);

    cout << "Equivalent Hexadecimal Value = "
         << hexnum << endl;
}

// This code is contributed by pratham76
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Convert Octal
// to Hexadecimal

import java.util.Scanner;

public class JavaProgram {
    public static void main(String args[])
    {
        String octnum, hexnum;
        int decnum;
        Scanner scan = new Scanner(System.in);

        // Taking 5123 as an example of
        // Octal Number.
        octnum = "5123";

        // Convert Octal to Decimal
        decnum = Integer.parseInt(octnum, 8);

        // Convert Decimal to Hexadecimal
        hexnum = Integer.toHexString(decnum);

        System.out.print("Equivalent Hexadecimal Value = "
                                                + hexnum);
    }
}
```

## 蟒蛇 3

```
# Python3 program to convert octal
# to hexadecimal

# Taking 5123 as an example of
# octal number
octnum = "5123"

# Convert octal to decimal
decnum = int(octnum, 8)

# Convert decimal to hexadecimal
hexadecimal = hex(decnum).replace("0x", "")

# Printing the hexadecimal value
print("Equivalent Hexadecimal Value =", hexadecimal)

# This code is contributed by virusbuddah_
```

## C#

```
// C# Program to Convert Octal
// to Hexadecimal
using System;
class GFG{

// Function to convert octal
// to decimal
static int octalToDecimal(int n)
{
  int num = n;
  int dec_value = 0;

  // Initializing base value 
  // to 1, i.e 8^0
  int b_ase = 1;

  int temp = num;
  while (temp > 0) 
  {
    // Extracting last digit
    int last_digit = temp % 10;
    temp = temp / 10;

    // Multiplying last digit 
    // with appropriate base 
    // value and adding it to 
    // dec_value
    dec_value += last_digit * b_ase;

    b_ase = b_ase * 8;
  }

  return dec_value;
}

// Function to convert decimal
// to hexadecimal
static string decToHexa(int n)
{ 
  // char array to store 
  // hexadecimal number
  char []hexaDeciNum = new char[100];

  // counter for hexadecimal
  // number array
  int i = 0;
  string ans = "";

  while(n != 0)
  { 
    // temporary variable to 
    // store remainder
    int temp = 0;

    // storing remainder
    // in temp variable.
    temp = n % 16;

    // check if temp < 10
    if(temp < 10)
    {
      hexaDeciNum[i] = (char)(temp + 48);
      i++;
    }
    else
    {
      hexaDeciNum[i] = (char)(temp + 87);
      i++;
    }

    n = n / 16;
  }

  for(int j = i - 1; j >= 0; j--)
  {
    ans += hexaDeciNum[j];
  }

  return ans;
}

// Driver code
public static void Main(string []args)
{
  string octnum, hexnum;
  int decnum;

  // Taking 5123 as an
  // example of Octal Number.
  octnum = "5123";

  // Convert Octal to Decimal
  decnum = octalToDecimal(Int32.Parse(octnum));

  // Convert Decimal to Hexadecimal
  hexnum = decToHexa(decnum);

  Console.Write("Equivalent Hexadecimal Value = " +
                 hexnum);
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
Equivalent Hexadecimal Value = a53
```

</figure>

</figure>