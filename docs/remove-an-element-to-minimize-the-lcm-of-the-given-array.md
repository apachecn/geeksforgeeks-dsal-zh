# 移除一个元素以最小化给定数组的 LCM

> 原文:[https://www . geesforgeks . org/remove-a-element-to-minimum-of-the-给定数组/](https://www.geeksforgeeks.org/remove-an-element-to-minimize-the-lcm-of-the-given-array/)

给定一个长度为 **N ≥ 2** 的数组 **arr[]** 。任务是从给定的数组中移除一个元素，以便在移除该元素后最小化该数组的 LCM。
**例:**

> **输入:** arr[] = {18，12，24}
> **输出:** 24
> 移除 12: LCM(18，24) = 72
> **移除 18: LCM(12，24) = 24**
> 移除 24: LCM(12，18) = 36
> **输入:** arr[] = {5，15，9，36} 【T13

**进场:**

*   想法是找到所有长度子序列**(N–1)**的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 值，并用该 LCM 去除子序列中不存在的元素。找到的最小 LCM 就是答案。
*   为了最佳地找到子序列的 LCM，使用单状态动态编程保持一个**前缀 CM[]** 和一个**后缀 LCM[]** 数组。
*   **LCM 的最小值(prefix LCM[I–1]，sufix LCM[I+1])**为必选项。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the LCM of two numbers
int lcm(int a, int b)
{
    int GCD = __gcd(a, b);
    return (a * b) / GCD;
}

// Function to return the minimum LCM
// after removing a single element
// from the given array
int MinLCM(int a[], int n)
{

    // Prefix and Suffix arrays
    int Prefix[n + 2];
    int Suffix[n + 2];

    // Single state dynamic programming relation
    // for storing LCM of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1) {
        Prefix[i] = lcm(Prefix[i - 1], a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing LCM of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1) {
        Suffix[i] = lcm(Suffix[i + 1], a[i - 1]);
    }

    // If first or last element of
    // the array has to be removed
    int ans = min(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1) {
        ans = min(ans, lcm(Prefix[i - 1], Suffix[i + 1]));
    }

    // Return the minimum LCM
    return ans;
}

// Driver code
int main()
{
    int a[] = { 5, 15, 9, 36 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MinLCM(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to return the LCM of two numbers
static int lcm(int a, int b)
{
    int GCD = __gcd(a, b);
    return (a * b) / GCD;
}

// Function to return the minimum LCM
// after removing a single element
// from the given array
static int MinLCM(int a[], int n)
{

    // Prefix and Suffix arrays
    int []Prefix = new int[n + 2];
    int []Suffix = new int[n + 2];

    // Single state dynamic programming relation
    // for storing LCM of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1)
    {
        Prefix[i] = lcm(Prefix[i - 1],
                             a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing LCM of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1)
    {
        Suffix[i] = lcm(Suffix[i + 1],
                             a[i - 1]);
    }

    // If first or last element of
    // the array has to be removed
    int ans = Math.min(Suffix[2],
                       Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1)
    {
        ans = Math.min(ans, lcm(Prefix[i - 1],
                                Suffix[i + 1]));
    }

    // Return the minimum LCM
    return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String []args)
{
    int a[] = { 5, 15, 9, 36 };
    int n = a.length;

    System.out.println(MinLCM(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
from math import gcd

# Function to return the LCM
# of two numbers
def lcm(a, b) :

    GCD = gcd(a, b);
    return (a * b) // GCD;

# Function to return the minimum LCM
# after removing a single element
# from the given array
def MinLCM(a, n) :

    # Prefix and Suffix arrays
    Prefix = [0] * (n + 2);
    Suffix = [0] * (n + 2);

    # Single state dynamic programming relation
    # for storing LCM of first i elements
    # from the left in Prefix[i]
    Prefix[1] = a[0];
    for i in range(2, n + 1) :
        Prefix[i] = lcm(Prefix[i - 1],
                             a[i - 1]);

    # Initializing Suffix array
    Suffix[n] = a[n - 1];

    # Single state dynamic programming relation
    # for storing LCM of all the elements having
    # index greater than or equal to i in Suffix[i]
    for i in range(n - 1, 0, -1) :
        Suffix[i] = lcm(Suffix[i + 1], a[i - 1]);

    # If first or last element of
    # the array has to be removed
    ans = min(Suffix[2], Prefix[n - 1]);

    # If any other element is replaced
    for i in range(2, n) :
        ans = min(ans, lcm(Prefix[i - 1],
                           Suffix[i + 1]));

    # Return the minimum LCM
    return ans;

# Driver code
if __name__ == "__main__" :

    a = [ 5, 15, 9, 36 ];
    n = len(a);

    print(MinLCM(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the LCM of two numbers
static int lcm(int a, int b)
{
    int GCD = __gcd(a, b);
    return (a * b) / GCD;
}

// Function to return the minimum LCM
// after removing a single element
// from the given array
static int MinLCM(int []a, int n)
{

    // Prefix and Suffix arrays
    int []Prefix = new int[n + 2];
    int []Suffix = new int[n + 2];

    // Single state dynamic programming relation
    // for storing LCM of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1)
    {
        Prefix[i] = lcm(Prefix[i - 1],
                             a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing LCM of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1)
    {
        Suffix[i] = lcm(Suffix[i + 1],
                             a[i - 1]);
    }

    // If first or last element of
    // the array has to be removed
    int ans = Math.Min(Suffix[2],
                       Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1)
    {
        ans = Math.Min(ans, lcm(Prefix[i - 1],
                                Suffix[i + 1]));
    }

    // Return the minimum LCM
    return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String []args)
{
    int []a = { 5, 15, 9, 36 };
    int n = a.Length;

    Console.WriteLine(MinLCM(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to return the LCM of two numbers
function lcm(a, b) {
    let GCD = __gcd(a, b);
    return Math.floor((a * b) / GCD);
}

function __gcd(a, b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Function to return the minimum LCM
// after removing a single element
// from the given array
function MinLCM(a, n) {

    // Prefix and Suffix arrays
    let Prefix = new Array(n + 2);
    let Suffix = new Array(n + 2);

    // Single state dynamic programming relation
    // for storing LCM of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (let i = 2; i <= n; i += 1) {
        Prefix[i] = lcm(Prefix[i - 1], a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing LCM of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (let i = n - 1; i >= 1; i -= 1) {
        Suffix[i] = lcm(Suffix[i + 1], a[i - 1]);
    }

    // If first or last element of
    // the array has to be removed
    let ans = Math.min(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (let i = 2; i < n; i += 1) {
        ans = Math.min(ans, lcm(Prefix[i - 1], Suffix[i + 1]));
    }

    // Return the minimum LCM
    return ans;
}

// Driver code

let a = [5, 15, 9, 36];
let n = a.length;

document.write(MinLCM(a, n));

</script>
```

**Output:** 

```
45
```

**时间复杂度:** O(N * log(M))，其中 M 是数组中的最大元素。