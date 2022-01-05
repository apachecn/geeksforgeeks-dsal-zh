# 不能被另一个给定数整除的数的最大除数

> 原文:[https://www . geesforgeks . org/一个不能被另一个给定数整除的数的最大除数/](https://www.geeksforgeeks.org/largest-divisor-of-a-number-not-divisible-by-another-given-number/)

给定两个正整数 **P** 和 **Q** ，任务是求 **P** 的最大除数，该除数不能被 **Q** 整除。

**示例:**

> **输入:** P = 10，Q = 4
> **输出:** 10
> **说明:** 10 是除 10 但不能被 4 整除的最大数。
> 
> **输入:** P = 12，Q = 6
> **输出:** 4
> **说明:** 4 是除 12 但不能被 6 整除的最大数。

**逼近:**最简单的逼近就是[求 P](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 的所有除数，得到这些除数中最大的一个，这个除数是不能被 **Q** 整除的。

***时间复杂度:** O(√P)*
***辅助空间:** O(1)*

**替代方法:**按照以下步骤解决问题:

*   将 Q 的[质因数的频率计数存储在](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)[散列表](https://www.geeksforgeeks.org/hashing-data-structure/)和**因子**中。
*   初始化一个变量，比如 **ans** ，存储最大的数字 **X** ，这样 **X** 除 **P** 但是不能被 **Q** 整除。
*   遍历 **Q** 的所有除数，并执行以下步骤:
    *   将当前素数除数的频率计数存储在一个变量中，比如**频率**。
    *   将当前素数除数除以 **P** 的次数存储在一个变量中，比如 **cur** ，并将**数**初始化为**当前素数除数*(频率–cur+1)**。
    *   如果 **cur** 的值小于**频率**，则将变量 **ans** 更新为 **P** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   否则，用**数**除 **P** ，并将结果存储在一个变量中，比如 **tempAns** 。
    *   完成上述步骤后，将 **ans** 的值更新为 **ans** 和 **tempAns** 的最大值。
*   完成以上步骤后，打印**和**的值作为最大可能结果。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest number
// X such that it divides P but is not
// divisible by Q
void findTheGreatestX(int P, int Q)
{
    // Stores the frequency count of
    // of all Prime Factors
    map<int, int> divisiors;

    for (int i = 2; i * i <= Q; i++) {

        while (Q % i == 0 and Q > 1) {

            Q /= i;

            // Increment the frequency
            // of the current prime factor
            divisiors[i]++;
        }
    }

    // If Q is a prime factor
    if (Q > 1)
        divisiors[Q]++;

    // Stores the desired result
    int ans = 0;

    // Iterate through all divisors of Q
    for (auto i : divisiors) {

        int frequency = i.second;
        int temp = P;

        // Stores the frequency count
        // of current prime divisor on
        // dividing P
        int cur = 0;

        while (temp % i.first == 0) {
            temp /= i.first;

            // Count the frequency of the
            // current prime factor
            cur++;
        }

        // If cur is less than frequency
        // then P is the final result
        if (cur < frequency) {
            ans = P;
            break;
        }

        temp = P;

        // Iterate to get temporary answer
        for (int j = cur; j >= frequency; j--) {
            temp /= i.first;
        }

        // Update current answer
        ans = max(temp, ans);
    }

    // Print the desired result
    cout << ans;
}

// Driver Code
int main()
{
    // Given P and Q
    int P = 10, Q = 4;

    // Function Call
    findTheGreatestX(P, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the largest number
// X such that it divides P but is not
// divisible by Q
static void findTheGreatestX(int P, int Q)
{

    // Stores the frequency count of
    // of all Prime Factors
    HashMap<Integer, Integer> divisiors = new HashMap<>();

    for(int i = 2; i * i <= Q; i++)
    {
        while (Q % i == 0 &&  Q > 1)
        {
            Q /= i;

            // Increment the frequency
            // of the current prime factor
            if (divisiors.containsKey(i))
            {
                divisiors.put(i, divisiors.get(i) + 1);
            }
            else
            {
                divisiors.put(i, 1);
            }
        }
    }

    // If Q is a prime factor
    if (Q > 1)
        if (divisiors.containsKey(Q))
        {
            divisiors.put(Q, divisiors.get(Q) + 1);
        }
        else
        {
            divisiors.put(Q, 1);
        }

    // Stores the desired result
    int ans = 0;

    // Iterate through all divisors of Q
    for(Map.Entry<Integer, Integer> i : divisiors.entrySet())
    {
        int frequency = i.getValue();
        int temp = P;

        // Stores the frequency count
        // of current prime divisor on
        // dividing P
        int cur = 0;

        while (temp % i.getKey() == 0)
        {
            temp /= i.getKey();

            // Count the frequency of the
            // current prime factor
            cur++;
        }

        // If cur is less than frequency
        // then P is the final result
        if (cur < frequency)
        {
            ans = P;
            break;
        }

        temp = P;

        // Iterate to get temporary answer
        for(int j = cur; j >= frequency; j--)
        {
            temp /= i.getKey();
        }

        // Update current answer
        ans = Math.max(temp, ans);
    }

    // Print the desired result
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given P and Q
    int P = 10, Q = 4;

    // Function Call
    findTheGreatestX(P, Q);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import defaultdict

# Function to find the largest number
# X such that it divides P but is not
# divisible by Q
def findTheGreatestX(P, Q):

    # Stores the frequency count of
    # of all Prime Factors
    divisiors = defaultdict(int)

    i = 2
    while i * i <= Q:

        while (Q % i == 0 and Q > 1):

            Q //= i

            # Increment the frequency
            # of the current prime factor
            divisiors[i] += 1
        i += 1

    # If Q is a prime factor
    if (Q > 1):
        divisiors[Q] += 1

    # Stores the desired result
    ans = 0

    # Iterate through all divisors of Q
    for i in divisiors:

        frequency = divisiors[i]
        temp = P

        # Stores the frequency count
        # of current prime divisor on
        # dividing P
        cur = 0

        while (temp % i == 0):
            temp //= i

            # Count the frequency of the
            # current prime factor
            cur += 1

        # If cur is less than frequency
        # then P is the final result
        if (cur < frequency):
            ans = P
            break

        temp = P

        # Iterate to get temporary answer
        for j in range(cur, frequency-1, -1):
            temp //= i

        # Update current answer
        ans = max(temp, ans)

    # Print the desired result
    print(ans)

# Driver Code
if __name__ == "__main__":

    # Given P and Q
    P = 10
    Q = 4

    # Function Call
    findTheGreatestX(P, Q)

    # This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System.Collections.Generic;
using System;
using System.Linq;

class GFG{

// Function to find the largest number
// X such that it divides P but is not
// divisible by Q
static void findTheGreatestX(int P, int Q)
{

    // Stores the frequency count of
    // of all Prime Factors
    Dictionary<int,
               int> divisers = new Dictionary<int,
                                              int>();

    for(int i = 2; i * i <= Q; i++)
    {
        while (Q % i == 0 && Q > 1)
        {
            Q /= i;

            // Increment the frequency
            // of the current prime factor
            if (divisers.ContainsKey(i))
                divisers[i]++;
            else
                divisers[i] = 1;
        }
    }

    // If Q is a prime factor
    if (Q > 1)
    {
        if (divisers.ContainsKey(Q))
            divisers[Q]++;
        else
            divisers[Q] = 1;
    }

    // Stores the desired result
    int ans = 0;
    var val = divisers.Keys.ToList();

    // Iterate through all divisors of Q
    foreach(var key in val)
    {
        int frequency = divisers[key];
        int temp = P;

        // Stores the frequency count
        // of current prime divisor on
        // dividing P
        int cur = 0;

        while (temp % key == 0)
        {
            temp /= key;

            // Count the frequency of the
            // current prime factor
            cur++;
        }

        // If cur is less than frequency
        // then P is the final result
        if (cur < frequency)
        {
            ans = P;
            break;
        }

        temp = P;

        // Iterate to get temporary answer
        for(int j = cur; j >= frequency; j--)
        {
            temp /= key;
        }

        // Update current answer
        ans = Math.Max(temp, ans);
    }

    // Print the desired result
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)
{

    // Given P and Q
    int P = 10, Q = 4;

    // Function Call
    findTheGreatestX(P, Q);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the largest number
// X such that it divides P but is not
// divisible by Q
function findTheGreatestX(P, Q)
{

    // Stores the frequency count of
    // of all Prime Factors
    var divisiors = new Map();

    for(var i = 2; i * i <= Q; i++)
    {
        while (Q % i == 0 && Q > 1)
        {
            Q = parseInt(Q / i);

            // Increment the frequency
            // of the current prime factor
            if (divisiors.has(i))
                divisiors.set(i, divisiors.get(i) + 1)
            else
                divisiors.set(i, 1)
        }
    }

    // If Q is a prime factor
    if (Q > 1)
        if (divisiors.has(Q))
            divisiors.set(Q, divisiors.get(Q) + 1)
        else
            divisiors.set(Q, 1)

    // Stores the desired result
    var ans = 0;

    // Iterate through all divisors of Q
    divisiors.forEach((value, key) => {
        var frequency = value;
        var temp = P;

        // Stores the frequency count
        // of current prime divisor on
        // dividing P
        var cur = 0;

        while (temp % key == 0)
        {
            temp = parseInt(temp / key);

            // Count the frequency of the
            // current prime factor
            cur++;
        }

        // If cur is less than frequency
        // then P is the final result
        if (cur < frequency)
        {
            ans = P;
        }
        temp = P;

        // Iterate to get temporary answer
        for(var j = cur; j >= frequency; j--)
        {
            temp = parseInt(temp / key);
        }

        // Update current answer
        ans = Math.max(temp, ans);
    });

    // Print the desired result
    document.write(ans);
}

// Driver Code

// Given P and Q
var P = 10, Q = 4;

// Function Call
findTheGreatestX(P, Q);

// This code is contributed by itsok

</script>
```

**Output**

```
10
```

***时间复杂度:**O(sqrt(Q)+log(P)* log(Q))*
***辅助空间:** O(Q)*