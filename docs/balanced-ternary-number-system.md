# 平衡三元数系

> 原文:[https://www . geesforgeks . org/balanced-三元数-系统/](https://www.geeksforgeeks.org/balanced-ternary-number-system/)

我们已经知道，一个 [**二进制数制**](https://www.geeksforgeeks.org/classification-of-number-system/) 是一个只有 2 位数字的数制，即 **0 和 1** 。同样，我们也知道一个 [**三元数制**](https://www.geeksforgeeks.org/ternary-number-system-or-base-3-numbers/) 是一个只有 3 位数字的数制，即 **0、1、2** 。在这篇文章中，我们将学习**平衡三进制数字系统**。
A **平衡三进制数字系统**是由数字 **-1、0 和 1** 组成的数字系统。由于不方便将-1 写成数字，为此我们将进一步使用字母 Z。
**<u>十进制到平衡三进制的转换</u>**
十进制到平衡三进制的转换分两步完成:

1.  将十进制转换为三进制。
2.  使用以下步骤将三元转换为平衡三元系统:
    *   从右向左遍历三进制数，保持 0 和 1 不变
    *   当遇到 2 时，将其改为 Z，并在迭代中的下一个数字上加上+1。
    *   有些数字可能变成+3，然后用 0 替换+3，并在迭代中将+1 添加到下一个数字。
    *   完成此过程，直到转换完所有数字。

**示例:**将 238 <sub>10</sub> 转换为平衡三元，反之亦然

> 首先将 238 <sub>10</sub> 转换为[三进制](https://www.geeksforgeeks.org/ternary-number-system-or-base-3-numbers/)。
> **238<sub>10</sub>= 22211<sub>3</sub>**
> 秒变三元为平衡三元数制:
> 
> *   从**开始从左到右**、**两个 1 被跳过**，因为它在平衡三元中保持不变。
> *   现在转换第一个遇到的 2，z 增加+1 迭代中的下一个数字。于是我们得到 **23Z11** 。
> *   在迭代的下一个数字中，用增量+1 将 3 转换为 0。于是我们得到 **30Z11** 。
> *   在迭代的下一个数字中，用增量+1 将 3 转换为 0。于是我们得到 **100Z11** 。(这里假设 0 出现在最高有效数字之前)
> 
> 最终结果是 **100Z11** 。

**注:-**
该系统还允许表示负数，不需要在数字前加负号。平衡三元系统中的所有负数都以 Z.
**开头，即:**
**1<sub>10</sub>= Z<sub>3</sub>、**
**2<sub>10</sub>= Z1<sub>3</sub>、**
T21】3<sub>10</sub>= Z0<sub>3</sub>、T27

下面是将正小数转换为平衡三元系的程序:

## C++

```
// C++ program to convert positive
// decimals into balanced ternary system

#include <bits/stdc++.h>
using namespace std;

string balancedTernary(int n)
{
    string output = "";
    while (n > 0) {
        int rem = n % 3;
        n = n / 3;
        if (rem == 2) {
            rem = -1;
            n++;
        }
        output = (rem == 0
                      ? '0'
                      : (rem == 1)
                            ? '1'
                            : 'Z')
                 + output;
    }
    return output;
}

// Driver code
int main()
{

    int n = 238;

    cout << "Equivalent Balanced Ternary of "
         << n << " is: "
         << balancedTernary(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert positive
// decimals into balanced ternary system
class GFG{

static String balancedTernary(int n)
{
    String output = "";
    while (n > 0)
    {
        int rem = n % 3;
        n = n / 3;
        if (rem == 2)
        {
            rem = -1;
            n++;
        }
        output = (rem == 0 ? '0' :
                 (rem == 1) ? '1' : 'Z') + output;
    }
    return output;
}

// Driver code
public static void main(String[] args)
{
    int n = 238;

    System.out.print("Equivalent Balanced Ternary of " +
                      n + " is: " + balancedTernary(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to convert positive
# decimals into balanced ternary system
def balancedTernary(n):

    output = ""

    while(n > 0):
        rem = n % 3
        n = n // 3

        if(rem == 2):
            rem = -1
            n += 1

        if(rem == 0):
            output = '0' + output
        else:
            if(rem == 1):
                output = '1' + output
            else:
                output = 'Z' + output

    return output

# Driver Code
n = 238

# Function call
print("Equivalent Balanced Ternary of",
       n , "is:", balancedTernary(n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to convert positive
// decimals into balanced ternary system
using System;
using System.Collections.Generic;
class GFG{

static String balancedTernary(int n)
{
    String output = "";
    while (n > 0)
    {
        int rem = n % 3;
        n = n / 3;
        if (rem == 2)
        {
            rem = -1;
            n++;
        }
        output = (rem == 0 ? '0' :
                 (rem == 1) ? '1' : 'Z') + output;
    }
    return output;
}

// Driver code
public static void Main(String[] args)
{
    int n = 238;

    Console.Write("Equivalent Balanced Ternary of " +
                   n + " is: " + balancedTernary(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to convert positive
// decimals into balanced ternary system

function balancedTernary(n)
{
    var output = "";
    while (n > 0) {
        var rem = n % 3;
        n = parseInt(n / 3);
        if (rem == 2) {
            rem = -1;
            n++;
        }
        output = (rem == 0
                      ? '0'
                      : (rem == 1)
                            ? '1'
                            : 'Z')
                 + output;
    }
    return output;
}

// Driver code
var n = 238;
document.write( "Equivalent Balanced Ternary of "
     + n + " is: "
     + balancedTernary(n));

</script>
```

**Output:** 

```
Equivalent Balanced Ternary of 238 is: 100Z11
```