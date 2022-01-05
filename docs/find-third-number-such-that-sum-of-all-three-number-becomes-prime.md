# 求第三个数，使三个数之和成为质数

> 原文:[https://www . geeksforgeeks . org/find-third-third-number-so-sum-all-three-number-成为质数/](https://www.geeksforgeeks.org/find-third-number-such-that-sum-of-all-three-number-becomes-prime/)

给定两个数字 **A** 和 **B** 。任务是找到大于或等于 1 的最小正整数，使这三个数的和成为素数。
**例:**

> **输入:** A = 2，B = 3
> **输出:** 2
> **解释:**
> 第三个数是 2，因为如果我们把这三个数加起来得到的
> 和是 7，这是一个质数。
> **输入:** A = 5，B = 3
> **输出:** 3

**进场:**

1.  首先在 **sum** 变量中存储给定 2 个数的和。
2.  现在，检查和 1 的**位“与”(& )** 是否等于 1(检查数字是否为奇数)。
3.  如果等于 1，则将 2 分配给变量**温度**，并进入步骤 4。
4.  否则检查 sum 和 temp 变量的和值是否为素数。如果是质数，则打印 temp 变量的值，否则将 temp 变量加 2，直到它小于质数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that will check
// whether number is prime or not
bool prime(int n)
{
    for (int i = 2; i * i <= n; i++) {

        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to print the 3rd number
void thirdNumber(int a, int b)
{
    int sum = 0, temp = 0;

    sum = a + b;
    temp = 1;

    // If the sum is odd
    if (sum & 1) {
        temp = 2;
    }

    // If sum is not prime
    while (!prime(sum + temp)) {
        temp += 2;
    }

    cout << temp;
}

// Driver code
int main()
{
    int a = 3, b = 5;

    thirdNumber(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that will check
// whether number is prime or not
static boolean prime(int n)
{
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to print the 3rd number
static void thirdNumber(int a, int b)
{
    int sum = 0, temp = 0;

    sum = a + b;
    temp = 1;

    // If the sum is odd
    if (sum == 0)
    {
        temp = 2;
    }

    // If sum is not prime
    while (!prime(sum + temp))
    {
        temp += 2;
    }
    System.out.print(temp);
}

// Driver code
static public void main (String []arr)
{
    int a = 3, b = 5;

    thirdNumber(a, b);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that will check
# whether number is prime or not
def prime(n):
    for i in range(2, n + 1):
        if i * i > n + 1:
            break

        if (n % i == 0):
            return False

    return True

# Function to print the 3rd number
def thirdNumber(a, b):
    summ = 0
    temp = 0

    summ = a + b
    temp = 1

    #If the summ is odd
    if (summ & 1):
        temp = 2

    #If summ is not prime
    while (prime(summ + temp) == False):
        temp += 2

    print(temp)

# Driver code
a = 3
b = 5

thirdNumber(a, b)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function that will check
// whether number is prime or not
static bool prime(int n)
{
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to print the 3rd number
static void thirdNumber(int a, int b)
{
    int sum = 0, temp = 0;

    sum = a + b;
    temp = 1;

    // If the sum is odd
    if (sum == 0)
    {
        temp = 2;
    }

    // If sum is not prime
    while (!prime(sum + temp))
    {
        temp += 2;
    }
    Console.Write (temp);
}

// Driver code
static public void Main ()
{
    int a = 3, b = 5;

    thirdNumber(a, b);
}
}

// This code is contributed by Sachin.
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function that will check
    // whether number is prime or not
    function prime(n)
    {
        for (let i = 2; i * i <= n; i++) {

            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Function to print the 3rd number
    function thirdNumber(a, b)
    {
        let sum = 0, temp = 0;

        sum = a + b;
        temp = 1;

        // If the sum is odd
        if ((sum & 1) != 0) {
            temp = 2;
        }

        // If sum is not prime
        while (!prime(sum + temp)) {
            temp += 2;
        }
        document.write(temp);
    }

    let a = 3, b = 5;
    thirdNumber(a, b);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```

时间复杂度:O(sqrt(n))

辅助空间:0(1)