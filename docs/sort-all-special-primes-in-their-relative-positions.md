# 将所有特殊素数按其相对位置排序

> 原文:[https://www . geesforgeks . org/sort-all-special-primes-in-它们的相对位置/](https://www.geeksforgeeks.org/sort-all-special-primes-in-their-relative-positions/)

给定一个正整数大小为 **N** 的数组 **arr[]** ，任务是将所有特殊素数按其相对位置排序(不影响其他元素的位置)。一个特殊的质数是一个质数，它可以表示为另外两个质数的和。

**示例:**

> **输入:** arr[] = {31，5，2，1，7}
> **输出:** 5 7 2 1 31
> 特殊素数为 31 (29 + 2)，5 (2 + 3)，7 (5 + 2)。
> 把它们排序，我们得到 5、7、31。
> 所以，原来的数组变成了{5，7，2，1，31}
> 
> **输入:** arr[] = {3，13，11，43，2，19，17}
> **输出:** 3 13 11 19 2 43 17

**进场:**

*   开始遍历数组，对于每个元素 **arr[i]** ，如果 **arr[i]** 是[特殊素数](https://www.geeksforgeeks.org/check-if-a-prime-number-can-be-expressed-as-sum-of-two-prime-numbers/)，则将其存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，并更新 **arr[i] = -1**
*   所有特殊素数存储在列表中后，[对更新后的列表进行](https://www.geeksforgeeks.org/quick-sort-vs-merge-sort/)排序。
*   再次遍历数组，对于每个元素，
    *   如果 **arr[i] = -1** ，则打印列表中之前没有打印过的第一个元素。
    *   否则，打印 **arr[i]** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function for the Sieve of Eratosthenes
void sieveOfEratosthenes(bool prime[], int n)
{
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to sort the special primes
// in their relative positions
void sortSpecialPrimes(int arr[], int n)
{

    // Maximum element from the array
    int maxVal = *max_element(arr, arr + n);

    // prime[i] will be true if i is a prime
    bool prime[maxVal + 1];
    memset(prime, true, sizeof(prime));
    sieveOfEratosthenes(prime, maxVal);

    // To store the special primes
    // from the array
    vector<int> list;

    for (int i = 0; i < n; i++) {

        // If current element is a special prime
        if (prime[arr[i]] && prime[arr[i] - 2]) {

            // Add it to the ArrayList
            // and set arr[i] to -1
            list.push_back(arr[i]);
            arr[i] = -1;
        }
    }

    // Sort the special primes
    sort(list.begin(), list.end());

    int j = 0;
    for (int i = 0; i < n; i++) {

        // Position of a special prime
        if (arr[i] == -1)
            cout << list[j++] << " ";
        else
            cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 31, 5, 2, 1, 7 };
    int n = sizeof(arr) / sizeof(int);

    sortSpecialPrimes(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function for the Sieve of Eratosthenes
static void sieveOfEratosthenes(boolean prime[],
                                int n)
{
    prime[0] = prime[1] = false;
    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // greater than or equal to the
            // square of it numbers which are
            // multiple of p and are less than
            // p^2 are already been marked.
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to sort the special primes
// in their relative positions
static void sortSpecialPrimes(int arr[], int n)
{

    // Maximum element from the array
    int maxVal = Arrays.stream(arr).max().getAsInt();

    // prime[i] will be true if i is a prime
    boolean []prime = new boolean[maxVal + 1];
    for(int i = 0; i < prime.length; i++)
        prime[i] = true;

    sieveOfEratosthenes(prime, maxVal);

    // To store the special primes
    // from the array
    Vector<Integer> list = new Vector<Integer>();

    for(int i = 0; i < n; i++)
    {

        // If current element is a special prime
        if (prime[arr[i]] && prime[arr[i] - 2])
        {

            // Add it to the ArrayList
            // and set arr[i] to -1
            list.add(arr[i]);
            arr[i] = -1;
        }
    }

    // Sort the special primes
    Collections.sort(list);

    int j = 0;
    for(int i = 0; i < n; i++)
    {

        // Position of a special prime
        if (arr[i] == -1)
            System.out.print(list.get(j++) + " ");
        else
            System.out.print(arr[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 31, 5, 2, 1, 7 };
    int n = arr.length;

    sortSpecialPrimes(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function for the Sieve of Eratosthenes
static void sieveOfEratosthenes(bool []prime,
                                int n)
{
    prime[0] = prime[1] = false;
    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // greater than or equal to the
            // square of it numbers which are
            // multiple of p and are less than
            // p^2 are already been marked.
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to sort the special primes
// in their relative positions
static void sortSpecialPrimes(int []arr, int n)
{

    // Maximum element from the array
    int maxVal = arr.Max();

    // prime[i] will be true if i is a prime
    bool []prime = new bool[maxVal + 1];
    for(int i = 0; i < prime.Length; i++)
        prime[i] = true;

    sieveOfEratosthenes(prime, maxVal);

    // To store the special primes
    // from the array
    List<int> list = new List<int>();

    for(int i = 0; i < n; i++)
    {

        // If current element is a special prime
        if (prime[arr[i]] && prime[arr[i] - 2])
        {

            // Add it to the List
            // and set arr[i] to -1
            list.Add(arr[i]);
            arr[i] = -1;
        }
    }

    // Sort the special primes
    list.Sort();

    int j = 0;
    for(int i = 0; i < n; i++)
    {

        // Position of a special prime
        if (arr[i] == -1)
            Console.Write(list[j++] + " ");
        else
            Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 31, 5, 2, 1, 7 };
    int n = arr.Length;

    sortSpecialPrimes(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function for the Sieve of Eratosthenes
function sieveOfEratosthenes(prime, n)
{
    prime[0] = prime[1] = false;
    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // greater than or equal to the
            // square of it numbers which are
            // multiple of p and are less than
            // p^2 are already been marked.
            for(let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to sort the special primes
// in their relative positions
function sortSpecialPrimes(arr, n)
{

    // Maximum element from the array
    let maxVal = Math.max(...arr);

    // prime[i] will be true if i is a prime
    let prime = Array.from(
        {length: maxVal + 1}, (_, i) => 0);
    for(let i = 0; i < prime.length; i++)
        prime[i] = true;

    sieveOfEratosthenes(prime, maxVal);

    // To store the special primes
    // from the array
    let list = [];

    for(let i = 0; i < n; i++)
    {

        // If current element is a special prime
        if (prime[arr[i]] && prime[arr[i] - 2])
        {

            // Add it to the List
            // and set arr[i] to -1
            list.push(arr[i]);
            arr[i] = -1;
        }
    }

    // Sort the special primes
    list.sort((a, b) => a - b);

    let j = 0;
    for(let i = 0; i < n; i++)
    {

        // Position of a special prime
        if (arr[i] == -1)
            document.write(list[j++] + " ");
        else
            document.write(arr[i] + " ");
    }
}

// Driver Code
let arr = [ 31, 5, 2, 1, 7 ];
let n = arr.length;

sortSpecialPrimes(arr, n);

// This code is contributed by target_2

</script>
```

**Output:** 

```
5 7 2 1 31
```

时间复杂度:O(n * log n)

辅助空间:O(n)