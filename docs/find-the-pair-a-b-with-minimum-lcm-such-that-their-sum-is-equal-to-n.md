# 找出 LCM 最小的对(a，b)，使其和等于 N

> 原文:[https://www . geeksforgeeks . org/find-the-pair-a-b-with-minimum-LCM-so-它们的和等于 n/](https://www.geeksforgeeks.org/find-the-pair-a-b-with-minimum-lcm-such-that-their-sum-is-equal-to-n/)

给定一个数字 **N** ，任务是找到两个数字 a 和 b，使得 **a + b = N** 和 **LCM(a，b)** 最小。

**示例:**

> **输入:** N = 15
> **输出:** a = 5，b = 10
> ***解释:***
> *5，10 对的和为 15，它们的 LCM 为 10，这是最小可能。*
> 
> **输入:** N = 4
> **输出:** a = 2，b = 2
> ***解释:***
> *对 2，2 的和为 4，它们的 LCM 为 2，这是最小可能。*

**进场:**思路是采用 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 和 [LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 的概念。以下是步骤:

*   如果 **N** 是一个[素数](https://www.geeksforgeeks.org/prime-numbers/)，那么答案是 **1** 和**N–1**，因为在任何其他情况下 **a + b > N** 或 **LCM( a，b)** 都是**T21】N–1**。这是因为如果 **N** 是素数，那么就意味着 **N** 是奇数。所以 a 和 b，其中任何一个必须是奇数，另一个必须是偶数。因此，LCM(a，b)必须大于 **N** (如果不是 1 和 N–1)，因为 2 始终是一个因素。
*   如果 **N** 不是**一个质数**，那么选择 a，b 使得他们的 **GCD 最大**，因为公式 ***LCM(a，b) = a*b / GCD (a，b)** 。*所以，为了最小化 LCM(a，b)我们必须最大化 GCD(a，b)。
*   如果 **x** 是 **N** 的除数，那么通过简单的数学**T5】a 和 b 可以分别表示为 **N / x** 和**N/x *(x–1)**。现在作为 **a = N / x** 和**b = N/x *(x–1)**，所以他们的 GCD 出来就是 **N / x** 。为了最大化这个 GCD，取**最小的**可能的 x 或者 **N** 最小的可能除数。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if number is
// prime or not
bool prime(int n)
{
    // As 1 is neither prime
    // nor composite return false
    if (n == 1)
        return false;

    // Check if it is divided by any
    // number then it is not prime,
    // return false
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }

    // Check if n is not divided
    // by any number then it is
    // prime and hence return true
    return true;
}

// Function to find the pair (a, b)
// such that sum is N & LCM is minimum
void minDivisior(int n)
{

    // Check if the number is prime
    if (prime(n)) {
        cout << 1 << " " << n - 1;
    }

    // Now, if it is not prime then
    // find the least divisior
    else {
        for (int i = 2; i * i <= n; i++) {

            // Check if divides n then
            // it is a factor
            if (n % i == 0) {

                // Required output is
                // a = n/i & b = n/i*(n-1)
                cout << n / i << " "
                     << n / i * (i - 1);
                break;
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 4;

    // Function call
    minDivisior(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if number is
// prime or not
static boolean prime(int n)
{
    // As 1 is neither prime
    // nor composite return false
    if (n == 1)
        return false;

    // Check if it is divided by any
    // number then it is not prime,
    // return false
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }

    // Check if n is not divided
    // by any number then it is
    // prime and hence return true
    return true;
}

// Function to find the pair (a, b)
// such that sum is N & LCM is minimum
static void minDivisior(int n)
{

    // Check if the number is prime
    if (prime(n))
    {
        System.out.print(1 + " " +  (n - 1));
    }

    // Now, if it is not prime then
    // find the least divisior
    else
    {
        for (int i = 2; i * i <= n; i++)
        {

            // Check if divides n then
            // it is a factor
            if (n % i == 0)
            {

                // Required output is
                // a = n/i & b = n/i*(n-1)
                System.out.print(n / i + " " +
                                (n / i * (i - 1)));
                break;
            }
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;

    // Function call
    minDivisior(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if number is
# prime or not
def prime(n):

    # As 1 is neither prime
    # nor composite return false
    if (n == 1):
        return False

    # Check if it is divided by any
    # number then it is not prime,
    # return false
    for i in range(2, n + 1):
        if i * i > n:
            break
        if (n % i == 0):
            return False

    # Check if n is not divided
    # by any number then it is
    # prime and hence return true
    return True

# Function to find the pair (a, b)
# such that sum is N & LCM is minimum
def minDivisior(n):

    # Check if the number is prime
    if (prime(n)):
        print(1, n - 1)

    # Now, if it is not prime then
    # find the least divisior
    else:
        for i in range(2, n + 1):
            if i * i > n:
                break

            # Check if divides n then
            # it is a factor
            if (n % i == 0):

                # Required output is
                # a = n/i & b = n/i*(n-1)
                print(n // i, n // i * (i - 1))
                break

# Driver Code
N = 4

# Function call
minDivisior(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if number is
// prime or not
static bool prime(int n)
{

    // As 1 is neither prime
    // nor composite return false
    if (n == 1)
        return false;

    // Check if it is divided by any
    // number then it is not prime,
    // return false
    for(int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }

    // Check if n is not divided
    // by any number then it is
    // prime and hence return true
    return true;
}

// Function to find the pair (a, b)
// such that sum is N & LCM is minimum
static void minDivisior(int n)
{

    // Check if the number is prime
    if (prime(n))
    {
        Console.Write(1 + " " + (n - 1));
    }

    // Now, if it is not prime then
    // find the least divisior
    else
    {
        for(int i = 2; i * i <= n; i++)
        {

            // Check if divides n then
            // it is a factor
            if (n % i == 0)
            {

                // Required output is
                // a = n/i & b = n/i*(n-1)
                Console.Write(n / i + " " +
                             (n / i * (i - 1)));
                break;
            }
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4;

    // Function call
    minDivisior(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to check if number is
    // prime or not
    function prime(n)
    {

        // As 1 is neither prime
        // nor composite return false
        if (n == 1)
            return false;

        // Check if it is divided by any
        // number then it is not prime,
        // return false
        for (i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
                return false;
        }

        // Check if n is not divided
        // by any number then it is
        // prime and hence return true
        return true;
    }

    // Function to find the pair (a, b)
    // such that sum is N & LCM is minimum
    function minDivisior(n)
    {

        // Check if the number is prime
        if (prime(n))
        {
            document.write(1 + " " + (n - 1));
        }

        // Now, if it is not prime then
        // find the least divisior
        else
        {
            for (i = 2; i * i <= n; i++)
            {

                // Check if divides n then
                // it is a factor
                if (n % i == 0)
                {

                    // Required output is
                    // a = n/i & b = n/i*(n-1)
                    document.write(n / i + " " + (n / i * (i - 1)));
                    break;
                }
            }
        }
    }

    // Driver Code
        var N = 4;

        // Function call
        minDivisior(N);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
2 2
```

**时间复杂度:*****O(sqrt(N))*** *****辅助空间:** O(1)***