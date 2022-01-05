# 数组元素乘法中最右边的非零数字

> 原文:[https://www . geeksforgeeks . org/数组元素乘法中最右边的非零数字/](https://www.geeksforgeeks.org/right-most-non-zero-digit-in-multiplication-of-array-elements/)

给定非负整数的数组**arr[]****N**。任务是找到数组元素乘积中最右边的非零数字。
**例:**

> **输入:** arr[] = {3，5，6，90909009}
> **输出:** 7
> **输入:** arr[] = {7，42，11，64}
> **输出:** 6
> 相乘的结果是 206976
> 所以最右边的数字是 6

**进场:**

1.  如果你懂基础数学，这个问题就太简单了。假设你必须找到最右边的正数。如果有 2 和 5，那么一个数字就是 10 的倍数。他们产生一个最后一位为 0 的数字。
2.  现在我们可以做的是把每个数组元素分成最短的可被 5 整除的形式，并增加这种出现的次数。
3.  现在将每个数组元素分成可被 2 整除的最短形式，并减少这样的出现次数。这样我们在乘法中就不会考虑 2 和 5 的乘法。
4.  如果上述两个循环后计数 5 不为 0，则将乘数设置为 1 或 5。
5.  现在将每个数组变量相乘，并通过将余数乘以 10 来存储最后一位数字

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the rightmost non-zero
// digit in the multiplication
// of the array elements
int rightmostNonZero(int a[], int n)
{
    // To store the count of times 5 can
    // divide the array elements
    int c5 = 0;

    // Divide the array elements by 5
    // as much as possible
    for (int i = 0; i < n; i++) {
        while (a[i] > 0 && a[i] % 5 == 0) {
            a[i] /= 5;
            // increase count of 5
            c5++;
        }
    }

    // Divide the array elements by
    // 2 as much as possible
    for (int i = 0; i < n; i++) {
        while (c5 && a[i] > 0 && !(a[i] & 1)) {
            a[i] >>= 1;

            // Decrease count of 5, because a '2' and
            // a '5' makes a number with last digit '0'
            c5--;
        }
    }
    long long ans = 1;
    for (int i = 0; i < n; i++) {
        ans = (ans * a[i] % 10) % 10;
    }

    // If c5 is more than the multiplier
    // should be taken as 5
    if (c5)
        ans = (ans * 5) % 10;

    if (ans)
        return ans;

    return -1;
}

// Driver code
int main()
{
    int a[] = { 7, 42, 11, 64 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << rightmostNonZero(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the rightmost non-zero
// digit in the multiplication
// of the array elements
static int rightmostNonZero(int a[], int n)
{
    // To store the count of times 5 can
    // divide the array elements
    int c5 = 0;

    // Divide the array elements by 5
    // as much as possible
    for (int i = 0; i < n; i++)
    {
        while (a[i] > 0 && a[i] % 5 == 0)
        {
            a[i] /= 5;

            // increase count of 5
            c5++;
        }
    }

    // Divide the array elements by
    // 2 as much as possible
    for (int i = 0; i < n; i++)
    {
        while (c5 != 0 && a[i] > 0 &&
                         (a[i] & 1) == 0)
        {
            a[i] >>= 1;

            // Decrease count of 5, because a '2' and
            // a '5' makes a number with last digit '0'
            c5--;
        }
    }

    int ans = 1;
    for (int i = 0; i < n; i++)
    {
        ans = (ans * a[i] % 10) % 10;
    }

    // If c5 is more than the multiplier
    // should be taken as 5
    if (c5 != 0)
        ans = (ans * 5) % 10;

    if (ans != 0)
        return ans;

    return -1;
}

// Driver code
public static void main(String args[])
{
    int a[] = { 7, 42, 11, 64 };
    int n = a.length;

    System.out.println(rightmostNonZero(a, n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the rightmost non-zero
# digit in the multiplication
# of the array elements
def rightmostNonZero(a, n):

    # To store the count of times 5 can
    # divide the array elements
    c5 = 0

    # Divide the array elements by 5
    # as much as possible
    for i in range(n):
        while (a[i] > 0 and a[i] % 5 == 0):
            a[i] //= 5

            # increase count of 5
            c5 += 1

    # Divide the array elements by
    # 2 as much as possible
    for i in range(n):
        while (c5 and a[i] > 0 and (a[i] & 1) == 0):
            a[i] >>= 1

            # Decrease count of 5, because a '2' and
            # a '5' makes a number with last digit '0'
            c5 -= 1

    ans = 1
    for i in range(n):
        ans = (ans * a[i] % 10) % 10

    # If c5 is more than the multiplier
    # should be taken as 5
    if (c5):
        ans = (ans * 5) % 10

    if (ans):
        return ans

    return -1

# Driver code
a = [7, 42, 11, 64]
n = len(a)

print(rightmostNonZero(a, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the rightmost non-zero
// digit in the multiplication
// of the array elements
static int rightmostNonZero(int[] a, int n)
{

    // To store the count of times 5 can
    // divide the array elements
    int c5 = 0;

    // Divide the array elements by 5
    // as much as possible
    for (int i = 0; i < n; i++)
    {
        while (a[i] > 0 && a[i] % 5 == 0)
        {
            a[i] /= 5;

            // increase count of 5
            c5++;
        }
    }

    // Divide the array elements by
    // 2 as much as possible
    for (int i = 0; i < n; i++)
    {
        while (c5 != 0 && a[i] > 0 &&
                         (a[i] & 1) == 0)
        {
            a[i] >>= 1;

            // Decrease count of 5, because a '2' and
            // a '5' makes a number with last digit '0'
            c5--;
        }
    }

    int ans = 1;
    for (int i = 0; i < n; i++)
    {
        ans = (ans * a[i] % 10) % 10;
    }

    // If c5 is more than the multiplier
    // should be taken as 5
    if (c5 != 0)
        ans = (ans * 5) % 10;

    if (ans != 0)
        return ans;

    return -1;
}

// Driver code
public static void Main()
{
    int[] a = { 7, 42, 11, 64 };
    int n = a.Length;

    Console.WriteLine(rightmostNonZero(a, n));
}
}

// This code is contributed by
// Code_@Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return the rightmost non-zero
    // digit in the multiplication
    // of the array elements
    function rightmostNonZero(a , n)
    {
        // To store the count of times 5 can
        // divide the array elements
        var c5 = 0;

        // Divide the array elements by 5
        // as much as possible
        for (i = 0; i < n; i++) {
            while (a[i] > 0 && a[i] % 5 == 0) {
                a[i] /= 5;

                // increase count of 5
                c5++;
            }
        }

        // Divide the array elements by
        // 2 as much as possible
        for (i = 0; i < n; i++) {
            while (c5 != 0 && a[i] > 0 &&
            (a[i] & 1) == 0)
            {
                a[i] >>= 1;

                // Decrease count of 5,
                // because a '2' and
                // a '5' makes a number with
                // last digit '0'
                c5--;
            }
        }

        var ans = 1;
        for (i = 0; i < n; i++) {
            ans = (ans * a[i] % 10) % 10;
        }

        // If c5 is more than the multiplier
        // should be taken as 5
        if (c5 != 0)
            ans = (ans * 5) % 10;

        if (ans != 0)
            return ans;

        return -1;
    }

    // Driver code

        var a = [ 7, 42, 11, 64 ];
        var n = a.length;

        document.write(rightmostNonZero(a, n));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
6
```