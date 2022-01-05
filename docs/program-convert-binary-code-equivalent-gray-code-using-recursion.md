# 使用递归的二进制到格雷码

> 原文:[https://www . geesforgeks . org/program-convert-binary-code-等价物-gray-code-use-recursion/](https://www.geeksforgeeks.org/program-convert-binary-code-equivalent-gray-code-using-recursion/)

给定一个数字的二进制代码为十进制数，我们需要将其转换为其等价的[格雷码](https://www.geeksforgeeks.org/gray-to-binary-and-binary-to-gray-conversion/)。
示例:

```
Input : 1001 
Output : 1101

Input : 11
Output : 10
```

在格雷码中，两个连续的数字中只有一位发生变化。

**算法:**

```
binary_to_grey(n)
 if n == 0
       grey = 0;
 else if last two bits are opposite  to each other
       grey = 1 + 10 * binary_to_gray(n/10))
 else if last two bits are same
       grey = 10 * binary_to_gray(n/10))
```

以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to convert Binary to
// Gray code using recursion
#include <bits/stdc++.h>
using namespace std;

// Function to change Binary to
// Gray using recursion
int binary_to_gray(int n)
{
    if (!n)
        return 0;

    // Taking last digit
    int a = n % 10;

    // Taking second last digit
    int b = (n / 10) % 10;

    // If last digit are opposite bits
    if ((a && !b) || (!a && b))        
            return (1 + 10 * binary_to_gray(n / 10));

    // If last two bits are same
    return (10 * binary_to_gray(n / 10));
}

// Driver Function
int main()
{
    int binary_number = 1011101;

    printf("%d", binary_to_gray(binary_number));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert
// Binary code to Gray code
import static java.lang.StrictMath.pow;
import java.util.Scanner;

class bin_gray
{
    // Function to change Binary to
    // Gray using recursion
    int binary_to_gray(int n, int i)
    {
        int a, b;
        int result = 0;
        if (n != 0)
        {
            // Taking last digit
            a = n % 10;

            n = n / 10;

            // Taking second last digit
            b = n % 10;

            if ((a & ~ b) == 1 || (~ a & b) == 1)
            {
                result = (int) (result + pow(10,i));
            }

            return binary_to_gray(n, ++i) + result;
        }
        return 0;
    }

    // Driver Function
    public static void main(String[] args)
    {
        int binary_number;
        int result = 0;
        binary_number = 1011101;

        bin_gray obj = new bin_gray();
        result = obj.binary_to_gray(binary_number,0);

        System.out.print(result);
    }
}

// This article is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python3 code to convert Binary
# to Gray code using recursion

# Function to change Binary to Gray using recursion
def binary_to_gray( n ):
    if not(n):
        return 0

    # Taking last digit   
    a = n % 10

     # Taking second last digit
    b = int(n / 10) % 10

    # If last digit are opposite bits
    if (a and not(b)) or (not(a) and b):
        return (1 + 10 * binary_to_gray(int(n / 10)))

    # If last two bits are same
    return (10 * binary_to_gray(int(n / 10)))

# Driver Code
binary_number = 1011101
print( binary_to_gray(binary_number), end='')

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to convert
// Binary code to Gray code
using System;

class GFG {

    // Function to change Binary to
    // Gray using recursion
    static int binary_to_gray(int n, int i)
    {
        int a, b;
        int result = 0;
        if (n != 0)
        {

            // Taking last digit
            a = n % 10;

            n = n / 10;

            // Taking second last digit
            b = n % 10;

            if ((a & ~ b) == 1 || (~ a & b) == 1)
            {
                result = (int) (result + Math.Pow(10,i));
            }

            return binary_to_gray(n, ++i) + result;
        }

        return 0;
    }

    // Driver Function
    public static void Main()
    {
        int binary_number;
        binary_number = 1011101;

        Console.WriteLine(binary_to_gray(binary_number,0));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert Binary to
// Gray code using recursion

// Function to change Binary to
// Gray using recursion
function binary_to_gray($n)
{
    if (!$n)
        return 0;

    // Taking last digit
    $a = $n % 10;

    // Taking second
    // last digit
    $b = ($n / 10) % 10;

    // If last digit are
    // opposite bits
    if (($a && !$b) || (!$a && $b))    
            return (1 + 10 * binary_to_gray($n / 10));

    // If last two
    // bits are same
    return (10 * binary_to_gray($n / 10));
}

    // Driver Code
    $binary_number = 1011101;
    echo binary_to_gray($binary_number);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to convert
// Binary code to Gray code

    // Function to change Binary to
    // Gray using recursion
    function binary_to_gray(n, i)
    {
        let a, b;
        let result = 0;
        if (n != 0)
        {
            // Taking last digit
            a = n % 10;

            n = n / 10;

            // Taking second last digit
            b = n % 10;

            if ((a & ~ b) == 1 || (~ a & b) == 1)
            {
                result =  (result + Math.pow(10,i));
            }

            return binary_to_gray(n, ++i) + result;
        }
        return 0;
    }

// Driver code                
        let binary_number;
        let result = 0;
        binary_number = 1011101;

        result = binary_to_gray(binary_number,0);

        document.write(result);

       // This code is contributed by code_hunt.
</script>
```

输出:

```
1110011
```

假设二进制数在整数范围内。对于较大的值，我们可以将二进制数作为字符串。