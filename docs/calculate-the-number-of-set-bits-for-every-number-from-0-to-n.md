# 计算从 0 到 N 的每个数字的设定位数

> 原文:[https://www . geesforgeks . org/计算从 0 到 n 的每个数字的集位数/](https://www.geeksforgeeks.org/calculate-the-number-of-set-bits-for-every-number-from-0-to-n/)

给定一个非负整数 **N** ，任务是找到从 **0** 到 **N** 的每个数字的设定位数。
**举例:**

> **输入:** N = 3
> **输出:** 0 1 1 2
> 0、1、2、3 可以写成二进制 0、1、10、1 1。
> 1 在二进制表示中的个数是 0、1、1 和 2。
> **输入:** N = 5
> **输出:**0 1 2 1 2

**天真的方法:**运行一个从 0 到 N 的循环，并使用内置的位计数函数 [__builtin_popcount()](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/) ，找到所有所需整数中的设置位数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count
// of set bits in all the
// integers from 0 to n
void findSetBits(int n)
{
    for (int i = 0; i <= n; i++)
        cout << __builtin_popcount(i) << " ";
}

// Driver code
int main()
{
    int n = 5;

    findSetBits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the count
// of set bits in all the
// integers from 0 to n
static void findSetBits(int n)
{
    for (int i = 0; i <= n; i++)
        System.out.print(Integer.bitCount(i) + " ");
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    findSetBits(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
def count(n):
    count = 0
    while (n):
        count += n & 1
        n >>= 1
    return count

# Function to find the count
# of set bits in all the
# integers from 0 to n
def findSetBits(n):
    for i in range(n + 1):
        print(count(i), end = " ")

# Driver code
if __name__ == '__main__':
    n = 5

    findSetBits(n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int count(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

// Function to find the count
// of set bits in all the
// integers from 0 to n
static void findSetBits(int n)
{
    for (int i = 0; i <= n; i++)
        Console.Write(count(i)+" ");
}

// Driver code
public static void Main(String []args)
{
    int n = 5;

    findSetBits(n);
}
}

// This code is contributed by SHUBHAMSINGH10
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    function count(n)
    {
        let count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to find the count
    // of set bits in all the
    // integers from 0 to n
    function findSetBits(n)
    {
        for (let i = 0; i <= n; i++)
            document.write(count(i)+" ");
    }

    let n = 5;

    findSetBits(n);

</script>
```

**Output:** 

```
0 1 1 2 1 2
```

**高效的方法:**让我们写出(0，6)范围内数字的二进制表示。

> 二进制 0–000
> 1 二进制 0–001
> 2 二进制 0–010
> 3 二进制 0–011
> 4 二进制 0–100
> 5 二进制 0–101
> 6 二进制 0–110

因为，任何偶数都可以写成 **(2 * i)** ，任何奇数都可以写成 **(2 * i + 1)** ，其中 **i** 是自然数。
**2，4** 和 **3，6** 的二进制表示中 1 的数量相等，因为乘以任何数字都相当于将其左移 1 [(在此阅读)](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)。
同样，任何偶数 **2 * i** 和 **i** 在其二进制表示中将具有相等数量的**1**。
在 **5(101)** 中 **1 的**数等于在 **2 的**二进制表示+ **1** 中 **1 的**数。所以在任何奇数 **(2 * i + 1)** 的情况下，都将是 **i** 的二进制表示中 **1 的**的个数)+ **1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count
// of set bits in all the
// integers from 0 to n
void findSetBits(int n)
{

    // dp[i] will store the count
    // of set bits in i
    int dp[n + 1];

    // Initialise the dp array
    memset(dp, 0, sizeof(dp));

    // Count of set bits in 0 is 0
    cout << dp[0] << " ";

    // For every number starting from 1
    for (int i = 1; i <= n; i++) {

        // If current number is even
        if (i % 2 == 0) {

            // Count of set bits in i is equal to
            // the count of set bits in (i / 2)
            dp[i] = dp[i / 2];
        }

        // If current element is odd
        else {

            // Count of set bits in i is equal to
            // the count of set bits in (i / 2) + 1
            dp[i] = dp[i / 2] + 1;
        }

        // Print the count of set bits in i
        cout << dp[i] << " ";
    }
}

// Driver code
int main()
{
    int n = 5;

    findSetBits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the count
// of set bits in all the
// integers from 0 to n
static void findSetBits(int n)
{

    // dp[i] will store the count
    // of set bits in i
    int []dp = new int[n + 1];

    // Count of set bits in 0 is 0
    System.out.print(dp[0] + " ");

    // For every number starting from 1
    for (int i = 1; i <= n; i++)
    {

        // If current number is even
        if (i % 2 == 0)
        {

            // Count of set bits in i is equal to
            // the count of set bits in (i / 2)
            dp[i] = dp[i / 2];
        }

        // If current element is odd
        else
        {

            // Count of set bits in i is equal to
            // the count of set bits in (i / 2) + 1
            dp[i] = dp[i / 2] + 1;
        }

        // Print the count of set bits in i
        System.out.print(dp[i] + " ");
    }
}

// Driver code
public static void main(String []args)
{
    int n = 5;

    findSetBits(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the count of set bits
# in all the integers from 0 to n
def findSetBits(n) :

    # dp[i] will store the count
    # of set bits in i
    # Initialise the dp array
    dp = [0] * (n + 1);

    # Count of set bits in 0 is 0
    print(dp[0], end = " ");

    # For every number starting from 1
    for i in range(1, n + 1) :

        # If current number is even
        if (i % 2 == 0) :

            # Count of set bits in i is equal to
            # the count of set bits in (i / 2)
            dp[i] = dp[i // 2];

        # If current element is odd
        else :

            # Count of set bits in i is equal to
            # the count of set bits in (i / 2) + 1
            dp[i] = dp[i // 2] + 1;

        # Print the count of set bits in i
        print(dp[i], end = " ");

# Driver code
if __name__ == "__main__" :

    n = 5;

    findSetBits(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the count
// of set bits in all the
// integers from 0 to n
static void findSetBits(int n)
{

    // dp[i] will store the count
    // of set bits in i
    int []dp = new int[n + 1];

    // Count of set bits in 0 is 0
    Console.Write(dp[0] + " ");

    // For every number starting from 1
    for (int i = 1; i <= n; i++)
    {

        // If current number is even
        if (i % 2 == 0)
        {

            // Count of set bits in i is equal to
            // the count of set bits in (i / 2)
            dp[i] = dp[i / 2];
        }

        // If current element is odd
        else
        {

            // Count of set bits in i is equal to
            // the count of set bits in (i / 2) + 1
            dp[i] = dp[i / 2] + 1;
        }

        // Print the count of set bits in i
        Console.Write(dp[i] + " ");
    }
}

// Driver code
public static void Main(String []args)
{
    int n = 5;

    findSetBits(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to find the count
    // of set bits in all the
    // integers from 0 to n
    function findSetBits(n)
    {

        // dp[i] will store the count
        // of set bits in i
        let dp = new Array(n + 1);
        dp.fill(0);

        // Count of set bits in 0 is 0
        document.write(dp[0] + " ");

        // For every number starting from 1
        for (let i = 1; i <= n; i++)
        {

            // If current number is even
            if (i % 2 == 0)
            {

                // Count of set bits in i is equal to
                // the count of set bits in (i / 2)
                dp[i] = dp[parseInt(i / 2, 10)];
            }

            // If current element is odd
            else
            {

                // Count of set bits in i is equal to
                // the count of set bits in (i / 2) + 1
                dp[i] = dp[parseInt(i / 2, 10)] + 1;
            }

            // Print the count of set bits in i
            document.write(dp[i] + " ");
        }
    }

    let n = 5;

    findSetBits(n);

// This code is contributed by divyeshrabadiya07   
</script>
```

**Output:** 

```
0 1 1 2 1 2
```