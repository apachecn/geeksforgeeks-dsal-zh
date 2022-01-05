# 给定为字符串的两个复数相乘

> 原文:[https://www . geeksforgeeks . org/乘法-二-复数-给定-字符串/](https://www.geeksforgeeks.org/multiplication-two-complex-numbers-given-strings/)

给定两个字符串形式的复数。我们的任务是打印这两个复数的乘积。

**示例:**

```
Input : str1 = "1+1i"
        str2 = "1+1i" 
Output : "0+2i"
Here, (1 + i) * (1 + i) = 
1 + i2 + 2 * i = 2i or "0+2i"

Input : str1 = "1+-1i"
        str2 = "1+-1i"
Output : "0+-2i"
Here, (1 - i) * (1 - i) = 
1 + i2 - 2 * i = -2i or "0+-2i"
```

两个复数的乘法可按如下方式进行:
![(a+ib) \times (x+iy)=ax+i^2by+i(bx+ay)=ax-by+i(bx+ay)    ](img/fbd8fcadb783eb26a1303b65e12630ff.png "Rendered by QuickLaTeX.com")

我们只需根据**“+”**和**“I”**符号来分割给定复杂字符串的实部和虚部。我们将两个弦的实部 **a** 和 **b** 分别存储为**x【0】**和**y【0】**，虚部分别存储为**x【1】**和**y【1】**。然后，在将提取的部分转换为整数后，我们根据需要将实部和虚部相乘。然后，我们再次以所需的格式形成返回字符串并返回结果。

## C++

```
// C++ Implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
string complexNumberMultiply(string a, string b)
{
    int i;
    string x1;
    int temp = 1;

    // Traverse both strings, and
    // check for negative numbers
    for (i = 0; i < a.length(); i++)
    {
        if (a[i] == '+')
            break;
        if (a[i] == '-')
        {
            temp = -1;
            continue;
        }
        x1.push_back(a[i]);
    }

    // String to int
    int t1 = stoi(x1) * temp;
    x1.clear();
    temp = 1;
    for (; i < a.length() - 1; i++)
    {
        if (a[i] == '-')
        {
            temp = -1;
            continue;
        }
        x1.push_back(a[i]);
    }
    int t2 = stoi(x1) * temp;
    x1.clear();
    temp = 1;
    for (i = 0; i < b.length(); i++)
    {
        if (b[i] == '+')
            break;
        if (b[i] == '-')
        {
            temp = -1;
            continue;
        }
        x1.push_back(b[i]);
    }
    int t3 = stoi(x1) * temp;
    x1.clear();
    temp = 1;
    for (; i < b.length() - 1; i++)
    {
        if (b[i] == '-')
        {
            temp = -1;
            continue;
        }
        x1.push_back(b[i]);
    }
    int t4 = stoi(x1) * temp;

    // Real Part
    int ans = t1 * t3 - t2 * t4;
    string s;
    s += to_string(ans);
    s += '+';

    // Imaginary part
    ans = t1 * t4 + t2 * t3;
    s += to_string(ans);
    s += 'i';

    // Return the result
    return s;
}

// Driver Code
int main()
{

    string str1 = "1+1i";
    string str2 = "1+1i";
    cout << complexNumberMultiply(str1, str2);

    return 0;

    // Contributed By Bhavneet Singh
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply two complex numbers
// given as strings.
import java.util.*;
import java.lang.*;

public class GfG{
    public static String complexNumberMultiply(String a, String b) {

        // Spiting the real and imaginary parts
        // of the given complex strings based on '+'
        // and 'i' symbols.
        String x[] = a.split("\\+|i");
        String y[] = b.split("\\+|i");

        // Storing the real part of complex string a
        int a_real = Integer.parseInt(x[0]);

        // Storing the imaginary part of complex string a
        int a_img = Integer.parseInt(x[1]);

        // Storing the real part of complex string b
        int b_real = Integer.parseInt(y[0]);

        // Storing the imaginary part of complex string b
        int b_img = Integer.parseInt(y[1]);

        // Returns the product.
        return (a_real * b_real - a_img * b_img) + "+" +
              (a_real * b_img + a_img * b_real) + "i";
    }

    // Driver function
    public static void main(String argc[]){
        String str1 = "1+1i";
        String str2 = "1+1i";
        System.out.println(complexNumberMultiply(str1, str2));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to multiply two complex numbers
# given as strings.
def complexNumberMultiply(a, b):

    # Spiting the real and imaginary parts
    # of the given complex strings based on '+'
    # and 'i' symbols.
    x = a.split('+')
    x[1] = x[1][:-1] # for removing 'i'

    y = b.split("+")
    y[1] = y[1][:-1] # for removing 'i'

    # Storing the real part of complex string a
    a_real = int(x[0])

    # Storing the imaginary part of complex string a
    a_img = int(x[1])

    # Storing the real part of complex string b
    b_real = int(y[0])

    # Storing the imaginary part of complex string b
    b_img = int(y[1])
    return str(a_real * b_real - a_img * b_img) \
        + "+" + str(a_real * b_img + a_img * b_real) + "i";

# Driver function

str1 = "1 + 1i"
str2 = "1 + 1i"
print(complexNumberMultiply(str1, str2))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# program to multiply two complex
// numbers given as strings.
using System;
using System.Text.RegularExpressions;

class GfG{

public static String complexNumberMultiply(String a,
                                           String b)
{

    // Spiting the real and imaginary parts
    // of the given complex strings based on '+'
    // and 'i' symbols.
    String []x = Regex.Split(a, @"\+|i");
    String []y = Regex.Split(b, @"\+|i");

    // Storing the real part of complex string a
    int a_real = Int32.Parse(x[0]);

    // Storing the imaginary part of complex string a
    int a_img = Int32.Parse(x[1]);

    // Storing the real part of complex string b
    int b_real = Int32.Parse(y[0]);

    // Storing the imaginary part of complex string b
    int b_img = Int32.Parse(y[1]);

    // Returns the product.
    return(a_real * b_real - a_img * b_img) + "+" +
          (a_real * b_img + a_img * b_real) + "i";
}

// Driver code
public static void Main(String []argc)
{
    String str1 = "1+1i";
    String str2 = "1+1i";

    Console.WriteLine(complexNumberMultiply(str1, str2));
}
}

// This code is contributed by shikhasingrajput
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to multiply
// two complex numbers
// given as strings.

function complexNumberMultiply($a, $b)
{

// Spiting the real and
// imaginary parts of the
// given complex strings
// based on '+' and 'i' symbols.
$x = preg_split("/[\s+]+|i/" , $a);
$y = preg_split("/[\s+]+|i/" , $b);

// Storing the real part
// of complex string a
$a_real = intval($x[0]);

// Storing the imaginary
// part of complex string a
$a_img = intval($x[1]);

// Storing the real part
// of complex string b
$b_real = intval($y[0]);

// Storing the imaginary
// part of complex string b
$b_img = intval($y[1]);

// Returns the product.
return ($a_real * $b_real -
        $a_img * $b_img) . "+" .
       ($a_real * $b_img +
        $a_img * $b_real) . "i";
}

// Driver Code
$str1 = "1+1i";
$str2 = "1+1i";
echo complexNumberMultiply($str1, $str2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to multiply two complex numbers
// given as strings.

function complexNumberMultiply(a, b) {

    // Spiting the real and imaginary parts
    // of the given complex strings based on '+'
    // and 'i' symbols.
    var x = a.split('+');
    var y = b.split('+');

    // Storing the real part of complex string a
    var a_real = parseInt(x[0]);

    // Storing the imaginary part of complex string a
    var a_img = parseInt(x[1]);

    // Storing the real part of complex string b
    var b_real = parseInt(y[0]);

    // Storing the imaginary part of complex string b
    var b_img = parseInt(y[1]);

    // Returns the product.
    return (a_real * b_real - a_img * b_img) + "+" +
          (a_real * b_img + a_img * b_real) + "i";
}

// Driver function
var str1 = "1+1i";
var str2 = "1+1i";
document.write(complexNumberMultiply(str1, str2));

// This code contributed by shikhasingrajput
</script>
```

**输出:**

```
0+2i
```