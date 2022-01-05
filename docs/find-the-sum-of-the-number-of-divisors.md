# 求除数之和

> 原文:[https://www . geesforgeks . org/find-除数之和/](https://www.geeksforgeeks.org/find-the-sum-of-the-number-of-divisors/)

给定三个整数 **A** 、 **B** 、 **C** ，任务是求
σ<sup>A</sup>T9】I = 1σ<sup>B</sup>T13】j = 1σ<sup>C</sup>T17】k = 1d(I . j . k)，其中 d(x)是 x 的除数，答案可能很大，所以
**例:**

```
Input: A = 2, B = 2, c = 2
Output: 20
Explanation: d(1.1.1) = d(1) = 1;
    d(1·1·2) = d(2) = 2;
    d(1·2·1) = d(2) = 2;
    d(1·2·2) = d(4) = 3;
    d(2·1·1) = d(2) = 2;
    d(2·1·2) = d(4) = 3;
    d(2·2·1) = d(4) = 3;
    d(2·2·2) = d(8) = 4\. 

Input: A = 5, B = 6, C = 7
Output: 1520
```

**进场:**

*   求[范围【1，N】](https://www.geeksforgeeks.org/find-the-number-of-divisors-of-all-numbers-in-the-range-1-n/)内所有数的除数
*   用迭代器 I，j，k 从 1 到 N 运行三个嵌套循环
*   然后用预先计算的除数找到 d(i.j.k)。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

#define N 100005
#define mod 1000000007

// To store the number of divisors
int cnt[N];

// Function to find the number of divisors
// of all numbers in  the range 1 to n
void Divisors()
{
    memset(cnt, 0, sizeof cnt);

    // For every number 1 to n
    for (int i = 1; i < N; i++) {

        // Increase divisors count for every number
        for (int j = 1; j * i < N; j++)
            cnt[i * j]++;
    }
}

// Function to find the sum of divisors
int Sumofdivisors(int A, int B, int C)
{
    // To store sum
    int sum = 0;

    Divisors();

    for (int i = 1; i <= A; i++) {
        for (int j = 1; j <= B; j++) {
            for (int k = 1; k <= C; k++) {
                int x = i * j * k;

                // Count the divisors
                sum += cnt[x];
                if (sum >= mod)
                    sum -= mod;
            }
        }
    }

    return sum;
}

// Driver code
int main()
{

    int A = 5, B = 6, C = 7;

    // Function call
    cout << Sumofdivisors(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above given approach
class GFG
{

    static int N = 100005;
    static int mod = 1000000007;

    // To store the number of divisors
    static int cnt[] = new int[N];

    // Function to find the number of divisors
    // of all numbers in the range 1 to n
    static void Divisors()
    {

        // For every number 1 to n
        for (int i = 1; i < N; i++)
        {

            // Increase divisors count for every number
            for (int j = 1; j * i < N; j++)
            {
                cnt[i * j]++;
            }
        }
    }

    // Function to find the sum of divisors
    static int Sumofdivisors(int A, int B, int C)
    {
        // To store sum
        int sum = 0;

        Divisors();

        for (int i = 1; i <= A; i++)
        {
            for (int j = 1; j <= B; j++)
            {
                for (int k = 1; k <= C; k++)
                {
                    int x = i * j * k;

                    // Count the divisors
                    sum += cnt[x];
                    if (sum >= mod)
                    {
                        sum -= mod;
                    }
                }
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int A = 5, B = 6, C = 7;

        // Function call
        System.out.println(Sumofdivisors(A, B, C));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 code for above given approach
N = 100005
mod = 1000000007

# To store the number of divisors
cnt = [0] * N;

# Function to find the number of divisors
# of all numbers in the range 1 to n
def Divisors() :

    # For every number 1 to n
    for i in range(1, N) :

        # Increase divisors count
        # for every number
        for j in range(1, N // i) :
            cnt[i * j] += 1;

# Function to find the sum of divisors
def Sumofdivisors(A, B, C) :

    # To store sum
    sum = 0;

    Divisors();

    for i in range(1,A + 1) :
        for j in range(1, B + 1) :
            for k in range(1, C + 1) :
                x = i * j * k;

                # Count the divisors
                sum += cnt[x];
                if (sum >= mod) :
                    sum -= mod;

    return sum;

# Driver code
if __name__ == "__main__" :

    A = 5; B = 6; C = 7;

    # Function call
    print(Sumofdivisors(A, B, C));

# This code is contributed by Ryuga
```

## C#

```
// C# code for above given approach
using System;

class GFG
{

    static int N = 100005;
    static int mod = 1000000007;

    // To store the number of divisors
    static int []cnt = new int[N];

    // Function to find the number of divisors
    // of all numbers in the range 1 to n
    static void Divisors()
    {

        // For every number 1 to n
        for (int i = 1; i < N; i++)
        {

            // Increase divisors count for every number
            for (int j = 1; j * i < N; j++)
            {
                cnt[i * j]++;
            }
        }
    }

    // Function to find the sum of divisors
    static int Sumofdivisors(int A, int B, int C)
    {
        // To store sum
        int sum = 0;

        Divisors();

        for (int i = 1; i <= A; i++)
        {
            for (int j = 1; j <= B; j++)
            {
                for (int k = 1; k <= C; k++)
                {
                    int x = i * j * k;

                    // Count the divisors
                    sum += cnt[x];
                    if (sum >= mod)
                    {
                        sum -= mod;
                    }
                }
            }
        }

        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int A = 5, B = 6, C = 7;

        // Function call
        Console.WriteLine(Sumofdivisors(A, B, C));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript code for above given approach

    let N = 100005;
    let mod = 1000000007;

    // To store the number of divisors
    let cnt = new Array(N);
    cnt.fill(0);

    // Function to find the number of divisors
    // of all numbers in the range 1 to n
    function Divisors()
    {

        // For every number 1 to n
        for (let i = 1; i < N; i++)
        {

            // Increase divisors count for every number
            for (let j = 1; j * i < N; j++)
            {
                cnt[i * j]++;
            }
        }
    }

    // Function to find the sum of divisors
    function Sumofdivisors(A, B, C)
    {
        // To store sum
        let sum = 0;

        Divisors();

        for (let i = 1; i <= A; i++)
        {
            for (let j = 1; j <= B; j++)
            {
                for (let k = 1; k <= C; k++)
                {
                    let x = i * j * k;

                    // Count the divisors
                    sum += cnt[x];
                    if (sum >= mod)
                    {
                        sum -= mod;
                    }
                }
            }
        }

        return sum;
    }   
    let A = 5, B = 6, C = 7;

    // Function call
    document.write(Sumofdivisors(A, B, C));

  // This code is contributed by divyeshrabdiya07.
</script>
```

**Output:** 

```
1520
```