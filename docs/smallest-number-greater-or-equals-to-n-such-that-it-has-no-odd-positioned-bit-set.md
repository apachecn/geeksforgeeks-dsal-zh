# 大于或等于 N 的最小数字，因此它没有奇数位置的位组

> 原文:[https://www . geesforgeks . org/最小数字大于或等于 n 这样它就没有奇数位的位集/](https://www.geeksforgeeks.org/smallest-number-greater-or-equals-to-n-such-that-it-has-no-odd-positioned-bit-set/)

给定一个整数 **N** ，任务是找到最小的整数 **X** ，使其没有奇数位置集， **X ≥ N** 。
**注:**位的定位从右侧假设，第一位假设为 **0 <sup>第</sup>** 位。

**示例:**

> **输入:** N = 9
> **输出:** 16
> 16 的二进制表示为 10000，其第 4 位
> 设置为满足给定条件的最小可能数。
> **输入:** N = 5
> **输出:** 5
> **输入:** N = 19
> **输出:** 20

**方法:**这个问题可以使用贪婪方法和一些位属性来解决。如果取 2 的较小幂**恰好一次**并相加，它们永远不能超过 2 的较大幂(例如(1 + 2 + 4) < 8)。以下贪婪方法用于解决上述问题:

*   首先计算位数。
*   获取设置位最左边的索引。
*   如果最左边的设置位在奇数索引处，那么答案总是 **(1 < <(最左边 _ 位 _ 索引+ 1))** 。
*   否则，贪婪地通过将所有偶数位从 0 设置为最左边的 _bit_index 来形成一个数字。现在贪婪地从右边去掉二的幂，检查我们是否得到一个满足给定条件的数。
*   如果上面的条件没有给出我们的数字，那么我们只需设置下一个最左边的偶数位并返回答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the total bits
int countBits(int n)
{
    int count = 0;

    // Iterate and find the
    // number of set bits
    while (n) {
        count++;

        // Right shift the number by 1
        n >>= 1;
    }
    return count;
}

// Function to find the nearest number
int findNearestNumber(int n)
{

    // Count the total number of bits
    int cnt = countBits(n);

    // To get the position
    cnt -= 1;

    // If the last set bit is
    // at odd position then
    // answer will always be a number
    // with the left bit set
    if (cnt % 2) {
        return 1 << (cnt + 1);
    }

    else {

        int tempnum = 0;

        // Set all the even bits which
        // are possible
        for (int i = 0; i <= cnt; i += 2)
            tempnum += 1 << i;

        // If the number still is less than N
        if (tempnum < n) {

            // Return the number by setting the
            // next even set bit
            return (1 << (cnt + 2));
        }

        else if (tempnum == n)
            return n;

        // If we have reached this position
        // it means tempsum > n
        // hence turn off even bits to get the
        // first possible number
        for (int i = 0; i <= cnt; i += 2) {

            // Turn off the bit
            tempnum -= (1 << i);

            // If it gets lower than N
            // then set it and return that number
            if (tempnum < n)
                return tempnum += (1 << i);
        }
    }
}

// Driver code
int main()
{
    int n = 19;
    cout << findNearestNumber(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to count the total bits
    static int countBits(int n)
    {
        int count = 0;

        // Iterate and find the
        // number of set bits
        while (n > 0)
        {
            count++;

            // Right shift the number by 1
            n >>= 1;
        }
        return count;
    }

    // Function to find the nearest number
    static int findNearestNumber(int n)
    {

        // Count the total number of bits
        int cnt = countBits(n);

        // To get the position
        cnt -= 1;

        // If the last set bit is
        // at odd position then
        // answer will always be a number
        // with the left bit set
        if (cnt % 2 == 1)
        {
            return 1 << (cnt + 1);
        }
        else
        {

            int tempnum = 0;

            // Set all the even bits which
            // are possible
            for (int i = 0; i <= cnt; i += 2)
            {
                tempnum += 1 << i;
            }

            // If the number still is less than N
            if (tempnum < n)
            {

                // Return the number by setting the
                // next even set bit
                return (1 << (cnt + 2));
            }
            else
            if (tempnum == n)
            {
                return n;
            }

            // If we have reached this position
            // it means tempsum > n
            // hence turn off even bits to get the
            // first possible number
            for (int i = 0; i <= cnt; i += 2)
            {

                // Turn off the bit
                tempnum -= (1 << i);

                // If it gets lower than N
                // then set it and return that number
                if (tempnum < n)
                {
                    return tempnum += (1 << i);
                }
            }
        }
        return Integer.MIN_VALUE;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 19;

        System.out.println(findNearestNumber(n));
    }
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to count the total bits
    static int countBits(int n)
    {
        int count = 0;

        // Iterate and find the
        // number of set bits
        while (n > 0)
        {
            count++;

            // Right shift the number by 1
            n >>= 1;
        }
        return count;
    }

    // Function to find the nearest number
    static int findNearestNumber(int n)
    {

        // Count the total number of bits
        int cnt = countBits(n);

        // To get the position
        cnt -= 1;

        // If the last set bit is
        // at odd position then
        // answer will always be a number
        // with the left bit set
        if (cnt % 2 == 1)
        {
            return 1 << (cnt + 1);
        }
        else
        {

            int tempnum = 0;

            // Set all the even bits which
            // are possible
            for (int i = 0; i <= cnt; i += 2)
            {
                tempnum += 1 << i;
            }

            // If the number still is less than N
            if (tempnum < n)
            {

                // Return the number by setting the
                // next even set bit
                return (1 << (cnt + 2));
            }
            else
            if (tempnum == n)
            {
                return n;
            }

            // If we have reached this position
            // it means tempsum > n
            // hence turn off even bits to get the
            // first possible number
            for (int i = 0; i <= cnt; i += 2)
            {

                // Turn off the bit
                tempnum -= (1 << i);

                // If it gets lower than N
                // then set it and return that number
                if (tempnum < n)
                {
                    return tempnum += (1 << i);
                }
            }
        }
        return int.MinValue;
    }

    // Driver code
    public static void Main()
    {
        int n = 19;

        Console.WriteLine(findNearestNumber(n));
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to count the total bits
def countBits(n):
    count = 0;

    # Iterate and find the
    # number of set bits
    while (n>0):
        count+=1;

        # Right shift the number by 1
        n >>= 1;
    return count;

# Function to find the nearest number
def findNearestNumber(n):

    # Count the total number of bits
    cnt = countBits(n);

    # To get the position
    cnt -= 1;

    # If the last set bit is
    # at odd position then
    # answer will always be a number
    # with the left bit set
    if (cnt % 2):
        return 1 << (cnt + 1);

    else:

        tempnum = 0;

        # Set all the even bits which
        # are possible
        for i in range(0,cnt+1,2):
            tempnum += 1 << i;

        # If the number still is less than N
        if (tempnum < n):

            # Return the number by setting the
            # next even set bit
            return (1 << (cnt + 2));

        elif (tempnum == n):
            return n;

        # If we have reached this position
        # it means tempsum > n
        # hence turn off even bits to get the
        # first possible number
        for i in range(0,cnt+1,2):

            # Turn off the bit
            tempnum -= (1 << i);

            # If it gets lower than N
            # then set it and return that number
            if (tempnum < n):
                tempnum += (1 << i);
                return tempnum;
# Driver code
n = 19;
print(findNearestNumber(n));

# This code contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to count the total bits
function countBits(n)
{
    let count = 0;

    // Iterate and find the
    // number of set bits
    while (n) {
        count++;

        // Right shift the number by 1
        n >>= 1;
    }
    return count;
}

// Function to find the nearest number
function findNearestNumber(n)
{

    // Count the total number of bits
    let cnt = countBits(n);

    // To get the position
    cnt -= 1;

    // If the last set bit is
    // at odd position then
    // answer will always be a number
    // with the left bit set
    if (cnt % 2) {
        return 1 << (cnt + 1);
    }

    else {

        let tempnum = 0;

        // Set all the even bits which
        // are possible
        for (let i = 0; i <= cnt; i += 2)
            tempnum += 1 << i;

        // If the number still is less than N
        if (tempnum < n) {

            // Return the number by setting the
            // next even set bit
            return (1 << (cnt + 2));
        }

        else if (tempnum == n)
            return n;

        // If we have reached this position
        // it means tempsum > n
        // hence turn off even bits to get the
        // first possible number
        for (let i = 0; i <= cnt; i += 2) {

            // Turn off the bit
            tempnum -= (1 << i);

            // If it gets lower than N
            // then set it and return that number
            if (tempnum < n)
                return tempnum += (1 << i);
        }
    }
}

// Driver code
    let n = 19;
    document.write(findNearestNumber(n));

</script>
```

**Output:** 

```
20
```