# 数列 1、2、4、3、5、7、9、6、8、10、11、13 的和..直到第 N 个学期

> 原文:[https://www . geeksforgeeks . org/series-sum-1-2-4-3-5-7-9-6-8-10-11-13-thill-n-term/](https://www.geeksforgeeks.org/sum-of-the-series-1-2-4-3-5-7-9-6-8-10-11-13-till-n-th-term/)

给定一系列数字 **1、2、4、3、5、7、9、6、8、10、11、13……**任务是找到所有系列数字的和，直到**第 N 个**数字。
**例:**

> **输入:** N = 4
> **输出:** 10
> 1 + 2 + 4 + 3 = 10
> **输入:** N = 10
> **输出:** 55

**趋近**:系列基本上是 2 <sup>0</sup> 奇数，2 <sup>1</sup> 偶数，2 <sup>2</sup> 偶数。前 N 个奇数之和为 **N * N** ，前 N 个偶数之和为 **(N * (N+1))** 。计算 2 个 <sup>i</sup> 奇数或偶数的总和，并不断将它们加到总和中。
每 2 的幂迭代一次，直到迭代次数超过 N，并根据奇偶性不断加奇数或偶数各自的和。对于每个段，该段的总和将为:**(X 个奇数/偶数的当前总和–Y 个奇数/偶数的先前总和)**，其中 X 是直到该段的奇数/偶数的总和，Y 是直到奇数/偶数出现的先前的奇数/偶数的总和。
以下是上述方法的实施:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// sum of first N odd numbers
int sumodd(int n)
{
    return (n * n);
}

// Function to find the
// sum of first N even numbers
int sumeven(int n)
{
    return (n * (n + 1));
}

// Function to overall
// find the sum of series
int findSum(int num)
{

    // Initial odd numbers
    int sumo = 0;

    // Initial even numbers
    int sume = 0;

    // First power of 2
    int x = 1;

    // Check for parity
    // for odd/even
    int cur = 0;

    // Counts the sum
    int ans = 0;
    while (num > 0) {

        // Get the minimum
        // out of remaining num
        // or power of 2
        int inc = min(x, num);

        // Decrease that much numbers
        // from num
        num -= inc;

        // If the segment has odd numbers
        if (cur == 0) {

            // Summate the odd numbers
            // By exclusion
            ans = ans + sumodd(sumo + inc) - sumodd(sumo);

            // Increase number of odd numbers
            sumo += inc;
        }
        // If the segment has even numbers
        else {

            // Summate the even numbers
            // By exclusion
            ans = ans + sumeven(sume + inc) - sumeven(sume);

            // Increase number of even numbers
            sume += inc;
        }

        // Next set of numbers
        x *= 2;

        // Change parity for odd/even
        cur ^= 1;
    }

    return ans;
}

// Driver code
int main()
{
    int n = 4;
    cout << findSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

class GFG
{

    // Function to find the
    // sum of first N odd numbers
    static int sumodd(int n)
    {
        return (n * n);
    }

    // Function to find the
    // sum of first N even numbers
    static int sumeven(int n)
    {
        return (n * (n + 1));
    }

    // Function to overall
    // find the sum of series
    static int findSum(int num)
    {

        // Initial odd numbers
        int sumo = 0;

        // Initial even numbers
        int sume = 0;

        // First power of 2
        int x = 1;

        // Check for parity
        // for odd/even
        int cur = 0;

        // Counts the sum
        int ans = 0;
        while (num > 0)
        {

            // Get the minimum
            // out of remaining num
            // or power of 2
            int inc = Math.min(x, num);

            // Decrease that much numbers
            // from num
            num -= inc;

            // If the segment has odd numbers
            if (cur == 0)
            {

                // Summate the odd numbers
                // By exclusion
                ans = ans + sumodd(sumo + inc) - sumodd(sumo);

                // Increase number of odd numbers
                sumo += inc;
            }

            // If the segment has even numbers
            else
            {

                // Summate the even numbers
                // By exclusion
                ans = ans + sumeven(sume + inc) - sumeven(sume);

                // Increase number of even numbers
                sume += inc;
            }

            // Next set of numbers
            x *= 2;

            // Change parity for odd/even
            cur ^= 1;
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        System.out.println(findSum(n));

    }
}

// This code contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python3 program to implement
# the above approach

# Function to find the
# sum of first N odd numbers
def sumodd(n):

    return (n * n)

# Function to find the
# sum of first N even numbers
def sumeven(n):

    return (n * (n + 1))

# Function to overall
# find the sum of series
def findSum(num):

    # Initial odd numbers
    sumo = 0

    # Initial even numbers
    sume = 0

    # First power of 2
    x = 1

    # Check for parity
    # for odd/even
    cur = 0

    # Counts the sum
    ans = 0
    while (num > 0):

        # Get the minimum
        # out of remaining num
        # or power of 2
        inc = min(x, num)

        # Decrease that much numbers
        # from num
        num -= inc

        # If the segment has odd numbers
        if (cur == 0):

            # Summate the odd numbers
            # By exclusion
            ans = ans + sumodd(sumo + inc) - sumodd(sumo)

            # Increase number of odd numbers
            sumo += inc

        # If the segment has even numbers
        else:

            # Summate the even numbers
            # By exclusion
            ans = ans + sumeven(sume + inc) - sumeven(sume)

            # Increase number of even numbers
            sume += inc

        # Next set of numbers
        x *= 2

        # Change parity for odd/even
        cur ^= 1

    return ans

# Driver code
n = 4
print(findSum(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

    // Function to find the
    // sum of first N odd numbers
    static int sumodd(int n)
    {
        return (n * n);
    }

    // Function to find the
    // sum of first N even numbers
    static int sumeven(int n)
    {
        return (n * (n + 1));
    }

    // Function to overall
    // find the sum of series
    static int findSum(int num)
    {

        // Initial odd numbers
        int sumo = 0;

        // Initial even numbers
        int sume = 0;

        // First power of 2
        int x = 1;

        // Check for parity
        // for odd/even
        int cur = 0;

        // Counts the sum
        int ans = 0;
        while (num > 0)
        {

            // Get the minimum
            // out of remaining num
            // or power of 2
            int inc = Math.Min(x, num);

            // Decrease that much numbers
            // from num
            num -= inc;

            // If the segment has odd numbers
            if (cur == 0)
            {

                // Summate the odd numbers
                // By exclusion
                ans = ans + sumodd(sumo + inc) - sumodd(sumo);

                // Increase number of odd numbers
                sumo += inc;
            }

            // If the segment has even numbers
            else
            {

                // Summate the even numbers
                // By exclusion
                ans = ans + sumeven(sume + inc) - sumeven(sume);

                // Increase number of even numbers
                sume += inc;
            }

            // Next set of numbers
            x *= 2;

            // Change parity for odd/even
            cur ^= 1;
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 4;
        Console.WriteLine(findSum(n));

    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function to find the
// sum of first N odd numbers
function sumodd($n)
{
    return ($n * $n);
}

// Function to find the
// sum of first N even numbers
function sumeven($n)
{
    return ($n * ($n + 1));
}

// Function to overall
// find the sum of series
function findSum( $num)
{

    // Initial odd numbers
    $sumo = 0;

    // Initial even numbers
    $sume = 0;

    // First power of 2
    $x = 1;

    // Check for parity
    // for odd/even
    $cur = 0;

    // Counts the sum
    $ans = 0;
    while ($num > 0)
    {

        // Get the minimum
        // out of remaining num
        // or power of 2
        $inc = min($x, $num);

        // Decrease that much numbers
        // from num
        $num -= $inc;

        // If the segment has odd numbers
        if ($cur == 0)
        {

            // Summate the odd numbers
            // By exclusion
            $ans = $ans + sumodd($sumo + $inc) -
                          sumodd($sumo);

            // Increase number of odd numbers
            $sumo += $inc;
        }

        // If the segment has even numbers
        else
        {

            // Summate the even numbers
            // By exclusion
            $ans = $ans + sumeven($sume + $inc) -
                          sumeven($sume);

            // Increase number of even numbers
            $sume += $inc;
        }

        // Next set of numbers
        $x *= 2;

        // Change parity for odd/even
        $cur ^= 1;
    }

    return $ans;
}

// Driver code
$n = 4;
echo findSum($n);

// This code contributed by princiraj1992
?>
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to find the
// sum of first N odd numbers
function sumodd( n)
{
    return (n * n);
}

// Function to find the
// sum of first N even numbers
function sumeven( n)
{
    return (n * (n + 1));
}

// Function to overall
// find the sum of series
function findSum( num)
{

    // Initial odd numbers
    let sumo = 0;

    // Initial even numbers
    let sume = 0;

    // First power of 2
    let x = 1;

    // Check for parity
    // for odd/even
    let cur = 0;

    // Counts the sum
    let ans = 0;
    while (num > 0) {

        // Get the minimum
        // out of remaining num
        // or power of 2
        let inc = Math.min(x, num);

        // Decrease that much numbers
        // from num
        num -= inc;

        // If the segment has odd numbers
        if (cur == 0) {

            // Summate the odd numbers
            // By exclusion
            ans = ans + sumodd(sumo + inc) - sumodd(sumo);

            // Increase number of odd numbers
            sumo += inc;
        }
        // If the segment has even numbers
        else {

            // Summate the even numbers
            // By exclusion
            ans = ans + sumeven(sume + inc) - sumeven(sume);

            // Increase number of even numbers
            sume += inc;
        }

        // Next set of numbers
        x *= 2;

        // Change parity for odd/even
        cur ^= 1;
    }

    return ans;
}

// Driver code

    let n = 4;
    document.write( findSum(n));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
10
```