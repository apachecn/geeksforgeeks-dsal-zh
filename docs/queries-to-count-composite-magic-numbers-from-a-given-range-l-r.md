# 对给定范围内的复合幻数进行计数的查询[L，R]

> 原文:[https://www . geesforgeks . org/query-to-count-composite-magic-numbers-from-a-给定范围-l-r/](https://www.geeksforgeeks.org/queries-to-count-composite-magic-numbers-from-a-given-range-l-r/)

给定两个大小为 **Q** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **L[]** 和 **R[]** ，任务是从范围**【L[I]，R[I]】**(0≤I<Q)中找出复合幻数即既是[复合数又是](https://www.geeksforgeeks.org/composite-number/)[幻数的数。](https://www.geeksforgeeks.org/check-number-magic-recursive-sum-digits-1/)

**示例:**

> **输入:** Q = 1，L[] = {10}，R[] = {100}
> **输出:** 8
> **说明:**范围内的数字[L[0]，R[0]]既有复合的也有幻数的是{10，28，46，55，64，82，91，100}。
> 
> **输入:** Q = 1，L[] = {1200}，R[] = {1300}
> **输出:** 9
> **说明:**范围[L[0]，R[0]]内既有复合又有幻数的数字为{1207，1216，1225，1234，1243，1252，1261，1270，1288}。

**天真法:**解决问题最简单的方法是遍历**【L【I】【R【I】】**(0≤I<Q)范围内的所有数字，检查每一个数字是不是复合的，是不是幻数。

***时间复杂度:**O(Q * N<sup>3/2</sup>)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，预先计算并存储一定范围内数组中复合幻数的计数。这优化了对 O(1)的每个查询的计算复杂性。按照以下步骤解决问题:

1.  初始化一个整数[数组](https://www.geeksforgeeks.org/array-data-structure/) **dp[]** ，这样 dp[i]存储**合成幻数**到 **i** 的计数。
2.  遍历**【1，10<sup>6</sup>**范围，对于范围内的每个数字，检查是否为**复合幻数**。如果发现为真，用**DP[I–1]+1**更新 **dp[i** 。否则，用**DP[I–1]**更新 **dp[i]**
3.  [同时遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **L[]** 和 **R[]** ，打印**DP[R[I]]–DP[L[I]–1]**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Check if a number is magic
// number or not
bool isMagic(int num)
{
    return (num % 9 == 1);
}

// Check number is composite
// number or not
bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return false;

    // Check if the number is
    // a multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check for multiples of remaining primes
    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to find Composite Magic
// Numbers in given ranges
void find(int L[], int R[], int q)
{
    // dp[i]: Stores the count of
    // composite Magic numbers up to i
    int dp[1000005];

    dp[0] = 0;
    dp[1] = 0;

    // Traverse in the range [1, 1e5)
    for (int i = 1; i < 1000005; i++) {

        // Check if number is Composite number
        // as well as a Magic number or not
        if (isComposite(i) && isMagic(i)) {
            dp[i] = dp[i - 1] + 1;
        }

        else
            dp[i] = dp[i - 1];
    }

    // Print results for each query
    for (int i = 0; i < q; i++)
        cout << dp[R[i]] - dp[L[i] - 1] << endl;
}

// Driver Code
int main()
{
    int L[] = { 10, 3 };
    int R[] = { 100, 2279 };
    int Q = 2;

    find(L, R, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

    // Check if a number is magic
    // number or not
    static boolean isMagic(int num)
    {
        return (num % 9 == 1);
    }

    // Check number is composite
    // number or not
    static boolean isComposite(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;

        if (n <= 3)
            return false;

        // Check if the number is
        // a multiple of 2 or 3
        if (n % 2 == 0 || n % 3 == 0)
            return true;

        // Check for multiples of remaining primes
        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return true;

        return false;
    }

    // Function to find Composite Magic
    // Numbers in given ranges
    static void find(int L[], int R[], int q)
    {
        // dp[i]: Stores the count of
        // composite Magic numbers up to i
        int dp[] = new int[1000005];

        dp[0] = 0;
        dp[1] = 0;

        // Traverse in the range [1, 1e5)
        for (int i = 1; i < 1000005; i++)
        {

            // Check if number is Composite number
            // as well as a Magic number or not
            if (isComposite(i) && isMagic(i) == true)
            {
                dp[i] = dp[i - 1] + 1;
            }

            else
                dp[i] = dp[i - 1];
        }

        // Print results for each query
        for (int i = 0; i < q; i++)
            System.out.println(dp[R[i]] - dp[L[i] - 1]);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int L[] = { 10, 3 };
        int R[] = { 100, 2279 };
        int Q = 2;

        find(L, R, Q);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Check if a number is magic
# number or not
def isMagic(num):

    return (num % 9 == 1)

# Check number is composite
# number or not
def isComposite(n):

    # Corner cases
    if (n <= 1):
        return False

    if (n <= 3):
        return False

    # Check if the number is
    # a multiple of 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return True

    # Check for multiples of remaining primes
    for i in range(5, n + 1, 6):
        if i * i > n + 1:
            break

        if (n % i == 0 or n % (i + 2) == 0):
            return True

    return False

# Function to find Composite Magic
# Numbers in given ranges
def find(L, R, q):

    # dp[i]: Stores the count of
    # composite Magic numbers up to i
    dp = [0] * 1000005

    dp[0] = 0
    dp[1] = 0

    # Traverse in the range [1, 1e5)
    for i in range(1, 1000005):

        # Check if number is Composite number
        # as well as a Magic number or not
        if (isComposite(i) and isMagic(i)):
            dp[i] = dp[i - 1] + 1
        else:
            dp[i] = dp[i - 1]

    # Print results for each query
    for i in range(q):
        print(dp[R[i]] - dp[L[i] - 1])

# Driver Code
if __name__ == '__main__':

    L = [ 10, 3 ]
    R = [ 100, 2279 ]
    Q = 2

    find(L, R, Q)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Check if a number is magic
// number or not
static bool isMagic(int num)
{
    return (num % 9 == 1);
}

// Check number is composite
// number or not
static bool isComposite(int n)
{

    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return false;

    // Check if the number is
    // a multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check for multiples of remaining primes
    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to find Composite Magic
// Numbers in given ranges
static void find(int[] L, int[] R, int q)
{

    // dp[i]: Stores the count of
    // composite Magic numbers up to i
    int[] dp = new int[1000005];

    dp[0] = 0;
    dp[1] = 0;

    // Traverse in the range [1, 1e5)
    for(int i = 1; i < 1000005; i++)
    {

        // Check if number is Composite number
        // as well as a Magic number or not
        if (isComposite(i) && isMagic(i) == true)
        {
            dp[i] = dp[i - 1] + 1;
        }

        else
            dp[i] = dp[i - 1];
    }

    // Print results for each query
    for(int i = 0; i < q; i++)
        Console.WriteLine(dp[R[i]] - dp[L[i] - 1]);
}

// Driver Code
public static void Main ()
{
    int[] L = { 10, 3 };
    int[] R = { 100, 2279 };
    int Q = 2;

    find(L, R, Q);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Check if a number is magic
    // number or not
    function isMagic(num)
    {
        return (num % 9 == 1);
    }

    // Check number is composite
    // number or not
    function isComposite(n)
    {
        // Corner cases
        if (n <= 1)
            return false;

        if (n <= 3)
            return false;

        // Check if the number is
        // a multiple of 2 or 3
        if (n % 2 == 0 || n % 3 == 0)
            return true;

        // Check for multiples of remaining primes
        for (let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return true;

        return false;
    }

    // Function to find Composite Magic
    // Numbers in given ranges
    function find(L, R, q)
    {
        // dp[i]: Stores the count of
        // composite Magic numbers up to i
        let dp = [];

        dp[0] = 0;
        dp[1] = 0;

        // Traverse in the range [1, 1e5)
        for (let i = 1; i < 1000005; i++)
        {

            // Check if number is Composite number
            // as well as a Magic number or not
            if (isComposite(i) && isMagic(i) == true)
            {
                dp[i] = dp[i - 1] + 1;
            }

            else
                dp[i] = dp[i - 1];
        }

        // Prlet results for each query
        for (let i = 0; i < q; i++)
            document.write(dp[R[i]] - dp[L[i] - 1] + "<br/>");
    }

// Driver code

        let L = [ 10, 3 ];
        let R = [100, 2279 ];
        let Q = 2;

        find(L, R, Q);

</script>
```

**Output:** 

```
8
198
```

***时间复杂度:**O(N<sup>3/2</sup>)*
*T8】辅助空间: O(N*