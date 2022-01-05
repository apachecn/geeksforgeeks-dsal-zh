# 求指数之和可被 K 整除的数组元素的素因子

> 原文:[https://www . geeksforgeeks . org/find-prime-factors-of-array-elements-其指数和可被 k 整除/](https://www.geeksforgeeks.org/find-prime-factors-of-array-elements-whose-sum-of-exponents-is-divisible-by-k/)

给定一个由正整数 **N** 和整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。，任务是创建一组素数，使得所有数组元素的素数因式分解中素数的所有幂的和可被 **K** 整除。

**示例:**

> **输入:** arr[] = {1，2，3}，K = 1
> **输出:** {2，3}
> **解释:**
> 2 = 2<sup>1</sup>
> 3 = 3<sup>1</sup>
> 2 的幂是 1，可被 K(=1)整除。
> 2 的幂是 1，可被 K(=1)整除。
> 
> **输入:** arr[] = {2，2，4，8}，K = 10
> **输出:** {}
> **解释:**
> 2 = 2<sup>1</sup>T11】2 = 2<sup>1</sup>T14】4 = 2<sup>2</sup>T17】8 = 2<sup>3</sup>T20】2 的幂是(1 + 1 + 2 + 3) = 7
> 由此可见，输出空集。

**天真方法:**想法是找到所有小于或等于数组最大元素**arr【】**的[素数](https://www.geeksforgeeks.org/prime-numbers/)。对于每个素数的计数次数，它除以数组元素。如果计数值可被 **K** 整除，则将质数插入结果集中。在集合的最后打印元素。

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*

**高效方法:**优化上述方法的思路是预先计算所有数字的所有质因数的计数。以下是步骤:

1.  创建[最小素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)数组 **spf[]** 直到数组中的最大数。这一步用于预先计算一个数的[质因数。](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)
2.  遍历给定的数组 **arr[]** ，对于每个元素，找出存储在 **spf[]** 数组中的所有因子的总数。
3.  对于上述步骤中质数的每次幂和，将其频率存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
4.  如果对于任何数字，频率可被 **K** 整除，则遍历地图，然后存储该数字。
5.  最后，打印以上步骤中存储的所有数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

// To store the smallest prime
// factor till 10^5
int spf[10001];

// Function to compute smallest
// prime factor array
void spf_array(int spf[])
{
    // Initialize the spf array
    // first element
    spf[1] = 1;

    for (int i = 2; i < 1000; i++)

        // Marking smallest prime
        // factor for every number
        // to be itself
        spf[i] = i;

    // Separately marking smallest
    // prime factor for every even
    // number as 2
    for (int i = 4; i < 1000; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < 1000; i++) {

        // Checking if i is prime
        if (spf[i] == i) {

            // Marking SPF for all
            // numbers divisible by i
            for (int j = i * i;
                j < 1000; j += i)

                // Marking spf[j] if it is
                // not previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function that finds minimum operation
void frequent_prime(int arr[], int N,
                    int K)
{

    // Create a spf[] array
    spf_array(spf);

    // Map created to store the
    // unique prime numbers
    unordered_map<int, int> Hmap;

    // To store the result
    vector<int> result;
    int i = 0;

    // To store minimum operations
    int c = 0;

    // To store every unique
    // prime number
    for (i = 0; i < N; i++) {

        int x = arr[i];
        while (x != 1) {

            Hmap[spf[x]]
                = Hmap[spf[x]] + 1;
            x = x / spf[x];
        }
    }

    // Erase 1 as a key because
    // it is not a prime number
    Hmap.erase(1);

    for (auto x : Hmap) {

        // First Prime Number
        int primeNum = x.first;
        int frequency = x.second;

        // Frequency is divisible
        // by K then insert primeNum
        // in the result[]
        if (frequency % K == 0) {
            result.push_back(primeNum);
        }
    }

    // Print the elements
    // if it exists
    if (result.size() > 0) {

        for (auto& it : result) {
            cout << it << ' ';
        }
    }
    else {
        cout << "{}";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 4, 6 };

    // Given K
    int K = 1;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    frequent_prime(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// To store the smallest prime
// factor till 10^5
static int[] spf = new int[10001];

// Function to compute smallest
// prime factor array
static void spf_array(int spf[])
{

    // Initialize the spf array
    // first element
    spf[1] = 1;

    for(int i = 2; i < 1000; i++)

        // Marking smallest prime
        // factor for every number
        // to be itself
        spf[i] = i;

    // Separately marking smallest
    // prime factor for every even
    // number as 2
    for(int i = 4; i < 1000; i += 2)
        spf[i] = 2;

    for(int i = 3; i * i < 1000; i++)
    {

        // Checking if i is prime
        if (spf[i] == i)
        {

            // Marking SPF for all
            // numbers divisible by i
            for(int j = i * i;
                    j < 1000; j += i)

                // Marking spf[j] if it is
                // not previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function that finds minimum operation
static void frequent_prime(int arr[], int N,
                                      int K)
{

    // Create a spf[] array
    spf_array(spf);

    // Map created to store the
    // unique prime numbers
    Map<Integer, Integer> Hmap = new TreeMap<>();

    // To store the result
    ArrayList<Integer> result = new ArrayList<>();
    int i = 0;

    // To store minimum operations
    int c = 0;

    // To store every unique
    // prime number
    for(i = 0; i < N; i++)
    {
        int x = arr[i];
        while (x != 1)
        {
            Hmap.put(spf[x],
                     Hmap.getOrDefault(spf[x], 0) + 1);
            x = x / spf[x];
        }
    }

    // Erase 1 as a key because
    // it is not a prime number
    Hmap.remove(1);

    for(Map.Entry<Integer,
                  Integer> x : Hmap.entrySet())
    {

        // First prime number
        int primeNum = x.getKey();
        int frequency = x.getValue();

        // Frequency is divisible
        // by K then insert primeNum
        // in the result[]
        if (frequency % K == 0)
        {
            result.add(primeNum);
        }
    }

    // Print the elements
    // if it exists
    if (result.size() > 0)
    {
        for(Integer it : result)
        {
            System.out.print(it + " ");
        }
    }
    else
    {
        System.out.print("{}");
    }
}

// Driver code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 4, 6 };

    // Given K
    int K = 1;

    int N = arr.length;

    // Function call
    frequent_prime(arr, N, K);
}
}

// This code is contributed by offbeat
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

  // To store the smallest prime
  // factor till 10^5
  static int[] spf = new int[10001];

  // Function to compute smallest
  // prime factor array
  static void spf_array(int[] spf)
  {

    // Initialize the spf array
    // first element
    spf[1] = 1;

    for (int i = 2; i < 1000; i++)

      // Marking smallest prime
      // factor for every number
      // to be itself
      spf[i] = i;

    // Separately marking smallest
    // prime factor for every even
    // number as 2
    for (int i = 4; i < 1000; i += 2)
      spf[i] = 2;

    for (int i = 3; i * i < 1000; i++)
    {

      // Checking if i is prime
      if (spf[i] == i)
      {

        // Marking SPF for all
        // numbers divisible by i
        for (int j = i * i; j < 1000; j += i)

          // Marking spf[j] if it is
          // not previously marked
          if (spf[j] == j)
            spf[j] = i;
      }
    }
  }

  // Function that finds minimum operation
  static void frequent_prime(int[] arr, int N, int K)
  {

    // Create a spf[] array
    spf_array(spf);

    // Map created to store the
    // unique prime numbers
    SortedDictionary<int,
                     int> Hmap = new SortedDictionary<int,
                                                      int>();

    // To store the result
    List<int> result = new List<int>();
    int i = 0;    

    // To store every unique
    // prime number
    for (i = 0; i < N; i++)
    {
      int x = arr[i];
      while (x != 1)
      {
        if (Hmap.ContainsKey(spf[x]))
          Hmap[spf[x]] = spf[x] + 1;
        else
          Hmap.Add(spf[x], 1);
        x = x / spf[x];
      }
    }

    // Erase 1 as a key because
    // it is not a prime number
    Hmap.Remove(1);

    foreach(KeyValuePair<int, int> x in Hmap)
    {

      // First prime number
      int primeNum = x.Key;
      int frequency = x.Value;

      // Frequency is divisible
      // by K then insert primeNum
      // in the result[]
      if (frequency % K == 0)
      {
        result.Add(primeNum);
      }
    }

    // Print the elements
    // if it exists
    if (result.Count > 0)
    {
      foreach(int it in result)
      {
        Console.Write(it + " ");
      }
    }
    else
    {
      Console.Write("{}");
    }
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Given array []arr
    int[] arr = {1, 4, 6};

    // Given K
    int K = 1;

    int N = arr.Length;

    // Function call
    frequent_prime(arr, N, K);
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To store the smallest prime
# factor till 10^5
spf  = [0 for i in range(10001)] 

# Function to compute smallest
# prime factor array
def spf_array(spf):

    # Initialize the spf array
    # first element
    spf[1] = 1

    for i in range(2, 1000, 1):

        # Marking smallest prime
        # factor for every number
        # to be itself
        spf[i] = i

    # Separately marking smallest
    # prime factor for every even
    # number as 2
    for i in range(4, 1000, 2):
        spf[i] = 2

    i = 3
    while( i* i < 1000):

        # Checking if i is prime
        if (spf[i] == i):

            # Marking SPF for all
            # numbers divisible by i
            j = i * i
            while(j < 1000):

                # Marking spf[j] if it is
                # not previously marked
                if (spf[j] == j):
                    spf[j] = i

                j += i

        i += 1

# Function that finds minimum operation
def frequent_prime(arr, N, K):

    # Create a spf[] array
    spf_array(spf)

    # Map created to store the
    # unique prime numbers
    Hmap = {}

    # To store the result
    result = []
    i = 0

    # To store minimum operations
    c = 0

    # To store every unique
    # prime number
    for i in range(N):
        x = arr[i]

        while (x != 1):
            Hmap[spf[x]] = Hmap.get(spf[x], 0) + 1
            x = x // spf[x]

    # Erase 1 as a key because
    # it is not a prime number
    if (1 in Hmap):
      Hmap.pop(1)

    for key, value in Hmap.items():

        # First Prime Number
        primeNum = key
        frequency = value

        # Frequency is divisible
        # by K then insert primeNum
        # in the result[]
        if (frequency % K == 0):
            result.append(primeNum)

    # Print the elements
    # if it exists
    result = result[::-1]

    if (len(result) > 0):
        for it in result:
            print(it, end = " ")
    else:
        print("{}")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr =  [ 1, 4, 6 ]

    # Given K
    K = 1

    N = len(arr)

    # Function Call
    frequent_prime(arr, N, K)

# This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// To store the smallest prime
// factor till 10^5
var spf = Array(10001);

// Function to compute smallest
// prime factor array
function spf_array(spf)
{
    // Initialize the spf array
    // first element
    spf[1] = 1;

    for (var i = 2; i < 1000; i++)

        // Marking smallest prime
        // factor for every number
        // to be itself
        spf[i] = i;

    // Separately marking smallest
    // prime factor for every even
    // number as 2
    for (var i = 4; i < 1000; i += 2)
        spf[i] = 2;

    for (var i = 3; i * i < 1000; i++) {

        // Checking if i is prime
        if (spf[i] == i) {

            // Marking SPF for all
            // numbers divisible by i
            for (var j = i * i;
                j < 1000; j += i)

                // Marking spf[j] if it is
                // not previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function that finds minimum operation
function frequent_prime(arr, N, K)
{

    // Create a spf[] array
    spf_array(spf);

    // Map created to store the
    // unique prime numbers
    var Hmap = new Map();

    // To store the result
    var result = [];
    var i = 0;

    // To store minimum operations
    var c = 0;

    // To store every unique
    // prime number
    for (i = 0; i < N; i++) {

        var x = arr[i];
        while (x != 1) {

            if(Hmap.has(spf[x]))
                Hmap.set(spf[x], Hmap.get(spf[x])+1)
            else
                Hmap.set(spf[x], 1);
            x = parseInt(x / spf[x]);
        }
    }

    // Erase 1 as a key because
    // it is not a prime number
    Hmap.delete(1);

    Hmap.forEach((value, key) => {

        // First Prime Number
        var primeNum = key;
        var frequency = value;

        // Frequency is divisible
        // by K then insert primeNum
        // in the result[]
        if (frequency % K == 0) {
            result.push(primeNum);
        }
    });

    // Print the elements
    // if it exists
    if (result.length > 0) {
        result.forEach(it => {
            document.write(it+" ");
        });

    }
    else {
        document.write( "{}");
    }
}

// Driver Code

// Given array arr[]
var arr = [1, 4, 6];

// Given K
var K = 1;
var N = arr.length;

// Function Call
frequent_prime(arr, N, K);

</script>
```

**输出:**

```
3 2
```

***时间复杂度:** O(M*log(M))，其中 M 是数组的最大元素。*
**辅助** ***空间:** O(M)*