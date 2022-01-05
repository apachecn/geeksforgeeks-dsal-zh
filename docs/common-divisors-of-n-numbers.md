# N 个数的公约数

> 原文:[https://www.geeksforgeeks.org/common-divisors-of-n-numbers/](https://www.geeksforgeeks.org/common-divisors-of-n-numbers/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找出所有 **N** 整数的所有公约数。
**示例**

> **输入:** arr[] = {6，90，12，18，30，18}
> **输出:** 1 2 3 6
> **说明:**
> 所有数字的 GCD 为 6。
> 现在要找到 6 的所有除数，我们有
> 6 = 1 * 6
> 6 = 2 * 3
> 因此 1，2，3 和 6 是{6，90，12，18，20，18}的公约数。
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1
> **说明:**
> 所有数字的 GCD 为 1。
> 因此所有数字只有一个公约数，即 1。

**进场:**

1.  求给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中所有 **N** 整数的公约数，求**arr【】**中所有整数的[最大公约数(gcd)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。
2.  使用[这篇](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)文章中讨论的方法，找出在上述步骤中获得的[最大公约数(gcd)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 的所有约数。

以下是上述方法的实现:

## C++

```
// C++ program to find all common
// divisors of N numbers
#include <bits/stdc++.h>
using namespace std;

// Function to calculate gcd of
// two numbers
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to print all the
// common divisors
void printAllDivisors(int arr[], int N)
{
    // Variable to find the gcd
    // of N numbers
    int g = arr[0];

    // Set to store all the
    // common divisors
    set<int> divisors;

    // Finding GCD of the given
    // N numbers
    for (int i = 1; i < N; i++) {
        g = gcd(arr[i], g);
    }

    // Finding divisors of the
    // HCF of n numbers
    for (int i = 1; i * i <= g; i++) {
        if (g % i == 0) {
            divisors.insert(i);
            if (g / i != i)
                divisors.insert(g / i);
        }
    }

    // Print all the divisors
    for (auto& it : divisors)
        cout << it << " ";
}

// Driver's Code
int main()
{
    int arr[] = { 6, 90, 12, 18, 30, 24 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function to print all the
    // common divisors
    printAllDivisors(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all common
// divisors of N numbers
import java.util.*;

class GFG
{

// Function to calculate gcd of
// two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to print all the
// common divisors
static void printAllDivisors(int arr[], int N)
{
    // Variable to find the gcd
    // of N numbers
    int g = arr[0];

    // Set to store all the
    // common divisors
    HashSet<Integer> divisors = new HashSet<Integer>();

    // Finding GCD of the given
    // N numbers
    for (int i = 1; i < N; i++)
    {
        g = gcd(arr[i], g);
    }

    // Finding divisors of the
    // HCF of n numbers
    for (int i = 1; i * i <= g; i++)
    {
        if (g % i == 0)
        {
            divisors.add(i);
            if (g / i != i)
                divisors.add(g / i);
        }
    }

    // Print all the divisors
    for (int it : divisors)
        System.out.print(it+ " ");
}

// Driver's Code
public static void main(String[] args)
{
    int arr[] = { 6, 90, 12, 18, 30, 24 };
    int n = arr.length;

    // Function to print all the
    // common divisors
    printAllDivisors(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find all common
# divisors of N numbers

# Function to calculate gcd of
# two numbers
def gcd(a, b):
    if (a == 0):
        return b
    return gcd(b % a, a)

# Function to prall the
# common divisors
def printAllDivisors(arr, N):

    # Variable to find the gcd
    # of N numbers
    g = arr[0]

    # Set to store all the
    # common divisors
    divisors = dict()

    # Finding GCD of the given
    # N numbers
    for i in range(1, N):
        g = gcd(arr[i], g)

    # Finding divisors of the
    # HCF of n numbers
    for i in range(1, g + 1):
        if i*i > g:
            break
        if (g % i == 0):
            divisors[i] = 1
            if (g // i != i):
                divisors[g // i] = 1

    # Prall the divisors
    for it in sorted(divisors):
        print(it, end=" ")

# Driver's Code
if __name__ == '__main__':
    arr= [6, 90, 12, 18, 30, 24]
    n = len(arr)

    # Function to prall the
    # common divisors
    printAllDivisors(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find all common
// divisors of N numbers
using System;
using System.Collections.Generic;

class GFG
{

// Function to calculate gcd of
// two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to print all the
// common divisors
static void printAllDivisors(int []arr, int N)
{
    // Variable to find the gcd
    // of N numbers
    int g = arr[0];

    // Set to store all the
    // common divisors
    HashSet<int> divisors = new HashSet<int>();

    // Finding GCD of the given
    // N numbers
    for (int i = 1; i < N; i++)
    {
        g = gcd(arr[i], g);
    }

    // Finding divisors of the
    // HCF of n numbers
    for (int i = 1; i * i <= g; i++)
    {
        if (g % i == 0)
        {
            divisors.Add(i);
            if (g / i != i)
                divisors.Add(g / i);
        }
    }

    // Print all the divisors
    foreach (int it in divisors)
        Console.Write(it+ " ");
}

// Driver's Code
public static void Main(String[] args)
{
    int []arr = { 6, 90, 12, 18, 30, 24 };
    int n = arr.Length;

    // Function to print all the
    // common divisors
    printAllDivisors(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find all common
// divisors of N numbers

// Function to calculate gcd of
// two numbers
function gcd(a,b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to print all the
// common divisors
function printAllDivisors(arr, N)
{

    // Variable to find the gcd
    // of N numbers
    let g = arr[0];

    // Set to store all the
    // common divisors
    let divisors = new Set();

    // Finding GCD of the given
    // N numbers
    for (let i = 1; i < N; i++)
    {
        g = gcd(arr[i], g);
    }

    // Finding divisors of the
    // HCF of n numbers
    for (let i = 1; i * i <= g; i++)
    {
        if (g % i == 0)
        {
            divisors.add(i);
            if (Math.floor(g / i) != i)
                divisors.add(Math.floor(g / i));
        }
    }

    // Print all the divisors
    for (let it of divisors.values())
        document.write(it+ " ");
}

// Driver's Code
let arr=[6, 90, 12, 18, 30, 24];
let n = arr.length;

// Function to print all the
// common divisors
printAllDivisors(arr, n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
1 2 3 6
```

**时间复杂度:** O(N*log(M))，其中 N 是给定数组的长度，M 是数组中的最大元素。

**辅助空间:** O((log(max(a，b))) <sup>3/2</sup> )