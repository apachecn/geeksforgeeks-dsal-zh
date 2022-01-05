# 通过执行给定的操作将数字减少到 1 |设置 2

> 原文:[https://www . geeksforgeeks . org/通过执行给定的操作将数字减少到 1-set-2/](https://www.geeksforgeeks.org/reduce-a-number-to-1-by-performing-given-operations-set-2/)

给定一个整数 **N** 。任务是在给定操作的最少次数中将给定次数 **N** 减少到 **1** 。您可以在每个步骤中执行以下任何一个操作。

1.  如果这个数是偶数，那么你可以用 **2** 除这个数。
2.  如果数字是奇数，则允许您执行 **(N + 1)** 或**(N–1)**。

任务是通过执行上述操作，打印将数量 **N** 减少到 **1** 所需的最小步数。
**例:**

> **输入:** N = 15
> **输出:** 5
> 15 为奇数 15 + 1 = 16
> 16 为偶数 16 / 2 = 8
> 8 为偶数 8 / 2 = 4
> 4 为偶数 4 / 2 = 2
> 2 为偶数 2 / 2 = 1
> **输入:** N = 4
> **输出:** 2

**方法:**解决上述问题的递归方法已经在[这篇](https://www.geeksforgeeks.org/reduce-a-number-to-1-by-performing-given-operations/)文章中讨论过。在本文中，我们将讨论一种更加优化的方法。
解决方案的第一步是认识到只有当 LSB 为零时才允许移除 LSB，即第一种类型的操作。那么奇数呢。有人可能认为你只需要去掉尽可能多的 1 来增加不正确数字的均匀性，例如:

> 111011 -> 111010 -> 11101 -> 11100 -> 1110 -> 111 -> 1000 -> 100 -> 10 -> 1

然而，这不是最好的方法，因为

> 111011 -> 111100 -> 11110 -> 1111 -> 10000 -> 1000 -> 100 -> 10 -> 1

两者 **111011 - > 111010 和 111011 - > 111100** 去掉相同数量的 1，但第二种方式更好。
因此，必须移除最大数量的 1，当 **n = 3** 时，在平局的情况下做+1 将会失败，因为 **11 - > 10 - > 1** 比**11->100->10->1**好。幸运的是，这是唯一的例外。
所以逻辑是:

*   如果 **N** 为偶数。
    *   执行第一个操作，即通过 **2** 进行分割。
*   如果 **N** 为奇数。
    *   如果 **N = 3** 或**(N–1)**的 **1 的**数量少于 **(N + 1)** 。
        *   减量 **N** 。
    *   其他
        *   递增 **N** 。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of set bits in n
int set_bits(int n)
{
    int count = 0;

    while (n) {
        count += n % 2;
        n /= 2;
    }

    return count;
}

// Function to return the minimum
// steps required to reach 1
int minSteps(int n)
{
    int ans = 0;

    while (n != 1) {

        // If n is even then divide it by 2
        if (n % 2 == 0)
            n /= 2;

        // If n is 3 or the number of set bits
        // in (n - 1) is less than the number
        // of set bits in (n + 1)
        else if (n == 3
                 or set_bits(n - 1) < set_bits(n + 1))
            n--;
        else
            n++;

        // Increment the number of steps
        ans++;
    }

    // Return the minimum number of steps
    return ans;
}

// Driver code
int main()
{
    int n = 15;

    cout << minSteps(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number
// of set bits in n
static int set_bits(int n)
{
    int count = 0;

    while (n > 0)
    {
        count += n % 2;
        n /= 2;
    }
    return count;
}

// Function to return the minimum
// steps required to reach 1
static int minSteps(int n)
{
    int ans = 0;

    while (n != 1)
    {

        // If n is even then divide it by 2
        if (n % 2 == 0)
            n /= 2;

        // If n is 3 or the number of set bits
        // in (n - 1) is less than the number
        // of set bits in (n + 1)
        else if (n == 3
                || set_bits(n - 1) < set_bits(n + 1))
            n--;
        else
            n++;

        // Increment the number of steps
        ans++;
    }

    // Return the minimum number of steps
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 15;

    System.out.print(minSteps(n));
}
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the number
# of set bits in n
def set_bits(n):
    count = 0

    while (n):
        count += n % 2
        n //= 2

    return count

# Function to return the minimum
# steps required to reach 1
def minSteps(n):
    ans = 0

    while (n != 1):

        # If n is even then divide it by 2
        if (n % 2 == 0):
            n //= 2

        # If n is 3 or the number of set bits
        # in (n - 1) is less than the number
        # of set bits in (n + 1)
        elif (n == 3 or set_bits(n - 1) < set_bits(n + 1)):
            n -= 1
        else:
            n += 1

        # Increment the number of steps
        ans += 1

    # Return the minimum number of steps
    return ans

# Driver code
n = 15

print(minSteps(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number
// of set bits in n
static int set_bits(int n)
{
    int count = 0;

    while (n > 0)
    {
        count += n % 2;
        n /= 2;
    }
    return count;
}

// Function to return the minimum
// steps required to reach 1
static int minSteps(int n)
{
    int ans = 0;

    while (n != 1)
    {

        // If n is even then divide it by 2
        if (n % 2 == 0)
            n /= 2;

        // If n is 3 or the number of set bits
        // in (n - 1) is less than the number
        // of set bits in (n + 1)
        else if (n == 3
                || set_bits(n - 1) < set_bits(n + 1))
            n--;
        else
            n++;

        // Increment the number of steps
        ans++;
    }

    // Return the minimum number of steps
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 15;

    Console.Write(minSteps(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the number
// of set bits in n
function set_bits(n)
{
    let count = 0;

    while (n) {
        count += n % 2;
        n = parseInt(n / 2);
    }

    return count;
}

// Function to return the minimum
// steps required to reach 1
function minSteps(n)
{
    let ans = 0;

    while (n != 1) {

        // If n is even then divide it by 2
        if (n % 2 == 0)
            n = parseInt(n / 2);

        // If n is 3 or the number of set bits
        // in (n - 1) is less than the number
        // of set bits in (n + 1)
        else if (n == 3
                 || set_bits(n - 1) < set_bits(n + 1))
            n--;
        else
            n++;

        // Increment the number of steps
        ans++;
    }

    // Return the minimum number of steps
    return ans;
}

// Driver code
    let n = 15;

    document.write(minSteps(n));

</script>
```

**Output:** 

```
5
```