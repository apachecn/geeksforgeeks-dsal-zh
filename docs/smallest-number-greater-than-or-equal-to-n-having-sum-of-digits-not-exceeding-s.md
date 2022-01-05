# 大于或等于 N 的最小数，位数之和不超过 S

> 原文:[https://www . geesforgeks . org/最小数字大于或等于 n 具有不超过-s 的数字总和/](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-n-having-sum-of-digits-not-exceeding-s/)

给定整数 **N** 和整数 **S** ，任务是找到大于或等于 **N** 的最小数，使得[的位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)不超过 **S** 。

**示例:**

> **输入:** N = 3，S = 2
> **输出:** 10
> **说明:**10 位数之和为 1，小于 2。
> 
> **输入:** N = 19，S = 3
> **输出:** 20
> **说明:**20 位数之和为 2，小于 3。

**方法:**使用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题。

1.  检查 **N** 的[位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)是否不超过 **S** ，返回 **N** 。
2.  初始化一个变量，说 **ans** 等于给定的整数 **N** 和 **k** 用 **1** 存储 **10** 的幂。
3.  整数范围内最多可以有 **10** 位数字。
4.  从 **i = 0 迭代到 8** 。每次迭代时，计算最后一位数字为 **(ans / k)%10** 。
5.  最后一位数字 **0** 的总和为**k *(10-最后一位数字)%10)** 。添加到**和**中。
6.  检查**和**的位数之和。如果不超过 **S** ，则打印 **ans** 并断开。否则，将 **k** 更新为 **k = k*10** ，重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum
// digits of n
int sum(int n)
{
    int res = 0;
    while (n > 0) {
        res += n % 10;
        n /= 10;
    }
    return res;
}

// Function to find the smallest
// possible integer satisfying the
// given condition
int smallestNumber(int n, int s)
{
    // If the sum of digits
    // is already smaller than S
    if (sum(n) <= s) {
        return n;
    }

    // Initialize variables
    int ans = n, k = 1;

    for (int i = 0; i < 9; ++i) {

        // Finding last kth digit
        int digit = (ans / k) % 10;

        // Add remaining to make digit 0
        int add = k * ((10 - digit) % 10);

        ans += add;

        // If sum of digits
        // does not exceed S
        if (sum(ans) <= s) {
            break;
        }

        // Update k
        k *= 10;
    }
    return ans;
}

// Driver Code
int main()
{

    // Given N and S
    int N = 3, S = 2;

    // Function call
    cout << smallestNumber(N, S) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate sum
// digits of n
static int sum(int n)
{
    int res = 0;
    while (n > 0)
    {
        res += n % 10;
        n /= 10;
    }
    return res;
}

// Function to find the smallest
// possible integer satisfying the
// given condition
static int smallestNumber(int n, int s)
{

    // If the sum of digits
    // is already smaller than S
    if (sum(n) <= s)
    {
        return n;
    }

    // Initialize variables
    int ans = n, k = 1;

    for(int i = 0; i < 9; ++i)
    {

        // Finding last kth digit
        int digit = (ans / k) % 10;

        // Add remaining to make digit 0
        int add = k * ((10 - digit) % 10);

        ans += add;

        // If sum of digits
        // does not exceed S
        if (sum(ans) <= s)
        {
            break;
        }

        // Update k
        k *= 10;
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given N and S
    int N = 3, S = 2;

    // Function call
    System.out.println(smallestNumber(N, S));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate
# sum of digits of n
def sum(n):
    sm = 0
    while(n > 0):
        sm += n % 10
        n //= 10
    return sm

# Function to find the smallest
# possible integer satisfying the
# given condition
def smallestNumber(n, s):

# If sum of digits is
# already smaller than s
    if(sum(n) <= s):
        return n

# Initialize variables
    ans, k = n, 1

    for i in range(9):

# Find the k-th digit
        digit = (ans // k) % 10

# Add remaining
        add = k * ((10 - digit) % 10)

        ans += add

# If sum of digits
# does not exceed s
        if(sum(ans) <= s):
            break

# Update K
        k *= 10

# Return answer
    return ans

# Driver Code

# Given N and S
n, s = 3, 2

# Function call
print(smallestNumber(n, s))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum
// digits of n
static int sum(int n)
{
    int res = 0;
    while (n > 0)
    {
        res += n % 10;
        n /= 10;
    }
    return res;
}

// Function to find the smallest
// possible integer satisfying the
// given condition
static int smallestNumber(int n, int s)
{

    // If the sum of digits
    // is already smaller than S
    if (sum(n) <= s)
    {
        return n;
    }

    // Initialize variables
    int ans = n, k = 1;

    for(int i = 0; i < 9; ++i)
    {

        // Finding last kth digit
        int digit = (ans / k) % 10;

        // Add remaining to make digit 0
        int add = k * ((10 - digit) % 10);

        ans += add;

        // If sum of digits
        // does not exceed S
        if (sum(ans) <= s)
        {
            break;
        }

        // Update k
        k *= 10;
    }
    return ans;
}

// Driver Code
public static void Main()
{

    // Given N and S
    int N = 3, S = 2;

    // Function call
    Console.WriteLine(smallestNumber(N, S));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to calculate sum
// digits of n
function sum(n)
{
    var res = 0;
    while (n > 0)
    {
        res += n % 10;
        n /= 10;
    }
    return res;
}

// Function to find the smallest
// possible integer satisfying the
// given condition
function smallestNumber(n , s)
{

    // If the sum of digits
    // is already smaller than S
    if (sum(n) <= s)
    {
        return n;
    }

    // Initialize variables
    var ans = n, k = 1;

    for(i = 0; i < 9; ++i)
    {

        // Finding last kth digit
        var digit = (ans / k) % 10;

        // Add remaining to make digit 0
        var add = k * ((10 - digit) % 10);

        ans += add;

        // If sum of digits
        // does not exceed S
        if (sum(ans) <= s)
        {
            break;
        }

        // Update k
        k *= 10;
    }
    return ans;
}

// Driver Code

// Given N and S
var N = 3, S = 2;

// Function call
document.write(smallestNumber(N, S));

// This code is contributed by shikhasingrajput.
</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(log<sup>2</sup>T5】10(N))其中 N 为给定整数。*
***空间复杂度:** O(1)*