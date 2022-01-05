# Q 查询的 L 到 R 范围内的第 k 个最小素数

> 原文:[https://www . geesforgeks . org/kth-最小范围质数-l 到 r-for-q-query/](https://www.geeksforgeeks.org/kth-smallest-prime-number-in-range-l-to-r-for-q-queries/)

给定三个变量 **L，R** 和 **Q** ，表示范围【L，R】和查询总数。每个查询都有一个变量 **K** 。任务是在**【L，R】**范围内找到 **Kth** 最小素数。如果 **K** 大于**【L，R】**范围内的素数个数，则返回 **-1** 。

**示例:**

> **输入:** Q = 3，L = 5，R = 20
> 查询:K = 4，
> K = 3，
> K = 9
> **输出:** 13 11 -1
> **说明:**给定范围内的素数为 5，7，11，13，17，19 和
> 第 4 和第 3 个最小素数为 13 和 11。
> 
> **输入:** Q = 1，L = 15，R = 32
> 查询:K = 3
> T4】输出: 23

**方法:**给定的问题可以借助厄拉多塞的[T3】筛](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)方法:
当算法终止时，列表中所有没有标记的数字都是质数。遵循以下步骤:

*   运行厄拉多塞的**筛，寻找范围【左，右】内的数字**
*   对于每个查询，从计算出的素数中找出第 Kt 个最小素数。
*   如果 K 超过该范围内的素数，返回-1。

为了更好地理解厄拉多塞筛子，请参见下图。

> **图解:**取范围**【20，40】**。
> 厄拉多塞筛将有助于找到这个范围内的素数。
> 创建从 1 到 40 的所有数字的列表。根据算法标记给定范围内的所有非素数。
> 所以质数是没有标记的:2，3，5，7，11，13，17，19，23，29，31，37。
> 范围[20，40]内的素数是:23，29，31 和 37

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
vector<int> primes;

// Function to implement
// Sieve Of Eratosthenes
void sieveOfEratosthenes(int R)
{
    primes.assign(R + 1, 0);
    primes[1] = 1;
    for (int i = 2; i * i <= R; i++) {
        if (primes[i] == 0) {
            for (int j = i + i; j <= R;
                 j += i)
                primes[j] = 1;
        }
    }
}

// Function to return Kth smallest
// prime number if it exists
int kthSmallest(int L, int R, int K)
{
    // To count the prime number
    int count = 0;

    // Loop to iterate the from L to R
    for (int i = L; i <= R; i++) {

        // Calculate the count Of
        // primes numbers
        if (primes[i] == 0) {
            count++;
        }

        // if count equals K, then
        // Kth smallest prime number is
        // found then return the number
        if (count == K) {
            return i;
        }
    }

    // Kth smallest prime number is not in
    // this range then return -1
    return -1;
}

// Driver Code
int main()
{
    // No of Queries
    int Q = 3;
    int L, R, K;
    L = 5, R = 20;
    sieveOfEratosthenes(R);

    // First Query
    K = 4;
    cout << kthSmallest(L, R, K) << endl;

    // Second Query
    K = 3;
    cout << kthSmallest(L, R, K) << endl;

    // Third Query
    K = 5;
    cout << kthSmallest(L, R, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;
public class GFG
{

  static int primes[] = new int[1000];

  // Function to implement
  // Sieve Of Eratosthenes
  static void sieveOfEratosthenes(int R)
  {

    for(int i = 0; i < R + 1; i++) {
      primes[i] = 0;
    }

    primes[1] = 1;
    for (int i = 2; i * i <= R; i++) {
      if (primes[i] == 0) {
        for (int j = i + i; j <= R;
             j += i)
          primes[j] = 1;
      }
    }
  }

  // Function to return Kth smallest
  // prime number if it exists
  static int kthSmallest(int L, int R, int K)
  {
    // To count the prime number
    int count = 0;

    // Loop to iterate the from L to R
    for (int i = L; i <= R; i++) {

      // Calculate the count Of
      // primes numbers
      if (primes[i] == 0) {
        count++;
      }

      // if count equals K, then
      // Kth smallest prime number is
      // found then return the number
      if (count == K) {
        return i;
      }
    }

    // Kth smallest prime number is not in
    // this range then return -1
    return -1;
  }

  // Driver code
  public static void main(String args[])
  {
    // No of Queries
    int Q = 3;
    int L = 5, R = 20;
    sieveOfEratosthenes(R);

    // First Query
    int K = 4;
    System.out.println(kthSmallest(L, R, K));

    // Second Query
    K = 3;
    System.out.println(kthSmallest(L, R, K));

    // Third Query
    K = 5;
    System.out.println(kthSmallest(L, R, K));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
let primes;

// Function to implement
// Sieve Of Eratosthenes
function sieveOfEratosthenes(R)
{
    primes = new Array(R + 1).fill(0);
    primes[1] = 1;

    for(let i = 2; i * i <= R; i++)
    {
        if (primes[i] == 0)
        {
            for(let j = i + i; j <= R;
                    j += i)
                primes[j] = 1;
        }
    }
}

// Function to return Kth smallest
// prime number if it exists
function kthSmallest(L, R, K)
{

    // To count the prime number
    let count = 0;

    // Loop to iterate the from L to R
    for(let i = L; i <= R; i++)
    {

        // Calculate the count Of
        // primes numbers
        if (primes[i] == 0)
        {
            count++;
        }

        // If count equals K, then
        // Kth smallest prime number is
        // found then return the number
        if (count == K)
        {
            return i;
        }
    }

    // Kth smallest prime number is not in
    // this range then return -1
    return -1;
}

// Driver Code

// No of Queries
let Q = 3;
let L, R, K;
L = 5, R = 20;
sieveOfEratosthenes(R);

// First Query
K = 4;
document.write(kthSmallest(L, R, K) + '<br>');

// Second Query
K = 3;
document.write(kthSmallest(L, R, K) + '<br>');

// Third Query
K = 5;
document.write(kthSmallest(L, R, K) + '<br>');

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
13
11
17
```

***时间复杂度:*****O(N * log(log N)))
***辅助空间:*** O(N)**