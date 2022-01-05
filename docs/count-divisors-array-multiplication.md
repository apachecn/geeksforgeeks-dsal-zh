# 计算数组乘法的除数

> 原文:[https://www . geesforgeks . org/count-除数-数组-乘法/](https://www.geeksforgeeks.org/count-divisors-array-multiplication/)

给定一个有 N 个元素的数组，任务是找出一个数 X 的因子数，它是所有数组元素的乘积。

**示例:**

```
Input : 5 5
Output : 3
5 * 5 = 25, the factors of 25 are 1, 5, 25
whose count is 3

Input : 3 5 7
Output : 8
3 * 5 * 7 = 105, the factors of 105 are 1,
3, 5, 7, 15, 21, 35, 105 whose count is 8
```

**方法 1(简单但会导致溢出)**
1。将数组的所有元素相乘。
2。[计算乘法后得到的数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)中的除数。

## C++

```
// A simple C++ program to count divisors
// in array multiplication.
#include <iostream>
using namespace std;

// To count number of factors in a number
int counDivisors(int X)
{
    // Initialize count with 0
    int count = 0;
    // Increment count for every factor
    // of the given number X.
    for (int i = 1; i <= X; ++i) {
        if (X % i == 0) {
            count++;
        }
    }

    // Return number of factors
    return count;
}

// Returns number of divisors in array
// multiplication
int countDivisorsMult(int arr[], int n)
{
    // Multipliying all elements of
    // the given array.
    int mul = 1;
    for (int i = 0; i < n; ++i)
        mul *= arr[i];

    // Calling function which count number of factors
    // of the number
    return counDivisors(mul);
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countDivisorsMult(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to count divisors
// in array multiplication.

class GFG
{
    // To count number of factors in a number
    static int counDivisors(int X)
    {
        // Initialize count with 0
        int count = 0;

        // Increment count for every factor
        // of the given number X.
        for (int i = 1; i <= X; ++i)
        {
            if (X % i == 0) {
                count++;
            }
        }

        // Return number of factors
        return count;
    }

    // Returns number of divisors in array
    // multiplication
    static int countDivisorsMult(int arr[], int n)
    {
        // Multipliying all elements of
        // the given array.
        int mul = 1;
        for (int i = 0; i < n; ++i)
            mul *= arr[i];

        // Calling function which count
        // number of factors of the number
        return counDivisors(mul);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 4, 6 };
        int n = arr.length;
        System.out.println(countDivisorsMult(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# A simple Python program
# to count divisors
# in array multiplication.

# To count number of
# factors in a number
def counDivisors(X):

    # Initialize count with 0
    count = 0
    # Increment count for
    # every factor
    # of the given number X.
    for i in range(1, X + 1):
        if (X % i == 0):
            count += 1

    # Return number of factors
    return count

# Returns number of
# divisors in array
# multiplication
def countDivisorsMult(arr, n):

    # Multipliying all elements of
    # the given array.
    mul = 1
    for i in range(n):
        mul *= arr[i]

    # Calling function which
    # count number of factors
    # of the number
    return counDivisors(mul)

# Driver code

arr = [ 2, 4, 6 ]
n =len(arr)

print(countDivisorsMult(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count divisors
// in array multiplication.
using System;

class GFG {

    // To count number of factors
    // in a number
    static int counDivisors(int X)
    {

        // Initialize count with 0
        int count = 0;

        // Increment count for every
        // factor of the given
        // number X.
        for (int i = 1; i <= X; ++i)
        {
            if (X % i == 0) {
                count++;
            }
        }

        // Return number of factors
        return count;
    }

    // Returns number of divisors in
    // array multiplication
    static int countDivisorsMult(
                    int []arr, int n)
    {

        // Multipliying all elements
        // of the given array.
        int mul = 1;

        for (int i = 0; i < n; ++i)
            mul *= arr[i];

        // Calling function which
        // count number of factors
        // of the number
        return counDivisors(mul);
    }

    // Driver code
    public static void Main ()
    {

        int []arr = { 2, 4, 6 };
        int n = arr.Length;

        Console.Write(
         countDivisorsMult(arr, n));
    }
}

// This code is contributed by
// nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to count divisors
// in array multiplication.

// To count number of factors in a number
function counDivisors($X)
{

    // Initialize count with 0
    $count = 0;

    // Increment count for every factor
    // of the given number X.
    for ($i = 1; $i <= $X; ++$i) {
        if ($X % $i == 0) {
            $count++;
        }
    }

    // Return number of factors
    return $count;
}

// Returns number of divisors in array
// multiplication
function countDivisorsMult($arr, $n)
{

    // Multipliying all elements of
    // the given array.
    $mul = 1;
    for ($i = 0; $i < $n; ++$i)
        $mul *= $arr[$i];

    // Calling function which count
    // number of factors of the number
    return counDivisors($mul);
}

// Driver code
$arr = array(2, 4, 6);
$n = sizeof($arr);
echo countDivisorsMult($arr, $n);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript program to count divisors
// in array multiplication.

    // To count number of factors in a number
    function counDivisors(X)
    {
        // Initialize count with 0
        let count = 0;

        // Increment count for every factor
        // of the given number X.
        for (let i = 1; i <= X; ++i)
        {
            if (X % i == 0) {
                count++;
            }
        }

        // Return number of factors
        return count;
    }

    // Returns number of divisors in array
    // multiplication
   function countDivisorsMult(arr, n)
    {
        // Multipliying all elements of
        // the given array.
        let mul = 1;
        for (let i = 0; i < n; ++i)
            mul *= arr[i];

        // Calling function which count
        // number of factors of the number
        return counDivisors(mul);
    }

// driver function
        let arr = [ 2, 4, 6 ];
        let n = arr.length;
        document.write(countDivisorsMult(arr, n));

  // This code is contributed by code_hunt.
</script>   
```

**输出:**

```
10
```

**方法 2(避免溢出)**
1。在数组中找到最大元素
2。寻找小于最大元素的质数
3。通过遍历所有数组元素并找到它们的素因子，找出每个素因子在整个数组中出现的总次数。我们使用散列法来计算出现次数。
4。设素数因子出现的次数为 a1，a2，…aK，如果我们有 K 个不同的素数因子，那么答案将是:(a1+1)(a2+1)(…)*(aK+1)。

## C++

```
// C++ program to count divisors in array multiplication.
#include <bits/stdc++.h>
using namespace std;

void SieveOfEratosthenes(int largest, vector<int> &prime)
{

    // Create a boolean array "isPrime[0..n]" and initialize
    // all entries it as true. A value in isPrime[i] will
    // finally be false if i is Not a isPrime, else true.
    bool isPrime[largest+1];
    memset(isPrime, true, sizeof(isPrime));

    for (int p = 2; p * p <= largest; p++)
    {

        // If isPrime[p] is not changed, then it is a isPrime
        if (isPrime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= largest; i += p)
                isPrime[i] = false;
        }
    }

    // Print all isPrime numbers
    for (int p = 2; p <= largest; p++)
        if (isPrime[p])
            prime.push_back(p);
}

// Returns number of divisors in array
// multiplication
int countDivisorsMult(int arr[], int n)
{

    // Find all prime numbers smaller than
    // the largest element.
    int largest = *max_element(arr, arr+n);
    vector<int> prime;
    SieveOfEratosthenes(largest, prime);

    // Find counts of occurrences of each prime
    // factor
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < prime.size(); j++)
        {
            while(arr[i] > 1 && arr[i]%prime[j] == 0)
            {
                arr[i] /= prime[j];
                mp[prime[j]]++;
            }
        }
        if (arr[i] != 1)
            mp[arr[i]]++;
    }

    // Compute count of all divisors using counts
    // prime factors.
    long long int res = 1;
    for (auto it : mp)
       res *= (it.second + 1L);
    return res;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countDivisorsMult(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count divisors in array multiplication.
import java.io.*;
import java.util.*;
class GFG
{

  static void SieveOfEratosthenes(int largest, ArrayList<Integer> prime)
  {

    // Create a boolean array "isPrime[0..n]" and initialize
    // all entries it as true. A value in isPrime[i] will
    // finally be false if i is Not a isPrime, else true.
    boolean[] isPrime = new boolean[largest + 1];
    Arrays.fill(isPrime, true);

    for (int p = 2; p * p <= largest; p++)
    {

      // If isPrime[p] is not changed, then it is a isPrime
      if (isPrime[p] == true)
      {

        // Update all multiples of p
        for (int i = p * 2; i <= largest; i += p)
          isPrime[i] = false;
      }
    }

    // Print all isPrime numbers
    for (int p = 2; p <= largest; p++)
      if (isPrime[p])
        prime.add(p);
  }

  // Returns number of divisors in array
  // multiplication
  static long countDivisorsMult(int[] arr, int n)
  {

    // Find all prime numbers smaller than
    // the largest element.
    int largest = 0;
    for(int a : arr )
    {
      largest=Math.max(largest, a);
    }

    ArrayList<Integer> prime = new ArrayList<Integer>();
    SieveOfEratosthenes(largest, prime);

    // Find counts of occurrences of each prime
    // factor
    Map<Integer,Integer> mp = new HashMap<>();
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < prime.size(); j++)
      {
        while(arr[i] > 1 && arr[i]%prime.get(j) == 0)
        {
          arr[i] /= prime.get(j);
          if(mp.containsKey(prime.get(j)))
          {
            mp.put(prime.get(j), mp.get(prime.get(j)) + 1);
          }
          else
          {
            mp.put(prime.get(j), 1);
          }
        }
      }
      if (arr[i] != 1)
      {
        if(mp.containsKey(arr[i]))
        {
          mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
          mp.put(arr[i], 1);
        }
      }
    }

    // Compute count of all divisors using counts
    // prime factors.
    long res = 1;
    for (int it : mp.keySet())
      res *= (mp.get(it) + 1L);
    return res;
  }

  // Driver code
  public static void main (String[] args) {
    int arr[] = { 2, 4, 6 };
    int n = arr.length;
    System.out.println(countDivisorsMult(arr, n));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python 3 program to count divisors in array multiplication.
from collections import defaultdict
def SieveOfEratosthenes(largest, prime):

    # Create a boolean array "isPrime[0..n]" and initialize
    # all entries it as true. A value in isPrime[i] will
    # finally be false if i is Not a isPrime, else true.
    isPrime = [True] * (largest + 1)

    p = 2
    while p * p <= largest:

        # If isPrime[p] is not changed, then it is a isPrime
        if (isPrime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, largest + 1, p):
                isPrime[i] = False
        p += 1

    # Print all isPrime numbers
    for p in range(2, largest + 1):
        if (isPrime[p]):
            prime.append(p)

# Returns number of divisors in array
# multiplication
def countDivisorsMult(arr, n):

    # Find all prime numbers smaller than
    # the largest element.
    largest = max(arr)
    prime = []
    SieveOfEratosthenes(largest, prime)

    # Find counts of occurrences of each prime
    # factor
    mp = defaultdict(int)
    for i in range(n):
        for j in range(len(prime)):
            while(arr[i] > 1 and arr[i] % prime[j] == 0):
                arr[i] //= prime[j]
                mp[prime[j]] += 1
        if (arr[i] != 1):
            mp[arr[i]] += 1

    # Compute count of all divisors using counts
    # prime factors.
    res = 1
    for it in mp.values():
        res *= (it + 1)
    return res

# Driver code
if __name__ == "__main__":

    arr = [2, 4, 6]
    n = len(arr)
    print(countDivisorsMult(arr, n))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program to count divisors in array multiplication.
using System;
using System.Collections.Generic;

class GFG{

static void SieveOfEratosthenes(int largest,
                                List<int> prime)
{

    // Create a boolean array "isPrime[0..n]" and initialize
    // all entries it as true. A value in isPrime[i] will
    // finally be false if i is Not a isPrime, else true.
    bool[] isPrime = new bool[largest + 1];
    Array.Fill(isPrime, true);

    for(int p = 2; p * p <= largest; p++)
    {

        // If isPrime[p] is not changed, then it is a isPrime
        if (isPrime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= largest; i += p)
                isPrime[i] = false;
        }
    }

    // Print all isPrime numbers
    for(int p = 2; p <= largest; p++)
        if (isPrime[p])
            prime.Add(p);
}

// Returns number of divisors in array
// multiplication
static long countDivisorsMult(int[] arr, int n)
{

    // Find all prime numbers smaller than
    // the largest element.
    int largest = 0;
    foreach(int a in arr )
    {
        largest = Math.Max(largest, a);
    }

    List<int> prime = new List<int>();
    SieveOfEratosthenes(largest, prime);

    // Find counts of occurrences of each prime
    // factor
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < prime.Count; j++)
        {
            while(arr[i] > 1 && arr[i] % prime[j] == 0)
            {
                arr[i] /= prime[j];
                if (mp.ContainsKey(prime[j]))
                {
                    mp[prime[j]]++;
                }
                else
                {
                    mp.Add(prime[j], 1);
                }
            }
        }
        if (arr[i] != 1)
        {
            if(mp.ContainsKey(arr[i]))
            {
                mp[arr[i]]++;
            }
            else
            {
                mp.Add(arr[i], 1);
            }
        }
    }

    // Compute count of all divisors using counts
    // prime factors.
    long res = 1;
    foreach(KeyValuePair<int, int> it in mp)
        res *= (it.Value + 1L);

    return res;
}

// Driver code
static public void Main()
{
    int[] arr = { 2, 4, 6 };
    int n = arr.Length;

    Console.WriteLine(countDivisorsMult(arr, n));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// javascript program to count divisors in array multiplication.

function SieveOfEratosthenes(largest, prime)
{

    // Create a boolean array "isPrime[0..n]" and initialize
    // all entries it as true. A value in isPrime[i] will
    // finally be false if i is Not a isPrime, else true.
    var isPrime = Array(largest+1).fill(true);

    var p,i;
    for (p = 2; p * p <= largest; p++)
    {

        // If isPrime[p] is not changed, then it is a isPrime
        if (isPrime[p] == true)
        {

            // Update all multiples of p
            for(i = p * 2; i <= largest; i += p)
                isPrime[i] = false;
        }
    }

    // Print all isPrime numbers
    for (p = 2; p <= largest; p++)
        if (isPrime[p])
            prime.push(p);
}

// Returns number of divisors in array
// multiplication
function countDivisorsMult(arr, n)
{

    // Find all prime numbers smaller than
    // the largest element.
    var largest = Math.max.apply(null,arr);
    var prime = [];
    SieveOfEratosthenes(largest, prime);

    // Find counts of occurrences of each prime
    // factor
    var j;
    var mp = new Map();
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < prime.length; j++)
        {
            while(arr[i] > 1 && arr[i]%prime[j] == 0)
            {
                arr[i] /= prime[j];
                if(mp.has(prime[j]))
                 mp.set(prime[j],mp.get(prime[j])+1);
                else
                  mp.set(prime[j],1);
            }
        }
        if (arr[i] != 1){
            if(mp.has(arr[i]))
                 mp.set(arr[i],mp.get(arr[i])+1);
                else
                  mp.set(arr[i],1);
        }
    }

    // Compute count of all divisors using counts
    // prime factors.
    var res = 1;
    for (const [key, value] of mp.entries()) {
        res *= (value + 1);
    }

    return res;
}

// Driver code
    var arr =  [2, 4, 6];
    var n = arr.length;
    document.write(countDivisorsMult(arr, n));

</script>
```

**输出:**

```
10
```

本文由 [**萨赫勒拉吉普特**](http://inkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。