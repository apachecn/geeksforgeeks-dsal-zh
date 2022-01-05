# 两个数除法小数点前的位数

> 原文:[https://www . geesforgeks . org/两位数除法小数点前位数/](https://www.geeksforgeeks.org/number-of-digits-before-the-decimal-point-in-the-division-of-two-numbers/)

给定两个整数 **a** 和 **b** 。任务是在 **a / b** 中找到小数点前的位数。
**举例:**

> **输入:** a = 100，b = 4
> **输出:** 2
> 100 / 4 = 25，25 中的位数= 2。
> **输入:** a = 100000，b = 10
> **输出:** 5

**天真的做法**:将两个数相除，然后求除法中的位数。取除法的绝对值求位数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of digits
// before the decimal in a / b
int countDigits(int a, int b)
{
    int count = 0;

    // Absolute value of a / b
    int p = abs(a / b);

    // If result is 0
    if (p == 0)
        return 1;

    // Count number of digits in the result
    while (p > 0) {
        count++;
        p = p / 10;
    }

    // Return the required count of digits
    return count;
}

// Driver code
int main()
{
    int a = 100;
    int b = 10;
    cout << countDigits(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the number of digits
    // before the decimal in a / b
    static int countDigits(int a, int b)
    {
        int count = 0;

        // Absolute value of a / b
        int p = Math.abs(a / b);

        // If result is 0
        if (p == 0)
            return 1;

        // Count number of digits in the result
        while (p > 0) {
            count++;
            p = p / 10;
        }

        // Return the required count of digits
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int a = 100;
        int b = 10;
        System.out.print(countDigits(a, b));
    }
}
```

## 计算机编程语言

```
# Python 3 implementation of the approach

# Function to return the number of digits
# before the decimal in a / b
def countDigits(a, b):
    count = 0

    # Absolute value of a / b
    p = abs(a // b)

    # If result is 0
    if (p == 0):
        return 1

    # Count number of digits in the result
    while (p > 0):
        count = count + 1
        p = p // 10

    # Return the required count of digits
    return count

# Driver code
a = 100
b = 10
print(countDigits(a, b))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the number of digits
    // before the decimal in a / b
    static int countDigits(int a, int b)
    {
        int count = 0;

        // Absolute value of a / b
        int p = Math.Abs(a / b);

        // If result is 0
        if (p == 0)
            return 1;

        // Count number of digits in the result
        while (p > 0) {
            count++;
            p = p / 10;
        }

        // Return the required count of digits
        return count;
    }

    // Driver code
    public static void Main()
    {
        int a = 100;
        int b = 10;
        Console.Write(countDigits(a, b));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of digits
// before the decimal in a / b
function countDigits($a, $b)
{
    $count = 0;

    // Absolute value of a / b
    $p = abs($a / $b);

    // If result is 0
    if ($p == 0)
        return 1;

    // Count number of digits in the result
    while ($p > 0) {
        $count++;
        $p = (int)($p / 10);
    }

    // Return the required count of digits
    return $count;
}

// Driver code
$a = 100;
$b = 10;
echo countDigits($a, $b);
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the number of digits
// before the decimal in a / b
function countDigits(a, b)
{
    var count = 0;

    // Absolute value of a / b
    var p = Math.abs(parseInt(a / b));

    // If result is 0
    if (p == 0)
        return 1;

    // Count number of digits in the result
    while (p > 0) {
        count++;
        p = parseInt(p / 10);
    }

    // Return the required count of digits
    return count;
}

// Driver code
var a = 100;
var b = 10;
document.write(countDigits(a, b));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```

**有效方法:**要计算 **a / b** 中的位数，我们可以使用公式:

> **楼层(原木<sub>10</sub>(a)–原木 <sub>10</sub> (b)) + 1**

这里两个数字都必须是正整数。为此我们可以取 **a** 和 **b** 的绝对值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of digits
// before the decimal in a / b
int countDigits(int a, int b)
{
    // Return the required count of digits
    return floor(log10(abs(a)) - log10(abs(b))) + 1;
}

// Driver code
int main()
{
    int a = 100;
    int b = 10;
    cout << countDigits(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the number of digits
    // before the decimal in a / b
    public static int countDigits(int a, int b)
    {
        double digits = Math.log10(Math.abs(a))
                        - Math.log10(Math.abs(b)) + 1;

        // Return the required count of digits
        return (int)Math.floor(digits);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 100;
        int b = 10;
        System.out.print(countDigits(a, b));
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach
import math

# Function to return the number of digits
# before the decimal in a / b
def countDigits(a, b):

    # Return the required count of digits    
    return math.floor(math.log10(abs(a)) -
                math.log10(abs(b))) + 1

# Driver code
a = 100
b = 10
print(countDigits(a, b))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the number of digits
    // before the decimal in a / b
    public static int countDigits(int a, int b)
    {
        double digits = Math.Log10(Math.Abs(a))
                        - Math.Log10(Math.Abs(b)) + 1;

        // Return the required count of digits
        return (int)Math.Floor(digits);
    }

    // Driver code
    static void Main()
    {
        int a = 100;
        int b = 10;
        Console.Write(countDigits(a, b));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of digits
// before the decimal in a / b
function countDigits($a, $b)
{

    // Return the required count of digits
    return floor(log10(abs($a)) -
                log10(abs($b))) + 1;
}

// Driver code
$a = 100;
$b = 10;
echo countDigits($a, $b);
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of digits
// before the decimal in a / b
function countDigits(a, b)
{
    // Return the required count of digits
    return Math.floor((Math.log(Math.abs(a))/Math.log(10)) - (Math.log(Math.abs(b))/Math.log(10))) + 1;
}

// Driver code
var a = 100;
var b = 10;
document.write(countDigits(a, b));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```