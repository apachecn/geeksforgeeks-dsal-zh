# 将给定的浮点值转换为等效分数

> 原文:[https://www . geesforgeks . org/convert-given-float-value-to-等价物-fraction/](https://www.geeksforgeeks.org/convert-given-float-value-to-equivalent-fraction/)

给定一个形式为[字符串](https://www.geeksforgeeks.org/string-data-structure/) **N** 的[浮点数，任务是将给定的](https://www.geeksforgeeks.org/introduction-of-floating-point-representation/)[浮点数](https://www.geeksforgeeks.org/introduction-of-floating-point-representation/)转换为[分数](https://www.geeksforgeeks.org/program-compare-two-fractions/)。

> 浮点表示法中的**“()”**中的封闭数字序列在十进制表示法中表示递归。
> 例如 **1。(6)** 代表 **1.666。**

**示例:**

> **输入:** N = "1.5"
> **输出:** 3 / 2
> **说明:**
> 3/2 的值将等于 1.5
> 
> **输入:**N =“1”。(6)“
> **输出:** 5 / 3
> **说明:**
> 5/3 的值将等于 1.666…表示为 1。(6).

**方法:**思路是用两个数的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)和一些数学方程来求解。按照以下步骤解决问题:

*   除了循环序列之外，在小数点后要有 **x** 个数字。
*   如果没有循环序列，那么将给定的数字乘以**10<sup>x</sup>T3，让**10<sup>x</sup>T9】的 **GCD** 和结果数为 **g** 。打印结果除以 **g** 作为分子， **10 <sup>x</sup>** 除以 **g** 作为分母。****

> 例如，如果**N =“1.5”**那么 **x = 1** 。
> 将 **N** 乘以 **10** ，结果为 **15** ， **10** ， **15** 的 **GCD** 为 **3** 。
> 因此，打印 **15/3 = 5** 作为分子， **10/5** 作为分母。

*   如果存在重复序列，则将 **N** 乘以**10<sup>x</sup>T5。比如 **N = 23.98(231)** 乘以 **N*(10 <sup>2</sup> )** 。**
*   让序列中的总位数为 **y** 。对于 **10 <sup>2</sup> *N** = **2398。(231)** ， **y** 变为 **3** 。
*   将**10<sup>y</sup>T3 与**N * 10<sup>x</sup>T7 相乘。对于**10<sup>2</sup>* N**=**2398。(231)** ，乘以 **10 <sup>3</sup>** 即**10<sup>2</sup>* N * 10<sup>3</sup>**=**2398231。(231)** 。****
*   现在，用**N * 10<sup>x</sup>T7】减去**N * 10<sup>y+x</sup>T3，结果为 **M** 。上例中，**10<sup>2</sup>* N *(10<sup>3</sup>-1)= 2395833**。****
*   因此，**N = M/((10<sup>x</sup>)*(10<sup>y</sup>–1))**。上例 **N = 2395833 / 999000** 。
*   找到 **M** 和**的**GCD**((10<sup>x</sup>)*(10<sup>y</sup>–1)**，打印 **M / gcd** 作为分子，**((10<sup>x</sup>)*(10<sup>y</sup>–1)**作为分母。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to convert the floating
// values into fraction
void findFraction(string s)
{
    // Initialize variables
    string be_deci = "",
           af_deci = "",
           reccu = "";

    bool x = true, y = false,
         z = false;

    // Traverse the floating string
    for (int i = 0; i < s.size(); ++i) {

        // Check if decimal part exist
        if (s[i] == '.') {
            x = false;
            y = true;
            continue;
        }

        // Check if recurrence
        // sequence exist
        if (s[i] == '(') {
            z = true;
            y = false;
            continue;
        }

        // Retrieve decimal part
        // and recurrence re sequence
        if (x)
            be_deci += s[i];

        if (y)
            af_deci += s[i];

        if (z) {

            // Traverse the string
            for (; i < s.size()
                   && s[i] != ')';
                 ++i)
                reccu += s[i];
            break;
        }
    }

    // Convert string to integer
    int num_be_deci = stoi(be_deci);
    int num_af_deci = 0;

    // If no recurrence sequence exist
    if (af_deci.size() != 0)
        num_af_deci = stoi(af_deci);

    // Initialize numerator & denominator
    int numr = num_be_deci
                   * pow(10, af_deci.size())
               + num_af_deci;

    int deno = pow(10, af_deci.size());

    // No reccuring term
    if (reccu.size() == 0) {
        int gd = __gcd(numr, deno);

        // Print the result
        cout << numr / gd << " / "
             << deno / gd;
    }

    // If reccuring term exist
    else {

        // Convert reccuring term to integer
        int reccu_num = stoi(reccu);

        // reccu.size() is num of
        // digit in reccur term
        int numr1
            = numr
                  * pow(10, reccu.size())
              + reccu_num;

        int deno1 = deno
                    * pow(10, reccu.size());

        // eq 2 - eq 1
        int res_numr = numr1 - numr,
            res_deno = deno1 - deno;

        int gd = __gcd(res_numr,
                       res_deno);

        // Print the result
        cout << res_numr / gd << " / "
             << res_deno / gd;
    }
}

// Driver Code
int main()
{
    // Given string str
    string str = "23.98(231)";

    // Function Call
    findFraction(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive function to return
// gcd of a and b 
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Function to convert the floating
// values into fraction
static void findFraction(String s)
{

    // Initialize variables
    String be_deci = "",
           af_deci = "",
             reccu = "";

    boolean x = true, y = false,
            z = false;

    // Traverse the floating String
    for(int i = 0; i < s.length(); ++i)
    {

        // Check if decimal part exist
        if (s.charAt(i) == '.')
        {
            x = false;
            y = true;
            continue;
        }

        // Check if recurrence
        // sequence exist
        if (s.charAt(i)  == '(')
        {
            z = true;
            y = false;
            continue;
        }

        // Retrieve decimal part
        // and recurrence resquence
        if (x)
            be_deci += s.charAt(i);

        if (y)
            af_deci += s.charAt(i);

        if (z)
        {

            // Traverse the String
            for(; i < s.length() && s.charAt(i) != ')';
                  ++i)
                reccu += s.charAt(i);

            break;
        }
    }

    // Convert String to integer
    int num_be_deci = Integer.valueOf(be_deci);
    int num_af_deci = 0;

    // If no recurrence sequence exist
    if (af_deci.length() != 0)
        num_af_deci = Integer.valueOf(af_deci);

    // Initialize numerator & denominator
    int numr = num_be_deci *
               (int)Math.pow(10, af_deci.length()) +
               num_af_deci;

    int deno = (int)Math.pow(10, af_deci.length());

    // No reccuring term
    if (reccu.length() == 0)
    {
        int gd = __gcd(numr, deno);

        // Print the result
        System.out.print(numr / gd + " / " +
                         deno / gd);
    }

    // If reccuring term exist
    else
    {

        // Convert reccuring term to integer
        int reccu_num = Integer.valueOf(reccu);

        // reccu.size() is num of
        // digit in reccur term
        int numr1 = numr *
                    (int)Math.pow(10, reccu.length()) +
                    reccu_num;

        int deno1 = deno * (int) Math.pow(
                    10, reccu.length());

        // eq 2 - eq 1
        int res_numr = numr1 - numr,
            res_deno = deno1 - deno;

        int gd = __gcd(res_numr,
                       res_deno);

        // Print the result
        System.out.print(res_numr / gd + " / " +
                         res_deno / gd);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String str = "23.98(231)";

    // Function Call
    findFraction(str);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import gcd

# Function to convert the floating
# values into fraction
def findFraction(s):

    # Initialize variables
    be_deci = ""
    af_deci = ""
    reccu = ""

    x = True
    y = False
    z = False

    # Traverse the floating string
    for i in range(len(s)):

        # Check if decimal part exist
        if (s[i] == '.'):
            x = False
            y = True
            continue

        # Check if recurrence
        # sequence exist
        if (s[i] == '('):
            z = True
            y = False
            continue

        # Retrieve decimal part
        # and recurrence resquence
        if (x):
            be_deci += s[i]

        if (y):
            af_deci += s[i]

        if (z):

            # Traverse the string
            while i < len(s) and s[i] != ')':
                reccu += s[i]
                i += 1

            break

    # Convert to integer
    num_be_deci = int(be_deci)
    num_af_deci = 0

    # If no recurrence sequence exist
    if len(af_deci) != 0:
        num_af_deci = int(af_deci)

    # Initialize numerator & denominator
    numr = (num_be_deci *
            pow(10, len(af_deci)) +
            num_af_deci)

    deno = pow(10, len(af_deci))

    # No reccuring term
    if len(reccu) == 0:
        gd = gcd(numr, deno)

        # Print the result
        print(numr // gd, "/", deno // gd)

    # If reccuring term exist
    else:

        # Convert reccuring term to integer
        reccu_num = int(reccu)

        # reccu.size() is num of
        # digit in reccur term
        numr1 = (numr * pow(10, len(reccu)) +
                 reccu_num)

        deno1 = deno * pow(10, len(reccu))

        # eq 2 - eq 1
        res_numr = numr1 - numr
        res_deno = deno1 - deno

        gd = gcd(res_numr, res_deno)

        # Print the result
        print(res_numr // gd, " / ",
              res_deno // gd)

# Driver Code
if __name__ == '__main__':

    # Given str
    str = "23.98(231)"

    # Function Call
    findFraction(str)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to return
// gcd of a and b 
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Function to convert the floating
// values into fraction
static void findFraction(String s)
{

    // Initialize variables
    String be_deci = "",
           af_deci = "",
             reccu = "";

    bool x = true, y = false,
                   z = false;

    // Traverse the floating String
    for(int i = 0; i < s.Length; ++i)
    {

        // Check if decimal part exist
        if (s[i] == '.')
        {
            x = false;
            y = true;
            continue;
        }

        // Check if recurrence
        // sequence exist
        if (s[i]  == '(')
        {
            z = true;
            y = false;
            continue;
        }

        // Retrieve decimal part
        // and recurrence resquence
        if (x)
            be_deci += s[i];

        if (y)
            af_deci += s[i];

        if (z)
        {

            // Traverse the String
            for(; i < s.Length && s[i] != ')';
                  ++i)
                reccu += s[i];

            break;
        }
    }

    // Convert String to integer
    int num_be_deci = Int32.Parse(be_deci);
    int num_af_deci = 0;

    // If no recurrence sequence exist
    if (af_deci.Length != 0)
        num_af_deci = Int32.Parse(af_deci);

    // Initialize numerator & denominator
    int numr = num_be_deci *
               (int)Math.Pow(10, af_deci.Length) +
               num_af_deci;

    int deno = (int)Math.Pow(10, af_deci.Length);

    // No reccuring term
    if (reccu.Length == 0)
    {
        int gd = __gcd(numr, deno);

        // Print the result
        Console.Write(numr / gd + " / " +
                      deno / gd);
    }

    // If reccuring term exist
    else
    {

        // Convert reccuring term to integer
        int reccu_num = Int32.Parse(reccu);

        // reccu.Count is num of
        // digit in reccur term
        int numr1 = numr *
                    (int)Math.Pow(10, reccu.Length) +
                    reccu_num;

        int deno1 = deno * (int)Math.Pow(
                    10, reccu.Length);

        // eq 2 - eq 1
        int res_numr = numr1 - numr,
            res_deno = deno1 - deno;

        int gd = __gcd(res_numr,
                       res_deno);

        // Print the result
        Console.Write(res_numr / gd + " / " +
                      res_deno / gd);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "23.98(231)";

    // Function Call
    findFraction(str);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Recursive function to return
// gcd of a and b
function __gcd(a,b)
{
    return b == 0 ? a : __gcd(b, a % b);  
}

// Function to convert the floating
// values into fraction
function findFraction(s)
{

    // Initialize variables
    let be_deci = "",
        af_deci = "",
          reccu = "";

    let x = true, y = false,
        z = false;

    // Traverse the floating String
    for(let i = 0; i < s.length; ++i)
    {

        // Check if decimal part exist
        if (s[i] == '.')
        {
            x = false;
            y = true;
            continue;
        }

        // Check if recurrence
        // sequence exist
        if (s[i]  == '(')
        {
            z = true;
            y = false;
            continue;
        }

        // Retrieve decimal part
        // and recurrence resquence
        if (x)
            be_deci += s[i];

        if (y)
            af_deci += s[i];

        if (z)
        {

            // Traverse the String
            for(; i < s.length && s[i] != ')'; ++i)
                reccu += s[i];

            break;
        }
    }

    // Convert String to integer
    let num_be_deci = parseInt(be_deci);
    let num_af_deci = 0;

    // If no recurrence sequence exist
    if (af_deci.length != 0)
        num_af_deci = parseInt(af_deci);

    // Initialize numerator & denominator
    let numr = num_be_deci *
               Math.pow(10, af_deci.length) +
               num_af_deci;

    let deno = Math.pow(10, af_deci.length);

    // No reccuring term
    if (reccu.length == 0)
    {
        let gd = __gcd(numr, deno);

        // Print the result
        document.write(numr / gd + " / " +
                       deno / gd);
    }

    // If reccuring term exist
    else
    {

        // Convert reccuring term to integer
        let reccu_num = parseInt(reccu);

        // reccu.size() is num of
        // digit in reccur term
        let numr1 = numr *
                    Math.pow(10, reccu.length) +
                    reccu_num;

        let deno1 = deno *  Math.pow(
                    10, reccu.length);

        // eq 2 - eq 1
        let res_numr = numr1 - numr,
            res_deno = deno1 - deno;

        let gd = __gcd(res_numr,
                       res_deno);

        // Print the result
        document.write(res_numr / gd + " / " +
                       res_deno / gd);
    }
}

// Driver Code

// Given String str
let str = "23.98(231)";

// Function Call
findFraction(str);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
798611 / 33300
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*