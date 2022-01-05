# 计算数组中每个元素的不同质因数

> 原文:[https://www . geeksforgeeks . org/count-distinct-prime-factors-for-每个数组元素/](https://www.geeksforgeeks.org/count-distinct-prime-factors-for-each-element-of-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组中每个元素的不同素因子的计数。

**示例:**

> **输入:** arr[] = {6，9，12}
> **输出:**2 1 2
> T6】解释:
> 
> *   6 = **2** × **3** 。因此，计数= 2
> *   9 = **3** × 3。因此，计数= 1
> *   12 = **2** × 2 × **3** 。因此，计数= 2
> 
> 每个数组元素不同素因子的个数分别为 **2，1，2** 。
> 
> **输入:** arr[] = {4，8，10，6}
> 输出 : 1 1 2 2

**天真法:**解决问题最简单的方法就是找到每个数组元素的[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。然后，找出其中不同的质数，并打印每个数组元素的计数。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过使用所有数字的[最小质因数](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)预计算它们的不同因数来优化。按照以下步骤解决问题

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **v** ，来存储不同的质因数。
*   使用厄拉多塞的[筛将](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[最小质因数](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/) **(SPF)** 存储至 **10 <sup>5</sup>** 。
*   计算所有数字的不同质因数，将数字递归地除以它们的最小质因数，直到它减少到 **1** ，并将 **X** 的不同质因数存储在**v【X】**中。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素，将计数打印为 **v[arr[i]]。尺寸()**。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 100001

// Stores smallest prime
// factor for every number
int spf[MAX];

// Stores distinct prime factors
vector<int> v[MAX];

// Function to find the smallest
// prime factor of every number
void sieve()
{
    // Mark the smallest prime factor
    // of every number to itself
    for (int i = 1; i < MAX; i++)
        spf[i] = i;

    // Separately mark all the
    // smallest prime factor of
    // every even number to be 2
    for (int i = 4; i < MAX; i = i + 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAX; i++)

        // If i is prime
        if (spf[i] == i) {

            // Mark spf for all numbers
            // divisible by i
            for (int j = i * i; j < MAX;
                 j = j + i) {

                // Mark spf[j] if it is
                // not previously marked
                if (spf[j] == j)
                    spf[j] = i;
            }
        }
}

// Function to find the distinct
// prime factors
void DistPrime()
{
    for (int i = 1; i < MAX; i++) {

        int idx = 1;
        int x = i;

        // Push all distinct of x
        // prime factor in v[x]
        if (x != 1)
            v[i].push_back(spf[x]);

        x = x / spf[x];

        while (x != 1) {

            if (v[i][idx - 1]
                != spf[x]) {

                // Pushback into v[i]
                v[i].push_back(spf[x]);

                // Increment the idx
                idx += 1;
            }

            // Update x = (x / spf[x])
            x = x / spf[x];
        }
    }
}

// Function to get the distinct
// factor count of arr[]
void getFactorCount(int arr[],
                    int N)
{
    // Precompute the smallest
    // Prime Factors
    sieve();

    // For distinct prime factors
    // Fill the v[] vector
    DistPrime();

    // Count of Distinct Prime
    // Factors of each array element
    for (int i = 0; i < N; i++) {
        cout << (int)v[arr[i]].size()
             << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 6, 9, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    getFactorCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG
{

  static int MAX = 100001;

  // Stores smallest prime
  // factor for every number
  static int spf[];

  // Stores distinct prime factors
  static ArrayList<Integer> v[];

  // Function to find the smallest
  // prime factor of every number
  static void sieve()
  {

    // Mark the smallest prime factor
    // of every number to itself
    for (int i = 1; i < MAX; i++)
      spf[i] = i;

    // Separately mark all the
    // smallest prime factor of
    // every even number to be 2
    for (int i = 4; i < MAX; i = i + 2)
      spf[i] = 2;
    for (int i = 3; i * i < MAX; i++)

      // If i is prime
      if (spf[i] == i) {

        // Mark spf for all numbers
        // divisible by i
        for (int j = i * i; j < MAX; j = j + i) {

          // Mark spf[j] if it is
          // not previously marked
          if (spf[j] == j)
            spf[j] = i;
        }
      }
  }

  // Function to find the distinct
  // prime factors
  static void DistPrime()
  {
    for (int i = 1; i < MAX; i++) {

      int idx = 1;
      int x = i;

      // Push all distinct of x
      // prime factor in v[x]
      if (x != 1)
        v[i].add(spf[x]);

      x = x / spf[x];

      while (x != 1) {

        if (v[i].get(idx - 1) != spf[x]) {

          // Pushback into v[i]
          v[i].add(spf[x]);

          // Increment the idx
          idx += 1;
        }

        // Update x = (x / spf[x])
        x = x / spf[x];
      }
    }
  }

  // Function to get the distinct
  // factor count of arr[]
  static void getFactorCount(int arr[], int N)
  {

    // initialization
    spf = new int[MAX];
    v = new ArrayList[MAX];
    for (int i = 0; i < MAX; i++)
      v[i] = new ArrayList<>();

    // Precompute the smallest
    // Prime Factors
    sieve();

    // For distinct prime factors
    // Fill the v[] vector
    DistPrime();

    // Count of Distinct Prime
    // Factors of each array element
    for (int i = 0; i < N; i++) {
      System.out.print((int)v[arr[i]].size() + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 6, 9, 12 };
    int N = arr.length;

    getFactorCount(arr, N);
  }
}

// This code is contributed by Kingash.
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    let MAX = 100001;

    // Stores smallest prime
    // factor for every number
    let spf;

    // Stores distinct prime factors
    let v;

    // Function to find the smallest
    // prime factor of every number
    function sieve()
    {

      // Mark the smallest prime factor
      // of every number to itself
      for (let i = 1; i < MAX; i++)
        spf[i] = i;

      // Separately mark all the
      // smallest prime factor of
      // every even number to be 2
      for (let i = 4; i < MAX; i = i + 2)
        spf[i] = 2;
      for (let i = 3; i * i < MAX; i++)

        // If i is prime
        if (spf[i] == i) {

          // Mark spf for all numbers
          // divisible by i
          for (let j = i * i; j < MAX; j = j + i) {

            // Mark spf[j] if it is
            // not previously marked
            if (spf[j] == j)
              spf[j] = i;
          }
        }
    }

    // Function to find the distinct
    // prime factors
    function DistPrime()
    {
      for (let i = 1; i < MAX; i++) {

        let idx = 1;
        let x = i;

        // Push all distinct of x
        // prime factor in v[x]
        if (x != 1)
          v[i].push(spf[x]);

        x = parseInt(x / spf[x], 10);

        while (x != 1) {

          if (v[i][idx - 1] != spf[x]) {

            // Pushback into v[i]
            v[i].push(spf[x]);

            // Increment the idx
            idx += 1;
          }

          // Update x = (x / spf[x])
          x = parseInt(x / spf[x], 10);
        }
      }
    }

    // Function to get the distinct
    // factor count of arr[]
    function getFactorCount(arr, N)
    {

      // initialization
      spf = new Array(MAX);
      v = new Array(MAX);
      for (let i = 0; i < MAX; i++)
        v[i] = [];

      // Precompute the smallest
      // Prime Factors
      sieve();

      // For distinct prime factors
      // Fill the v[] vector
      DistPrime();

      // Count of Distinct Prime
      // Factors of each array element
      for (let i = 0; i < N; i++) {
        document.write(v[arr[i]].length + " ");
      }
    }

    let arr = [ 6, 9, 12 ];
    let N = arr.length;

    getFactorCount(arr, N);

</script>
```

**Output:** 

```
2 1 2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*