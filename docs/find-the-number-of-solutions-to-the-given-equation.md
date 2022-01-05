# 求给定方程的解的个数

> 原文:[https://www . geesforgeks . org/find-给定方程的解的数量/](https://www.geeksforgeeks.org/find-the-number-of-solutions-to-the-given-equation/)

给定三个整数 **A** 、 **B** 和 **C** ，任务是求 **X** 的计数值，使得满足以下条件，
**X = B * Sm(X)<sup>A</sup>+C**其中 **Sm(X)** 表示 X 和**1<X<14 的**位数之和
**例:****** 

> **输入:** A = 3，B = 2，C = 8
> **输出:** 3
> 为 **X = 10** ，2 * (1) <sup>3</sup> + 8 = 10
> 为 **X = 2008** ，2 * (10) <sup>3</sup> + 8 = 2008
> 为 **X = 13726**

**方法:**这里可以做一个重要的观察，位数之和可以是 atmost 81(即 X = 999999999)，对应每个位数之和，我们得到一个单值 **X** 。所以我们可以迭代每个数字的和，检查 **X** 的结果值是否有效。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// valid values of X
int getCount(int a, int b, int c)
{
    int count = 0;

    // Iterate through all possible
    // sum of digits of X
    for (int i = 1; i <= 81; i++) {

        // Get current value of X for sum of digits i
        int cr = b * pow(i, a) + c;

        int tmp = cr;
        int sm = 0;

        // Find sum of digits of cr
        while (tmp) {
            sm += tmp % 10;
            tmp /= 10;
        }

        // If cr is a valid choice for X
        if (sm == i && cr < 1e9)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
int main()
{
    int a = 3, b = 2, c = 8;
    cout << getCount(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to return the count of
// valid values of X
static int getCount(int a, int b, int c)
{
    int count = 0;

    // Iterate through all possible
    // sum of digits of X
    for (int i = 1; i <= 81; i++)
    {

        // Get current value of X for sum of digits i
        int cr = b * (int)Math.pow(i, a) + c;

        int tmp = cr;
        int sm = 0;

        // Find sum of digits of cr
        while (tmp != 0)
        {
            sm += tmp % 10;
            tmp /= 10;
        }

        // If cr is a valid choice for X
        if (sm == i && cr < 1e9)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int a = 3, b = 2, c = 8;
    System.out.println(getCount(a, b, c));
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# valid values of X
def getCount(a, b, c):

    count = 0

    # Iterate through all possible
    # sum of digits of X
    for i in range(1, 82):

        # Get current value of X for
        # sum of digits i
        cr = b * pow(i, a) + c

        tmp = cr
        sm = 0

        # Find sum of digits of cr
        while (tmp):
            sm += tmp % 10
            tmp //= 10

        # If cr is a valid choice for X
        if (sm == i and cr < 10**9):
            count += 1

    # Return the count
    return count

# Driver code
a, b, c = 3, 2, 8
print(getCount(a, b, c))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// valid values of X
static int getCount(int a, int b, int c)
{
    int count = 0;

    // Iterate through all possible
    // sum of digits of X
    for (int i = 1; i <= 81; i++)
    {

        // Get current value of X for sum
        // of digits i
        int cr = b * (int)Math.Pow(i, a) + c;

        int tmp = cr;
        int sm = 0;

        // Find sum of digits of cr
        while (tmp != 0)
        {
            sm += tmp % 10;
            tmp /= 10;
        }

        // If cr is a valid choice for X
        if (sm == i && cr < 1e9)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
public static void Main()
{
    int a = 3, b = 2, c = 8;
    Console.Write(getCount(a, b, c));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// valid values of X
function getCount($a, $b, $c)
{
    $count = 0;

    // Iterate through all possible
    // sum of digits of X
    for ($i = 1; $i <= 81; $i++)
    {

        // Get current value of X for sum of digits i
        $cr = $b * (int)pow($i, $a) + $c;

        $tmp = $cr;
        $sm = 0;

        // Find sum of digits of cr
        while ($tmp != 0)
        {
            $sm += $tmp % 10;
            $tmp /= 10;
        }

        // If cr is a valid choice for X
        if ($sm == $i && $cr < 1e9)
            $count++;
    }

    // Return the count
    return $count;
}

// Driver code
{
    $a = 3; $b = 2;$c = 8;
    echo(getCount($a, $b, $c));
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the count of
// valid values of X
function getCount(a, b, c)
{
    let count = 0;

    // Iterate through all possible
    // sum of digits of X
    for (let i = 1; i <= 81; i++)
    {

        // Get current value of X for sum of digits i
        let cr = b * Math.pow(i, a) + c;

        let tmp = cr;
        let sm = 0;

        // Find sum of digits of cr
        while (tmp != 0)
        {
            sm += tmp % 10;
            tmp = Math.floor(tmp / 10);
        }

        // If cr is a valid choice for X
        if (sm == i && cr < 1e9)
            count++;
    }

    // Return the count
    return count;
}

// driver program

    let a = 3, b = 2, c = 8;
    document.write(getCount(a, b, c));

</script>
```

**Output:** 

```
3
```