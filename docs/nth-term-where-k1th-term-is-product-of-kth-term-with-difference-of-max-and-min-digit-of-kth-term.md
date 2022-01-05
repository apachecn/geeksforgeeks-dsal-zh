# 第 n 项，其中 K+1 项是第 K 项与第 K 项的最大和最小位数之差的乘积

> 原文:[https://www . geeksforgeeks . org/n-term-where-k1th-term-是 kth-term-带有最大和最小数字差值的产品-kth-term/](https://www.geeksforgeeks.org/nth-term-where-k1th-term-is-product-of-kth-term-with-difference-of-max-and-min-digit-of-kth-term/)

给定两个整数 **N** 和 **D** ，任务是求 F(N)的值，其中 F(1)的值为 D，其中 F(K)的给定为:

**例:**

> **输入:** N = 3，D = 487
> **输出:** 15584
> **解释:**
> As F(1) = 487，
> F(2)= 487 *(maxDigit(487)–minDigit(487))= 487 * 4 = 1948
> F(3)= 1948 *(maxDigit(1948)–minDigit(1948

**方法:**思路是借助[循环](https://www.geeksforgeeks.org/c-c-do-while-loop-with-examples/)迭代计算 F(2)到 F(N)的值。此外，每个数字中的最大和最小位数可以通过将数字除以 10 来计算，同时取模得到位数。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the value
// of the given function for the value

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum digit
// in the decimal representation of N
int MIN(int n)
{
    int ans = 11;

    // Loop to find the minimum
    // digit in the number
    while (n) {
        ans = min(ans, n % 10);
        n /= 10;
    }
    return ans;
}

// Function to find maximum digit
// in the decimal representation of N
int MAX(int n)
{
    int ans = -1;

    // Loop to find the maximum
    // digit in the number
    while (n) {
        ans = max(ans, n % 10);
        n /= 10;
    }
    return ans;
}

// Function to find the value
// of the given function
void Find_value(int n, int k)
{
    k--;
    int x = 0;
    int y = 0;

    // Loop to compute the values
    // of the given number
    while (k--) {
        x = MIN(n);
        y = MAX(n);

        if (y - x == 0)
            break;
        n *= (y - x);
    }
    cout << n;
}

// Driver Code
int main()
{
    int N = 487, D = 5;

    // Function Call
    Find_value(N, D);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the value
// of the given function for the value

class GFG{

// Function to find minimum digit in
// the decimal representation of N
static int MIN(int n)
{
    int ans = 11;

    // Loop to find the minimum
    // digit in the number
    while (n > 0)
    {
        ans = Math.min(ans, n % 10);
        n /= 10;
    }
    return ans;
}

// Function to find maximum digit
// in the decimal representation of N
static int MAX(int n)
{
    int ans = -1;

    // Loop to find the maximum
    // digit in the number
    while (n > 0)
    {
        ans = Math.max(ans, n % 10);
        n /= 10;
    }
    return ans;
}

// Function to find the value
// of the given function
static void Find_value(int n, int k)
{
    k--;
    int x = 0;
    int y = 0;

    // Loop to compute the values
    // of the given number
    while (k-- > 0)
    {
        x = MIN(n);
        y = MAX(n);

        if (y - x == 0)
            break;
        n *= (y - x);
    }
    System.out.print(n);
}

// Driver Code
public static void main(String[] args)
{
    int N = 487, D = 5;

    // Function Call
    Find_value(N, D);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the value
# of the given function for the value

# Function to find minimum digit
# in the decimal representation of N
def MIN(n):

    ans = 11

    # Loop to find the minimum
    # digit in the number
    while n:
        ans = min(ans, n % 10)
        n //= 10
    return ans

# Function to find maximum digit in
# the decimal representation of N
def MAX(n):

    ans = -1

    # Loop to find the maximum
    # digit in the number
    while n:
        ans = max(ans, n % 10)
        n //= 10
    return ans

# Function to find the value
# of the given function
def Find_value(n, k):

    k -= 1
    (x, y) = (0, 0)

    # Loop to compute the values
    # of the given number
    while k:
        k -= 1
        x = MIN(n)
        y = MAX(n)
        if ((y - x) == 0):
            break
        n *= (y - x)

    print(n, end = ' ')

# Driver Code
if __name__=='__main__':

    (N, D) = (487, 5)

    # Function Call
    Find_value(N, D)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to find the value
// of the given function for the value
using System;

class GFG{

// Function to find minimum digit in
// the decimal representation of N
static int MIN(int n)
{
    int ans = 11;

    // Loop to find the minimum
    // digit in the number
    while (n > 0)
    {
        ans = Math.Min(ans, n % 10);
        n /= 10;
    }
    return ans;
}

// Function to find maximum digit
// in the decimal representation of N
static int MAX(int n)
{
    int ans = -1;

    // Loop to find the maximum
    // digit in the number
    while (n > 0)
    {
        ans = Math.Max(ans, n % 10);
        n /= 10;
    }
    return ans;
}

// Function to find the value
// of the given function
static void Find_value(int n, int k)
{
    k--;
    int x = 0;
    int y = 0;

    // Loop to compute the values
    // of the given number
    while (k-- > 0)
    {
        x = MIN(n);
        y = MAX(n);

        if (y - x == 0)
            break;
        n *= (y - x);
    }
    Console.Write(n);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 487, D = 5;

    // Function Call
    Find_value(N, D);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript implementation to find the value
// of the given function for the value

// Function to find minimum digit
// in the decimal representation of N
function MIN( n)
{
    let ans = 11;

    // Loop to find the minimum
    // digit in the number
    while (n) {
        ans = parseInt(Math.min(ans, n % 10));
        n = parseInt(n/ 10);
    }
    return ans;
}

// Function to find maximum digit
// in the decimal representation of N
function MAX( n)
{
    let ans = -1;

    // Loop to find the maximum
    // digit in the number
    while (n) {
        ans = parseInt(Math.max(ans, n % 10));
       n = parseInt(n/ 10);
    }
    return ans;
}

// Function to find the value
// of the given function
function Find_value( n,  k)
{
    k--;
    let x = 0;
    let y = 0;

    // Loop to compute the values
    // of the given number
    while (k--) {
        x = parseInt(MIN(n));
        y = parseInt(MAX(n));

        if (y - x == 0)
            break;
        n *= (y - x);
    }
    document.write(n);
}

// Driver Code
let N = 487, D = 5;

    // Function Call
    Find_value(N, D);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
981792
```

**时间复杂度:** O(D*log(N))

**辅助空间:** O(1)