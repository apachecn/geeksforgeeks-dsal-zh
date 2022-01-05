# Honaker 质数

> 原文:[https://www.geeksforgeeks.org/honaker-prime-number/](https://www.geeksforgeeks.org/honaker-prime-number/)

**Honaker 质数**为质数 **P** ，使得 **P** 的位数和 **P** 的指数位数之和为[质数](https://www.geeksforgeeks.org/prime-numbers/)。
很少有 Honaker 质数是:

> 131, 263, 457, 1039, 1049, 1091, 1301, 1361, 1433, 1571, 1913, 1933, 2141, 2221,…

### 检查 N 是否是 Honaker 质数

给定一个整数 **N** ，任务是检查 **N** 是否为 **Honaker 质数**。如果 **N** 是 **Honaker 质数**，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:** N = 131
> **输出:**是
> **说明:**
> 131 位数之和= 1+3+1 = 5
> 32 位数之和= 3 + 2 = 5
> 
> **输入:**N = 161
> T3】输出:否

**方法:**思路是找到给定数字的索引，检查索引和 **N** 的位数之和是否相同。如果相同，则 **N** 为 **Honaker 质数**并打印**“是”**否则打印**“否”**。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define limit 10000000
using namespace std;

int position[limit + 1];

// Function to precompute the position
// of every prime number using Sieve
void sieve()
{
    // 0 and 1 are not prime numbers
    position[0] = -1, position[1] = -1;

    // Variable to store the position
    int pos = 0;

    for (int i = 2; i <= limit; i++) {

        if (position[i] == 0) {

            // Incrementing the position for
            // every prime number
            position[i] = ++pos;
            for (int j = i * 2; j <= limit; j += i)
                position[j] = -1;
        }
    }
}

// Function to get sum of digits
int getSum(int n)
{
    int sum = 0;
    while (n != 0) {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to check whether the given number
// is Honaker Prime number or not
bool isHonakerPrime(int n)
{
    int pos = position[n];
    if (pos == -1)
        return false;
    return getSum(n) == getSum(pos);
}

// Driver Code
int main()
{
    // Precompute the prime numbers till 10^6
    sieve();

    // Given Number
    int N = 121;

    // Function Call
    if (isHonakerPrime(N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

static final int limit = 10000000;
static int []position = new int[limit + 1];

// Function to precompute the position
// of every prime number using Sieve
static void sieve()
{
    // 0 and 1 are not prime numbers
    position[0] = -1;
    position[1] = -1;

    // Variable to store the position
    int pos = 0;
    for (int i = 2; i <= limit; i++)
    {
        if (position[i] == 0)
        {

            // Incrementing the position for
            // every prime number
            position[i] = ++pos;
            for (int j = i * 2; j <= limit; j += i)
                position[j] = -1;
        }
    }
}

// Function to get sum of digits
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to check whether the given number
// is Honaker Prime number or not
static boolean isHonakerPrime(int n)
{
    int pos = position[n];
    if (pos == -1)
        return false;
    return getSum(n) == getSum(pos);
}

// Driver code
public static void main(String[] args)
{
    // Precompute the prime numbers till 10^6
    sieve();

    // Given Number
    int N = 121;

    // Function Call
    if (isHonakerPrime(N))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program for the above approach
limit = 10000000

position = [0] * (limit + 1)

# Function to precompute the position
# of every prime number using Sieve
def sieve():

    # 0 and 1 are not prime numbers
    position[0] = -1
    position[1] = -1

    # Variable to store the position
    pos = 0

    for i in range(2, limit + 1):
        if (position[i] == 0):

            # Incrementing the position for
            # every prime number
            pos += 1
            position[i] = pos

            for j in range(i * 2, limit + 1, i):
                position[j] = -1

# Function to get sum of digits
def getSum(n):

    Sum = 0

    while (n != 0):
        Sum = Sum + n % 10
        n = n // 10

    return Sum

# Function to check whether the given
# number is Honaker Prime number or not
def isHonakerPrime(n):

    pos = position[n]

    if (pos == -1):
        return False

    return bool(getSum(n) == getSum(pos))

# Driver code

# Precompute the prime numbers till 10^6
sieve()

# Given Number
N = 121

# Function Call
if (isHonakerPrime(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for above approach
using System;
class GFG{

static readonly int limit = 10000000;
static int []position = new int[limit + 1];

// Function to precompute the position
// of every prime number using Sieve
static void sieve()
{
    // 0 and 1 are not prime numbers
    position[0] = -1;
    position[1] = -1;

    // Variable to store the position
    int pos = 0;
    for (int i = 2; i <= limit; i++)
    {
        if (position[i] == 0)
        {

            // Incrementing the position for
            // every prime number
            position[i] = ++pos;
            for (int j = i * 2; j <= limit; j += i)
                position[j] = -1;
        }
    }
}

// Function to get sum of digits
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to check whether the given number
// is Honaker Prime number or not
static bool isHonakerPrime(int n)
{
    int pos = position[n];
    if (pos == -1)
        return false;
    return getSum(n) == getSum(pos);
}

// Driver code
public static void Main(String[] args)
{
    // Precompute the prime numbers till 10^6
    sieve();

    // Given Number
    int N = 121;

    // Function Call
    if (isHonakerPrime(N))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for above approach
     const  limit = 10000000;
    let position = Array(limit + 1).fill(0);

    // Function to precompute the position
    // of every prime number using Sieve
    function sieve()
    {

        // 0 and 1 are not prime numbers
        position[0] = -1;
        position[1] = -1;

        // Variable to store the position
        let pos = 0;
        for (let i = 2; i <= limit; i++)
        {
            if (position[i] == 0)
            {

                // Incrementing the position for
                // every prime number
                position[i] = ++pos;
                for (let j = i * 2; j <= limit; j += i)
                    position[j] = -1;
            }
        }
    }

    // Function to get sum of digits
    function getSum( n) {
        let sum = 0;
        while (n != 0) {
            sum = sum + n % 10;
            n = parseInt(n / 10);
        }
        return sum;
    }

    // Function to check whether the given number
    // is Honaker Prime number or not
    function isHonakerPrime( n) {
        let pos = position[n];
        if (pos == -1)
            return false;
        return getSum(n) == getSum(pos);
    }

    // Driver code
    // Precompute the prime numbers till 10^6
    sieve();

    // Given Number
    let N = 121;

    // Function Call
    if (isHonakerPrime(N))
        document.write("Yes\n");
    else
        document.write("No\n");

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
No
```

**参考:**T2https://oeis.org/A033548