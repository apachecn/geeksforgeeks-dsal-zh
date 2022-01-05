# 计算给定年数中奇数天数的程序

> 原文:[https://www . geesforgeks . org/计算给定年数中奇数天数的程序/](https://www.geeksforgeeks.org/program-to-calculate-the-number-of-odd-days-in-given-number-of-years/)

给定一个整数 **N** ，任务是找出年内从 **1** 到 **N** 的奇数天数。
**奇数天:**奇数天的数量是指某一年中剩余的天数转换为周数。比方说，一个普通年有 365 天，也就是 52 周零一天。这意味着，在一年的 365 天中，364 天将被转换为 52 周，剩下一天。这一天被称为 1 天。

*   简单地将总天数除以 7(一周中的天数)得到奇数天的数量。
*   它的值只在 0 到 6 之间。[0, 6]
*   闰年:每年可以被 400 或 4 整除，但不能被 100 整除
*   普通年份:闰年以外的年份
*   每一个平凡的一年都有一个奇怪的日子。
*   每个闰年都有两天。

**例:**

> **输入:** N = 8
> **输出:**3
> 8 年中，只有 4 年和 8 年是闰年。
> (6×1)+(2×2)= 10 即 1 周 3 天
> **输入:** N = 400
> **输出:** 0

**进场:**

1.  计算给定 N 年中的普通年数和闰年数。
2.  计算总天数。
3.  打印总天数的模(7)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count of odd days
int oddDays(int N)
{

    // Count of years divisible
    // by 100 and 400
    int hund1 = N / 100;
    int hund4 = N / 400;

    // Every 4th year is a leap year
    int leap = N >> 2;
    int ord = N - leap;

    // Every 100th year is divisible by 4
    // but is not a leap year
    if (hund1) {
        ord += hund1;
        leap -= hund1;
    }

    // Every 400th year is divisible by 100
    // but is a leap year
    if (hund4) {
        ord -= hund4;
        leap += hund4;
    }

    // Total number of extra days
    int days = ord + leap * 2;

    // modulo(7) for final answer
    int odd = days % 7;

    return odd;
}

// Driver code
int main()
{

    // Number of days
    int N = 100;
    cout << oddDays(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of odd days
    static int oddDays(int N)
    {
        // Count of years divisible
        // by 100 and 400
        int hund1 = N / 100;
        int hund4 = N / 400;

        // Every 4th year is a leap year
        int leap = N >> 2;
        int ord = N - leap;

        // Every 100th year is divisible by 4
        // but is not a leap year
        if (hund1 > 0) {
            ord += hund1;
            leap -= hund1;
        }

        // Every 400th year is divisible by 100
        // but is a leap year
        if (hund4 > 0) {
            ord -= hund4;
            leap += hund4;
        }

        // Total number of extra days
        int days = ord + leap * 2;

        // modulo(7) for final answer
        int odd = days % 7;

        return odd;
    }

    // Driver code
    public static void main(String args[])
    {

        // Number of days
        int N = 100;
        System.out.print(oddDays(N));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of odd days
def oddDays(N):

    # Count of years divisible
    # by 100 and 400
    hund1 = N // 100
    hund4 = N // 400

    # Every 4th year is a leap year
    leap = N >> 2
    ordd = N - leap

    # Every 100th year is divisible by 4
    # but is not a leap year
    if (hund1):
        ordd += hund1
        leap -= hund1

    # Every 400th year is divisible by 100
    # but is a leap year
    if (hund4):
        ordd -= hund4
        leap += hund4

    # Total number of extra days
    days = ordd + leap * 2

    # modulo(7) for final answer
    odd = days % 7

    return odd

# Driver code

# Number of days
N = 100
print(oddDays(N))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of odd days
    static int oddDays(int N)
    {
        // Count of years divisible
        // by 100 and 400
        int hund1 = N / 100;
        int hund4 = N / 400;

        // Every 4th year is a leap year
        int leap = N >> 2;
        int ord = N - leap;

        // Every 100th year is divisible by 4
        // but is not a leap year
        if (hund1 > 0)
        {
            ord += hund1;
            leap -= hund1;
        }

        // Every 400th year is divisible by 100
        // but is a leap year
        if (hund4 > 0)
        {
            ord -= hund4;
            leap += hund4;
        }

        // Total number of extra days
        int days = ord + leap * 2;

        // modulo(7) for final answer
        int odd = days % 7;

        return odd;
    }

    // Driver code
    static void Main()
    {

        // Number of days
        int N = 100;
        Console.WriteLine(oddDays(N));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of odd days
function oddDays($N)
{

    // Count of years divisible
    // by 100 and 400
    $hund1 = floor($N / 100);
    $hund4 = floor($N / 400);

    // Every 4th year is a leap year
    $leap = $N >> 2;
    $ord = $N - $leap;

    // Every 100th year is divisible by 4
    // but is not a leap year
    if ($hund1)
    {
        $ord += $hund1;
        $leap -= $hund1;
    }

    // Every 400th year is divisible by 100
    // but is a leap year
    if ($hund4)
    {
        $ord -= $hund4;
        $leap += $hund4;
    }

    // Total number of extra days
    $days = $ord + $leap * 2;

    // modulo(7) for final answer
    $odd = $days % 7;

    return $odd;
}

// Driver code

// Number of days
$N = 100;

echo oddDays($N);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach   

// Function to return the count of odd days
    function oddDays(N) {
        // Count of years divisible
        // by 100 and 400
        var hund1 = N / 100;
        var hund4 = N / 400;

        // Every 4th year is a leap year
        var leap = N >> 2;
        var ord = N - leap;

        // Every 100th year is divisible by 4
        // but is not a leap year
        if (hund1 > 0) {
            ord += hund1;
            leap -= hund1;
        }

        // Every 400th year is divisible by 100
        // but is a leap year
        if (hund4 > 0) {
            ord -= hund4;
            leap += hund4;
        }

        // Total number of extra days
        var days = ord + leap * 2;

        // modulo(7) for final answer
        var odd = days % 7;

        return odd;
    }

    // Driver code

        // Number of days
        var N = 100;
        document.write(oddDays(N).toFixed());

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
5
```