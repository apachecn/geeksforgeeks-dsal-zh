# 求可被 3 整除的元素最大个数

> 原文:[https://www . geesforgeks . org/find-最大元素数-可被 3 整除/](https://www.geeksforgeeks.org/find-the-maximum-number-of-elements-divisible-by-3/)

给定大小为 **N** 的数组。在执行任意(可能是零)次运算后，查找数组中可被 3 整除的元素的最大可能数量的任务。在每个操作中，可以添加数组的任意两个元素。
**例:**

> **输入:** a[] = {1，2，3}
> **输出:** 2
> 对元素 1，2 进行一次运算后，数组变成{3，3}。
> 包含 2 个可被 3 整除的数字，最大可能。
> **输入:** a[] = {1，1，1，1，1，2，2}
> **输出:** 3

**方法:**
让 cnt <sub>i</sub> 是一个的元素数，余数 I 取模 3。那么初始答案可以表示为 cnt <sub>0</sub> ，我们必须以某种最佳方式用余数 1 和 2 组成数字。可以看出，最好的方法如下:

*   首先，当至少有一个 1 的余数和至少一个 2 的余数时，将它们合成一个 0。在此之后，cnt <sub>1</sub> 、cnt <sub>2</sub> 中的至少一个数字将为零，然后我们必须将剩余的数字组成可被 3 整除的数字。
*   如果 cnt <sub>1</sub> =0，那么我们可以获得的最大剩余元素数是【cnt <sub>2</sub> /3】(因为 2+2+2=6)，而在另一种情况下(cnt <sub>2</sub> =0)，最大元素数是【cnt <sub>1</sub> /3】(因为 1+1+1=3)。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum
// number of elements divisible by 3
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// number of elements divisible by 3
int MaxNumbers(int a[], int n)
{
    // To store frequency of each number
    int fre[3] = { 0 };

    for (int i = 0; i < n; i++) {
        // Store modulo value
        a[i] %= 3;

        // Store frequency
        fre[a[i]]++;
    }

    // Add numbers with zero modulo to answer
    int ans = fre[0];

    // Find minimum of elements with modulo
    // frequency one and zero
    int k = min(fre[1], fre[2]);

    // Add k to the answer
    ans += k;

    // Remove them from frequency
    fre[1] -= k;
    fre[2] -= k;

    // Add numbers possible with
    // remaining frequency
    ans += fre[1] / 3 + fre[2] / 3;

    // Return the required answer
    return ans;
}

// Driver code
int main()
{

    int a[] = { 1, 4, 10, 7, 11, 2, 8, 5, 9 };

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << MaxNumbers(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// number of elements divisible by 3
import java.io.*;

class GFG
{

    // Function to find the maximum
    // number of elements divisible by 3
    static int MaxNumbers(int a[], int n)
    {
        // To store frequency of each number
        int []fre = { 0,0,0 };

        for (int i = 0; i < n; i++)
        {
            // Store modulo value
            a[i] %= 3;

            // Store frequency
            fre[a[i]]++;
        }

        // Add numbers with zero modulo to answer
        int ans = fre[0];

        // Find minimum of elements with modulo
        // frequency one and zero
        int k = Math.min(fre[1], fre[2]);

        // Add k to the answer
        ans += k;

        // Remove them from frequency
        fre[1] -= k;
        fre[2] -= k;

        // Add numbers possible with
        // remaining frequency
        ans += fre[1] / 3 + fre[2] / 3;

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 1, 4, 10, 7, 11, 2, 8, 5, 9 };

        int n = a.length;

        // Function call
        System.out.println(MaxNumbers(a, n));
    }
}

// This code is contributed by @@ajit..
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# number of elements divisible by 3

# Function to find the maximum
# number of elements divisible by 3
def MaxNumbers(a, n):

    # To store frequency of each number
    fre = [0 for i in range(3)]

    for i in range(n):

        # Store modulo value
        a[i] %= 3

        # Store frequency
        fre[a[i]] += 1

    # Add numbers with zero modulo to answer
    ans = fre[0]

    # Find minimum of elements with modulo
    # frequency one and zero
    k = min(fre[1], fre[2])

    # Add k to the answer
    ans += k

    # Remove them from frequency
    fre[1] -= k
    fre[2] -= k

    # Add numbers possible with
    # remaining frequency
    ans += fre[1] // 3 + fre[2] // 3

    # Return the required answer
    return ans

# Driver code
a = [1, 4, 10, 7, 11, 2, 8, 5, 9]

n = len(a)

# Function call
print(MaxNumbers(a, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the maximum
// number of elements divisible by 3
using System;

class GFG
{

    // Function to find the maximum
    // number of elements divisible by 3
    static int MaxNumbers(int []a, int n)
    {
        // To store frequency of each number
        int []fre = { 0,0,0 };

        for (int i = 0; i < n; i++)
        {
            // Store modulo value
            a[i] %= 3;

            // Store frequency
            fre[a[i]]++;
        }

        // Add numbers with zero modulo to answer
        int ans = fre[0];

        // Find minimum of elements with modulo
        // frequency one and zero
        int k = Math.Min(fre[1], fre[2]);

        // Add k to the answer
        ans += k;

        // Remove them from frequency
        fre[1] -= k;
        fre[2] -= k;

        // Add numbers possible with
        // remaining frequency
        ans += fre[1] / 3 + fre[2] / 3;

        // Return the required answer
        return ans;
    }

    // Driver code
    static public void Main ()
    {

        int []a = { 1, 4, 10, 7, 11, 2, 8, 5, 9 };

        int n = a.Length;

        // Function call
        Console.WriteLine(MaxNumbers(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// number of elements divisible by 3

// Function to find the maximum
// number of elements divisible by 3
function MaxNumbers(a, n)
{
    // To store frequency of each number
    let fre = new Array(3).fill(0);

    for (let i = 0; i < n; i++) {
        // Store modulo value
        a[i] %= 3;

        // Store frequency
        fre[a[i]]++;
    }

    // Add numbers with zero modulo to answer
    let ans = fre[0];

    // Find minimum of elements with modulo
    // frequency one and zero
    let k = Math.min(fre[1], fre[2]);

    // Add k to the answer
    ans += k;

    // Remove them from frequency
    fre[1] -= k;
    fre[2] -= k;

    // Add numbers possible with
    // remaining frequency
    ans += parseInt(fre[1] / 3) + parseInt(fre[2] / 3);

    // Return the required answer
    return ans;
}

// Driver code

    let a = [ 1, 4, 10, 7, 11, 2, 8, 5, 9 ];

    let n = a.length;

    // Function call
    document.write(MaxNumbers(a, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)