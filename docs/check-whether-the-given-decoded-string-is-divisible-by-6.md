# 检查给定的解码字符串是否能被 6 整除

> 原文:[https://www . geesforgeks . org/check-给定解码字符串是否可被 6 整除/](https://www.geeksforgeeks.org/check-whether-the-given-decoded-string-is-divisible-by-6/)

给定由小写字符组成的字符串 **str** ，任务是根据给定规则进行更改后，检查该字符串是否可被 **6** 整除:

*   **‘a’**改为 **1** 。
*   **‘b’**改为 **2** …
*   同样地，**‘z’**变成了 **26** 。

例如，字符串**“abz”**将更改为 **1226** 。

**示例:**

> **输入:**str = " ab "
> T3】输出:是
> “ab”相当于 12，可被 6 整除。
> 
> **输入:**str = " ABC "
> T3】输出:否
> 123 不能被 6 整除。

**方法:**只要一个数的所有位数之和能被 **3** 整除，且该数的最后一个位数能被 **2** 整除，就可以用一个简单的数学技巧解决这个问题。求形成数的位数之和，存入变量 **sum** 。此外，找到号码的最后一位数字并存储在**最后一位数字**中。
现在，如果总和被 **3** 整除，**最后一位数字**被 **2** 整除，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum
// of the digits of n
int sumDigits(int n)
{
    int sum = 0;
    while (n > 0) {
        int digit = n % 10;
        sum += digit;
        n /= 10;
    }
    return sum;
}

// Function that return true if the
// decoded string is divisible by 6
bool isDivBySix(string str, int n)
{
    // To store the sum of the digits
    int sum = 0;

    // For each character, get the
    // sum of the digits
    for (int i = 0; i < n; i++) {
        sum += (int)(str[i] - 'a' + 1);
    }

    // If the sum of digits is
    // not divisible by 3
    if (sum % 3 != 0)
        return false;

    // Get the last digit of
    // the number formed
    int lastDigit = ((int)(str[n - 1]
                           - 'a' + 1))
                    % 10;

    // If the last digit is
    // not divisible by 2
    if (lastDigit % 2 != 0)
        return false;
    return true;
}

// Driver code
int main()
{
    string str = "ab";
    int n = str.length();

    if (isDivBySix(str, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the sum
// of the digits of n
static int sumDigits(int n)
{
    int sum = 0;
    while (n > 0)
    {
        int digit = n % 10;
        sum += digit;
        n /= 10;
    }
    return sum;
}

// Function that return true if the
// decoded string is divisible by 6
static boolean isDivBySix(String str, int n)
{
    // To store the sum of the digits
    int sum = 0;

    // For each character, get the
    // sum of the digits
    for (int i = 0; i < n; i++)
    {
        sum += (int)(str.charAt(i) - 'a' + 1);
    }

    // If the sum of digits is
    // not divisible by 3
    if (sum % 3 != 0)
        return false;

    // Get the last digit of
    // the number formed
    int lastDigit = ((int)(str.charAt(n - 1) -
                                    'a' + 1)) % 10;

    // If the last digit is
    // not divisible by 2
    if (lastDigit % 2 != 0)
        return false;
    return true;
}

// Driver code
public static void main(String []args)
{
    String str = "ab";
    int n = str.length();

    if (isDivBySix(str, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum
# of the digits of n
def sumDigits(n) :

    sum = 0;
    while (n > 0) :
        digit = n % 10;
        sum += digit;
        n //= 10;

    return sum;

# Function that return true if the
# decoded string is divisible by 6
def isDivBySix(string , n) :

    # To store the sum of the digits
    sum = 0;

    # For each character, get the
    # sum of the digits
    for i in range(n) :
        sum += (ord(string[i]) -
                ord('a') + 1);

    # If the sum of digits is
    # not divisible by 3
    if (sum % 3 != 0) :
        return False;

    # Get the last digit of
    # the number formed
    lastDigit = (ord(string[n - 1]) -
                 ord('a') + 1) % 10;

    # If the last digit is
    # not divisible by 2
    if (lastDigit % 2 != 0) :
        return False;
    return True;

# Driver code
if __name__ == "__main__" :

    string = "ab";
    n = len(string);

    if (isDivBySix(string, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the sum
// of the digits of n
static int sumDigits(int n)
{
    int sum = 0;
    while (n > 0)
    {
        int digit = n % 10;
        sum += digit;
        n /= 10;
    }
    return sum;
}

// Function that return true if the
// decoded string is divisible by 6
static bool isDivBySix(String str, int n)
{
    // To store the sum of the digits
    int sum = 0;

    // For each character, get the
    // sum of the digits
    for (int i = 0; i < n; i++)
    {
        sum += (int)(str[i] - 'a' + 1);
    }

    // If the sum of digits is
    // not divisible by 3
    if (sum % 3 != 0)
        return false;

    // Get the last digit of
    // the number formed
    int lastDigit = ((int)(str[n - 1] -
                             'a' + 1)) % 10;

    // If the last digit is
    // not divisible by 2
    if (lastDigit % 2 != 0)
        return false;
    return true;
}

// Driver code
public static void Main(String []args)
{
    String str = "ab";
    int n = str.Length;

    if (isDivBySix(str, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum
// of the digits of n
function sumDigits(n)
{
    var sum = 0;
    while (n > 0) {
        var digit = n % 10;
        sum += digit;
        n = parseInt(n/10);
    }
    return sum;
}

// Function that return true if the
// decoded string is divisible by 6
function isDivBySix(str, n)
{
    // To store the sum of the digits
    var sum = 0;

    // For each character, get the
    // sum of the digits
    for (var i = 0; i < n; i++) {
        sum += (str[i].charCodeAt(0) - 'a'.charCodeAt(0) + 1);
    }

    // If the sum of digits is
    // not divisible by 3
    if (sum % 3 != 0)
        return false;

    // Get the last digit of
    // the number formed
    var lastDigit = ((str[n - 1].charCodeAt(0)
                           - 'a'.charCodeAt(0) + 1))
                    % 10;

    // If the last digit is
    // not divisible by 2
    if (lastDigit % 2 != 0)
        return false;
    return true;
}

// Driver code
var str = "ab";
var n = str.length;
if (isDivBySix(str, n))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output**

```
Yes
```

**时间复杂度** : O(N)

**辅助空间:** O(1)