# 稀有数字

> 原文:[https://www.geeksforgeeks.org/rare-numbers/](https://www.geeksforgeeks.org/rare-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否为稀有数。

> 稀有数是一个非回文的数 N，N+rev(N)和 N-rev(N)都是完美平方，其中 rev(N)是数 N 的倒数，例如 rev(65) = 56

**示例:**

> **输入:**N = 65
> T3】输出:是
> 65–56 = 9 和 65 + 56 = 121 都是完美平方
> 
> **输入:**N = 10
> T3】输出:否

**方法:**思路是检查 N 是否是回文号，然后返回 false。如果它是非回文的，那么只需检查 N + rev(N)和 N–rev(N)是否都是完美的正方形。

下面是上述方法的实现:

## C++

```
// C++ implementation to check if
// N is a Rare number
#include<bits/stdc++.h>
using namespace std;

// Iterative function to
// reverse digits of num
int reversDigits(int num)
{
    int rev_num = 0;
    while(num > 0)
    {
        rev_num = rev_num*10 + num%10;
        num = num/10;
    }
    return rev_num;
}

// Function to check if N
// is perfect square
bool isPerfectSquare(long double x)
{  
  // Find floating point value of 
  // square root of x.
  long double sr = sqrt(x);

  // If square root is an integer
  return ((sr - floor(sr)) == 0);
}

// Function to check if N is an
// Rare number
bool isRare(int N)
{
    // Find reverse of N
    int reverseN = reversDigits(N);

    // Number should be non-palindromic
    if(reverseN == N)
        return false;

    return isPerfectSquare(N + reverseN) &&
                isPerfectSquare(N - reverseN);
}

// Driver Code
int main()
{
    int n = 65;
    if (isRare(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if N
// is a Rare number
class GFG{

// Iterative function to
// reverse digits of num
static int reversDigits(int num)
{
    int rev_num = 0;
    while(num > 0)
    {
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to check if N
// is perfect square
static boolean isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to check if N is an
// Rare number
static boolean isRare(int N)
{

    // Find reverse of N
    int reverseN = reversDigits(N);

    // Number should be non-palindromic
    if(reverseN == N)
        return false;

    return isPerfectSquare(N + reverseN) &&
           isPerfectSquare(N - reverseN);
}

// Driver code
public static void main(String[] args)
{
    int n = 65;

    if (isRare(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation to check if
# N is a Rare number
import math

# Iterative function to
# reverse digits of num
def reversDigits(num):
    rev_num = 0
    while(num > 0):
        rev_num = rev_num * 10 + num % 10
        num = num // 10

    return rev_num

# Function to check if N
# is perfect square
def isPerfectSquare(x):

    # Find floating point value of
    # square root of x.
    sr = math.sqrt(x)

    # If square root is an integer
    return ((sr - int(sr)) == 0)

# Function to check if N is an
# Rare number
def isRare(N):

    # Find reverse of N
    reverseN = reversDigits(N)

    # Number should be non-palindromic
    if(reverseN == N):
        return False

    return (isPerfectSquare(N + reverseN) and
            isPerfectSquare(N - reverseN))

# Driver Code
N = 65
if (isRare(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya
```

## C#

```
// C# implementation to check if N
// is a Rare number
using System;
class GFG{

// Iterative function to
// reverse digits of num
static int reversDigits(int num)
{
    int rev_num = 0;
    while(num > 0)
    {
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to check if N
// is perfect square
static bool isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function to check if N is an
// Rare number
static bool isRare(int N)
{

    // Find reverse of N
    int reverseN = reversDigits(N);

    // Number should be non-palindromic
    if(reverseN == N)
        return false;

    return isPerfectSquare(N + reverseN) &&
           isPerfectSquare(N - reverseN);
}

// Driver code
public static void Main(String[] args)
{
    int n = 65;

    if (isRare(n))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation to check if N
// is a Rare number

    // Iterative function to
    // reverse digits of num
    function reversDigits( num)
    {
        let rev_num = 0;
        while (num > 0)
        {
            rev_num = rev_num * 10 + num % 10;
            num = parseInt(num / 10);
        }
        return rev_num;
    }

    // Function to check if N
    // is perfect square
    function isPerfectSquare( x)
    {

        // Find floating point value of
        // square root of x.
        let sr = Math.sqrt(x);

        // If square root is an integer
        return ((sr - Math.floor(sr)) == 0);
    }

    // Function to check if N is an
    // Rare number
    function isRare( N)
    {

        // Find reverse of N
        let reverseN = reversDigits(N);

        // Number should be non-palindromic
        if (reverseN == N)
            return false;

        return isPerfectSquare(N + reverseN) && isPerfectSquare(N - reverseN);
    }

    // Driver code    
    let n = 65;

    if (isRare(n)) {
        document.write("Yes");
    } else {
        document.write("No");
    }

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(N <sup>1/2</sup> )
**参考文献:** [OEIS](https://oeis.org/A035519)