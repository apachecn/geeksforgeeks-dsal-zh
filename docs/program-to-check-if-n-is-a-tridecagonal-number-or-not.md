# 检查 N 是否为三叉数的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-is-a-tridecagonal-number-or-not/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-tridecagonal-number-or-not/)

给定一个整数 **N** ，任务是检查它是否是一个[三叉戟号码](https://www.geeksforgeeks.org/tridecagonal-number/)。

> [**三叉戟编号**](https://www.geeksforgeeks.org/tridecagonal-number/) 是一个十三边多边形。前几个三叉戟数字是 1，13，36，70，115，171，…

**例:**

> **输入:** N = 13
> **输出:**是
> **说明:**
> 第二个三叉戟编号为 13。
> **输入:** N = 30
> **输出:**否

**进场:**

1.  三叉戟编号的第 K <sup>个</sup>项给出为
    ![K^{th} Term = \frac{11*K^{2} - 9*K}{2}   ](img/22e4f460e5b0219c9bf2d0f384db983d.png "Rendered by QuickLaTeX.com")

2.  因为我们必须检查给定的数是否可以表示为三叉戟数。这可以通过以下方式进行检查–

> => ![N = \frac{11*K^{2} - 9*K}{2}   ](img/9f78f4a2dda9c8e3c6e7185b4f83d37a.png "Rendered by QuickLaTeX.com")
> = > ![K = \frac{9 + \sqrt{88*N + 81}}{22}   ](img/958f3e67e5d66bedf0ad2ab6fb868480.png "Rendered by QuickLaTeX.com")

2.  最后，检查使用该公式计算的值是否为整数，这意味着 N 是一个三叉戟数。

以下是上述方法的实现:

## C++

```
// C++ implementation to check that
// a number is a Tridecagon number or not

#include <bits/stdc++.h>

using namespace std;

// Function to check that the
// number is a Tridecagon number
bool isTridecagon(int N)
{
    float n
        = (9 + sqrt(88 * N + 81))
          / 22;

    // Condition to check if the
    // number is a Tridecagon number
    return (n - (int)n) == 0;
}

// Driver Code
int main()
{
    int i = 13;

    // Function call
    if (isTridecagon(i)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check that a
// number is a tridecagon number or not
class GFG{

// Function to check that the
// number is a tridecagon number
static boolean isTridecagon(int N)
{
    float n = (float) ((9 + Math.sqrt(88 * N +
                                      81)) / 22);

    // Condition to check if the
    // number is a tridecagon number
    return (n - (int)n) == 0;
}

// Driver Code
public static void main(String[] args)
{
    int i = 13;

    // Function call
    if (isTridecagon(i))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to check that
# a number is a tridecagon number or not
import math

# Function to check that the
# number is a tridecagon number
def isTridecagon(N):

    n = (9 + math.sqrt(88 * N + 81)) / 22

    # Condition to check if the
    # number is a tridecagon number
    return (n - int(n)) == 0

# Driver Code
i = 13

# Function call
if (isTridecagon(i)):
    print("Yes")
else:
    print("No")

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to check that a
// number is a tridecagon number or not
using System;

class GFG{

// Function to check that the
// number is a tridecagon number
static bool isTridecagon(int N)
{
    float n = (float)((9 + Math.Sqrt(88 * N +
                                     81)) / 22);

    // Condition to check if the
    // number is a tridecagon number
    return (n - (int)n) == 0;
}

// Driver Code
public static void Main()
{
    int i = 13;

    // Function call
    if (isTridecagon(i))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript implementation to check that
// a number is a Tridecagon number or not

// Function to check that the
// number is a Tridecagon number
function isTridecagon(N)
{
    var n
        = (9 + Math.sqrt(88 * N + 81))
          / 22;

    // Condition to check if the
    // number is a Tridecagon number
    return (n - parseInt(n)) == 0;
}

// Driver Code
var i = 13;
// Function call
if (isTridecagon(i)) {
    document.write("Yes");
}
else {
    document.write("No");
}

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*