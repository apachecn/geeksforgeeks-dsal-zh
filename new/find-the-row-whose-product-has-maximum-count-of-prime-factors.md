# 查找其乘积具有最大素数的行

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)

给定大小为 **N x M** 的矩阵，任务是打印其乘积具有最大素数计数的行元素。

**示例**：

> **输入**：arr [] [] = {{1,2,3}，{4，5，6}，{7，8，9}};
> **输出**：7 8 9
> **说明**：
> 第 1 行：（1、2、3）具有乘积 6，并且具有 2 个素数。
> 第 2 行：（4、5、6）具有乘积 120，并且具有 3 个素因。
> 第 3 行：（7、8、9）具有乘积 504，并且具有 6 个素因。
> 因此，输出为 7 8 9，因为它具有最大的质因数。
> **输入**：arr [] [] = {{11，12，13}，{14，15，16}，{17，18，19}}
> **输出**：14 15 16

**方法**：

*   通过遍历所有元素并找到其主要因子，可以找到整行中每个主要因子的整体出现次数。 我们使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)进行计数。

*   令素数出现的次数为 **a1，a2，…aK** 。 如果我们有 K 个不同的素因子，那么答案将是：

![(a_{1}+1)(a_{2}+1)(...)*(a_{K}+1) ](img/c9d1f03ed5059c267c3a54b37fc47e9f.png "Rendered by QuickLaTeX.com")

*   将此值与 *max_factor* 中连续存储最大素数的值进行比较。 如果更大，则更新该行的值。

*   继续直到遍历所有行。

    以下是上述方法的实现：

## C++

```cpp

// C++ implementation to find the row
// whose product has maximum number
// of prime factors

#include <bits/stdc++.h>
using namespace std;

#define N 3
#define M 5

int Large = 1e6;

vector<int> prime;

// function for SieveOfEratosthenes
void SieveOfEratosthenes()
{

    // Create a boolean array "isPrime[0..N]"
    // and initialize all entries it as true.
    // A value in isPrime[i] will finally be
    // false if i is not a prime, else true.
    bool isPrime[Large + 1];
    memset(isPrime, true, sizeof(isPrime));

    for (int p = 2; p * p <= Large; p++) {

        // check if isPrime[p] is not changed
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= Large; i += p)
                isPrime[i] = false;
        }
    }

    // Print all isPrime numbers
    for (int p = 2; p <= Large; p++)

        if (isPrime[p])

            prime.push_back(p);
}

// function to display the answer
void Display(int arr[][M], int row)
{

    for (int i = 0; i < M; i++)
        cout << arr[row][i] << " ";
}

// function to Count the row number of
// divisors in particular row multiplication
void countDivisorsMult(int arr[][M])
{

    // Find count of occurrences
    // of each prime factor
    unordered_map<int, int> mp;
    int row_no = 0;
    long long max_factor = 0;

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            int no = arr[i][j];

            for (int k = 0; k < prime.size(); k++) {
                while (no > 1
                       && no % prime[k] == 0) {

                    no /= prime[k];
                    mp[prime[k]]++;
                }

                if (no == 1)
                    break;
            }
        }

        // Compute count of all divisors
        long long int res = 1;
        for (auto it : mp) {
            res *= (it.second + 1L);
        }

        // Update row number if
        // factors of this row is max
        if (max_factor < res) {
            row_no = i;
            max_factor = res;
        }

        // Clearing map to store
        // prime factors for next row
        mp.clear();
    }

    Display(arr, row_no);
}

// Driver code
int main()
{

    int arr[N][M] = { { 1, 2, 3, 10, 23 },
                      { 4, 5, 6, 7, 8 },
                      { 7, 8, 9, 15, 45 } };

    SieveOfEratosthenes();

    countDivisorsMult(arr);

    return 0;
}

```

## Java

```java

// Java implementation to find the row
// whose product has maximum number
// of prime factors
import java.util.*;

class GFG{

static final int N = 3;
static final int M = 5;

static int Large = (int) 1e6;

static Vector<Integer> prime = new Vector<Integer>();

// function for SieveOfEratosthenes
static void SieveOfEratosthenes()
{

    // Create a boolean array "isPrime[0..N]"
    // and initialize all entries it as true.
    // A value in isPrime[i] will finally be
    // false if i is not a prime, else true.
    boolean []isPrime = new boolean[Large + 1];
    Arrays.fill(isPrime, true);

    for (int p = 2; p * p <= Large; p++) {

        // check if isPrime[p] is not changed
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= Large; i += p)
                isPrime[i] = false;
        }
    }

    // Print all isPrime numbers
    for (int p = 2; p <= Large; p++)

        if (isPrime[p])

            prime.add(p);
}

// function to display the answer
static void Display(int arr[][], int row)
{

    for (int i = 0; i < M; i++)
        System.out.print(arr[row][i]+ " ");
}

// function to Count the row number of
// divisors in particular row multiplication
static void countDivisorsMult(int arr[][])
{

    // Find count of occurrences
    // of each prime factor
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();
    int row_no = 0;
    long max_factor = 0;

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            int no = arr[i][j];

            for (int k = 0; k < prime.size(); k++) {
                while (no > 1
                       && no % prime.get(k) == 0) {

                    no /= prime.get(k);
                    if(mp.containsKey(prime.get(k)))
                        mp.put(prime.get(k), prime.get(k)+1);
                    else
                        mp.put(prime.get(k), 1);
                }

                if (no == 1)
                    break;
            }
        }

        // Compute count of all divisors
        int res = 1;
        for (Map.Entry<Integer,Integer> it : mp.entrySet()) {
            res *= (it.getValue() + 1L);
        }

        // Update row number if
        // factors of this row is max
        if (max_factor < res) {
            row_no = i;
            max_factor = res;
        }

        // Clearing map to store
        // prime factors for next row
        mp.clear();
    }

    Display(arr, row_no);
}

// Driver code
public static void main(String[] args)
{

    int arr[][] = { { 1, 2, 3, 10, 23 },
                      { 4, 5, 6, 7, 8 },
                      { 7, 8, 9, 15, 45 } };

    SieveOfEratosthenes();

    countDivisorsMult(arr);

}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 implementation to find the row 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
# whose product has maximum number 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
# of prime factors 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
N = 3
M = 5

Large = int(1e6); 

prime = []; 

# function for SieveOfEratosthenes 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
def SieveOfEratosthenes() :

    # Create a boolean array "isPrime[0..N]" 
    # and initialize all entries it as true. 
    # A value in isPrime[i] will finally be 
    # false if i is not a prime, else true. 
    isPrime = [True]*(Large + 1); 

    for p in range(2, int(Large**(1/2))) : 

        # check if isPrime[p] is not changed 
        if (isPrime[p] == True) :

            # Update all multiples of p 
            for i in range(p*2, Large + 1, p) : 
                isPrime[i] = False; 

    # Print all isPrime numbers 
    for p in range(2, Large + 1) :

        if (isPrime[p]) :

            prime.append(p); 

# function to display the answer 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
def Display(arr, row) : 

    for i in range(M) : 
        print(arr[row][i], end=" "); 

# function to Count the row number of 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
# divisors in particular row multiplication 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
def countDivisorsMult(arr) : 

    # Find count of occurrences 
    # of each prime factor 
    mp = {};
    row_no = 0;max_factor = 0; 

    for i in range(N) :
        for j in range(M) : 
            no = arr[i][j]

            for k in range(len(prime)) :
                while (no > 1 and no % prime[k] == 0) :

                    no //= prime[k];

                    if prime[k] not in mp :
                        mp[prime[k]] = 0

                    mp[prime[k]] += 1;

                if (no == 1) :
                    break; 

        # Compute count of all divisors 
        res = 1; 
        for it in mp :
            res *= mp[it]; 

        # Update row number if 
        # factors of this row is max 
        if (max_factor < res) :
            row_no = i; 
            max_factor = res; 

        # Clearing map to store 
        # prime factors for next row 
        mp.clear(); 

    Display(arr, row_no); 

# Driver code 

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)
if __name__ == "__main__" : 

    arr = [ [ 1, 2, 3, 10, 23 ], 
            [ 4, 5, 6, 7, 8 ], 
            [ 7, 8, 9, 15, 45 ] ]; 

    SieveOfEratosthenes(); 

    countDivisorsMult(arr); 

# This code is contributed by Yash_R

> 原文：[https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/](https://www.geeksforgeeks.org/find-the-row-whose-product-has-maximum-count-of-prime-factors/)

```

## C#

```cs

// C# implementation to find the row
// whose product has maximum number
// of prime factors
using System;
using System.Collections.Generic;
class GFG{ 
static readonly int N = 3;
static readonly int M = 5; 
static int Large = (int) 1e6; 
static List<int> prime = new List<int>();

// function for SieveOfEratosthenes
static void SieveOfEratosthenes()
{ 
    // Create a bool array "isPrime[0..N]"
    // and initialize all entries it as true.
    // A value in isPrime[i] will finally be
    // false if i is not a prime, else true.
    bool []isPrime = new bool[Large + 1];
    for (int p = 0; p <= Large; p++)
        isPrime[p] = true;

    for (int p = 2; p * p <= Large; p++) 
    { 
        // check if isPrime[p] is not changed
        if (isPrime[p] == true) 
        { 
            // Update all multiples of p
            for (int i = p * 2; i <= Large; i += p)
                isPrime[i] = false;
        }
    }

    // Print all isPrime numbers
    for (int p = 2; p <= Large; p++) 
        if (isPrime[p]) 
            prime.Add(p);
}

// function to display the answer
static void Display(int [, ]arr, int row)
{ 
    for (int i = 0; i < M; i++)
        Console.Write(arr[row, i] + " ");
}

// function to Count the row number of
// divisors in particular row multiplication
static void countDivisorsMult(int [, ]arr)
{ 
    // Find count of occurrences
    // of each prime factor
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    int row_no = 0;
    long max_factor = 0; 
    for (int i = 0; i < N; i++) 
    {
        for (int j = 0; j < M; j++) 
        {
            int no = arr[i,j]; 
            for (int k = 0; k < prime.Count; k++) 
            {
                while (no > 1 && no % 
                       prime[k] == 0) 
                { 
                    no /= prime[k];
                    if(mp.ContainsKey(prime[k]))
                        mp[prime[k]] = prime[k] + 1;
                    else
                        mp.Add(prime[k], 1);
                }

                if (no == 1)
                    break;
            }
        }

        // Compute count of all divisors
        int res = 1;
        foreach (KeyValuePair<int,int> it in mp) 
        {
            res *= (it.Value + 1);
        }

        // Update row number if
        // factors of this row is max
        if (max_factor < res) 
        {
            row_no = i;
            max_factor = res;
        }

        // Clearing map to store
        // prime factors for next row
        mp.Clear();
    } 
    Display(arr, row_no);
}

// Driver code
public static void Main(String[] args)
{ 
    int [, ]arr = {{1, 2, 3, 10, 23},
                  {4, 5, 6, 7, 8},
                  {7, 8, 9, 15, 45}}; 
    SieveOfEratosthenes(); 
    countDivisorsMult(arr);
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
7 8 9 15 45

```



* * *

* * *



