# GCD 等于 K 的四倍体数量

> 原文:[https://www . geesforgeks . org/四倍体数量-带-gcd-等于-k/](https://www.geeksforgeeks.org/number-of-quadruples-with-gcd-equal-to-k/)

给定两个整数 **N** 和 **K** ，任务是求 **(i，j，K，l)** 的四倍计数，使得 **1 ≤ i < j < k < l ≤ N** 和 **gcd(i，j，K，l) = K** 。
**举例:**

> **输入:** N = 10，K = 2
> **输出:** 5
> 有效四元组为(2，4，6，8)、(2，4，6，10)、
> (2，4，8，10)、(2，6，8，10)和(4，6，8，10)
> **输入:** N = 8，K = 1
> **输出:** 69

**进场:**

*   如果一个序列的 gcd 是 **K** ，那么当我们将所有这些数字除以 **K** 时，剩余数字的 gcd 将是 **1** 。
*   现在，为了满足最大数量为 **N** 的四足动物的约束，如果我们找出所有最大数量小于或等于 **N / K** 且具有 gcd **1** 的四足动物的数量，那么我们可以简单地将所有四足动物乘以 **K** 得到答案。
*   用 gcd **1** 求四倍计数，必须用包含排除原理。取 **N / K = M** 。
*   **T1】MC<sub>4</sub>T5】四倍都是可能的总量。**<sup>(M/2)</sup>C<sub>4</sub>**四倍体的 gcd 是 **2** 的倍数。(使用 2 的 M/2 倍数)。同样的，**<sup>(M/3)</sup>C<sub>4</sub>**四倍体的 gcd 是 **3** 的倍数。但是如果两个量都减，那么 **6** 的倍数 gcd 要减两次，所以必须包含**<sup>(M/6)</sup>C<sub>4</sub>**才能加一次。**
*   所以从 **2** 迭代到 **M** ，如果一个数有奇数个不同的质因数(像 2，3，5，11)，那么用该数的 gcd 倍数减去四倍的计数，如果它有偶数个不同的质因数(像 6，10，33)，那么用该数的 gcd 倍数加上四倍的计数。(数不能像 4 一样重复质因数)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate NC4
int nCr(int n)
{
    // Base case to calculate NC4
    if (n < 4)
        return 0;

    int answer = n * (n - 1) * (n - 2) * (n - 3);
    answer /= 24;
    return answer;
}

// Function to return the count of required
// quadruples using Inclusion Exclusion
int countQuadruples(int N, int K)
{
    // Effective N
    int M = N / K;

    int answer = nCr(M);

    // Iterate over 2 to M
    for (int i = 2; i < M; i++) {
        int j = i;

        // Number of divisors of i till M
        int temp2 = M / i;

        // Count stores the number of prime
        // divisors occurring exactly once
        int count = 0;

        // To prevent repetition of prime divisors
        int check = 0;
        int temp = j;

        while (j % 2 == 0) {
            count++;
            j /= 2;
            if (count >= 2)
                break;
        }

        if (count >= 2) {
            check = 1;
        }

        for (int k = 3; k <= sqrt(temp); k += 2) {
            int cnt = 0;

            while (j % k == 0) {
                cnt++;
                j /= k;
                if (cnt >= 2)
                    break;
            }

            if (cnt >= 2) {
                check = 1;
                break;
            }
            else if (cnt == 1)
                count++;
        }

        if (j > 2) {
            count++;
        }

        // If repetition of prime divisors present
        // ignore this number
        if (check)
            continue;
        else {

            // If prime divisor count is odd
            // subtract it from answer else add
            if (count % 2 == 1) {
                answer -= nCr(temp2);
            }
            else {
                answer += nCr(temp2);
            }
        }
    }

    return answer;
}

// Driver code
int main()
{
    int N = 10, K = 2;

    cout << countQuadruples(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to calculate NC4
static int nCr(int n)
{
    // Base case to calculate NC4
    if (n < 4)
        return 0;

    int answer = n * (n - 1) * (n - 2) * (n - 3);
    answer /= 24;
    return answer;
}

// Function to return the count of required
// quadruples using Inclusion Exclusion
static int countQuadruples(int N, int K)
{
    // Effective N
    int M = N / K;

    int answer = nCr(M);

    // Iterate over 2 to M
    for (int i = 2; i < M; i++)
    {
        int j = i;

        // Number of divisors of i till M
        int temp2 = M / i;

        // Count stores the number of prime
        // divisors occurring exactly once
        int count = 0;

        // To prevent repetition of prime divisors
        int check = 0;
        int temp = j;

        while (j % 2 == 0)
        {
            count++;
            j /= 2;
            if (count >= 2)
                break;
        }

        if (count >= 2)
        {
            check = 1;
        }

        for (int k = 3; k <= Math.sqrt(temp); k += 2)
        {
            int cnt = 0;

            while (j % k == 0)
            {
                cnt++;
                j /= k;
                if (cnt >= 2)
                    break;
            }

            if (cnt >= 2)
            {
                check = 1;
                break;
            }
            else if (cnt == 1)
                count++;
        }

        if (j > 2)
        {
            count++;
        }

        // If repetition of prime divisors present
        // ignore this number
        if (check==1)
            continue;
        else
        {

            // If prime divisor count is odd
            // subtract it from answer else add
            if (count % 2 == 1)
            {
                answer -= nCr(temp2);
            }
            else
            {
                answer += nCr(temp2);
            }
        }
    }

    return answer;
}

// Driver code
public static void main(String[] args)
{

    int N = 10, K = 2;

    System.out.println(countQuadruples(N, K));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to calculate NC4
def nCr(n) :

    # Base case to calculate NC4
    if (n < 4) :
        return 0;

    answer = n * (n - 1) * (n - 2) * (n - 3);
    answer //= 24;

    return answer;

# Function to return the count of required
# quadruples using Inclusion Exclusion
def countQuadruples(N, K) :

    # Effective N
    M = N // K;

    answer = nCr(M);

    # Iterate over 2 to M
    for i in range(2, M) :
        j = i;

        # Number of divisors of i till M
        temp2 = M // i;

        # Count stores the number of prime
        # divisors occurring exactly once
        count = 0;

        # To prevent repetition of prime divisors
        check = 0;
        temp = j;

        while (j % 2 == 0) :
            count += 1;
            j //= 2;
            if (count >= 2) :
                break;

        if (count >= 2) :
            check = 1;

        for k in range(3, int(sqrt(temp)), 2) :
            cnt = 0;

            while (j % k == 0) :
                cnt += 1;
                j //= k;
                if (cnt >= 2) :
                    break;

            if (cnt >= 2) :
                check = 1;
                break;
            elif (cnt == 1) :
                count += 1;

        if (j > 2) :
            count += 1;

        # If repetition of prime divisors present
        # ignore this number
        if (check) :
            continue;
        else :

            # If prime divisor count is odd
            # subtract it from answer else add
            if (count % 2 == 1) :
                answer -= nCr(temp2);
            else :
                answer += nCr(temp2);

    return answer;

# Driver code
if __name__ == "__main__" :

    N = 10; K = 2;

    print(countQuadruples(N, K));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to calculate NC4
static int nCr(int n)
{
    // Base case to calculate NC4
    if (n < 4)
        return 0;

    int answer = n * (n - 1) * (n - 2) * (n - 3);
    answer /= 24;
    return answer;
}

// Function to return the count of required
// quadruples using Inclusion Exclusion
static int countQuadruples(int N, int K)
{
    // Effective N
    int M = N / K;

    int answer = nCr(M);

    // Iterate over 2 to M
    for (int i = 2; i < M; i++)
    {
        int j = i;

        // Number of divisors of i till M
        int temp2 = M / i;

        // Count stores the number of prime
        // divisors occurring exactly once
        int count = 0;

        // To prevent repetition of prime divisors
        int check = 0;
        int temp = j;

        while (j % 2 == 0)
        {
            count++;
            j /= 2;
            if (count >= 2)
                break;
        }

        if (count >= 2)
        {
            check = 1;
        }

        for (int k = 3; k <= Math.Sqrt(temp); k += 2)
        {
            int cnt = 0;

            while (j % k == 0)
            {
                cnt++;
                j /= k;
                if (cnt >= 2)
                    break;
            }

            if (cnt >= 2)
            {
                check = 1;
                break;
            }
            else if (cnt == 1)
                count++;
        }

        if (j > 2)
        {
            count++;
        }

        // If repetition of prime divisors present
        // ignore this number
        if (check==1)
            continue;
        else
        {

            // If prime divisor count is odd
            // subtract it from answer else add
            if (count % 2 == 1)
            {
                answer -= nCr(temp2);
            }
            else
            {
                answer += nCr(temp2);
            }
        }
    }

    return answer;
}

// Driver code
public static void Main(String[] args)
{

    int N = 10, K = 2;

    Console.WriteLine(countQuadruples(N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to calculate NC4
function nCr(n)
{
    // Base case to calculate NC4
    if (n < 4)
        return 0;

    let answer = n * (n - 1) * (n - 2) * (n - 3);
    answer = parseInt(answer / 24);
    return answer;
}

// Function to return the count of required
// quadruples using Inclusion Exclusion
function countQuadruples(N, K)
{
    // Effective N
    let M = parseInt(N / K);

    let answer = nCr(M);

    // Iterate over 2 to M
    for (let i = 2; i < M; i++) {
        let j = i;

        // Number of divisors of i till M
        let temp2 = parseInt(M / i);

        // Count stores the number of prime
        // divisors occurring exactly once
        let count = 0;

        // To prevent repetition of prime divisors
        let check = 0;
        let temp = j;

        while (j % 2 == 0) {
            count++;
            j = parseInt(j / 2);
            if (count >= 2)
                break;
        }

        if (count >= 2) {
            check = 1;
        }

        for (let k = 3; k <= Math.sqrt(temp); k += 2)
        {
            let cnt = 0;

            while (j % k == 0) {
                cnt++;
                j = parseInt(j / k);
                if (cnt >= 2)
                    break;
            }

            if (cnt >= 2) {
                check = 1;
                break;
            }
            else if (cnt == 1)
                count++;
        }

        if (j > 2) {
            count++;
        }

        // If repetition of prime divisors present
        // ignore this number
        if (check)
            continue;
        else {

            // If prime divisor count is odd
            // subtract it from answer else add
            if (count % 2 == 1) {
                answer -= nCr(temp2);
            }
            else {
                answer += nCr(temp2);
            }
        }
    }

    return answer;
}

// Driver code
    let N = 10, K = 2;

    document.write(countQuadruples(N, K));

</script>
```

**Output:** 

```
5
```