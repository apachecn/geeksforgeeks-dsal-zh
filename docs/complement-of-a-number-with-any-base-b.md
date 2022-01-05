# 任意基数 b 的数的补码

> 原文:[https://www . geeksforgeeks . org/带任意基数 b 的数字补码/](https://www.geeksforgeeks.org/complement-of-a-number-with-any-base-b/)

*   [整数的补码](https://www.geeksforgeeks.org/find-ones-complement-integer/)
*   [二进制数的 1 和 2 的补码](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)

在这篇文章中，讨论了一种寻找任意基数补码的一般方法![b    ](img/56c19e62ea115719245402c109e4c477.png "Rendered by QuickLaTeX.com")。
**寻找(b-1)补语的步骤**:寻找(b-1)补语，

*   用基数为![b    ](img/56c19e62ea115719245402c109e4c477.png "Rendered by QuickLaTeX.com")的数字系统中最大的数字减去数字的每个数字。
*   例如，如果数字是以 9 为基数的三位数，则从 888 中减去该数字，因为 8 是以 9 为基数的数字系统中最大的数字。
*   得到的结果是(b-1)的(8 的补码)补码。

**求 b 的补码的步骤**:要求 b 的补码，只需在计算出的(b-1)的补码上加 1 即可。
现在，这适用于任何存在于数系中的基数。它可以用熟悉的 1 和 2 补码来测试。
**示例** :

```
Let the number be 10111 base 2 (b=2)
Then, 1's complement will be 01000 (b-1)
2's complement will be 01001 (b)

Taking a number with Octal base:
Let the number be -456.
Then 7's complement will be 321
and 8's complement will be 322
```

以下是上述思路的实现:

## C++

```
// CPP program to find complement of a
// number with any base b
#include<iostream>
#include<cmath>

using namespace std;

// Function to find (b-1)'s complement
int prevComplement(int n, int b)
{
    int maxDigit, maxNum = 0, digits = 0, num = n;

    // Calculate number of digits
    // in the given number
    while(n!=0)
    {
        digits++;
        n = n/10;
    }

    // Largest digit in the number
    // system with base b
    maxDigit = b-1;

    // Largest number in the number
    // system with base b
    while(digits--)
    {
        maxNum = maxNum*10 + maxDigit;
    }

    // return Complement
    return maxNum - num;
}

// Function to find b's complement
int complement(int n, int b)
{  
    // b's complement = (b-1)'s complement + 1
    return prevComplement(n,b) + 1;
}

// Driver code
int main()
{
    cout << prevComplement(25, 7)<<endl;

    cout << complement(25, 7);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find complement
// of a number with any base b
class GFG
{

// Function to find (b-1)'s complement
static int prevComplement(int n, int b)
{
    int maxDigit, maxNum = 0,
        digits = 0, num = n;

    // Calculate number of digits
    // in the given number
    while(n != 0)
    {
        digits++;
        n = n / 10;
    }

    // Largest digit in the number
    // system with base b
    maxDigit = b - 1;

    // Largest number in the number
    // system with base b
    while((digits--) > 0)
    {
        maxNum = maxNum * 10 + maxDigit;
    }

    // return Complement
    return maxNum - num;
}

// Function to find b's complement
static int complement(int n, int b)
{
    // b's complement = (b-1)'s
    // complement + 1
    return prevComplement(n, b) + 1;
}

// Driver code
public static void main(String args[])
{
    System.out.println(prevComplement(25, 7));

    System.out.println(complement(25, 7));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python 3 program to find
# complement of a number
# with any base b

# Function to find
# (b-1)'s complement
def prevComplement(n, b) :
    maxNum, digits, num = 0, 0, n

    # Calculate number of digits
    # in the given number
    while n > 1 :
        digits += 1
        n = n // 10

    # Largest digit in the number
    # system with base b
    maxDigit = b - 1

    # Largest number in the number
    # system with base b
    while digits :
        maxNum = maxNum * 10 + maxDigit
        digits -= 1

    # return Complement
    return maxNum - num

# Function to find b's complement
def complement(n, b) :

    # b's complement = (b-1)'s
    # complement + 1
    return prevComplement(n, b) + 1

# Driver code
if __name__ == "__main__" :

    # Function calling
    print(prevComplement(25, 7))
    print(complement(25, 7))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to find complement
// of a number with any base b
class GFG
{

// Function to find (b-1)'s complement
static int prevComplement(int n, int b)
{
    int maxDigit, maxNum = 0,
        digits = 0, num = n;

    // Calculate number of digits
    // in the given number
    while(n != 0)
    {
        digits++;
        n = n / 10;
    }

    // Largest digit in the number
    // system with base b
    maxDigit = b - 1;

    // Largest number in the number
    // system with base b
    while((digits--) > 0)
    {
        maxNum = maxNum * 10 + maxDigit;
    }

    // return Complement
    return maxNum - num;
}

// Function to find b's complement
static int complement(int n, int b)
{
    // b's complement = (b-1)'s
    // complement + 1
    return prevComplement(n, b) + 1;
}

// Driver code
public static void Main()
{
    System.Console.WriteLine(prevComplement(25, 7));

    System.Console.WriteLine(complement(25, 7));
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find complement
// of a number with any base b

// Function to find (b-1)'s complement
function prevComplement($n, $b)
{
    $maxNum = 0;
    $digits = 0;
    $num = $n;

    // Calculate number of digits
    // in the given number
    while((int)$n != 0)
    {
        $digits++;
        $n = $n / 10;
    }

    // Largest digit in the number
    // system with base b
    $maxDigit = $b - 1;

    // Largest number in the number
    // system with base b
    while($digits--)
    {
        $maxNum = $maxNum * 10 +
                  $maxDigit;
    }

    // return Complement
    return $maxNum - $num;
}

// Function to find b's complement
function complement($n, $b)
{
    // b's complement = (b-1)'s
    // complement + 1
    return prevComplement($n, $b) + 1;
}

// Driver code
echo prevComplement(25, 7), "\n";

echo(complement(25, 7));

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript program to find complement
// of a number with any base b

// Function to find (b-1)'s complement
    function prevComplement(n , b) {
        var maxDigit, maxNum = 0, digits = 0,
        num = n;

        // Calculate number of digits
        // in the given number
        while (n != 0) {
            digits++;
            n = parseInt(n / 10);
        }

        // Largest digit in the number
        // system with base b
        maxDigit = b - 1;

        // Largest number in the number
        // system with base b
        while ((digits--) > 0) {
            maxNum = maxNum * 10 + maxDigit;
        }

        // return Complement
        return maxNum - num;
    }

    // Function to find b's complement
    function complement(n , b) {
        // b's complement = (b-1)'s
        // complement + 1
        return prevComplement(n, b) + 1;
    }

    // Driver code

        document.write(prevComplement(25, 7)+"<br/>");

        document.write(complement(25, 7));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
41
42
```