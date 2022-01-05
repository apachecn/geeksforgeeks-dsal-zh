# 检查一个数是否能被 23 整除

> 原文:[https://www . geeksforgeeks . org/check-如果一个数字被 23 整除或不被整除/](https://www.geeksforgeeks.org/check-if-a-number-is-divisible-by-23-or-not/)

给定一个数，任务是快速检查这个数是否能被 23 整除。
**例:**

```
Input : x  = 46
Output : Yes

Input : 47
Output : No
```

解决这个问题的方法是提取最后一个数字，将最后一个数字的 7 倍加到剩余的数字上，重复这个过程，直到得到一个两位数。如果得到的两位数能被 23 整除，那么给定的数就能被 23 整除。
**进场:**

*   每次提取数字/截断数字的最后一位数字
*   将 7*(前一个数字的最后一位数字)加到截断的数字上
*   根据需要重复以上三个步骤。

插图:

```

17043-->1704+7*3 
= 1725-->172+7*5
= 207 which is 9*23, 
so 17043 is also divisible by 23.
```

> **数学证明:**
> 设![\overline{a b c}  ](img/517e12b69969dfb8e1a08031bf3e25c4.png "Rendered by QuickLaTeX.com")为任意数，使得![\overline{a b c}  ](img/517e12b69969dfb8e1a08031bf3e25c4.png "Rendered by QuickLaTeX.com")= 100 a+10b+c。
> 现在假设![\overline{a b c}  ](img/517e12b69969dfb8e1a08031bf3e25c4.png "Rendered by QuickLaTeX.com")可被 23 整除。然后
> ![\overline{a b c}\equiv  ](img/8a360337b012644a3f21519e45f41e2c.png "Rendered by QuickLaTeX.com")0(mod 23)
> 100 a+10b+c![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com")0(mod 23)
> 10(10a+b)+c![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com")0(mod 23)
> 10![\overline{a b}  ](img/bbec9f15952313362910c98c78da7689.png "Rendered by QuickLaTeX.com")+c![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com")0(mod 23)
> 既然已经把最后一位数字和数字分开了，那就要想办法使用了。
> 使![\overline{a b}  ](img/bbec9f15952313362910c98c78da7689.png "Rendered by QuickLaTeX.com")的系数为 1。
> 换句话说，我们要找到一个整数，这样 n 使得 10n ![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com") 1 mod 23。
> 可以观察到满足这个性质的最小 n 为 7 as 70 ![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com") 1 mod 23。
> 现在我们可以将原来的方程 10 ![\overline{a b}  ](img/bbec9f15952313362910c98c78da7689.png "Rendered by QuickLaTeX.com") +c ![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com") 0 (mod 23)
> 乘以 7 并简化:
> 70![\overline{a b}  ](img/bbec9f15952313362910c98c78da7689.png "Rendered by QuickLaTeX.com")+7c![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com")0(mod 23)
> +7c![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com")0(mod 23)
> 我们已经发现如果![\overline{a b c}\equiv  ](img/8a360337b012644a3f21519e45f41e2c.png "Rendered by QuickLaTeX.com") 0 (mod 23)那么，
> ![\overline{a b}  ](img/bbec9f15952313362910c98c78da7689.png "Rendered by QuickLaTeX.com") +7c ![\equiv  ](img/1a1191c0268b97604e336a3e8536fcc3.png "Rendered by QuickLaTeX.com") 0 (mod 23)。
> 换句话说，要检查一个 3 位数是否能被 23 整除，
> 我们只需去掉最后一位数字，乘以 7，
> 再从剩下的两位数中减去。

## C++

```
// CPP program to validate above logic
#include <iostream>
using namespace std;

// Function to check if the number is
// divisible by 23 or not
bool isDivisible(long long int n)
{

    // While there are at least 3 digits
    while (n / 100)
    {
        int d = n % 10; // Extracting the last digit
        n /= 10; // Truncating the number

        // Adding seven times the last
        // digit to the remaining number
        n += d * 7;
    }

    return (n % 23 == 0);
}

int main()
{
    long long int n = 1191216;
    if (isDivisible(n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate above logic
class GFG
{

// Function to check if the
// number is divisible by
// 23 or not
static boolean isDivisible(long n)
{

    // While there are at
    // least 3 digits
    while (n / 100 != 0)
    {
        // Extracting the last digit
        long d = n % 10;

        n /= 10; // Truncating the number

        // Adding seven times the last
        // digit to the remaining number
        n += d * 7;
    }

    return (n % 23 == 0);
}

// Driver Code
public static void main(String[] args)
{
    long n = 1191216;
    if(isDivisible(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to validate above logic

# Function to check if the number is
# divisible by 23 or not
def isDivisible(n) :

    # While there are at least 3 digits
    while n // 100 :

        # Extracting the last
        d = n % 10

        # Truncating the number
        n //= 10

        # Adding seven times the last 
        # digit to the remaining number
        n += d * 7

    return (n % 23 == 0)

# Driver Code
if __name__ == "__main__" :

    n = 1191216

    # function calling
    if (isDivisible(n)) :
        print("Yes")

    else :
        print("No")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to validate
// above logic
class GFG
{

// Function to check if the
// number is divisible by
// 23 or not
static bool isDivisible(long n)
{

    // While there are at
    // least 3 digits
    while (n / 100 != 0)
    {
        // Extracting the last digit
        long d = n % 10;

        n /= 10; // Truncating the number

        // Adding seven times the last
        // digit to the remaining number
        n += d * 7;
    }

    return (n % 23 == 0);
}

// Driver Code
public static void Main()
{
    long n = 1191216;
    if(isDivisible(n))
        System.Console.WriteLine("Yes");
    else
        System.Console.WriteLine("No");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to validate above logic

// Function to check if the number
// is divisible by 23 or not
function isDivisible($n)
{

    // While there are at
    // least 3 digits
    while (intval($n / 100))
    {
        $n = intval($n);
        $d = $n % 10; // Extracting the last digit
        $n /= 10; // Truncating the number

        // Adding seven times the last
        // digit to the remaining number
        $n += $d * 7;
    }

    return ($n % 23 == 0);
}

$n = 1191216;
if (isDivisible($n))
echo "Yes" . "\n";
else
echo "No" . "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to validate above logic

// Function to check if the
// number is divisible by
// 23 or not
function isDivisible(n)
{
    // While there are at
    // least 3 digits
    while (Math.floor(n / 100) != 0)
    {
        // Extracting the last digit
        let d = n % 10;

        n = Math.floor(n/10); // Truncating the number

        // Adding seven times the last
        // digit to the remaining number
        n += d * 7;
    }

    return (n % 23 == 0);
}

// Driver Code
let n = 1191216;
if(isDivisible(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
Yes
```

请注意，上面的程序可能没有多大意义，因为可以简单地做 n % 23 来检查可分性。这个程序的想法是验证这个概念。此外，如果输入数字很大并且以字符串形式给出，这可能是一种有效的方法。