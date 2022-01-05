# 求数组中所有对的最小 GCD

> 原文:[https://www . geesforgeks . org/find-minimum-gcd-of-all-pairs-in-a-array/](https://www.geeksforgeeks.org/find-minimum-gcd-of-all-pairs-in-an-array/)

给定一个正整数数组 **arr** ，任务是为给定数组的任意一对找到最小可能 GCD。
**例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1
> **解释:**
> GCD(1，2) = 1。
> **输入:** arr[] = {2，4，6，8，3}
> **输出:** 1

**逼近:**
如果我们观察清楚，会注意到任意两个数的最小 GCD 将是数组中所有元素的 GCD。这种观察背后的原因是，如果最小化整个阵列的 GCD 的元素出现在任何对中，则出现该对的最小 GCD。

> **图解:**
> 让我们考虑一个数组 arr[] = {2，4，6，8，3}。
> 除 3 以外的所有数组元素的 GCD 为 2。考虑到 3，gcd 最小化为 1。
> 所有可能对的 GCD 为:
> gcd(2，4) = 2
> gcd(2，6) = 2
> gcd(2，8) = 2
> gcd(2，3) = 1
> gcd(4，6) = 2
> gcd(4，8) = 4
> gcd(4，3) = 1
> gcd(6，3) = 3
> gcd(6，8) = 2

下面的代码是上述方法的实现:

## C++

```
// C++ program to find the
// minimum GCD of any pair
// in the array
#include <bits/stdc++.h>
using namespace std;

// Function returns the
// Minimum GCD of any pair
int MinimumGCD(int arr[], int n)
{
    int g = 0;

    // Finding GCD of all the
    // elements in the array.
    for (int i = 0; i < n; i++) {
        g = __gcd(g, arr[i]);
    }
    return g;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << MinimumGCD(arr, N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum GCD of any pair
// in the array
import java.util.*;

class GFG{

static int __gcd(int a, int b)
{
    if(b == 0)
        return a;
    else
        return __gcd(b, a % b);
}

// Function returns the
// minimum GCD of any pair
static int MinimumGCD(int arr[], int n)
{
    int g = 0;

    // Finding GCD of all the
    // elements in the array.
    for(int i = 0; i < n; i++)
    {
       g = __gcd(g, arr[i]);
    }

    return g;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 6, 8, 3 };
    int N = arr.length;

    System.out.println(MinimumGCD(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the
# minimum GCD of any pair
# in the array

from math import gcd

# Function returns the
# Minimum GCD of any pair
def MinimumGCD(arr, n):
    g = 0

    # Finding GCD of all the
    # elements in the array.
    for i in range(n):
        g = gcd(g, arr[i])
    return g

# Driver code
if __name__ == '__main__':

    arr = [ 2, 4, 6, 8, 3 ]

    N = len(arr)
    print(MinimumGCD(arr, N))

# This code is contributed by Samarth
```

## C#

```
// C# program to find the
// minimum GCD of any pair
// in the array
using System;

class GFG{

static int __gcd(int a, int b)
{
    if(b == 0)
        return a;
    else
        return __gcd(b, a % b);
}

// Function returns the
// minimum GCD of any pair
static int MinimumGCD(int []arr, int n)
{
    int g = 0;

    // Finding GCD of all the
    // elements in the array.
    for(int i = 0; i < n; i++)
    {
       g = __gcd(g, arr[i]);
    }

    return g;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 4, 6, 8, 3 };
    int N = arr.Length;

    Console.WriteLine(MinimumGCD(arr, N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program to find the
// minimum GCD of any pair
// in the array

function calGCD(a, b) {
  if (!b) {
    return a;
  }

  return calGCD(b, a % b);
}

// Function returns the
// Minimum GCD of any pair
function MinimumGCD(arr, n)
{
    var g = 0;
    var i;
    // Finding GCD of all the
    // elements in the array.
    for (i = 0; i < n; i++) {
        g = calGCD(g, arr[i]);
    }
    return g;
}

// Driver code
    var arr = [2, 4, 6, 8, 3];
    var N = arr.length;
    document.write(MinimumGCD(arr, N));

</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*