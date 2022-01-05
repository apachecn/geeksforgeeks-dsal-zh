# 和可被 K 整除的前 N 个自然数的对数

> 原文:[https://www . geeksforgeeks . org/从第一个 n 个自然数开始的对数，其和可被 k 整除/](https://www.geeksforgeeks.org/number-of-pairs-from-the-first-n-natural-numbers-whose-sum-is-divisible-by-k/)

给定 **N** 和 **K** 的整数值。任务是从 N{1，2，3 …- n-1，N}以内的自然数集合中找出其和可被 k 整除的对的数目
**注:** 1 < = K < = N < = 10^6.
**示例:**

> **输入:** N = 10，K = 5
> **输出:** 9
> **解释:**和可被 5 整除的可能对是(1，4)，(1，9)，(6，4)，(6，9)，(2，3)，(2，8)，(3，7)，(7，8)和(5，10)。因此计数是 9。
> **输入:** N = 7，K = 3
> **输出:**
> **解释:**和可被 3 整除的可能对是(1，2)，(1，5)，(2，4)，(2，7)，(3，6)，(4，5)和(5，7)。因此计数是 7。

**简单的方法:**一种简单的方法是使用嵌套循环，并检查所有可能的对及其 k 的可除性。这种方法的时间复杂度是 O(N^2(),效率不是很高。
**有效方法**:一个有效的方法是使用基本的哈希技术。
**首先**创建数组 rem[K]，其中 rem[i]包含从 1 到 N 的整数计数，当除以 K 时给出余数 I，rem[i]可以通过公式 rem[I]=(N–I)/K+1 计算。
**其次**，两个整数之和可以被 K 整除，如果:

*   两个整数都可以被 k 整除，其计数由 rem[0]*(rem[0]-1)/2 计算。
*   第一个整数的余数是 R，其他数的余数是 K-R，其计数由 rem[R]*rem[K-R]计算，其中 R 从 1 到 K/2 不等。
*   K 是偶数，两个余数都是 K/2。其计数由 rem[K/2]*(rem[K/2]-1)/2 计算。

所有这些情况的计数总和给出了所需的对的计数，使得它们的总和可被 k 整除。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to  find  the number of pairs
// from the set of natural numbers up to
// N whose sum is divisible by K
int findPairCount(int N, int K)
{
    int count = 0;

    // Declaring a Hash to store count
    int rem[K];

    rem[0] = N / K;

    // Storing the count of integers with
    // a specific remainder in Hash array
    for (int i = 1; i < K; i++)
        rem[i] = (N - i) / K + 1;

    // Check if K is even
    if (K % 2 == 0) {
        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder
        // is R and other remainder is K - R
        for (int i = 1; i < K / 2; i++)
            count += rem[i] * rem[K - i];

        // Count of pairs when both the
        // remainders are K / 2
        count += (rem[K / 2] * (rem[K / 2] - 1)) / 2;
    }
    else {
        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder is R
        // and other remainder is K - R
        for (int i = 1; i <= K / 2; i++)
            count += rem[i] * rem[K - i];
    }

    return count;
}

// Driver code
int main()
{
    int N = 10, K = 4;

    // Print the count of pairs
    cout << findPairCount(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to find the number of pairs
// from the set of natural numbers up to
// N whose sum is divisible by K
static int findPairCount(int N, int K)
{
    int count = 0;

    // Declaring a Hash to store count
    int rem[] = new int[K];

    rem[0] = N / K;

    // Storing the count of integers with
    // a specific remainder in Hash array
    for (int i = 1; i < K; i++)
        rem[i] = (N - i) / K + 1;

    // Check if K is even
    if (K % 2 == 0)
    {
        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder
        // is R and other remainder is K - R
        for (int i = 1; i < K / 2; i++)
            count += rem[i] * rem[K - i];

        // Count of pairs when both the
        // remainders are K / 2
        count += (rem[K / 2] * (rem[K / 2] - 1)) / 2;
    }
    else
    {
        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder is R
        // and other remainder is K - R
        for (int i = 1; i <= K / 2; i++)
            count += rem[i] * rem[K - i];
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 10, K = 4;

    // Print the count of pairs
    System.out.println(findPairCount(N, K));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the number of pairs
# from the set of natural numbers up to
# N whose sum is divisible by K
def findPairCount(N, K) :
    count = 0;

    # Declaring a Hash to store count
    rem = [0] * K;

    rem[0] = N // K;

    # Storing the count of integers with
    # a specific remainder in Hash array
    for i in range(1, K) :
        rem[i] = (N - i) // K + 1;

    # Check if K is even
    if (K % 2 == 0) :

        # Count of pairs when both
        # integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) // 2;

        # Count of pairs when one remainder
        # is R and other remainder is K - R
        for i in range(1, K // 2) :
            count += rem[i] * rem[K - i];

        # Count of pairs when both the
        # remainders are K / 2
        count += (rem[K // 2] * (rem[K // 2] - 1)) // 2;

    else :

        # Count of pairs when both
        # integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) // 2;

        # Count of pairs when one remainder is R
        # and other remainder is K - R
        for i in rage(1, K//2 + 1) :
            count += rem[i] * rem[K - i];

    return count;

# Driver code
if __name__ == "__main__" :

    N = 10 ; K = 4;

    # Print the count of pairs
    print(findPairCount(N, K));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
class GfG
{

// Function to find the number of pairs
// from the set of natural numbers up to
// N whose sum is divisible by K
static int findPairCount(int N, int K)
{
    int count = 0;

    // Declaring a Hash to store count
    int[] rem = new int[K];

    rem[0] = N / K;

    // Storing the count of integers with
    // a specific remainder in Hash array
    for (int i = 1; i < K; i++)
        rem[i] = (N - i) / K + 1;

    // Check if K is even
    if (K % 2 == 0)
    {
        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder
        // is R and other remainder is K - R
        for (int i = 1; i < K / 2; i++)
            count += rem[i] * rem[K - i];

        // Count of pairs when both the
        // remainders are K / 2
        count += (rem[K / 2] * (rem[K / 2] - 1)) / 2;
    }
    else
    {
        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder is R
        // and other remainder is K - R
        for (int i = 1; i <= K / 2; i++)
            count += rem[i] * rem[K - i];
    }

    return count;
}

// Driver code
static void Main()
{
    int N = 10, K = 4;

    // Print the count of pairs
    System.Console.WriteLine(findPairCount(N, K));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find the number of pairs
// from the set of natural numbers up
// to N whose sum is divisible by K
function findPairCount($N, $K)
{
    $count = 0;

    // Declaring a Hash to store count
    $rem = array(0, $K, NULL);

    $rem[0] = intval($N / $K);

    // Storing the count of integers with
    // a specific remainder in Hash array
    for ($i = 1; $i < $K; $i++)
        $rem[$i] = intval(($N - $i) / $K ) + 1;

    // Check if K is even
    if ($K % 2 == 0)
    {
        // Count of pairs when both
        // integers are divisible by K
        $count += ($rem[0] * intval(($rem[0] - 1)) / 2);

        // Count of pairs when one remainder
        // is R and other remainder is K - R
        for ($i = 1; $i < intval($K / 2); $i++)
            $count += $rem[$i] * $rem[$K - $i];

        // Count of pairs when both the
        // remainders are K / 2
        $count += ($rem[intval($K / 2)] *
                        intval(($rem[intval($K / 2)] - 1)) / 2);
    }
    else
    {

        // Count of pairs when both
        // integers are divisible by K
        $count += ($rem[0] * intval(($rem[0] - 1)) / 2);

        // Count of pairs when one remainder is R
        // and other remainder is K - R
        for ($i = 1; $i <= intval($K / 2); $i++)
            $count += $rem[$i] * $rem[$K - $i];
    }

    return $count;
}

// Driver code
$N = 10;
$K = 4;

// Print the count of pairs
echo findPairCount($N, $K);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to find the number of pairs
// from the set of natural numbers up to
// N whose sum is divisible by K
function findPairCount(N , K)
{
    var count = 0;

    // Declaring a Hash to store count
    var rem = Array.from({length: K}, (_, i) => 0);

    rem[0] = parseInt(N / K);

    // Storing the count of integers with
    // a specific remainder in Hash array
    for (i = 1; i < K; i++)
        rem[i] = parseInt((N - i) / K + 1);

    // Check if K is even
    if (K % 2 == 0)
    {

        // Count of pairs when both
        // integers are divisible by K
        count += parseInt((rem[0] * (rem[0] - 1)) / 2);

        // Count of pairs when one remainder
        // is R and other remainder is K - R
        for (i = 1; i < K / 2; i++)
            count += rem[i] * rem[K - i];

        // Count of pairs when both the
        // remainders are K / 2
        count += (rem[K / 2] * (rem[K / 2] - 1)) / 2;
    }
    else
    {

        // Count of pairs when both
        // integers are divisible by K
        count += (rem[0] * (rem[0] - 1)) / 2;

        // Count of pairs when one remainder is R
        // and other remainder is K - R
        for (i = 1; i <= K / 2; i++)
            count += rem[i] * rem[K - i];
    }
    return count;
}

// Driver code
var N = 10, K = 4;

// Print the count of pairs
document.write(findPairCount(N, K));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
10
```

**时间复杂度** : O(K)。