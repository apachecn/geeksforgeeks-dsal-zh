# 从数组 arr[]生成 N 长度数组 A[]，使得 arr[i]是由 A[i]

的倍数组成的最后一个索引

> 原文:[https://www . geesforgeks . org/generate-an-n-length-arr-from-a-arr-as-arri-is-the-last-index-由多个 ai 组成/](https://www.geeksforgeeks.org/generate-an-n-length-array-a-from-an-array-arr-such-that-arri-is-the-last-index-consisting-of-a-multiple-of-ai/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)****arr【】**，其值小于 **N** ，任务是构造另一个长度相同的数组**A【】**，使得对于数组**A【】**中的每一个 **i** <sup>第</sup>个元素， **arr[i]** 是基于 1 的最后一个索引(**

******示例:******

> ******输入:** arr[] = {4，1，2，3，4}
> **输出:** 2 3 5 7 2
> **解释:**
> A[0]:可以包含 A[0]倍数的最后一个索引必须是 A[arr[0]] = A[4]。
> A[1]:可以包含 A[1]倍数的最后一个索引必须是 A[arr[1]] = A[1]。
> A[2]:可以包含 A[2]倍数的最后一个索引必须是 A[arr[2]] = A[2]。
> A[3]:可以包含 A[3]倍数的最后一个索引必须是 A[arr[3]] = A[3]。
> A[4]:可以包含 A[4]倍数的最后一个索引必须是 A[arr[4]] = A[4]。
> 因此，在最终数组中，A[4]必须能被 A[0]和 A[1]整除，A[2]和 A[3]不能被任何其他数组元素整除。
> 因此，数组 A[] = {2，3，5，7，2}满足条件。****
> 
> ******输入:** arr[] = {0，1，2，3，4 }
> T3】输出: 2 3 5 7 11****

******方法:**思路是将[素数](https://www.geeksforgeeks.org/print-prime-numbers-given-range-using-c-stl/)作为数组元素放置在满足条件的所需索引中。按照以下步骤解决问题:****

*   ****使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) **筛**生成所有[质数](https://www.geeksforgeeks.org/prime-numbers/)，并将其存储在另一个数组中。****
*   ****用 **{0}** 初始化数组 **A[]** ，存储需要的数组。****
*   ****[遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下步骤:

    *   检查 **A[arr[i]]** 是否非零，但 **A[i]** 是否为 0。如果发现是真的，那么分配 **A[i] = A[arr[i]]。**
    *   检查 **A[arr[i]]** 和 **A[i]** 是否都为 0。如果发现是真的，那么给两个索引**arr【I】**和 **i** 分配一个不同于已经分配的数组元素的质数。**** 
*   ****完成以上步骤后，打印数组 **A[]** 的元素。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int sieve[1000000];

// Function to generate all
// prime numbers upto 10^6
void sieveOfPrimes()
{
    // Initialize sieve[] as 1
    memset(sieve, 1, sizeof(sieve));

    int N = 1000000;

    // Iterate over the range [2, N]
    for (int i = 2; i * i <= N; i++) {

        // If current element is non-prime
        if (sieve[i] == 0)
            continue;

        // Make all multiples of i as 0
        for (int j = i * i; j <= N; j += i)
            sieve[j] = 0;
    }
}

// Function to construct an array A[]
// satisfying the given conditions
void getArray(int* arr, int N)
{
    // Stores the resultant array
    int A[N] = { 0 };

    // Stores all prime numbers
    vector<int> v;

    // Sieve of Erastosthenes
    sieveOfPrimes();

    for (int i = 2; i <= 1e5; i++)

        // Append the integer i
        // if it is a prime
        if (sieve[i])
            v.push_back(i);

    // Indicates current position
    // in list of prime numbers
    int j = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        int ind = arr[i];

        // If already filled with
        // another prime number
        if (A[i] != 0)
            continue;

        // If A[i] is not filled
        // but A[ind] is filled
        else if (A[ind] != 0)

            // Store A[i] = A[ind]
            A[i] = A[ind];

        // If none of them were filled
        else {

            // To make sure A[i] does
            // not affect other values,
            // store next prime number
            int prime = v[j++];

            A[i] = prime;
            A[ind] = A[i];
        }
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        cout << A[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    getArray(arr, N);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;
class GFG
{

static int[] sieve = new int[10000000];

// Function to generate all
// prime numbers upto 10^6
static void sieveOfPrimes()
{

    // Initialize sieve[] as 1
    Arrays.fill(sieve, 1);
    int N = 1000000;

    // Iterate over the range [2, N]
    for (int i = 2; i * i <= N; i++)
    {

        // If current element is non-prime
        if (sieve[i] == 0)
            continue;

        // Make all multiples of i as 0
        for (int j = i * i; j <= N; j += i)
            sieve[j] = 0;
    }
}

// Function to construct an array A[]
// satisfying the given conditions
static void getArray(int[] arr, int N)
{

    // Stores the resultant array
    int A[] = new int[N];
    Arrays.fill(A, 0);

    // Stores all prime numbers
    ArrayList<Integer> v
            = new ArrayList<Integer>();

    // Sieve of Erastosthenes
    sieveOfPrimes();

    for (int i = 2; i <= 1000000; i++)

        // Append the integer i
        // if it is a prime
        if (sieve[i] != 0)
            v.add(i);

    // Indicates current position
    // in list of prime numbers
    int j = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {
        int ind = arr[i];

        // If already filled with
        // another prime number
        if (A[i] != 0)
            continue;

        // If A[i] is not filled
        // but A[ind] is filled
        else if (A[ind] != 0)

            // Store A[i] = A[ind]
            A[i] = A[ind];

        // If none of them were filled
        else {

            // To make sure A[i] does
            // not affect other values,
            // store next prime number
            int prime = v.get(j++);

            A[i] = prime;
            A[ind] = A[i];
        }
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        System.out.print( A[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 1, 2, 3, 4 };
    int N = arr.length;

    // Function Call
    getArray(arr, N);

}
}

// This code is contributed by code_hunt.**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach
sieve = [1]*(1000000+1)

# Function to generate all
# prime numbers upto 10^6
def sieveOfPrimes():
    global sieve
    N = 1000000

    # Iterate over the range [2, N]
    for i in range(2, N + 1):
        if i * i > N:
            break

        # If current element is non-prime
        if (sieve[i] == 0):
            continue

        # Make all multiples of i as 0
        for j in range(i * i, N + 1, i):
            sieve[j] = 0

# Function to construct an array A[]
# satisfying the given conditions
def getArray(arr, N):
    global sieve

    # Stores the resultant array
    A = [0]*N

    # Stores all prime numbers
    v = []

    # Sieve of Erastosthenes
    sieveOfPrimes()
    for i in range(2,int(1e5)+1):

        # Append the integer i
        # if it is a prime
        if (sieve[i]):
            v.append(i)

    # Indicates current position
    # in list of prime numbers
    j = 0

    # Traverse the array arr[]
    for i in range(N):
        ind = arr[i]

        # If already filled with
        # another prime number
        if (A[i] != 0):
            continue

        # If A[i] is not filled
        # but A[ind] is filled
        elif (A[ind] != 0):

            # Store A[i] = A[ind]
            A[i] = A[ind]

        # If none of them were filled
        else:

            # To make sure A[i] does
            # not affect other values,
            # store next prime number
            prime = v[j]
            A[i] = prime
            A[ind] = A[i]
            j += 1

    # Print the resultant array
    for i in range(N):
        print(A[i], end = " ")

        # Driver Code
if __name__ == '__main__':
    arr = [4, 1, 2, 3, 4]
    N = len(arr)

    # Function Call
    getArray(arr, N)

    # This code is contributed by mohit kumar 29.**
```

## ****C#****

```
**// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{
  static int[] sieve = new int[10000000];

  // Function to generate all
  // prime numbers upto 10^6
  static void sieveOfPrimes()
  {

    // Initialize sieve[] as 1
    for(int i = 0; i < 10000000; i++)
    {
      sieve[i] = 1;
    }
    int N = 1000000;

    // Iterate over the range [2, N]
    for (int i = 2; i * i <= N; i++)
    {

      // If current element is non-prime
      if (sieve[i] == 0)
        continue;

      // Make all multiples of i as 0
      for (int j = i * i; j <= N; j += i)
        sieve[j] = 0;
    }
  }

  // Function to construct an array A[]
  // satisfying the given conditions
  static void getArray(int[] arr, int N)
  {

    // Stores the resultant array
    int[] A = new int[N];
    for(int i = 0; i < N; i++)
    {
      A[i] = 0;
    }

    // Stores all prime numbers
    List<int> v
      = new List<int>();

    // Sieve of Erastosthenes
    sieveOfPrimes();

    for (int i = 2; i <= 1000000; i++)

      // Append the integer i
      // if it is a prime
      if (sieve[i] != 0)
        v.Add(i);

    // Indicates current position
    // in list of prime numbers
    int j = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {
      int ind = arr[i];

      // If already filled with
      // another prime number
      if (A[i] != 0)
        continue;

      // If A[i] is not filled
      // but A[ind] is filled
      else if (A[ind] != 0)

        // Store A[i] = A[ind]
        A[i] = A[ind];

      // If none of them were filled
      else {

        // To make sure A[i] does
        // not affect other values,
        // store next prime number
        int prime = v[j++];

        A[i] = prime;
        A[ind] = A[i];
      }
    }

    // Print the resultant array
    for (int i = 0; i < N; i++)
    {
      Console.Write( A[i] + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 4, 1, 2, 3, 4 };
    int N = arr.Length;

    // Function Call
    getArray(arr, N);
  }
}

// This code is contributed by splevel62.**
```

## ****java 描述语言****

```
**<script>

// JavaScript program for the above approach

var sieve = Array(1000000);

// Function to generate all
// prime numbers upto 10^6
function sieveOfPrimes()
{
    // Initialize sieve[] as 1
    sieve = Array(1000000).fill(1);

    var N = 1000000;

    // Iterate over the range [2, N]
    for (var i = 2; i * i <= N; i++) {

        // If current element is non-prime
        if (sieve[i] == 0)
            continue;

        // Make all multiples of i as 0
        for (var j = i * i; j <= N; j += i)
            sieve[j] = 0;
    }
}

// Function to construct an array A[]
// satisfying the given conditions
function getArray(arr, N)
{
    // Stores the resultant array
    var A = Array(N).fill(0);

    // Stores all prime numbers
    var v = [];

    // Sieve of Erastosthenes
    sieveOfPrimes();

    for (var i = 2; i <= 1e5; i++)

        // Append the integer i
        // if it is a prime
        if (sieve[i])
            v.push(i);

    // Indicates current position
    // in list of prime numbers
    var j = 0;

    // Traverse the array arr[]
    for (var i = 0; i < N; i++) {

        var ind = arr[i];

        // If already filled with
        // another prime number
        if (A[i] != 0)
            continue;

        // If A[i] is not filled
        // but A[ind] is filled
        else if (A[ind] != 0)

            // Store A[i] = A[ind]
            A[i] = A[ind];

        // If none of them were filled
        else {

            // To make sure A[i] does
            // not affect other values,
            // store next prime number
            var prime = v[j++];

            A[i] = prime;
            A[ind] = A[i];
        }
    }

    // Print the resultant array
    for (var i = 0; i < N; i++) {
        document.write( A[i] + " ");
    }
}

// Driver Code

var arr = [4, 1, 2, 3, 4];
var N = arr.length;

// Function Call
getArray(arr, N);

</script>**
```

******Output:** 

```
2 3 5 7 2
```**** 

*******时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*****