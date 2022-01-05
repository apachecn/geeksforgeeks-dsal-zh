# 用最少的给定操作次数将 N 减少到 1

> 原文:[https://www . geesforgeks . org/reduce-n-to-1 最小给定操作数/](https://www.geeksforgeeks.org/reduce-n-to-1-with-minimum-number-of-given-operations/)

给定一个整数 **N** ，任务是通过以下两个操作将 **N** 减少到**1【T5:** 

1.  **1** 只有在数字大于 **0** 且结果数字没有任何前导**0**时，才能从数字的每个数字中减去。
2.  **1** 可以从数字本身减去。

任务是找到将 **N** 减少到 **1** 所需的此类操作的最小数量。
**例:**

> **输入:** N = 35
> **输出:**14
> 35->24->14->13->12->11->10->……->1(14 次运算)
> **输入:** N = 240
> **输出:** 23

**逼近:**可以观察到，如果数是 **10** 的幂，即 **N = 10 <sup>p</sup>** 那么运算数就是**(10 * p)–1**。例如，如果 **N = 10 <sup>2</sup>** ，那么操作将是**(10 * 2)–2 = 19**
即**100->99->88->77->……->33->22->11->10->9->
现在，任务是首先用给定的操作将给定的转换成 **10** 的幂，然后计算将 **10** 的幂减少到 **1** 所需的操作次数。这些操作的总和就是所需的答案。将一个数转换为的幂所需的运算次数将是**最大值(第一个 _ 数字–1，第二个 _ 数字，第三个 _ 数字，…，最后一个 _ 数字)**，这是因为每个数字都可以减少到 0，但第一个数字必须是 1，才能是相同位数的 **10** 的幂。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// given operations required to reduce n to 1
long long int minOperations(long long int n)
{
    // To store the count of operations
    long long int count = 0;

    // To store the digit
    long long int d = 0;

    // If n is already then no
    // operation is required
    if (n == 1)
        return 0;

    // Extract all the digits except
    // the first digit
    while (n > 9) {

        // Store the maximum of that digits
        d = max(n % 10, d);
        n /= 10;

        // for each digit
        count += 10;
    }

    // First digit
    d = max(d, n - 1);

    // Add the value to count
    count += abs(d);

    return count - 1;
}

// Driver code
int main()
{
    long long int n = 240;

    cout << minOperations(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimum number of
    // given operations required to reduce n to 1
    static long minOperations(long n)
    {
        // To store the count of operations
        long count = 0;

        // To store the digit
        long d = 0;

        // If n is already then no
        // operation is required
        if (n == 1)
            return 0;

        // Extract all the digits except
        // the first digit
        while (n > 9)
        {

            // Store the maximum of that digits
            d = Math.max(n % 10, d);
            n /= 10;

            // for each digit
            count += 10;
        }

        // First digit
        d = Math.max(d, n - 1);

        // Add the value to count
        count += Math.abs(d);

        return count - 1;
    }

    // Driver code
    public static void main (String[] args)
    {
        long n = 240;

        System.out.println(minOperations(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number of
# given operations required to reduce n to 1
def minOperations(n):

    # To store the count of operations
    count = 0

    # To store the digit
    d = 0

    # If n is already then no
    # operation is required
    if (n == 1):
        return 0

    # Extract all the digits except
    # the first digit
    while (n > 9):

        # Store the maximum of that digits
        d = max(n % 10, d)
        n //= 10

        # for each digit
        count += 10

    # First digit
    d = max(d, n - 1)

    # Add the value to count
    count += abs(d)

    return count - 1

# Driver code
if __name__ == '__main__':

    n = 240

    print(minOperations(n))

# This code is contributed by ashutosh450
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum number of
    // given operations required to reduce n to 1
    static long minOperations(long n)
    {
        // To store the count of operations
        long count = 0;

        // To store the digit
        long d = 0;

        // If n is already then no
        // operation is required
        if (n == 1)
            return 0;

        // Extract all the digits except
        // the first digit
        while (n > 9)
        {

            // Store the maximum of that digits
            d = Math.Max(n % 10, d);
            n /= 10;

            // for each digit
            count += 10;
        }

        // First digit
        d = Math.Max(d, n - 1);

        // Add the value to count
        count += Math.Abs(d);

        return count - 1;
    }

    // Driver code
    public static void Main (String[] args)
    {
        long n = 240;

        Console.WriteLine(minOperations(n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum number of
// given operations required to reduce n to 1
function minOperations( n)
{
    // To store the count of operations
    var count = 0;

    // To store the digit
    var d = 0;

    // If n is already then no
    // operation is required
    if (n == 1)
        return 0;

    // Extract all the digits except
    // the first digit
    while (n > 9) {

        // Store the maximum of that digits
        d = Math.max(n % 10, d);
        n /= 10;

        // for each digit
        count += 10;
    }

    // First digit
    d = Math.max(d, n - 1);

    // Add the value to count
    count += Math.abs(d);

    return count - 1;
}

var n = 240;
document.write(minOperations(n));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
23
```