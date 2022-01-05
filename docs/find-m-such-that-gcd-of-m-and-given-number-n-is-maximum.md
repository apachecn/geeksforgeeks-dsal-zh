# 求 M，使得 M 和给定数 N 的 GCD 最大

> 原文:[https://www . geesforgeks . org/find-m-so-gcd-of-m-and-给定的数字-n-is-maximum/](https://www.geeksforgeeks.org/find-m-such-that-gcd-of-m-and-given-number-n-is-maximum/)

给定一个大于 2 的整数 **N** ，任务是找到一个元素 **M** ，使得 **GCD(N，M)** 最大。

**示例:**

> **输入:** N = 10
> **输出:** 5
> **解释:**
> gcd(1，10)，gcd(3，10)，gcd(7，10)，gcd(9，10)为 1，
> gcd(2，10)，gcd(4，10)，gcd(6，10)，gcd(8，10)为 2，
> gcd(5，10)为 5 这是
> 
> **输入:** N = 21
> **输出:** 7
> **说明:**
> gcd(7，21)在 1 到 21 的所有整数中最大。

**天真法:**最简单的方法是循环遍历**【1，N-1】**范围内的所有号码，用 **N** 找到每个号码的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。给定最大 GCD 和 N 的数字是要求的结果。

***时间复杂度:**O(N)*
T5】辅助空间: *O(1)*

**高效途径:**为了优化上述途径，我们观察到两个数的 [GCD 肯定会是其在**【1，N-1】**范围内的除数之一。并且，如果除数最大，GCD 将最大。
因此，想法是找到 **N**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 的所有[因子，并存储这些因子的最大值，这是所需的结果。](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the integer M
// such that gcd(N, M) is maximum
int findMaximumGcd(int n)
{
    // Initialize a variable
    int max_gcd = 1;

    // Find all the divisors of N and
    // return the maximum divisor
    for (int i = 1; i * i <= n; i++) {

        // Check if i is divisible by N
        if (n % i == 0) {

            // Update max_gcd
            if (i > max_gcd)
                max_gcd = i;

            if ((n / i != i)
                && (n / i != n)
                && ((n / i) > max_gcd))
                max_gcd = n / i;
        }
    }

    // Return the maximum value
    return max_gcd;
}

// Driver Code
int main()
{
    // Given Number
    int N = 10;

    // Function Call
    cout << findMaximumGcd(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the integer M
// such that gcd(N, M) is maximum
static int findMaximumGcd(int n)
{

    // Initialize a variable
    int max_gcd = 1;

    // Find all the divisors of N and
    // return the maximum divisor
    for(int i = 1; i * i <= n; i++)
    {

        // Check if i is divisible by N
        if (n % i == 0)
        {

            // Update max_gcd
            if (i > max_gcd)
                max_gcd = i;

            if ((n / i != i) &&
                (n / i != n) &&
               ((n / i) > max_gcd))
                max_gcd = n / i;
        }
    }

    // Return the maximum value
    return max_gcd;
}

// Driver Code
public static void main(String[] args)
{

    // Given Number
    int N = 10;

    // Function Call
    System.out.print(findMaximumGcd(N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the integer M
# such that gcd(N, M) is maximum
def findMaximumGcd(n):

    # Initialize variables
    max_gcd = 1
    i = 1

    # Find all the divisors of N and
    # return the maximum divisor
    while (i * i <= n):

        # Check if i is divisible by N
        if n % i == 0:

            # Update max_gcd
            if (i > max_gcd):
                max_gcd = i

            if ((n / i != i) and
                (n / i != n) and
               ((n / i) > max_gcd)):
                max_gcd = n / i
        i += 1

    # Return the maximum value
    return (int(max_gcd))

# Driver Code
if __name__ == '__main__':

    # Given number
    n = 10

    # Function call
    print(findMaximumGcd(n))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the
// integer M such that
// gcd(N, M) is maximum
static int findMaximumGcd(int n)
{   
  // Initialize a variable
  int max_gcd = 1;

  // Find all the divisors of
  // N and return the maximum
  // divisor
  for(int i = 1;
          i * i <= n; i++)
  {
    // Check if i is
    // divisible by N
    if (n % i == 0)
    {
      // Update max_gcd
      if (i > max_gcd)
        max_gcd = i;

      if ((n / i != i) &&
          (n / i != n) &&
          ((n / i) > max_gcd))
        max_gcd = n / i;
    }
  }

  // Return the maximum
  // value
  return max_gcd;
}

// Driver Code
public static void Main(String[] args)
{   
  // Given Number
  int N = 10;

  // Function Call
  Console.Write(findMaximumGcd(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the integer M
// such that gcd(N, M) is maximum
function findMaximumGcd(n)
{

    // Initialize a variable
    let max_gcd = 1;

    // Find all the divisors of N and
    // return the maximum divisor
    for(let i = 1; i * i <= n; i++)
    {

        // Check if i is divisible by N
        if (n % i == 0)
        {

            // Update max_gcd
            if (i > max_gcd)
                max_gcd = i;

            if ((n / i != i) &&
                (n / i != n) &&
               ((n / i) > max_gcd))
                max_gcd = n / i;
        }
    }

    // Return the maximum value
    return max_gcd;
}

    // Driver Code

    // Given Number
    let N = 10;

    // Function Call
    document.write(findMaximumGcd(N));

</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(log<sub>2</sub>N)*
T7】辅助空间: *O(1)*