# 按照给定的约束

构建二进制字符串

> 原文:[https://www . geeksforgeeks . org/construct-a-binary-string-follow-the-given-constraints/](https://www.geeksforgeeks.org/construct-a-binary-string-following-the-given-constraints/)

给定三个整数 **A** 、 **B** 和 **X** 。任务是构建一个二进制字符串 **str** ，其具有精确的 **A** 数量的**0**和 **B** 数量的**1**，前提是必须至少有 **X** 个索引，使得 **str[i]！= str[i+1]** 。输入是这样的，总是有一个有效的解决方案。
**例:**

> **输入:** A = 2，B = 2，X = 1
> **输出:** 1100
> 有两个 0 和两个 1 和一个(=X)索引这样 s[i]！= s[i+1](即 i = 1)
> **输入:** A = 4，B = 3，X = 2
> **输出:** 0111000

**进场:**

*   将 **x** 除以 **2** ，并将其存储在变量 **d** 中。
*   检查 **d** 是否为**甚至**和 **d / 2！= a** ，如果条件为真，则打印 **0** 并将 **d** 和 **a** 减少 **1** 。
*   从 **1 循环到 d** 并打印 **10** ，最后更新**a = a–d**和**b = b–d**。
*   最后根据 **a** 和 **b** 的值打印剩余的**0**和**1**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to print a binary string which has
// 'a' number of 0's, 'b' number of 1's and there are
// at least 'x' indices such that s[i] != s[i+1]
int constructBinString(int a, int b, int x)
{
    int d, i;

    // Divide index value by 2 and store
    // it into d
    d = x / 2;

    // If index value x is even and
    // x/2 is not equal to a
    if (x % 2 == 0 && x / 2 != a) {
        d--;
        cout << 0;
        a--;
    }

    // Loop for d for each d print 10
    for (i = 0; i < d; i++)
        cout << "10";

    // subtract d from a and b
    a = a - d;
    b = b - d;

    // Loop for b to print remaining 1's
    for (i = 0; i < b; i++) {
        cout << "1";
    }

    // Loop for a to print remaining 0's
    for (i = 0; i < a; i++) {
        cout << "0";
    }
}

// Driver code
int main()
{
    int a = 4, b = 3, x = 2;
    constructBinString(a, b, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
// Function to print a binary string which has
// 'a' number of 0's, 'b' number of 1's and there are
// at least 'x' indices such that s[i] != s[i+1]
static void constructBinString(int a, int b, int x)
{
    int d, i;

    // Divide index value by 2 and store
    // it into d
    d = x / 2;

    // If index value x is even and
    // x/2 is not equal to a
    if (x % 2 == 0 && x / 2 != a)
    {
        d--;
        System.out.print("0");
        a--;
    }

    // Loop for d for each d print 10
    for (i = 0; i < d; i++)
        System.out.print("10");

    // subtract d from a and b
    a = a - d;
    b = b - d;

    // Loop for b to print remaining 1's
    for (i = 0; i < b; i++)
    {
        System.out.print("1");
    }

    // Loop for a to print remaining 0's
    for (i = 0; i < a; i++)
    {
        System.out.print("0");
    }
}

// Driver code
public static void main(String[] args)
{
    int a = 4, b = 3, x = 2;
    constructBinString(a, b, x);
}
}

// This code is contributed
// by Mukul Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print a binary string which
# has 'a' number of 0's, 'b' number of 1's
# and there are at least 'x' indices such
# that s[i] != s[i+1]
def constructBinString(a, b, x):

    # Divide index value by 2 and
    # store it into d
    d = x // 2

    # If index value x is even and
    # x/2 is not equal to a
    if x % 2 == 0 and x // 2 != a:
        d -= 1
        print("0", end = "")
        a -= 1

    # Loop for d for each d print 10
    for i in range(d):
        print("10", end = "")

    # subtract d from a and b
    a = a - d
    b = b - d

    # Loop for b to print remaining 1's
    for i in range(b):
        print("1", end = "")

    # Loop for a to print remaining 0's
    for i in range(a):
        print("0", end = "")

# Driver Code
if __name__ == "__main__":

    a, b, x = 4, 3, 2
    constructBinString(a, b, x)

# This code is contributed by Rituraj_Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function to print a binary string which has
// 'a' number of 0's, 'b' number of 1's and there are
// at least 'x' indices such that s[i] != s[i+1]
static void constructBinString(int a, int b, int x)
{
    int d, i;

    // Divide index value by 2 and store
    // it into d
    d = x / 2;

    // If index value x is even and
    // x/2 is not equal to a
    if (x % 2 == 0 && x / 2 != a)
    {
        d--;
        Console.Write("0");
        a--;
    }

    // Loop for d for each d print 10
    for (i = 0; i < d; i++)
        Console.Write("10");

    // subtract d from a and b
    a = a - d;
    b = b - d;

    // Loop for b to print remaining 1's
    for (i = 0; i < b; i++)
    {
        Console.Write("1");
    }

    // Loop for a to print remaining 0's
    for (i = 0; i < a; i++)
    {
        Console.Write("0");
    }
}

// Driver code
public static void Main()
{
    int a = 4, b = 3, x = 2;
    constructBinString(a, b, x);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to print a binary string
// which has 'a' number of 0's, 'b'
// number of 1's and there are at least
// 'x' indices such that s[i] != s[i+1]
function constructBinString($a, $b, $x)
{
    $d; $i;

    // Divide index value by 2
    // and store it into d
    $d = $x / 2;

    // If index value x is even and
    // x/2 is not equal to a
    if ($x % 2 == 0 && $x / 2 != $a)
    {
        $d--;
        echo 0;
        $a--;
    }

    // Loop for d for each d print 10
    for ($i = 0; $i < $d; $i++)
        echo "10";

    // subtract d from a and b
    $a = $a - $d;
    $b = $b - $d;

    // Loop for b to print remaining 1's
    for ($i = 0; $i < $b; $i++)
    {
        echo "1";
    }

    // Loop for a to print remaining 0's
    for ($i = 0; $i < $a; $i++)
    {
        echo "0";
    }
}

// Driver code
$a = 4;
$b = 3;
$x = 2;
constructBinString($a, $b, $x);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to print a binary string which has
    // 'a' number of 0's, 'b' number of 1's and there are
    // at least 'x' indices such that s[i] != s[i+1]
    function constructBinString(a, b, x)
    {
        let d, i;

        // Divide index value by 2 and store
        // it into d
        d = parseInt(x / 2, 10);

        // If index value x is even and
        // x/2 is not equal to a
        if (x % 2 == 0 && parseInt(x / 2, 10) != a)
        {
            d--;
            document.write("0");
            a--;
        }

        // Loop for d for each d print 10
        for (i = 0; i < d; i++)
            document.write("10");

        // subtract d from a and b
        a = a - d;
        b = b - d;

        // Loop for b to print remaining 1's
        for (i = 0; i < b; i++)
        {
            document.write("1");
        }

        // Loop for a to print remaining 0's
        for (i = 0; i < a; i++)
        {
            document.write("0");
        }
    }

    let a = 4, b = 3, x = 2;
    constructBinString(a, b, x);

</script>
```

**Output:** 

```
0111000
```

**时间复杂度:** O(最大值(a，b，x))

**辅助空间:** O(1)