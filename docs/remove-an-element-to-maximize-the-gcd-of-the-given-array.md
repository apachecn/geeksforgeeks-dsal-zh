# 移除一个元素以最大化给定数组的 GCD

> 原文:[https://www . geeksforgeeks . org/移除元素以最大化给定数组的 gcd/](https://www.geeksforgeeks.org/remove-an-element-to-maximize-the-gcd-of-the-given-array/)

给定一个长度为 **N ≥ 2** 的数组 **arr[]** 。任务是从给定的数组中移除一个元素，以便移除该元素后数组的 GCD 最大化。

**示例:**

> **输入:** arr[] = {12，15，18}
> **输出:** 6
> 移除 12: GCD(15，18) = 3
> **移除 15: GCD(12，18) = 6**
> 移除 18: GCD(12，15) = 3
> 
> **输入:** arr[] = {14，17，28，70 }
> T3】输出: 14

**进场:**

*   想法是找到所有长度为**(N–1)**的子序列的 GCD 值，并用该 GCD 移除子序列中不存在的元素。找到的最大 GCD 将是答案。
*   为了最佳地找到子序列的 GCD，使用单状态动态编程来维护一个**前缀 GCD[]** 和一个**后缀 GCD[]** 数组。
*   **GCD 的最大值(prefixGCD[I–1]，sufixgcd[I+1])**为必选项。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized gcd
// after removing a single element
// from the given array
int MaxGCD(int a[], int n)
{

    // Prefix and Suffix arrays
    int Prefix[n + 2];
    int Suffix[n + 2];

    // Single state dynamic programming relation
    // for storing gcd of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1) {
        Prefix[i] = __gcd(Prefix[i - 1], a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing gcd of all the elements having
    // greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1) {
        Suffix[i] = __gcd(Suffix[i + 1], a[i - 1]);
    }

    // If first or last element of
    // the array has to be removed
    int ans = max(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1) {
        ans = max(ans, __gcd(Prefix[i - 1], Suffix[i + 1]));
    }

    // Return the maximized gcd
    return ans;
}

// Driver code
int main()
{
    int a[] = { 14, 17, 28, 70 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MaxGCD(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class Test
{
    // Recursive function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the maximized gcd
    // after removing a single element
    // from the given array
    static int MaxGCD(int a[], int n)
    {

        // Prefix and Suffix arrays
        int Prefix[] = new int[n + 2];
        int Suffix[] = new int[n + 2] ;

        // Single state dynamic programming relation
        // for storing gcd of first i elements
        // from the left in Prefix[i]
        Prefix[1] = a[0];
        for (int i = 2; i <= n; i += 1)
        {
            Prefix[i] = gcd(Prefix[i - 1], a[i - 1]);
        }

        // Initializing Suffix array
        Suffix[n] = a[n - 1];

        // Single state dynamic programming relation
        // for storing gcd of all the elements having
        // greater than or equal to i in Suffix[i]
        for (int i = n - 1; i >= 1; i -= 1)
        {
            Suffix[i] = gcd(Suffix[i + 1], a[i - 1]);
        }

        // If first or last element of
        // the array has to be removed
        int ans = Math.max(Suffix[2], Prefix[n - 1]);

        // If any other element is replaced
        for (int i = 2; i < n; i += 1)
        {
            ans = Math.max(ans, gcd(Prefix[i - 1], Suffix[i + 1]));
        }

        // Return the maximized gcd
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

        int a[] = { 14, 17, 28, 70 };
        int n = a.length;

        System.out.println(MaxGCD(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import math as mt

# Function to return the maximized gcd
# after removing a single element
# from the given array

def MaxGCD(a, n):

    # Prefix and Suffix arrays
    Prefix=[0 for i in range(n + 2)]
    Suffix=[0 for i in range(n + 2)]

    # Single state dynamic programming relation
    # for storing gcd of first i elements
    # from the left in Prefix[i]
    Prefix[1] = a[0]
    for i in range(2,n+1):
        Prefix[i] = mt.gcd(Prefix[i - 1], a[i - 1])

    # Initializing Suffix array
    Suffix[n] = a[n - 1]

    # Single state dynamic programming relation
    # for storing gcd of all the elements having
    # greater than or equal to i in Suffix[i]
    for i in range(n-1,0,-1):
        Suffix[i] =mt.gcd(Suffix[i + 1], a[i - 1])

    # If first or last element of
    # the array has to be removed
    ans = max(Suffix[2], Prefix[n - 1])

    # If any other element is replaced
    for i in range(2,n):
        ans = max(ans, mt.gcd(Prefix[i - 1], Suffix[i + 1]))

    # Return the maximized gcd
    return ans

# Driver code

a=[14, 17, 28, 70]
n = len(a)

print(MaxGCD(a, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Recursive function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the maximized gcd
    // after removing a single element
    // from the given array
    static int MaxGCD(int []a, int n)
    {

        // Prefix and Suffix arrays
        int []Prefix = new int[n + 2];
        int []Suffix = new int[n + 2] ;

        // Single state dynamic programming relation
        // for storing gcd of first i elements
        // from the left in Prefix[i]
        Prefix[1] = a[0];
        for (int i = 2; i <= n; i += 1)
        {
            Prefix[i] = gcd(Prefix[i - 1], a[i - 1]);
        }

        // Initializing Suffix array
        Suffix[n] = a[n - 1];

        // Single state dynamic programming relation
        // for storing gcd of all the elements having
        // greater than or equal to i in Suffix[i]
        for (int i = n - 1; i >= 1; i -= 1)
        {
            Suffix[i] = gcd(Suffix[i + 1], a[i - 1]);
        }

        // If first or last element of
        // the array has to be removed
        int ans = Math.Max(Suffix[2], Prefix[n - 1]);

        // If any other element is replaced
        for (int i = 2; i < n; i += 1)
        {
            ans = Math.Max(ans, gcd(Prefix[i - 1], Suffix[i + 1]));
        }

        // Return the maximized gcd
        return ans;
    }

    // Driver code
    static public void Main ()
    {

        int []a = { 14, 17, 28, 70 };
        int n = a.Length;

        Console.Write(MaxGCD(a, n));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Recursive function to return gcd of a and b 
function gcd(a, b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to return the maximized gcd
// after removing a single element
// from the given array
function MaxGCD(a, n)
{

    // Prefix and Suffix arrays
    let Prefix = new Array(n + 2);
    let Suffix = new Array(n + 2);

    // Single state dynamic programming relation
    // for storing gcd of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for(let i = 2; i <= n; i += 1)
    {
        Prefix[i] = gcd(Prefix[i - 1], a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing gcd of all the elements having
    // greater than or equal to i in Suffix[i]
    for(let i = n - 1; i >= 1; i -= 1)
    {
        Suffix[i] = gcd(Suffix[i + 1], a[i - 1]);
    }

    // If first or last element of
    // the array has to be removed
    let ans = Math.max(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for(let i = 2; i < n; i += 1)
    {
        ans = Math.max(ans, gcd(Prefix[i - 1],
                                Suffix[i + 1]));
    }

    // Return the maximized gcd
    return ans;
}

// Driver code
let a = [ 14, 17, 28, 70 ];
let n = a.length;

document.write(MaxGCD(a, n));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
14
```

**时间复杂度:** O(N * log(M))，其中 M 是数组中的最大元素。