# 完美立方体串

> 原文:[https://www.geeksforgeeks.org/perfect-cube-string/](https://www.geeksforgeeks.org/perfect-cube-string/)

给定一个字符串 **str** ，任务是检查这个字符串中所有字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)之和是否是一个完美的立方体。

**示例:**

```
Input: str = "ll"
Output: Yes
ASCII value of l = 108
Therefore, sum of ASCII values = 108 + 108 = 216
which is a perfect cube 6 (6 * 6 * 6 = 216)

Input: str = "a"
Output: No
ASCII value of a = 97
Therefore, sum of ASCII values = 97
which is not a perfect cube
```

**算法**

*   对于字符串中的每个字符，找出其 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)
*   计算所有字符的 ASCII 值之和
*   检查这个和是否是[完美立方体](https://www.geeksforgeeks.org/tag/maths-perfect-cube/)。
*   如果总和是一个完美的立方体，则打印“是”，否则打印“否”

下面是上述方法的实现:

## C++

```
// C++ program to find if string is a
// perfect cube or not.

#include <bits/stdc++.h>
using namespace std;

bool isPerfectCubeString(string str)
{
    int sum = 0;

    // Finding ASCII values of each
    // character and finding its sum
    for (int i = 0; i < str.length(); i++)
        sum += (int)str[i];

    // Find the cube root of sum
    long double cr = round(cbrt(sum));

    // Check if sum is a perfect cube
    return (cr * cr * cr == sum);
}

// Driver code
int main()
{
    string str = "ll";

    if (isPerfectCubeString(str))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if String is a
// perfect cube or not.
import java.util.*;

class GFG{

static boolean isPerfectCubeString(String str)
{
    int sum = 0;

    // Finding ASCII values of each
    // character and finding its sum
    for (int i = 0; i < str.length(); i++)
        sum += (int)str.charAt(i);

    // Find the cube root of sum
    double cr = Math.round(Math.cbrt(sum));

    // Check if sum is a perfect cube
    return (cr * cr * cr == sum);
}

// Driver code
public static void main(String[] args)
{
    String str = "ll";

    if (isPerfectCubeString(str))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find if str1ing is a
# perfect cube or not.
from math import ceil

def isPerfectCubeString(str1):
    sum = 0

    # Finding ASCII values of each
    # character and finding its sum
    for i in range(len(str1)):
        sum += ord(str1[i])

    # Find the cube root of sum
    cr = ceil((sum)**(1/3))

    # Check if sum is a perfect cube
    return (cr * cr * cr == sum)

# Driver code
str1 = "ll"

if (isPerfectCubeString(str1)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find if String is a
// perfect cube or not.
using System;

class GFG{

static bool isPerfectCubeString(String str)
{
    int sum = 0;

    // Finding ASCII values of each
    // character and finding its sum
    for (int i = 0; i < str.Length; i++)
        sum += (int)str[i];

    // Find the cube root of sum
    double cr = Math.Round(Math.Pow(sum, (double) 1 / 3));

    // Check if sum is a perfect cube
    return (cr * cr * cr == sum);
}

// Driver code
public static void Main(String[] args)
{
    String str = "ll";

    if (isPerfectCubeString(str))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find if string
// is a perfect cube or not.
function isPerfectCubeString(str)
{
    var sum = 0;

    // Finding ASCII values of each
    // character and finding its sum
    for(var i = 0; i < str.length; i++)
    {
        sum += str.charCodeAt(i);
    }

    // Find the cube root of sum
    var cr = Math.round(Math.cbrt(sum));

    // Check if sum is a perfect cube
    return cr * cr * cr == sum;
}

// Driver code
var str = "ll";

if (isPerfectCubeString(str))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rdtank

</script>
```

**Output:** 

```
Yes
```