# 将实数(0 到 1 之间)转换为二进制字符串

> 原文:[https://www . geeksforgeeks . org/将 0 到 1 之间的实数转换为二进制字符串/](https://www.geeksforgeeks.org/converting-a-real-number-between-0-and-1-to-binary-string/)

给定一个 0 到 1 之间的实数(例如 0.72)，作为双精度值传入，打印二进制表示。如果数字不能用最多 32 个字符的二进制数准确表示，请打印“ERROR:”

**示例:**

```
Input :  (0.625)10
Output : (0.101)2

Input : (0.72)10
Output : ERROR

```

**解决方法:**首先，我们先问问自己，二进制中的非整数是什么样子的。通过类比十进制数，二进制数 0 .101 <sub>2</sub> 看起来像:
0。101<sub>2</sub>= 1 * 1/2<sup>1</sup>+0 * 1/2<sup>2</sup>+1 * 1/2<sup>3</sup>。

**方法 1:小数部分乘以 2**

要打印小数部分，我们可以乘以 2，并检查 2*n 是否大于或等于 1。这实质上是“移动”分数和。那就是:

```
r = 210 * n;
  = 210 * 0.1012;
  = 1 * 1/20 + 0 *1/21 + 1 * 1/22;
  = 1.012;
```

如果 r >= 1，那么我们知道 n 在小数点后有一个 1。通过持续这样做，我们可以检查每个数字。

## C++

```
// C++ program to binary real number to string
#include <iostream>
#include<string>
using namespace std;

// Function to convert Binary real
// number to String
string toBinary(double n)
{
    // Check if the number is Between 0 to 1 or Not
    if (n >= 1 || n <= 0)
        return "ERROR";

    string answer;
    double frac = 0.5;
    answer.append(".");

    // Setting a limit on length: 32 characters.        
    while (n > 0)
    {

        //Setting a limit on length: 32 characters    
        if (answer.length() >= 32)
                return "ERROR";

            // Multiply n by 2 to check it 1 or 0
            double b = n * 2;
            if (b >= 1)
            {
                answer.append("1");
                n = b - 1;
            }
            else
            {
                answer.append("0");
                n = b;
            }
        }
        return answer;
}

// Driver code
int main()
{
    // Input value
    double n = 0.625;

    string result = toBinary(n);
    cout<<"(0"<< result <<") in base 2"<<endl;

    double m = 0.72;
    result= toBinary(m);
    cout<<"("<<result<<")"<<endl;
}

// This code is contributed by Himanshu Batra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Binary real number to String.
import java.lang.*;
import java.io.*;
import java.util.*;

// Class Representation of Binary real number
// to String
class BinaryToString
{
    // Main function to convert Binary real number
    // to String
    static String printBinary(double num)
    {
        // Check Number is Between 0 to 1 or Not
        if (num >= 1 || num <= 0)
            return "ERROR";

        StringBuilder binary = new StringBuilder();
        binary.append(".");

        while (num > 0)
        {
            /* Setting a limit on length: 32 characters,
               If the number cannot be represented
               accurately in binary with at most 32
               character  */
            if (binary.length() >= 32)
                return "ERROR";

            // Multiply by 2 in num to check it 1 or 0
            double r = num * 2;
            if (r >= 1)
            {
                binary.append(1);
                num = r - 1;
            }
            else
            {
                binary.append(0);
                num = r;
            }
        }
        return binary.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {
        double num1 = 0.625; // Input value in Decimal
        String output = printBinary(num1);
        System.out.println("(0" + output + ")  in base 2");

        double num2 = 0.72;
        output = printBinary(num2);
        System.out.println("(" + output + ") ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to binary real number to string

# Function to convert Binary real
# number to String
def toBinary(n):

    # Check if the number is Between 0 to 1 or Not
    if(n >= 1 or n <= 0):
        return "ERROR"

    answer = ""
    frac = 0.5
    answer = answer + "."

    # Setting a limit on length: 32 characters.
    while(n > 0):

        # Setting a limit on length: 32 characters
        if(len(answer) >= 32):
            return "ERROR"

        # Multiply n by 2 to check it 1 or 0
        b = n * 2
        if (b >= 1):

            answer = answer + "1"
            n = b - 1

        else:
            answer = answer + "0"
            n = b

    return answer

# Driver code
if __name__=='__main__':
    n = 0.625
    result = toBinary(n)
    print("(0", result, ") in base 2")
    m = 0.72
    result = toBinary(m)
    print("(", result, ")")

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to Binary real number to String.

using System;
using System.Text;

// Class Representation of Binary real number
// to String
class BinaryToString
{
    // Main function to convert Binary real number
    // to String
    static String printBinary(double num)
    {
        // Check Number is Between 0 to 1 or Not
        if (num >= 1 || num <= 0)
            return "ERROR";

        StringBuilder binary = new StringBuilder();
        binary.Append(".");

        while (num > 0)
        {
            /* Setting a limit on length: 32 characters,
            If the number cannot be represented
            accurately in binary with at most 32
            character */
            if (binary.Length >= 32)
                return "ERROR";

            // Multiply by 2 in num to check it 1 or 0
            double r = num * 2;
            if (r >= 1)
            {
                binary.Append(1);
                num = r - 1;
            }
            else
            {
                binary.Append(0);
                num = r;
            }
        }
        return binary.ToString();
    }

    // Driver Code
    public static void Main()
    {
        double num1 = 0.625; // Input value in Decimal
        String output = printBinary(num1);
        Console.WriteLine("(0 " + output + ") in base 2");

        double num2 = 0.72;
        output = printBinary(num2);
    Console.WriteLine("(" + output + ") ");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to binary real number
// to string

// Function to convert Binary real
// number to String
function toBinary($n)
{
    // Check if the number is Between
    // 0 to 1 or Not
    if ($n >= 1 || $n <= 0)
        return "ERROR";

    $answer = "";
    $frac = 0.5;
    $answer .= ".";

    // Setting a limit on length: 32 characters.        
    while ($n > 0)
    {

        //Setting a limit on length: 32 characters
        if (strlen($answer) >= 32)
                return "ERROR";

            // Multiply n by 2 to check it 1 or 0
            $b = $n * 2;
            if ($b >= 1)
            {
                $answer .= "1";
                $n = $b - 1;
            }
            else
            {
                $answer .= "0";
                $n = $b;
            }
        }
        return $answer;
}

// Driver code

// Input value
$n = 0.625;

$result = toBinary($n);
echo "(0" . $result . ") in base 2\n";

$m = 0.72;
$result= toBinary($m);
echo "(" . $result . ")";

// This code is contributed by mits
?>
```

**输出:**

```
(0.101)  in base 2
(ERROR) 
```

**方法二**

或者，我们可以将数字与进行比较，而不是将数字乘以 2 并与 1 进行比较。那就 5 块。25，以此类推。下面的代码演示了这种方法。

## C++

```
// C++ program to Binary real number to String.
#include <iostream>
#include<string>
using namespace std;

// Function to convert Binary real
// number to String
string toBinary(double n)
{
    // Check if the number is Between 0 to 1 or Not
    if (n >= 1 || n <= 0)
        return "ERROR";

    string answer;
    double frac = 0.5;
    answer.append(".");

    // Setting a limit on length: 32 characters.        
    while (n > 0)
    {
        // 32 char max
        if (answer.length() >= 32)
            return "ERROR";
    // compare the number to .5
        if (n >= frac)
        {
            answer.append("1");
            n = n- frac;
        }
        else
        {
            answer.append("0");
        }

        frac /= 2;
    }
    return answer;
}

// Driver code
int main()
{
    // Input value
    double n = 0.625;

    string result = toBinary(n);
    cout<<"(0"<< result <<") in base 2"<<endl;

    double m = 0.72;
    result= toBinary(m);
    cout<<"("<<result<<")"<<endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Binary real number to String.
import java.lang.*;
import java.io.*;
import java.util.*;

// Class Reperesentation of Binary real number
// to String
class BinaryToString
{
    // Main function to convert Binary real
    // number to String
    static String printBinary(double num)
    {
        // Check Number is Between 0 to 1 or Not
        if (num >= 1 || num <= 0)
            return "ERROR";

        StringBuilder binary = new StringBuilder();
        double frac = 0.5;
        binary.append(".");

        while (num > 0)
        {
            /* Setting a limit on length: 32 characters,
               If the number cannot be represented
               accurately in binary with at most 32
               characters  */
            if (binary.length() >= 32)
                return "ERROR";

            // It compare the number to . 5.
            if (num >= frac)
            {
                binary.append(1);
                num -= frac;
            }
            else           
                binary.append(0);

            // Now it become 0.25
            frac /= 2;
        }
        return binary.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {
        double num1 = 0.625; // Input value in Decimal
        String output = printBinary(num1);
        System.out.println("(0" + output + ")  in base 2");

        double num2 = 0.72;
        output = printBinary(num2);
        System.out.println("(" + output + ") ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to Binary real number to String.

# Function to convert Binary real
# number to String
def toBinary(n):

    # Check if the number is Between
    # 0 to 1 or Not
    if (n >= 1 or n <= 0):
        return "ERROR";

    frac = 0.5;
    answer = ".";

    # Setting a limit on length: 32 characters.    
    while (n > 0):

        # 32 char max
        if (len(answer) >= 32):
            return "ERROR";

        # compare the number to .5
        if (n >= frac):
            answer += "1";
            n = n - frac;
        else:
            answer += "0";

        frac = (frac / 2);

    return answer;

# Driver code

# Input value
n = 0.625;

result = toBinary(n);
print("( 0", result, ") in base 2");

m = 0.72;
result = toBinary(m);
print("(", result, ")");

# This code is contributed
# by mits
```

## C#

```
// C# program to Binary real number to String.
using System;

// Class Reperesentation of Binary
// real number to String
class BinaryToString
{
    // Main function to convert Binary
    // real number to String
    static string printBinary(double num)
    {
        // Check Number is Between
        // 0 to 1 or Not
        if (num >= 1 || num <= 0)
            return "ERROR";

        string binary = "";
        double frac = 0.5;
        binary += ".";

        while (num > 0)
        {
            /* Setting a limit on length: 32 characters,
            If the number cannot be represented
            accurately in binary with at most 32
            characters */
            if (binary.Length >= 32)
                return "ERROR";

            // It compare the number to . 5.
            if (num >= frac)
            {
                binary += "1";
                num -= frac;
            }
            else       
                binary += "0";

            // Now it become 0.25
            frac /= 2;
        }
        return binary;
    }

    // Driver Code
    public static void Main()
    {
        double num1 = 0.625; // Input value in Decimal
        String output = printBinary(num1);
        Console.WriteLine("(0" + output + ") in base 2");

        double num2 = 0.72;
        output = printBinary(num2);
        Console.WriteLine("(" + output + ") ");
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Binary real number to String.

// Function to convert Binary real
// number to String
function toBinary($n)
{
    // Check if the number is Between
    // 0 to 1 or Not
    if ($n >= 1 || $n <= 0)
        return "ERROR";

    $frac = 0.5;
    $answer = ".";

    // Setting a limit on length: 32 characters.        
    while ($n > 0)
    {
        // 32 char max
        if (strlen($answer) >= 32)
            return "ERROR";

        // compare the number to .5
        if ($n >= $frac)
        {
            $answer.="1";
            $n = $n - $frac;
        }
        else
        {
            $answer.="0";
        }

        $frac = ($frac / 2);
    }
    return $answer;
}

// Driver code

// Input value
$n = 0.625;

$result = toBinary($n);
print("(0".$result.") in base 2\n");

$m = 0.72;
$result = toBinary($m);
print("(".$result.")");

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript program to Binary real
// number to String.

// Main function to convert Binary
// real number to String
function printBinary(num)
{

    // Check Number is Between
    // 0 to 1 or Not
    if (num >= 1 || num <= 0)
        return "ERROR";

    let binary = "";
    let frac = 0.5;
    binary += ".";

    while (num > 0)
    {

        /* Setting a limit on length: 32 characters,
        If the number cannot be represented
        accurately in binary with at most 32
        characters */
        if (binary.length >= 32)
            return "ERROR";

        // It compare the number to . 5.
        if (num >= frac)
        {
            binary += "1";
            num -= frac;
        }
        else       
            binary += "0";

        // Now it become 0.25
        frac = frac / 2;
    }
    return binary;
}

// Driver code

// Input value in Decimal
let num1 = 0.625;
let output = printBinary(num1);
document.write("(0" + output +
               ") in base 2" + "</br>");

let num2 = 0.72;
output = printBinary(num2);
document.write("(" + output + ") ");

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
(0.101)  in base 2
(ERROR)  
```

两种方法都同样好；选择一个你觉得最舒服的。
本文由**Somesh Awasthi**先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。