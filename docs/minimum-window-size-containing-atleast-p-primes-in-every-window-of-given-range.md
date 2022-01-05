# 在给定范围的每个窗口中包含至少 P 个素数的最小窗口大小

> 原文:[https://www . geesforgeks . org/给定范围的每个窗口中至少包含 p 个素数的最小窗口大小/](https://www.geeksforgeeks.org/minimum-window-size-containing-atleast-p-primes-in-every-window-of-given-range/)

给定三个整数 **X** 、 **Y** 和 **P** ，任务是找到最小窗口大小 **K** ，使得这个大小的范围【X，Y】中的每个窗口至少有 **P** 个素数。
**举例:**

> **输入:** X = 2，Y = 8，P = 2
> **输出:** 4
> **说明:**
> 在[2，8]的范围内，窗口大小为 4 在每个窗口中至少包含 2 个素数。
> 可能的窗口–
> { 2，3，4，5 }–素数数量= 3
> {3，4，5，6 }–素数数量= 2
> {4，5，6，7 }–素数数量= 2
> {5，6，7，8 }–素数数量= 2
> **输入:** X = 12，Y = 42，P = 3
> **输出:**

**简单方法:**遍历所有可能的窗口大小，对于每个窗口大小遍历范围[X，Y]，并检查每个窗口至少包含 K 个素数。这些窗口大小的最小值将是所需的值。
**有效途径:**这个问题的关键观察点是，如果窗口大小 W 是满足条件的最小窗口大小，那么[W，Y–X+1]范围内的所有窗口大小都将满足条件。利用这一点，我们可以将每一步的搜索空间减少一半，这正是[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的想法。以下是步骤说明:

*   **搜索空间:**这个问题的搜索空间可以是窗口大小为 1 的最小长度，最大窗口大小可以是范围的结束值和范围的开始值之差。

```
low = 1
high = Y - X + 1
```

*   **下一个搜索空间:**在每个步骤中，通常的想法是在[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)的帮助下，检查对于给定的窗口大小，每个窗口中的素数是否可能具有 **P** 素数。而问题的搜索空间可以基于以下决定而减小:
    *   **情况 1:** 当每个窗口中的素数至少包含 **P** 个素数时，则可以缩小窗口的大小，找到小于当前窗口的窗口大小。

```
if (checkPPrimes(mid) == True)
    high = mid - 1
```

*   **情况 2:** 当每个窗口中包含的素数不具备时，则窗口大小必须大于当前窗口大小。然后，

```
if (checkPPrimes(mid) == False)
    low = mid + 1
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum window size in the range
// such that each window of that size
// contains atleast P primes

#include <bits/stdc++.h>

using namespace std;

// Function to check that a number is
// a prime or not in O(sqrt(N))
bool isPrime(int N)
{
    if (N < 2)
        return false;
    if (N < 4)
        return true;
    if ((N & 1) == 0)
        return false;
    if (N % 3 == 0)
        return false;
    int curr = 5, s = sqrt(N);

    // Loop to check if any number
    // number is divisible by any
    // other number or not
    while (curr <= s) {
        if (N % curr == 0)
            return false;
        curr += 2;
        if (N % curr == 0)
            return false;
        curr += 4;
    }
    return true;
}

// Function to check whether window
// size satisfies condition or not
bool check(int s, int p,
      int prefix_sum[], int n)
{
    bool satisfies = true;

    // Loop to check each window of
    // size have atleast P primes
    for (int i = 0; i < n; i++) {
        if (i + s - 1 >= n)
            break;

        // Checking condition
        // using prefix sum
        if (prefix_sum[i + s - 1] -
          (i - 1 >= 0 ?
          prefix_sum[i - 1] : 0) < p)
            satisfies = false;
    }
    return satisfies;
}

// Function to find the minimum
// window size possible for the
// given range in X and Y
int minimumWindowSize(int x, int y,
                             int p)
{
    // Prefix array
    int prefix_sum[y - x + 1] = { 0 };

    // Mark those numbers
    // which are primes as 1
    for (int i = x; i <= y; i++) {
        if (isPrime(i))
            prefix_sum[i - x] = 1;
    }

    // Convert to prefix sum
    for (int i = 1; i < y - x + 1; i++)
        prefix_sum[i] +=
              prefix_sum[i - 1];

    // Applying binary search
    // over window size
    int low = 1, high = y - x + 1;
    int mid;
    while (high - low > 1) {
        mid = (low + high) / 2;

        // Check whether mid satisfies
        // the condition or not
        if (check(mid, p,
           prefix_sum, y - x + 1)) {

            // If satisfies search
            // in first half
            high = mid;
        }

        // Else search in second half
        else
            low = mid;
    }
    if (check(low, p,
       prefix_sum, y - x + 1))
        return low;
    return high;
}

// Driver Code
int main()
{
    int x = 12;
    int y = 42;
    int p = 3;

    cout << minimumWindowSize(x, y, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum window size in the range
// such that each window of that size
// contains atleast P primes
import java.util.*;

class GFG{

// Function to check that a number is
// a prime or not in O(Math.sqrt(N))
static boolean isPrime(int N)
{
    if (N < 2)
        return false;
    if (N < 4)
        return true;
    if ((N & 1) == 0)
        return false;
    if (N % 3 == 0)
        return false;
    int curr = 5, s = (int) Math.sqrt(N);

    // Loop to check if any number
    // number is divisible by any
    // other number or not
    while (curr <= s) {
        if (N % curr == 0)
            return false;
        curr += 2;
        if (N % curr == 0)
            return false;
        curr += 4;
    }
    return true;
}

// Function to check whether window
// size satisfies condition or not
static boolean check(int s, int p,
      int prefix_sum[], int n)
{
    boolean satisfies = true;

    // Loop to check each window of
    // size have atleast P primes
    for (int i = 0; i < n; i++) {
        if (i + s - 1 >= n)
            break;

        // Checking condition
        // using prefix sum
        if (prefix_sum[i + s - 1] -
          (i - 1 >= 0 ?
          prefix_sum[i - 1] : 0) < p)
            satisfies = false;
    }
    return satisfies;
}

// Function to find the minimum
// window size possible for the
// given range in X and Y
static int minimumWindowSize(int x, int y,
                             int p)
{
    // Prefix array
    int []prefix_sum = new int[y - x + 1];

    // Mark those numbers
    // which are primes as 1
    for (int i = x; i <= y; i++) {
        if (isPrime(i))
            prefix_sum[i - x] = 1;
    }

    // Convert to prefix sum
    for (int i = 1; i < y - x + 1; i++)
        prefix_sum[i] +=
              prefix_sum[i - 1];

    // Applying binary search
    // over window size
    int low = 1, high = y - x + 1;
    int mid;
    while (high - low > 1) {
        mid = (low + high) / 2;

        // Check whether mid satisfies
        // the condition or not
        if (check(mid, p,
           prefix_sum, y - x + 1)) {

            // If satisfies search
            // in first half
            high = mid;
        }

        // Else search in second half
        else
            low = mid;
    }
    if (check(low, p,
       prefix_sum, y - x + 1))
        return low;
    return high;
}

// Driver Code
public static void main(String[] args)
{
    int x = 12;
    int y = 42;
    int p = 3;

    System.out.print(minimumWindowSize(x, y, p));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum window size in the range
# such that each window of that size
# contains atleast P primes

from math import sqrt

# Function to check that a number is
# a prime or not in O(sqrt(N))
def isPrime(N):
    if (N < 2):
        return False
    if (N < 4):
        return True
    if ((N & 1) == 0):
        return False
    if (N % 3 == 0):
        return False

    curr = 5
    s = sqrt(N)

    # Loop to check if any number
    # number is divisible by any
    # other number or not
    while (curr <= s):
        if (N % curr == 0):
            return False
        curr += 2
        if (N % curr == 0):
            return False

        curr += 4

    return True

# Function to check whether window
# size satisfies condition or not
def check(s, p, prefix_sum, n):

    satisfies = True
    # Loop to check each window of
    # size have atleast P primes
    for i in range(n):
        if (i + s - 1 >= n):
            break
        # Checking condition
        # using prefix sum
        if (i - 1 >= 0):
            x = prefix_sum[i - 1]
        else:
            x = 0
        if (prefix_sum[i + s - 1] - x < p):
            satisfies = False

    return satisfies

# Function to find the minimum
# window size possible for the
# given range in X and Y
def minimumWindowSize(x, y, p):

    # Prefix array
    prefix_sum = [0]*(y - x + 1)

    # Mark those numbers
    # which are primes as 1   
    for i in range(x ,y+1):
        if (isPrime(i)):
            prefix_sum[i - x] = 1

    # Convert to prefix sum
    for i in range(1 ,y - x + 1):
        prefix_sum[i] += prefix_sum[i - 1]

    # Applying binary search
    # over window size
    low = 1
    high = y - x + 1

    while (high - low > 1):
        mid = (low + high) // 2

        # Check whether mid satisfies
        # the condition or not
        if (check(mid, p ,prefix_sum, y - x + 1)):

            # If satisfies search
            # in first half
            high = mid

        # Else search in second half
        else:
            low = mid
    if (check(low, p, prefix_sum, y - x + 1)):
        return low
    return high

# Driver Code
x = 12
y = 42
p = 3

print(minimumWindowSize(x, y, p))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find the
// minimum window size in the range
// such that each window of that size
// contains atleast P primes
using System;

class GFG{

// Function to check that a number is
// a prime or not in O(Math.Sqrt(N))
static bool isPrime(int N)
{
    if (N < 2)
        return false;
    if (N < 4)
        return true;
    if ((N & 1) == 0)
        return false;
    if (N % 3 == 0)
        return false;
    int curr = 5, s = (int) Math.Sqrt(N);

    // Loop to check if any number
    // number is divisible by any
    // other number or not
    while (curr <= s) {
        if (N % curr == 0)
            return false;
        curr += 2;
        if (N % curr == 0)
            return false;
        curr += 4;
    }
    return true;
}

// Function to check whether window
// size satisfies condition or not
static bool check(int s, int p,
      int []prefix_sum, int n)
{
    bool satisfies = true;

    // Loop to check each window of
    // size have atleast P primes
    for (int i = 0; i < n; i++) {
        if (i + s - 1 >= n)
            break;

        // Checking condition
        // using prefix sum
        if (prefix_sum[i + s - 1] -
          (i - 1 >= 0 ?
          prefix_sum[i - 1] : 0) < p)
            satisfies = false;
    }
    return satisfies;
}

// Function to find the minimum
// window size possible for the
// given range in X and Y
static int minimumWindowSize(int x, int y,
                             int p)
{
    // Prefix array
    int []prefix_sum = new int[y - x + 1];

    // Mark those numbers
    // which are primes as 1
    for (int i = x; i <= y; i++) {
        if (isPrime(i))
            prefix_sum[i - x] = 1;
    }

    // Convert to prefix sum
    for (int i = 1; i < y - x + 1; i++)
        prefix_sum[i] +=
              prefix_sum[i - 1];

    // Applying binary search
    // over window size
    int low = 1, high = y - x + 1;
    int mid;
    while (high - low > 1) {
        mid = (low + high) / 2;

        // Check whether mid satisfies
        // the condition or not
        if (check(mid, p,
           prefix_sum, y - x + 1)) {

            // If satisfies search
            // in first half
            high = mid;
        }

        // Else search in second half
        else
            low = mid;
    }
    if (check(low, p,
       prefix_sum, y - x + 1))
        return low;
    return high;
}

// Driver Code
public static void Main(String[] args)
{
    int x = 12;
    int y = 42;
    int p = 3;

    Console.Write(minimumWindowSize(x, y, p));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript implementation to find the
// minimum window size in the range
// such that each window of that size
// contains atleast P primes

// Function to check that a number is
// a prime or not in O(Math.sqrt(N))
function isPrime(N)
{
    if (N < 2)
        return false;
    if (N < 4)
        return true;
    if ((N & 1) == 0)
        return false;
    if (N % 3 == 0)
        return false;
    let curr = 5, s = Math.floor(Math.sqrt(N));

    // Loop to check if any number
    // number is divisible by any
    // other number or not
    while (curr <= s) {
        if (N % curr == 0)
            return false;
        curr += 2;
        if (N % curr == 0)
            return false;
        curr += 4;
    }
    return true;
}

// Function to check whether window
// size satisfies condition or not
function check(s, p,
      prefix_sum, n)
{
    let satisfies = true;

    // Loop to check each window of
    // size have atleast P primes
    for (let i = 0; i < n; i++) {
        if (i + s - 1 >= n)
            break;

        // Checking condition
        // using prefix sum
        if (prefix_sum[i + s - 1] -
          (i - 1 >= 0 ?
          prefix_sum[i - 1] : 0) < p)
            satisfies = false;
    }
    return satisfies;
}

// Function to find the minimum
// window size possible for the
// given range in X and Y
function minimumWindowSize(x, y, p)
{
    // Prefix array
    let prefix_sum = new Array(y - x + 1).fill(0);

    // Mark those numbers
    // which are primes as 1
    for (let i = x; i <= y; i++) {
        if (isPrime(i))
            prefix_sum[i - x] = 1;
    }

    // Convert to prefix sum
    for (let i = 1; i < y - x + 1; i++)
        prefix_sum[i] +=
              prefix_sum[i - 1];

    // Applying binary search
    // over window size
    let low = 1, high = y - x + 1;
    let mid;
    while (high - low > 1) {
        mid = Math.floor((low + high) / 2);

        // Check whether mid satisfies
        // the condition or not
        if (check(mid, p,
           prefix_sum, y - x + 1)) {

            // If satisfies search
            // in first half
            high = mid;
        }

        // Else search in second half
        else
            low = mid;
    }
    if (check(low, p,
       prefix_sum, y - x + 1))
        return low;
    return high;
}

// Driver Code

    let x = 12;
    let y = 42;
    let p = 3;

    document.write(minimumWindowSize(x, y, p));

</script>
```

**Output:** 

```
14
```

**时间复杂度:** O(N*log(N))
**辅助空间:** O(N)