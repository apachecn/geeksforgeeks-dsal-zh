# 使用艾森斯坦不可约性准则

检查不可约性的程序

> 原文:[https://www . geesforgeks . org/program-to-check-for-reducibility-use-eisensteins-reducibility-criteria/](https://www.geeksforgeeks.org/program-to-check-for-irreducibility-using-eisensteins-irreducibility-criterion/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，使得每个数组元素 **arr[i]** 表示以最高次数( **A[0])开始的多项式表达式的系数。x<sup>(N–1)</sup>+A[1]。x<sup>(N–2)</sup>+…+A【N–2】。x+A[N–1])**，任务是通过 [**艾森斯坦不可约准则**](https://en.wikipedia.org/wiki/Eisenstein%27s_criterion) 检查给定方程是否不可约。如果发现**为真**，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** arr[] = {4，7，21，28}
> **输出:**是
> **解释:**
> 给定数组 arr[]表示多项式 4x<sup>3</sup>+7x<sup>2</sup>+21x+28。
> 素数 7 满足艾森斯坦不可约条件，因此多项式是不可约的。
> 
> **输入:** arr[] = {1，2，1}
> **输出:**否

**进场:**考虑**F(x)= a<sub>n</sub>x<sup>n</sup>+a<sub>n–1</sub>x<sup>n–1</sup>+…+a<sub>0</sub>**<sub>。</sub>满足 E **伊森斯坦不可约准则**需要满足的条件如下:

*   存在一个质数 **P** ，这样:
    *   **P** 不除一 <sub>n</sub> 。
    *   **P** 除所有其他系数，即 a<sub>N–1、</sub>a<sub>N–2</sub>、…、a <sub>0</sub> 。
    *   **P<sup>2</sup>T3】不除一 <sub>0</sub> 。**

按照以下步骤解决问题:

*   初始化一个变量，说 **M** 到 **-1，**存储 **A** 的最大值。
*   创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说**素数[]** ，它包含所有小于等于 **A** 的[素数](https://www.geeksforgeeks.org/prime-numbers/)。
*   遍历**素数**数组，对于每个当前索引 **i，**执行以下操作:
    *   检查当前**素数素数【I】**是否满足所有 3 个条件，即:
        *   **A[0]** 不能被**素数【I】**整除。
        *   从 **A[1]** 到**A[N–1]**的所有数字都可以被**素数【I】**整除。
        *   a**【N-1】**不能被**素数【I】**整除。
    *   如果数满足这三个条件，则多项式不可约，因此打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to to implement the sieve
// of eratosthenes
vector<int> SieveOfEratosthenes(int M)
{
    // Stores the prime numbers
    bool isPrime[M + 1];

    // Initialize the prime numbers
    memset(isPrime, true,
           sizeof(isPrime));

    for (int p = 2; p * p <= M; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of
            // p as non-prime
            for (int i = p * p;
                 i <= M; i += p) {
                isPrime[i] = false;
            }
        }
    }

    // Stores all prime numbers less
    // than M
    vector<int> prime;

    for (int i = 2; i <= M; i++) {

        // If the i is the prime numbers
        if (isPrime[i]) {
            prime.push_back(i);
        }
    }

    // Return array having the primes
    return prime;
}

// Function to check whether the three
// conditions of Eisenstein's
// Irreducibility criterion for prime P
bool check(int A[], int P, int N)
{
    // 1st condition
    if (A[0] % P == 0)
        return 0;

    // 2nd condition
    for (int i = 1; i < N; i++)
        if (A[i] % P)
            return 0;

    // 3rd condition
    if (A[N - 1] % (P * P) == 0)
        return 0;

    return 1;
}
// Function to check for Eisensteins
// Irreducubility Criterion
bool checkIrreducibilty(int A[], int N)
{
    // Stores the largest element in A
    int M = -1;

    // Find the maximum element in A
    for (int i = 0; i < N; i++) {
        M = max(M, A[i]);
    }

    // Stores all the prime numbers
    vector<int> primes
        = SieveOfEratosthenes(M + 1);

    // Check if any prime
    // satisfies the conditions
    for (int i = 0;
         i < primes.size(); i++) {

        // Function Call to check
        // for the three conditions
        if (check(A, primes[i], N)) {
            return 1;
        }
    }
    return 0;
}

// Driver Code
int main()
{
    int A[] = { 4, 7, 21, 28 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << checkIrreducibilty(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to to implement the sieve
// of eratosthenes
static ArrayList<Integer> SieveOfEratosthenes(int M)
{

    // Stores the prime numbers
    boolean []isPrime = new boolean[M + 1];

    // Initialize the prime numbers
    for(int i = 0; i < M + 1; i++)
        isPrime[i] = true;

    for(int p = 2; p * p <= M; p++)
    {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true)
        {

            // Update all multiples of
            // p as non-prime
            for(int i = p * p; i <= M; i += p)
            {
                isPrime[i] = false;
            }
        }
    }

    // Stores all prime numbers less
    // than M
    ArrayList<Integer> prime = new ArrayList<Integer>();

    for(int i = 2; i <= M; i++)
    {

        // If the i is the prime numbers
        if (isPrime[i])
        {
            prime.add(i);
        }
    }

    // Return array having the primes
    return prime;
}

// Function to check whether the three
// conditions of Eisenstein's
// Irreducibility criterion for prime P
static int check(int []A, int P, int N)
{

    // 1st condition
    if (A[0] % P == 0)
        return 0;

    // 2nd condition
    for(int i = 1; i < N; i++)
        if (A[i] % P != 0)
            return 0;

    // 3rd condition
    if (A[N - 1] % (P * P) == 0)
        return 0;

    return 1;
}

// Function to check for Eisensteins
// Irreducubility Criterion
static int checkIrreducibilty(int []A, int N)
{

    // Stores the largest element in A
    int M = -1;

    // Find the maximum element in A
    for(int i = 0; i < N; i++)
    {
        M = Math.max(M, A[i]);
    }

    // Stores all the prime numbers
    ArrayList<Integer> primes = SieveOfEratosthenes(M + 1);

    // Check if any prime
    // satisfies the conditions
    for(int i = 0; i < primes.size(); i++)
    {

        // Function Call to check
        // for the three conditions
        if (check(A, primes.get(i), N) == 1)
        {
            return 1;
        }
    }
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int []A = { 4, 7, 21, 28 };
    int N = A.length;

    System.out.print(checkIrreducibilty(A, N));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to to implement the sieve
# of eratosthenes
def SieveOfEratosthenes(M):

    # Stores the prime numbers
    isPrime = [True]*(M + 1)

    for p in range(2, M + 1):
        if p * p > M:
            break

        # If isPrime[p] is not changed,
        # then it is a prime
        if (isPrime[p] == True):

            # Update all multiples of
            # p as non-prime
            for i in range(p * p, M + 1, p):
                isPrime[i] = False

    # Stores all prime numbers less
    # than M
    prime = []

    for i in range(2, M + 1):

        # If the i is the prime numbers
        if (isPrime[i]):
            prime.append(i)

    # Return array having the primes
    return prime

# Function to check whether the three
# conditions of Eisenstein's
# Irreducibility criterion for prime P
def check(A, P, N):
    # 1st condition
    if (A[0] % P == 0):
        return 0

    # 2nd condition
    for i in range(1,N):
        if (A[i] % P):
            return 0

    # 3rd condition
    if (A[N - 1] % (P * P) == 0):
        return 0

    return 1
# Function to check for Eisensteins
# Irreducubility Criterion
def checkIrreducibilty(A, N):
    # Stores the largest element in A
    M = -1

    # Find the maximum element in A
    for i in range(N):
        M = max(M, A[i])

    # Stores all the prime numbers
    primes = SieveOfEratosthenes(M + 1)

    # Check if any prime
    # satisfies the conditions
    for i in range(len(primes)):

        # Function Call to check
        # for the three conditions
        if (check(A, primes[i], N)):
            return 1
    return 0

# Driver Code
if __name__ == '__main__':
    A = [4, 7, 21, 28]
    N = len(A)
    print (checkIrreducibilty(A, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to to implement the sieve
// of eratosthenes
static List<int> SieveOfEratosthenes(int M)
{

    // Stores the prime numbers
    bool []isPrime = new bool[M + 1];

    // Initialize the prime numbers
    for(int i = 0; i < M + 1; i++)
        isPrime[i] = true;

    for(int p = 2; p * p <= M; p++)
    {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true)
        {

            // Update all multiples of
            // p as non-prime
            for(int i = p * p; i <= M; i += p)
            {
                isPrime[i] = false;
            }
        }
    }

    // Stores all prime numbers less
    // than M
    List<int> prime = new List<int>();

    for(int i = 2; i <= M; i++)
    {

        // If the i is the prime numbers
        if (isPrime[i])
        {
            prime.Add(i);
        }
    }

    // Return array having the primes
    return prime;
}

// Function to check whether the three
// conditions of Eisenstein's
// Irreducibility criterion for prime P
static int check(int []A, int P, int N)
{

    // 1st condition
    if (A[0] % P == 0)
        return 0;

    // 2nd condition
    for(int i = 1; i < N; i++)
        if (A[i] % P !=0)
            return 0;

    // 3rd condition
    if (A[N - 1] % (P * P) == 0)
        return 0;

    return 1;
}

// Function to check for Eisensteins
// Irreducubility Criterion
static int checkIrreducibilty(int []A, int N)
{

    // Stores the largest element in A
    int M = -1;

    // Find the maximum element in A
    for(int i = 0; i < N; i++)
    {
        M = Math.Max(M, A[i]);
    }

    // Stores all the prime numbers
    List<int> primes = SieveOfEratosthenes(M + 1);

    // Check if any prime
    // satisfies the conditions
    for(int i = 0; i < primes.Count; i++)
    {

        // Function Call to check
        // for the three conditions
        if (check(A, primes[i], N) == 1)
        {
            return 1;
        }
    }
    return 0;
}

// Driver Code
public static void Main()
{
    int []A = { 4, 7, 21, 28 };
    int N = A.Length;

    Console.Write(checkIrreducibilty(A, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to to implement the sieve
// of eratosthenes
function SieveOfEratosthenes(M)
{
    // Stores the prime numbers
    let isPrime = new Array(M + 1).fill(true);

    for (let p = 2; p * p <= M; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of
            // p as non-prime
            for (let i = p * p;
                 i <= M; i += p) {
                isPrime[i] = false;
            }
        }
    }

    // Stores all prime numbers less
    // than M
    let prime = [];

    for (let i = 2; i <= M; i++) {

        // If the i is the prime numbers
        if (isPrime[i]) {
            prime.push(i);
        }
    }

    // Return array having the primes
    return prime;
}

// Function to check whether the three
// conditions of Eisenstein's
// Irreducibility criterion for prime P
function check(A, P, N)
{
    // 1st condition
    if (A[0] % P == 0)
        return 0;

    // 2nd condition
    for (let i = 1; i < N; i++)
        if (A[i] % P)
            return 0;

    // 3rd condition
    if (A[N - 1] % (P * P) == 0)
        return 0;

    return 1;
}
// Function to check for Eisensteins
// Irreducubility Criterion
function checkIrreducibilty(A, N)
{
    // Stores the largest element in A
    let M = -1;

    // Find the maximum element in A
    for (let i = 0; i < N; i++) {
        M = Math.max(M, A[i]);
    }

    // Stores all the prime numbers
    let primes
        = SieveOfEratosthenes(M + 1);

    // Check if any prime
    // satisfies the conditions
    for (let i = 0;
         i < primes.length; i++) {

        // Function Call to check
        // for the three conditions
        if (check(A, primes[i], N)) {
            return 1;
        }
    }
    return 0;
}

// Driver Code
    let A = [ 4, 7, 21, 28 ];
    let N = A.length;
    document.write(checkIrreducibilty(A, N));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(M + N*P)，其中 M 是数组中* [*最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *而 P 是* [*素数小于 N*](https://www.geeksforgeeks.org/print-all-prime-numbers-less-than-or-equal-to-n/)
***辅助空间:** O(P)*