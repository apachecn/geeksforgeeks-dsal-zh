# 检查任意一个大数是否能被 17 整除

> 原文:[https://www . geesforgeks . org/check-if-any-大数是否可被 17 整除/](https://www.geeksforgeeks.org/check-if-any-large-number-is-divisible-by-17-or-not/)

给定一个数字，任务是快速检查这个数字是否能被 17 整除。
**例:**

```
Input : x = 34
Output : Yes

Input : x = 47
Output : No
```

解决这个问题的方法是提取最后一个数字，从剩余的数字中减去最后一个数字的 5 倍，重复这个过程，直到得到一个两位数。如果得到的两位数能被 17 整除，那么给定的数就能被 17 整除。
**进场:**

*   每次提取数字/截断数字的最后一位数字
*   从截断的数字中减去 5*(前一个数字的最后一位)
*   根据需要重复以上三个步骤。

插图:

```
3978-->397-5*8=357-->35-5*7=0\. 
So 3978 is divisible by 17.
```

> **数学证明:**
> 设![\overline{a b c}    ](img/259dac70f3944767bae96cc0a46bc6fb.png "Rendered by QuickLaTeX.com")为任意数，使得![\overline{a b c}    ](img/259dac70f3944767bae96cc0a46bc6fb.png "Rendered by QuickLaTeX.com")= 100 a+10b+c。
> 现在假设![\overline{a b c}    ](img/259dac70f3944767bae96cc0a46bc6fb.png "Rendered by QuickLaTeX.com")可被 17 整除。然后
> ![\overline{a b c}\equiv    ](img/352eaa9d47e67093a4d93f809f0eada2.png "Rendered by QuickLaTeX.com")0(mod 17)
> 100 a+10b+c![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com")0(mod 17)
> 10(10a+b)+c![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com")0(mod 17)
> 10![\overline{a b}    ](img/dfc8f170dbfc11f11183c87704d3ee62.png "Rendered by QuickLaTeX.com")+c![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com")0(mod 17)
> 既然已经把最后一位数字和数字分开了，那就要想办法使用了。
> 使![\overline{a b}    ](img/dfc8f170dbfc11f11183c87704d3ee62.png "Rendered by QuickLaTeX.com")的系数为 1。
> 换句话说，我们要找到一个整数，这样 n 这样 10n ![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com") 1 mod 17。
> 可以观察到满足这个性质的最小 n 是-5 as -50 ![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com") 1 mod 17。
> 现在我们可以将原方程 10 ![\overline{a b}    ](img/dfc8f170dbfc11f11183c87704d3ee62.png "Rendered by QuickLaTeX.com") +c ![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com") 0 (mod 17)
> 乘以-5，简化为:
> -50![\overline{a b}    ](img/dfc8f170dbfc11f11183c87704d3ee62.png "Rendered by QuickLaTeX.com")-5c![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com")0(mod 17)![\overline{a b}    ](img/dfc8f170dbfc11f11183c87704d3ee62.png "Rendered by QuickLaTeX.com")-5c![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com")0(mod 17)
> 我们发现如果![\overline{a b c}\equiv    ](img/352eaa9d47e67093a4d93f809f0eada2.png "Rendered by QuickLaTeX.com") 0 (mod 17)那么，
> ![\overline{a b}    ](img/dfc8f170dbfc11f11183c87704d3ee62.png "Rendered by QuickLaTeX.com") -5c ![\equiv    ](img/ad691242ceee64c96dea7a827e6955eb.png "Rendered by QuickLaTeX.com") 0 (mod 17)。
> 换句话说，要检查一个 3 位数是否能被 17 整除，
> 我们只需去掉最后一位数字，乘以 5，
> 再从剩下的两位数中减去。

**程序:**

## C++

```
// CPP Program to validate the above logic
#include <bits/stdc++.h>

using namespace std;

// Function to check if the
// number is divisible by 17 or not
bool isDivisible(long long int n)
{

    while (n / 100)
    {
        // Extracting the last digit
        int d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting the five times the
        // last digit from the remaining number
        n -= d * 5;
    }

    // Return n is divisible by 17
    return (n % 17 == 0);
}

// Driver code
int main()
{
    long long int n = 19877658;
    if (isDivisible(n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to validate the above logic

import java.io.*;

class GFG {

// Function to check if the
// number is divisible by 17 or not
 static boolean isDivisible(long n)
{

    while (n / 100>0)
    {
        // Extracting the last digit
        long d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting the five times the
        // last digit from the remaining number
        n -= d * 5;
    }

    // Return n is divisible by 17
    return (n % 17 == 0);
}

// Driver code

    public static void main (String[] args) {
    long n = 19877658;
    if (isDivisible(n))
        System.out.println( "Yes");
    else
        System.out.println( "No");
    }
}
// This code is contributed by inder_verma.
```

## 蟒蛇 3

```
# Python 3 Program to validate
# the above logic

# Function to check if the
# number is divisible by 17 or not
def isDivisible(n) :

    while(n // 100) :

        # Extracting the last digit
        d = n % 10

        # Truncating the number
        n //= 10

        # Subtracting the five times 
        # the last digit from the
        # remaining number
        n -= d * 5

    # Return n is divisible by 17
    return (n % 17 == 0)

# Driver Code
if __name__ == "__main__" :

    n = 19877658

    if isDivisible(n) :
        print("Yes")
    else :
        print("No")

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# Program to validate the above logic

using System;

class GFG {

// Function to check if the
// number is divisible by 17 or not
 static bool isDivisible(long n)
{

    while (n / 100>0)
    {
        // Extracting the last digit
        long d = n % 10;

        // Truncating the number
        n /= 10;

        // Subtracting the five times the
        // last digit from the remaining number
        n -= d * 5;
    }

    // Return n is divisible by 17
    return (n % 17 == 0);
}

// Driver code

    public static void Main () {
    long n = 19877658;
    if (isDivisible(n))
        Console.Write( "Yes");
    else
        Console.Write( "No");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to validate the above logic

// Function to check if the
// number is divisible by 17 or not
function isDivisible($n)
{

    while ($n / 100 != 0)
    {
        // Extracting the last digit
        $d = (int)$n % 10;

        // Truncating the number
        $n /= 10;

        // Subtracting the five times
        // the last digit from the
        // remaining number
        $n -= $d * 5;
    }

    // Return n is divisible by 17
    return ($n % 17 == 0);
}

// Driver code
$n = 19877658;
if (isDivisible($n))
    print("Yes");
else
    print("No");

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>

// JavaScript Program to validate the above logic

    // Function to check if the
// number is divisible by 17 or not
    function isDivisible(n)
    {
        while (Math.floor(n / 100)>0)
    {
        // Extracting the last digit
        let d = n % 10;

        // Truncating the number
        n = Math.floor(n/10);

        // Subtracting the five times the
        // last digit from the remaining number
        n -= d * 5;
    }

    // Return n is divisible by 17
    return (n % 17 == 0);
    }

    // Driver code
    let n = 19877658;
    if (isDivisible(n))
        document.write( "Yes");
    else
        document.write( "No");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Yes
```

请注意，上面的程序可能没有多大意义，因为可以简单地做 n % 23 来检查可分性。这个程序的想法是验证这个概念。此外，如果输入数字很大并且以字符串形式给出，这可能是一种有效的方法。