# 检查一个大数是否能被 2、3 和 5 整除

> 原文:[https://www . geeksforgeeks . org/check-如果一个大数能被 2-3 和-5 整除或不能/](https://www.geeksforgeeks.org/check-if-a-large-number-is-divisible-by-2-3-and-5-or-not/)

给定一个数，任务是检查一个数是否能被 2、3 和 5 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储，因此该数字被视为字符串。
**例:**

```
Input : str = "725" 
Output : NO

Input : str = "263730746028908374890"
Output : YES
```

如果一个数的最右边的数字是偶数，它可以被 2 整除；如果一个数的最右边的数字是零或五，它也可以被 5 整除。
所以，从上面的两个观察，我们可以得出结论，要让这个数被 2 和 5 整除，这个数最右边的数字必须是零。
现在，如果一个数的总和能被 3 整除，那么这个数就能被 3 整除。
因此，一个数可以被 2、3 和 5 整除，如果:

*   它最右边的数字是零。
*   它所有数字的总和可以被 3 整除。

以下是上述方法的实现:

## C++

```
// CPP program to Check if a large number is
// divisible by 2, 3 and 5 or not.
#include <bits/stdc++.h>
using namespace std;

// function to return sum of digits of
// a number
int SumOfDigits(string str, int n)
{
    int sum = 0;

    for (int i = 0; i < n; i++)
        sum += (int)(str[i] - '0');

    return sum;
}

// function to Check if a large number is
// divisible by 2, 3 and 5 or not
bool Divisible(string str, int n)
{
    if (SumOfDigits(str, n) % 3 == 0 and str[n - 1] == '0')
        return true;

    return false;
}

// Driver code
int main()
{
    string str = "263730746028908374890";

    int n = str.size();

    if (Divisible(str, n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if a large
// number is divisible by 2, 3 and
// 5 or not.
class GFG
{
// function to return sum of
// digits of a number
static int SumOfDigits(String str,
                       int n)
{
    int sum = 0;

    for (int i = 0; i < n; i++)
        sum += (int)(str.charAt(i) - '0');

    return sum;
}

// function to Check if a large number
// is divisible by 2, 3 and 5 or not
static boolean Divisible(String str,
                         int n)
{
    if (SumOfDigits(str, n) % 3 == 0 &&
        str.charAt(n - 1) == '0')
        return true;

    return false;
}

// Driver code
public static void main(String []args)
{
    String str = "263730746028908374890";

    int n = str.length();

    if (Divisible(str, n))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to Check if
# a large number is
# divisible by 2, 3 and 5 or not.

# function to return sum of digits of
# a number
def SumOfDigits(str, n):

    sum = 0
    for i in range(0,n):
        sum += int(ord(str[i] )- ord('0'))

    return sum

# function to Check if a large number is
# divisible by 2, 3 and 5 or not
def Divisible(str, n):
    if ((SumOfDigits(str, n) % 3 == 0 and
        str[n - 1] == '0')):
        return True

    return False

# Driver code
if __name__ == "__main__":
    str = "263730746028908374890"

    n = len(str)

    if (Divisible(str, n)):
        print("YES")
    else:
        print("NO")

# this code is contributed by
# ChitraNayal
```

## C#

```
// C# program to Check if a large number
// is divisible by 2, 3 and 5 or not.
using System;

class GFG
{
// function to return sum of digits
// of a number
static int SumOfDigits(String str,
                       int n)
{
    int sum = 0;

    for (int i = 0; i < n; i++)
        sum += (int)(str[i] - '0');

    return sum;
}

// function to Check if a large number
// is divisible by 2, 3 and 5 or not
static bool Divisible(String str, int n)
{
    if (SumOfDigits(str, n) % 3 == 0 &&
                    str[n - 1] == '0')
        return true;

    return false;
}

// Driver code
public static void Main()
{
    String str = "263730746028908374890";

    int n = str.Length;

    if (Divisible(str, n))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Check if a large number
// is divisible by 2, 3 and 5 or not.

// function to return sum of digits
// of a number
function SumOfDigits($str, $n)
{
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
        $sum += (int)($str[$i] - '0');

    return $sum;
}

// function to Check if a large number
// is divisible by 2, 3 and 5 or not
function Divisible($str, $n)
{
    if (SumOfDigits($str, $n) % 3 == 0 and
                    $str[$n - 1] == '0')
        return true;

    return false;
}

// Driver code
$str = "263730746028908374890";

$n = strlen($str);

if (Divisible($str, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript program to Check if a large
// number is divisible by 2, 3 and
// 5 or not.

// Function to return sum of
// digits of a number
function SumOfDigits(str, n)
{
    var sum = 0;

    for(var i = 0; i < n; i++)
        sum += (str.charAt(i) - '0');

    return sum;
}

// Function to Check if a large number
// is divisible by 2, 3 and 5 or not
function Divisible(str, n)
{
    if (SumOfDigits(str, n) % 3 == 0 &&
        str.charAt(n - 1) == '0')
        return true;

    return false;
}

// Driver code
var str = "263730746028908374890";
var n = str.length;

if (Divisible(str, n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
YES
```