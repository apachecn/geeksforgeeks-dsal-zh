# K 大小的子阵，有质数和

> 原文:[https://www . geeksforgeeks . org/subarray-of-size-k-with-prime-sum/](https://www.geeksforgeeks.org/subarray-of-size-k-with-prime-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** 和一个整数 **K** ，任务是打印一个大小为 **K** 的子数组，其元素之和为[素数](https://www.geeksforgeeks.org/prime-numbers/)。如果存在多个这样的子阵列，则打印其中任何一个。

**示例:**

> ***输入:** arr[] = {20，7，5，4，3，11，99，87，23，45}，K = 4*
> ***输出:** 7 5 4 3*
> ***说明:**子阵列{7，5，4，3}的元素之和为 19。*
> *因此，需要的输出是 7 5 4 3。*
> 
> ***输入:** arr[] = {11，13，17}，K = 1*
> ***输出:** 11*

**方法:**解决问题的思路是利用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)[找到 K 大小的所有子阵的和，检查是否是素数](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/)。按照以下步骤解决问题。

1.  使用厄拉多塞的[筛生成范围【1，1000000】内的所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质数](https://www.geeksforgeeks.org/prime-numbers/)，检查一个数是否是质数。
2.  初始化一个变量，比如 **currSum** 来存储大小为 **K** 的子阵列的元素之和。
3.  求数组第一个 **K** 元素的和，存储在 **currSum** 中。
4.  逐个迭代剩余的数组元素，通过添加第 **i <sup>第</sup>T5】元素并从数组中移除第**(I–K)<sup>第</sup>T9】元素来更新 **currSum** 。现在，检查 **currSum** 是否为质数。****
5.  如果发现 **currSum** 是质数，则打印当前子阵列的所有元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Generate all prime numbers
// in the range [1, 1000000]
void sieve(bool prime[])
{
    // Set all numbers as
    // prime initially
    for (int i = 0; i < 1000000;
         i++) {
        prime[i] = true;
    }

    // Mark 0 and 1 as non-prime
    prime[0] = prime[1] = false;

    for (int i = 2; i * i <= 1000000; i++) {

        // If current element is prime
        if (prime[i]) {

            // Mark all its multiples
            // as non-prime
            for (int j = i * i; j <= 1000000;
                 j += i) {

                prime[j] = false;
            }
        }
    }
}

// Function to print the subarray
// whose sum of elements is prime
void subPrimeSum(int N, int K,
                 int arr[],
                 bool prime[])
{
    // Store the current subarray
    // of size K
    int currSum = 0;

    // Calculate the sum of
    // first K elements
    for (int i = 0; i < K; i++) {

        currSum += arr[i];
    }

    // Check if currSum is prime
    if (prime[currSum]) {
        for (int i = 0; i < K; i++) {

            cout << arr[i] << " ";
        }
        return;
    }

    // Store the start and last
    // index of subarray of size K
    int st = 1, en = K;

    // Iterate over remaining array
    while (en < N) {

        currSum += arr[en] - arr[st - 1];

        // Check if currSum
        if (prime[currSum]) {

            for (int i = st; i <= en; i++) {
                cout << arr[i] << " ";
            }
            return;
        }

        en++;
        st++;
    }
}
// Driver Code
int main()
{
    int arr[] = { 20, 7, 5, 4, 3, 11,
                  99, 87, 23, 45 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    bool prime[1000000];

    sieve(prime);

    subPrimeSum(N, K, arr, prime);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Generate all prime numbers
// in the range [1, 1000000]
static void sieve(boolean prime[])
{
  // Set all numbers as
  // prime initially
  for (int i = 0; i < 1000000; i++)
  {
    prime[i] = true;
  }

  // Mark 0 and 1 as non-prime
  prime[0] = prime[1] = false;

  for (int i = 2; i * i <= 1000000; i++)
  {
    // If current element is prime
    if (prime[i])
    {
      // Mark all its multiples
      // as non-prime
      for (int j = i * i; j < 1000000; j += i)
      {
        prime[j] = false;
      }
    }
  }
}

// Function to print the subarray
// whose sum of elements is prime
static void subPrimeSum(int N, int K,
                        int arr[],
                        boolean prime[])
{
  // Store the current subarray
  // of size K
  int currSum = 0;

  // Calculate the sum of
  // first K elements
  for (int i = 0; i < K; i++)
  {
    currSum += arr[i];
  }

  // Check if currSum is prime
  if (prime[currSum])
  {
    for (int i = 0; i < K; i++)
    {
      System.out.print(arr[i] + " ");
    }
    return;
  }

  // Store the start and last
  // index of subarray of size K
  int st = 1, en = K;

  // Iterate over remaining array
  while (en < N)
  {
    currSum += arr[en] - arr[st - 1];

    // Check if currSum
    if (prime[currSum])
    {
      for (int i = st; i <= en; i++)
      {
        System.out.print(arr[i] + " ");
      }
      return;
    }
    en++;
    st++;
  }
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {20, 7, 5, 4, 3, 11,
               99, 87, 23, 45};
  int K = 4;
  int N = arr.length;
  boolean []prime = new boolean[1000000];
  sieve(prime);
  subPrimeSum(N, K, arr, prime);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Generate all prime numbers
# in the range [1, 1000000]
def sieve(prime):

    # Set all numbers as
    # prime initially
    for i in range(1000000):
        prime[i] = True

    # Mark 0 and 1 as non-prime
    prime[0] = prime[1] = False

    for i in range(2, 1000 + 1):

        # If current element is prime
        if (prime[i]):

            # Mark all its multiples
            # as non-prime
            for j in range(i * i, 1000000, i):
                prime[j] = False

    return prime

# Function to print the subarray
# whose sum of elements is prime
def subPrimeSum(N, K, arr, prime):

    # Store the current subarray
    # of size K
    currSum = 0

    # Calculate the sum of
    # first K elements
    for i in range(0, K):
        currSum += arr[i]

    # Check if currSum is prime
    if (prime[currSum]):
        for i in range(K):
            print(arr[i], end = " ")

        return

    # Store the start and last
    # index of subarray of size K
    st = 1
    en = K

    # Iterate over remaining array
    while (en < N):
        currSum += arr[en] - arr[st - 1]

        # Check if currSum
        if (prime[currSum]):
            for i in range(st, en + 1):
                print(arr[i], end = " ")

            return

        en += 1
        st += 1

# Driver Code
if __name__ == '__main__':

    arr = [ 20, 7, 5, 4, 3,
            11, 99, 87, 23, 45 ]
    K = 4
    N = len(arr)
    prime = [False] * 1000000
    prime = sieve(prime)

    subPrimeSum(N, K, arr, prime)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Generate all prime numbers
// in the range [1, 1000000]
static void sieve(bool []prime)
{
  // Set all numbers as
  // prime initially
  for (int i = 0; i < 1000000; i++)
  {
    prime[i] = true;
  }

  // Mark 0 and 1 as non-prime
  prime[0] = prime[1] = false;

  for (int i = 2; i * i <= 1000000; i++)
  {
    // If current element is prime
    if (prime[i])
    {
      // Mark all its multiples
      // as non-prime
      for (int j = i * i; j < 1000000; j += i)
      {
        prime[j] = false;
      }
    }
  }
}

// Function to print the subarray
// whose sum of elements is prime
static void subPrimeSum(int N, int K,
                        int []arr,
                        bool []prime)
{
  // Store the current subarray
  // of size K
  int currSum = 0;

  // Calculate the sum of
  // first K elements
  for (int i = 0; i < K; i++)
  {
    currSum += arr[i];
  }

  // Check if currSum is prime
  if (prime[currSum])
  {
    for (int i = 0; i < K; i++)
    {
      Console.Write(arr[i] + " ");
    }
    return;
  }

  // Store the start and last
  // index of subarray of size K
  int st = 1, en = K;

  // Iterate over remaining array
  while (en < N)
  {
    currSum += arr[en] - arr[st - 1];

    // Check if currSum
    if (prime[currSum])
    {
      for (int i = st; i <= en; i++)
      {
        Console.Write(arr[i] + " ");
      }
      return;
    }
    en++;
    st++;
  }
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {20, 7, 5, 4, 3, 11,
               99, 87, 23, 45};
  int K = 4;
  int N = arr.Length;
  bool []prime = new bool[1000000];
  sieve(prime);
  subPrimeSum(N, K, arr, prime);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Generate all prime numbers
// in the range [1, 1000000]
function sieve(prime)
{

    // Set all numbers as
    // prime initially
    for (var i = 0; i < 1000000;
        i++) {
        prime[i] = true;
    }

    // Mark 0 and 1 as non-prime
    prime[0] = prime[1] = false;

    for (var i = 2; i * i <= 1000000; i++)
    {

        // If current element is prime
        if (prime[i])
        {

            // Mark all its multiples
            // as non-prime
            for (var j = i * i; j <= 1000000;
                j += i) {

                prime[j] = false;
            }
        }
    }
}

// Function to print the subarray
// whose sum of elements is prime
function subPrimeSum( N, K, arr, prime)
{
    // Store the current subarray
    // of size K
    var currSum = 0;

    // Calculate the sum of
    // first K elements
    for (var i = 0; i < K; i++) {

        currSum += arr[i];
    }

    // Check if currSum is prime
    if (prime[currSum]) {
        for (var i = 0; i < K; i++) {

            document.write(arr[i] + " ");
        }
        return;
    }

    // Store the start and last
    // index of subarray of size K
    var st = 1, en = K;

    // Iterate over remaining array
    while (en < N) {

        currSum += arr[en] - arr[st - 1];

        // Check if currSum
        if (prime[currSum]) {

            for (var i = st; i <= en; i++) {
                document.write(arr[i] + " ");
            }
            return;
        }

        en++;
        st++;
    }
}
// Driver Code
var arr = [ 20, 7, 5, 4, 3, 11,
            99, 87, 23, 45 ]
var K = 4;
var N = arr.length;
prime = Array(1000000).fill(0);
sieve(prime);
subPrimeSum(N, K, arr, prime);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
7 5 4 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)