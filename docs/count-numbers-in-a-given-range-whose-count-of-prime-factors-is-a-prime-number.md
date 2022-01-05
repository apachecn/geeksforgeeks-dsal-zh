# 对给定范围内质因数计数为质数的数进行计数

> 原文:[https://www . geesforgeks . org/count-numbers-in-给定范围-谁的素数因子计数是素数/](https://www.geeksforgeeks.org/count-numbers-in-a-given-range-whose-count-of-prime-factors-is-a-prime-number/)

给定大小为 **N * 2** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** ，表示形式为 **{L，R}** 的查询。对于每个查询，任务是打印**【L，R】**范围内的数字计数，其中[质数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)等于一个[质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。

**示例:**

> **输入:** Q[][] = {{4，8}，{30，32}}
> **输出:** 3 2
> **解释:**
> 查询 1:
> 素因子 4 = {2，2}且素因子计数= 2
> 素因子 5 = {5}且素因子计数= 1
> 素因子 6 = {2， 3}和质因数的计数= 2
> 质因数为 7 = {7}和质因数的计数= 1
> 质因数为 8 = {2，2，2}和质因数的计数= 3
> 因此，具有质因数计数的范围[4，8]中的总数是质数是 3。
> 查询 2:
> 30 的素因子= {2，3，5}和素因子的计数= 3
> 31 的素因子= {31}和素因子的计数= 1
> 32 的素因子= {2，2，2，2，2}和素因子的计数= 5
> 因此，具有素因子计数的范围[4，8]中的数的总数是 2。
> 
> **输入:** Q[][] = {{7，12}，{10，99 } }
> T3】输出: 4

**天真法:**解决这个问题最简单的方法就是遍历**【L，R】**范围内的所有数字，对于每个数字，检查的质因数的[计数是否为](https://www.geeksforgeeks.org/count-occurrences-of-a-prime-number-in-the-prime-factorization-of-every-element-from-the-given-range/)[质数](https://www.geeksforgeeks.org/prime-numbers/)。如果发现为真，将**计数器**增加 **1** 。遍历后，为每个查询打印**计数器**的值。

***时间复杂度:**O(| Q | *(max(arr[I][1]–arr[I][0]+1))* sqrt(max(arr[I][1])*
***辅助空间:** O (1)*

**高效法:**优化上述方法的思路是利用厄拉多塞的[筛，预计算出](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**【L】<sub>I</sub>，R<sub>I</sub>**范围内各数的[最小质因数。按照以下步骤解决问题:](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)

*   使用厄拉多塞的[筛生成并存储每个元素的](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[最小质因数](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)。
*   使用[筛](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)找出范围**【L】<sub>I</sub>，R<sub>I</sub>**中每个数字的质因数计数。
*   对于每个数，检查质因数的总数是否是质数。如果发现为真，则递增计数器。
*   创建一个前缀和数组，比如 sum[]，其中**和【I】**将存储范围**【0，I】**中元素的和，这些元素的质因数计数是一个质数。
*   最后，对于每个查询，打印值**sum[arr[I][1]]–sum[arr[I][0]–1]**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1001

// Function to find the smallest prime factor
// of all the numbers in range [0, MAX]
vector<int> sieve()
{

    // Stores smallest prime factor of all
    // the numbers in the range [0, MAX]
    vector<int> spf(MAX);

    // No smallest prime factor of
    // 0 and 1 exists
    spf[0] = spf[1] = -1;

    // Traverse all the numbers
    // in the range [1, MAX]
    for (int i = 2; i < MAX; i++) {

        // Update spf[i]
        spf[i] = i;
    }

    // Update all the numbers whose
    // smallest prime factor is 2
    for (int i = 4; i < MAX; i = i + 2) {
        spf[i] = 2;
    }

    // Traverse all the numbers in
    // the range [1, sqrt(MAX)]
    for (int i = 3; i * i < MAX; i++) {

        // Check if i is a prime number
        if (spf[i] == i) {

            // Update all the numbers whose
            // smallest prime factor is i
            for (int j = i * i; j < MAX;
                 j = j + i) {

                // Check if j is
                // a prime number
                if (spf[j] == j) {
                    spf[j] = i;
                }
            }
        }
    }
    return spf;
}

// Function to find count of
// prime factor of num
int countFactors(vector<int>& spf, int num)
{
    // Stores count of
    // prime factor of num
    int count = 0;

    // Calculate count of
    // prime factor
    while (num > 1) {

        // Update count
        count++;

        // Update num
        num = num / spf[num];
    }
    return count;
}

// Function to precalculate the count of
// numbers in the range [0, i] whose count
// of prime factors is a prime number
vector<int> precalculateSum(vector<int>& spf)
{

    // Stores the sum of all the numbers
    // in the range[0, i] count of
    // prime factor is a prime number
    vector<int> sum(MAX);

    // Update sum[0]
    sum[0] = 0;

    // Traverse all the numbers in
    // the range [1, MAX]
    for (int i = 1; i < MAX; i++) {

        // Stores count of prime factor of i
        int prime_factor
            = countFactors(spf, i);

        // If count of prime factor is
        // a prime number
        if (spf[prime_factor] == prime_factor) {

            // Update sum[i]
            sum[i] = sum[i - 1] + 1;
        }
        else {

            // Update sum[i]
            sum[i] = sum[i - 1];
        }
    }
    return sum;
}

// Driver Code
int main()
{
    // Stores smallest prime factor of all
    // the numbers in the range [0, MAX]
    vector<int> spf = sieve();

    // Stores the sum of all the numbers
    // in the range[0, i] count of
    // prime factor is a prime number
    vector<int> sum = precalculateSum(spf);

    int Q[][2] = { { 4, 8 }, { 30, 32 } };

    // int N = sizeof(Q) / sizeof(Q[0]);
    for (int i = 0; i < 2; i++) {
        cout << (sum[Q[i][1]] - sum[Q[i][0] - 1])
             << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

public static int MAX = 1001;

// Function to find the smallest prime factor
// of all the numbers in range [0, MAX]
public static int[] sieve()
{

    // Stores smallest prime factor of all
    // the numbers in the range [0, MAX]
    int spf[] = new int[MAX];

    // No smallest prime factor of
    // 0 and 1 exists
    spf[0] = spf[1] = -1;

    // Traverse all the numbers
    // in the range [1, MAX]
    for(int i = 2; i < MAX; i++)
    {

        // Update spf[i]
        spf[i] = i;
    }

    // Update all the numbers whose
    // smallest prime factor is 2
    for(int i = 4; i < MAX; i = i + 2)
    {
        spf[i] = 2;
    }

    // Traverse all the numbers in
    // the range [1, sqrt(MAX)]
    for(int i = 3; i * i < MAX; i++)
    {

        // Check if i is a prime number
        if (spf[i] == i)
        {

            // Update all the numbers whose
            // smallest prime factor is i
            for(int j = i * i; j < MAX; j = j + i)
            {

                // Check if j is
                // a prime number
                if (spf[j] == j)
                {
                    spf[j] = i;
                }
            }
        }
    }
    return spf;
}

// Function to find count of
// prime factor of num
public static int countFactors(int spf[], int num)
{

    // Stores count of
    // prime factor of num
    int count = 0;

    // Calculate count of
    // prime factor
    while (num > 1)
    {

        // Update count
        count++;

        // Update num
        num = num / spf[num];
    }
    return count;
}

// Function to precalculate the count of
// numbers in the range [0, i] whose count
// of prime factors is a prime number
public static int[] precalculateSum(int spf[])
{

    // Stores the sum of all the numbers
    // in the range[0, i] count of
    // prime factor is a prime number
    int sum[] = new int[MAX];

    // Update sum[0]
    sum[0] = 0;

    // Traverse all the numbers in
    // the range [1, MAX]
    for(int i = 1; i < MAX; i++)
    {

        // Stores count of prime factor of i
        int prime_factor = countFactors(spf, i);

        // If count of prime factor is
        // a prime number
        if (spf[prime_factor] == prime_factor)
        {

            // Update sum[i]
            sum[i] = sum[i - 1] + 1;
        }
        else
        {

            // Update sum[i]
            sum[i] = sum[i - 1];
        }
    }
    return sum;
}  

// Driver code
public static void main(String[] args)
{

    // Stores smallest prime factor of all
    // the numbers in the range [0, MAX]
    int spf[] = sieve();

    // Stores the sum of all the numbers
    // in the range[0, i] count of
    // prime factor is a prime number
    int sum[] = precalculateSum(spf);

    int Q[][] = { { 4, 8 }, { 30, 32 } };

    // int N = sizeof(Q) / sizeof(Q[0]);
    for(int i = 0; i < 2; i++)
    {
        System.out.print((sum[Q[i][1]] -
                          sum[Q[i][0] - 1]) + " ");
    }
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
MAX = 1001

# Function to find the smallest
# prime factor of all the numbers
# in range [0, MAX]
def sieve():

    # Stores smallest prime factor of all
    # the numbers in the range [0, MAX]
    global MAX
    spf = [0] * MAX

    # No smallest prime factor of
    # 0 and 1 exists
    spf[0] = spf[1] = -1

    # Traverse all the numbers
    # in the range [1, MAX]
    for i in range(2, MAX):

        # Update spf[i]
        spf[i] = i

    # Update all the numbers whose
    # smallest prime factor is 2
    for i in range(4, MAX, 2):
        spf[i] = 2

    # Traverse all the numbers in
    # the range [1, sqrt(MAX)]
    for i in range(3, MAX):

        # Check if i is a prime number
        if (spf[i] == i):

            # Update all the numbers whose
            # smallest prime factor is i
            for j in range(i * i, MAX):

                # Check if j is
                # a prime number
                if (spf[j] == j):
                    spf[j] = i

    return spf

# Function to find count of
# prime factor of num
def countFactors(spf, num):

    # Stores count of
    # prime factor of num
    count = 0

    # Calculate count of
    # prime factor
    while (num > 1):

        # Update count
        count += 1

        # Update num
        num = num // spf[num]

    return count

# Function to precalculate the count of
# numbers in the range [0, i] whose count
# of prime factors is a prime number
def precalculateSum(spf):

    # Stores the sum of all the numbers
    # in the range[0, i] count of
    # prime factor is a prime number
    sum = [0] * MAX

    # Traverse all the numbers in
    # the range [1, MAX]
    for i in range(1, MAX):

        # Stores count of prime factor of i
        prime_factor = countFactors(spf, i)

        # If count of prime factor is
        # a prime number
        if (spf[prime_factor] == prime_factor):

            # Update sum[i]
            sum[i] = sum[i - 1] + 1
        else:

            # Update sum[i]
            sum[i] = sum[i - 1]

    return sum

# Driver code
if __name__ == '__main__':

    # Stores smallest prime factor of all
    # the numbers in the range [0, MAX]
    spf = sieve()

    # Stores the sum of all the numbers
    # in the range[0, i] count of
    # prime factor is a prime number
    sum = precalculateSum(spf)

    Q = [ [ 4, 8 ], [ 30, 32 ] ]
    sum[Q[0][1]] += 1

    # N = sizeof(Q) / sizeof(Q[0]);
    for i in range(0, 2):
        print((sum[Q[i][1]] -
               sum[Q[i][0]]), end = " ")

# This code is contributed by Princi Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

public static int MAX = 1001;

// Function to find the smallest
// prime factor of all the numbers
// in range [0, MAX]
public static int[] sieve()
{    
  // Stores smallest prime factor
  // of all the numbers in the
  // range [0, MAX]
  int []spf = new int[MAX];

  // No smallest prime factor
  // of 0 and 1 exists
  spf[0] = spf[1] = -1;

  // Traverse all the numbers
  // in the range [1, MAX]
  for(int i = 2; i < MAX; i++)
  {
    // Update spf[i]
    spf[i] = i;
  }

  // Update all the numbers whose
  // smallest prime factor is 2
  for(int i = 4; i < MAX; i = i + 2)
  {
    spf[i] = 2;
  }

  // Traverse all the numbers in
  // the range [1, sqrt(MAX)]
  for(int i = 3; i * i < MAX; i++)
  {
    // Check if i is a prime number
    if (spf[i] == i)
    {
      // Update all the numbers
      // whose smallest prime
      // factor is i
      for(int j = i * i;
              j < MAX; j = j + i)
      {
        // Check if j is
        // a prime number
        if (spf[j] == j)
        {
          spf[j] = i;
        }
      }
    }
  }
  return spf;
}

// Function to find count of
// prime factor of num
public static int countFactors(int []spf,
                               int num)
{    
  // Stores count of
  // prime factor of num
  int count = 0;

  // Calculate count of
  // prime factor
  while (num > 1)
  {
    // Update count
    count++;

    // Update num
    num = num / spf[num];
  }
  return count;
}

// Function to precalculate the count of
// numbers in the range [0, i] whose count
// of prime factors is a prime number
public static int[] precalculateSum(int []spf)
{    
  // Stores the sum of all the numbers
  // in the range[0, i] count of
  // prime factor is a prime number
  int []sum = new int[MAX];

  // Update sum[0]
  sum[0] = 0;

  // Traverse all the numbers in
  // the range [1, MAX]
  for(int i = 1; i < MAX; i++)
  {

    // Stores count of prime factor of i
    int prime_factor = countFactors(spf, i);

    // If count of prime factor is
    // a prime number
    if (spf[prime_factor] == prime_factor)
    {

      // Update sum[i]
      sum[i] = sum[i - 1] + 1;
    }
    else
    {

      // Update sum[i]
      sum[i] = sum[i - 1];
    }
  }
  return sum;
}  

// Driver code
public static void Main(String[] args)
{
  // Stores smallest prime factor
  // of all the numbers in the
  // range [0, MAX]
  int []spf = sieve();

  // Stores the sum of all the
  // numbers in the range[0, i]
  // count of prime factor is a
  // prime number
  int []sum = precalculateSum(spf);

  int [,]Q = {{4, 8}, {30, 32}};

  // int N = sizeof(Q) / sizeof(Q[0]);
  for(int i = 0; i < 2; i++)
  {
    Console.Write((sum[Q[i, 1]] -
                   sum[Q[i, 0] - 1]) +
                   " ");
  }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

let MAX = 1001

// Function to find the smallest prime factor
// of all the numbers in range [0, MAX]
function sieve()
{

    // Stores smallest prime factor of all
    // the numbers in the range [0, MAX]
    let spf = new Array(MAX);

    // No smallest prime factor of
    // 0 and 1 exists
    spf[0] = spf[1] = -1;

    // Traverse all the numbers
    // in the range [1, MAX]
    for (let i = 2; i < MAX; i++) {

        // Update spf[i]
        spf[i] = i;
    }

    // Update all the numbers whose
    // smallest prime factor is 2
    for (let i = 4; i < MAX; i = i + 2) {
        spf[i] = 2;
    }

    // Traverse all the numbers in
    // the range [1, sqrt(MAX)]
    for (let i = 3; i * i < MAX; i++) {

        // Check if i is a prime number
        if (spf[i] == i) {

            // Update all the numbers whose
            // smallest prime factor is i
            for (let j = i * i; j < MAX;
                 j = j + i) {

                // Check if j is
                // a prime number
                if (spf[j] == j) {
                    spf[j] = i;
                }
            }
        }
    }
    return spf;
}

// Function to find count of
// prime factor of num
function countFactors(spf, num)
{
    // Stores count of
    // prime factor of num
    let count = 0;

    // Calculate count of
    // prime factor
    while (num > 1) {

        // Update count
        count++;

        // Update num
        num = num / spf[num];
    }
    return count;
}

// Function to precalculate the count of
// numbers in the range [0, i] whose count
// of prime factors is a prime number
function precalculateSum(spf)
{

    // Stores the sum of all the numbers
    // in the range[0, i] count of
    // prime factor is a prime number
    let sum = new Array(MAX);

    // Update sum[0]
    sum[0] = 0;

    // Traverse all the numbers in
    // the range [1, MAX]
    for (let i = 1; i < MAX; i++) {

        // Stores count of prime factor of i
        let prime_factor
            = countFactors(spf, i);

        // If count of prime factor is
        // a prime number
        if (spf[prime_factor] == prime_factor) {

            // Update sum[i]
            sum[i] = sum[i - 1] + 1;
        }
        else {

            // Update sum[i]
            sum[i] = sum[i - 1];
        }
    }
    return sum;
}

// Driver Code

    // Stores smallest prime factor of all
    // the numbers in the range [0, MAX]
    let spf = sieve();

    // Stores the sum of all the numbers
    // in the range[0, i] count of
    // prime factor is a prime number
    let sum = precalculateSum(spf);

    let Q = [ [ 4, 8 ], [ 30, 32 ] ];

    // let N = sizeof(Q) / sizeof(Q[0]);
    for (let i = 0; i < 2; i++) {
        document.write((sum[Q[i][1]] - sum[Q[i][0] - 1]) +
        " ");
    }

// This code is contributed by gfgking

</script>
```

**Output:** 

```
3 2
```

***时间复杂度:**O(| Q |+(MAX * log(log(MAX))))*
***辅助空间:** O(MAX)*