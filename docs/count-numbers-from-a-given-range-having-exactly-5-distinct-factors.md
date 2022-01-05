# 从一个给定的范围内计数出正好有 5 个不同因素的数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-给定范围-具有-恰好-5 个不同的因素/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-having-exactly-5-distinct-factors/)

给定两个整数 **L** 和 **R** ，任务是从正好具有 **5 个不同正因子的范围**【L，R】**中计算数字的计数。**

**示例:**

> **输入:** L = 1，R= 100
> **输出:** 2
> **说明:**在[1，100]范围内仅有的两个正好有 5 个质因数的数字是 16 和 81。
> 16 的因子是{1，2，4，8，16}。
> 8 的因子为{1，3，9，27，81}。
> 
> **输入:** L = 1，R = 100
> T3】输出: 2

**天真法:**解决这个问题最简单的方法就是遍历**【L，R】**的范围，对每一个数字，统计其因子。如果因子计数等于 **5** ，则增加计数 **1** 。
***时间复杂度:**(R–L)×√N*
***辅助空间:** O(1)*
**高效方法:**为了优化上述方法，需要对恰好具有 5 个因子的数字进行以下观察。

> 让一个数的素数因式分解为 p<sub>1</sub>T2【aT4<sup>1</sup>×p<sub>2</sub>T10】aT12<sup>2</sup>T15】×p<sub>n</sub>T18】aT20】T21【nT23】。
> 所以这个数的因子数可以写成(a<sub>1</sub>+1)×(a<sub>2</sub>+1)×…×(a<sub>n</sub>+1)。
> 由于本产品必须等于 **5** (是一个[质数](https://www.geeksforgeeks.org/prime-numbers/)，因此本产品中只能存在一个大于 1 的项。那个项必须等于 5。
> 因此，如果 a<sub>I</sub>+1 = 5
> =>a<sub>I</sub>= 4

按照以下步骤解决问题:

*   所需计数是包含 p <sup>4</sup> 作为因子的范围内的数字计数，其中 **p** 是一个质数。
*   为了高效地计算大范围内的 p<sup>4</sup>(**【1，10<sup>18</sup>**)，其思路是使用厄拉多塞的[筛来存储所有素数直到 **10 <sup>4.5</sup> 。**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

const int N = 2e5;

// Stores all prime numbers
// up to 2 * 10^5
vector<long long> prime;

// Function to generate all prime
// numbers up to 2 * 10 ^ 5 using
// Sieve of Eratosthenes
void Sieve()
{
    prime.clear();
    vector<bool> p(N + 1, true);

    // Mark 0 and 1 as non-prime
    p[0] = p[1] = false;

    for (int i = 2; i * i <= N; i++) {

        // If i is prime
        if (p[i] == true) {

            // Mark all its factors as non-prime
            for (int j = i * i; j <= N; j += i) {
                p[j] = false;
            }
        }
    }

    for (int i = 1; i < N; i++) {

        // If current number is prime
        if (p[i]) {

            // Store the prime
            prime.push_back(1LL * pow(i, 4));
        }
    }
}

// Function to count numbers in the
// range [L, R] having exactly 5 factors
void countNumbers(long long int L,
                  long long int R)
{

    // Stores the required count
    int Count = 0;

    for (int p : prime) {

        if (p >= L && p <= R) {
            Count++;
        }
    }
    cout << Count << endl;
}

// Driver Code
int main()
{
    long long L = 16, R = 85000;

    Sieve();

    countNumbers(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{
  static int N = 200000;

  // Stores all prime numbers
  // up to 2 * 10^5
  static int prime[] = new int [20000];
  static int index = 0;

  // Function to generate all prime
  // numbers up to 2 * 10 ^ 5 using
  // Sieve of Eratosthenes
  static void Sieve()
  {
    index = 0;
    int p[] = new int [N + 1];
    for(int i = 0; i <= N; i++)
    {
      p[i] = 1;
    }

    // Mark 0 and 1 as non-prime
    p[0] = p[1] = 0;
    for (int i = 2; i * i <= N; i++)
    {

      // If i is prime
      if (p[i] == 1)
      {

        // Mark all its factors as non-prime
        for (int j = i * i; j <= N; j += i)
        {
          p[j] = 0;
        }
      }
    }
    for (int i = 1; i < N; i++)
    {

      // If current number is prime
      if (p[i] == 1)
      {

        // Store the prime
        prime[index++] = (int)(Math.pow(i, 4));
      }
    }
  }

  // Function to count numbers in the
  // range [L, R] having exactly 5 factors
  static void countNumbers(int L,int R)
  {

    // Stores the required count
    int Count = 0;
    for(int i = 0; i < index; i++)
    {
      int p = prime[i];
      if (p >= L && p <= R)
      {
        Count++;
      }
    }
    System.out.println(Count);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int L = 16, R = 85000;
    Sieve();
    countNumbers(L, R);
  }
}

// This code is contributed by amreshkumar3.
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
N = 2 * 100000

# Stores all prime numbers
# up to 2 * 10^5
prime = [0] * N

# Function to generate all prime
# numbers up to 2 * 10 ^ 5 using
# Sieve of Eratosthenes
def Sieve() :
    p = [True] * (N + 1)

    # Mark 0 and 1 as non-prime
    p[0] = p[1] = False
    i = 2
    while(i * i <= N) :

        # If i is prime
        if (p[i] == True) :

            # Mark all its factors as non-prime
            for j in range(i * i, N, i):
                p[j] = False    
        i += 1
    for i in range(N):

        # If current number is prime
        if (p[i] != False) :

            # Store the prime
            prime.append(pow(i, 4))

# Function to count numbers in the
# range [L, R] having exactly 5 factors
def countNumbers(L, R) :

    # Stores the required count
    Count = 0
    for p in prime :
        if (p >= L and p <= R) :
            Count += 1
    print(Count)

# Driver Code
L = 16
R = 85000
Sieve()
countNumbers(L, R)

# This code is contributed by code_hunt.
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{
  static int N = 200000;

  // Stores all prime numbers
  // up to 2 * 10^5
  static int []prime = new int [20000];
  static int index = 0;

  // Function to generate all prime
  // numbers up to 2 * 10 ^ 5 using
  // Sieve of Eratosthenes
  static void Sieve()
  {
    index = 0;
    int []p = new int [N + 1];
    for(int i = 0; i <= N; i++)
    {
      p[i] = 1;
    }

    // Mark 0 and 1 as non-prime
    p[0] = p[1] = 0;
    for (int i = 2; i * i <= N; i++)
    {

      // If i is prime
      if (p[i] == 1)
      {

        // Mark all its factors as non-prime
        for (int j = i * i; j <= N; j += i)
        {
          p[j] = 0;
        }
      }
    }
    for (int i = 1; i < N; i++)
    {

      // If current number is prime
      if (p[i] == 1)
      {

        // Store the prime
        prime[index++] = (int)(Math.Pow(i, 4));
      }
    }
  }

  // Function to count numbers in the
  // range [L, R] having exactly 5 factors
  static void countNumbers(int L,int R)
  {

    // Stores the required count
    int Count = 0;
    for(int i = 0; i < index; i++)
    {
      int p = prime[i];
      if (p >= L && p <= R)
      {
        Count++;
      }
    }
    Console.WriteLine(Count);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int L = 16, R = 85000;
    Sieve();
    countNumbers(L, R);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program of the above approach

let N = 200000;

  // Stores all prime numbers
  // up to 2 * 10^5
  let prime = new Array(20000).fill(0);
  let index = 0;

  // Function to generate all prime
  // numbers up to 2 * 10 ^ 5 using
  // Sieve of Eratosthenes
  function Sieve()
  {
    index = 0;
    let p = new Array (N + 1).fill(0);
    for(let i = 0; i <= N; i++)
    {
      p[i] = 1;
    }

    // Mark 0 and 1 as non-prime
    p[0] = p[1] = 0;
    for (let i = 2; i * i <= N; i++)
    {

      // If i is prime
      if (p[i] == 1)
      {

        // Mark all its factors as non-prime
        for (let j = i * i; j <= N; j += i)
        {
          p[j] = 0;
        }
      }
    }
    for (let i = 1; i < N; i++)
    {

      // If current number is prime
      if (p[i] == 1)
      {

        // Store the prime
        prime[index++] = (Math.pow(i, 4));
      }
    }
  }

  // Function to count numbers in the
  // range [L, R] having exactly 5 factors
  function countNumbers(L, R)
  {

    // Stores the required count
    let Count = 0;
    for(let i = 0; i < index; i++)
    {
      let p = prime[i];
      if (p >= L && p <= R)
      {
        Count++;
      }
    }
    document.write(Count);
  }

    // Driver Code

    let L = 16, R = 85000;
    Sieve();
    countNumbers(L, R);

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*