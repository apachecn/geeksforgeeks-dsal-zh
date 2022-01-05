# 从两个不同的数组中找出成对的元素，它们的乘积是一个完美的正方形

> 原文:[https://www . geeksforgeeks . org/find-从两个不同的数组中找到元素对-其乘积是一个完美的正方形/](https://www.geeksforgeeks.org/find-pairs-of-elements-from-two-different-arrays-whose-product-is-a-perfect-square/)

**先决条件:** [使用筛子的素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)
给定两个大小为 **M** 和 **N** 的数组**arr 1【】**和**arr 2【】**，每个数组中有不同的元素，任务是找到乘积为完美平方的那对元素(一个来自第一个数组，另一个来自第二个数组)。如果无法形成对，打印-1。

**示例:**

> **输入:** arr1[] = {1，8，6，9}，arr2[] = {2，24，49}
> **输出:** (1，49)、(8，2)、(6，24)、(9，49)
> **解释:**
> 输出中的对积都是完美平方。
> 对 1: 1 x 49 = 49
> 对 2: 8 x 2 = 16
> 对 3: 6 x 24 = 144
> 对 4: 9 x 49 = 441
> 
> **输入:** arr1[] = {2，3，4}，arr2[] = {9，5}
> **输出:** -1

**天真法:**天真法是选择所有可能的对，检查它们是否形成一个完美的正方形。这可以在二次时间内完成。
**时间复杂度:** O(M*N)

**有效途径:**思路是利用素分解的概念。让我们分析一下如何在这个问题中使用这个概念。
以下是两个数字的乘积形成一个完美正方形的情况:

*   如果两个数都是完美的正方形，它们的乘积总是形成一个完美的正方形。
*   如果其中一个数字不是完美的正方形，那么它们的乘积永远不可能是完美的正方形。
*   如果两个数都是非完美平方数，那么两个数的质因数之和必须是偶数。
*   例如，

> 设 x = 6，y = 1176
> x = 2 x 3 的素因子分解(2 和 3 出现奇数次)
> y = 2 x 2 x 3 x 7 x 7(2 和 3 出现奇数次)
> x * y = 7056 这是 84 的平方

*   因为 x 和 y 都有奇数次出现的素数，但是 x * y 有偶数个素数因子。因此，它们将形成一个完美的正方形。

因此，遍历数组 **arr1[]** ，对于 **arr1[]** 中的每个元素，数组 **arr2[]** 中的数字具有与当前元素相同的奇数次出现素数的乘积。这可以在 **logn** 时间内使用 C++中的[映射 STL](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 来完成。

下面是上述方法的实现:

## C++

```
// C++ program to print pairs whose
// product is a perfect square
#include <bits/stdc++.h>
using namespace std;

// Maximum number upto which sieve is performed
#define MAXN 100001

// Array to perform Sieve of Eratosthenes
// and store prime numbers
int spf[MAXN];

// Function to perform sieve of
// eratosthenes on the array spf.
void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)
        spf[i] = i;

    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j < MAXN; j += i)

                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to return the product of the
// odd occurring prime factors of a number
int getProductOddOccuringPrimes(int x)
{
    // Product of 1 with perfect square gives
    // perfect square, 1 is returned for x = 1
    if (x == 1)
        return 1;

    // Temporary container of prime factors
    vector<int> ret;
    while (x != 1) {
        ret.push_back(spf[x]);
        x = x / spf[x];
    }

    // ans contains the product of primes
    // which occurs odd number of times
    int count = 1, ans = 1;
    for (int i = 0, j = 1; j < ret.size(); ++j, ++i) {
        if (ret[i] != ret[j]) {
            if (count & 1)
                ans *= ret[i];
            count = 0;
        }
        count++;
    }

    // Checks if count is odd or not
    if (count & 1)
        ans *= ret[ret.size() - 1];

    return ans;
}

// Function to print the pairs whose product is
// a perfect square
void printPairs(int n, int m, int a[], int b[])
{
    int countPairs = 0;

    // For storing the indicies with same
    // product of odd times occurring Primes as key
    map<int, vector<int> > productOfPrimes;

    // Every number from both the array is iterated
    // getProductOddOccuringPrimes function is called
    // and the product of odd occurring primes is
    // stored in the map productOfPrimes.
    // A pair is printed if the product is same
    for (int i = 0; i < n; ++i) {

        // Generating the product of odd times
        // occurring primes
        int productPrimesOfA
            = getProductOddOccuringPrimes(a[i]);

        // Pushing the indices to the to the
        // vector with the product of
        // odd times occurring Primes
        productOfPrimes[productPrimesOfA].push_back(i);
    }

    for (int i = 0; i < m; ++i) {
        // Generating the product of odd times
        // occurring Primes
        int productPrimesOfB
            = getProductOddOccuringPrimes(b[i]);

        // Checking if productPrimesOfB
        // lies in the productOfPrimes
        if (productOfPrimes.find(productPrimesOfB)
            != productOfPrimes.end()) {
            for (auto itr : productOfPrimes[productPrimesOfB]) {
                countPairs++;
                cout << " (" << b[i] << ", "
                     << a[itr] << ") ";
            }
        }
    }
    if (countPairs <= 0)
        cout << "No pairs Found!";
    cout << endl;
}
// Driver function
int main()
{
    sieve();

    // N, M are size of array a and b respectively
    int N = 5, M = 5;
    int a[] = { 4, 1, 6, 35, 120 };
    int b[] = { 24, 140, 4, 30, 1 };

    // Function that prints the pairs
    // whose product is a perfect square
    printPairs(N, M, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print pairs whose
// product is a perfect square
import java.util.*;

class GFG{

// Maximum number upto which sieve is performed
static final int MAXN = 100001;

// Array to perform Sieve of Eratosthenes
// and store prime numbers
static int []spf = new int[MAXN];

// Function to perform sieve of
// eratosthenes on the array spf.
static void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)
        spf[i] = i;

    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j < MAXN; j += i)

                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to return the product of the
// odd occurring prime factors of a number
static int getProductOddOccuringPrimes(int x)
{
    // Product of 1 with perfect square gives
    // perfect square, 1 is returned for x = 1
    if (x == 1)
        return 1;

    // Temporary container of prime factors
    Vector<Integer> ret = new Vector<Integer>();
    while (x != 1) {
        ret.add(spf[x]);
        x = x / spf[x];
    }

    // ans contains the product of primes
    // which occurs odd number of times
    int count = 1, ans = 1;
    for (int i = 0, j = 1; j < ret.size(); ++j, ++i) {
        if (ret.get(i) != ret.get(j)) {
            if (count % 2 == 1)
                ans *= ret.get(i);
            count = 0;
        }
        count++;
    }

    // Checks if count is odd or not
    if (count %2 == 1)
        ans *= ret.get(ret.size() - 1);

    return ans;
}

// Function to print the pairs whose product is
// a perfect square
static void printPairs(int n, int m, int a[], int b[])
{
    int countPairs = 0;

    // For storing the indicies with same
    // product of odd times occurring Primes as key
    Map<Integer, Vector<Integer>> productOfPrimes =
            new HashMap<Integer, Vector<Integer>>();

    // Every number from both the array is iterated
    // getProductOddOccuringPrimes function is called
    // and the product of odd occurring primes is
    // stored in the map productOfPrimes.
    // A pair is printed if the product is same
    for (int i = 0; i < n; ++i) {

        // Generating the product of odd times
        // occurring primes
        int productPrimesOfA
            = getProductOddOccuringPrimes(a[i]);

        // Pushing the indices to the to the
        // vector with the product of
        // odd times occurring Primes
        Vector<Integer> temp = new Vector<Integer>();
        if(productOfPrimes.containsKey(productPrimesOfA))
        for (Integer s:productOfPrimes.get(productPrimesOfA)){
            temp.add(s);
        }
        temp.add(i);
        productOfPrimes.put(productPrimesOfA, temp);
    }

    for (int i = 0; i < m; ++i)
    {

        // Generating the product of odd times
        // occurring Primes
        int productPrimesOfB
            = getProductOddOccuringPrimes(b[i]);

        // Checking if productPrimesOfB
        // lies in the productOfPrimes
        if (productOfPrimes.containsKey(productPrimesOfB)) {
            for (Integer itr : productOfPrimes.get(productPrimesOfB)) {
                countPairs++;
                System.out.print(" (" + b[i]+ ", "
                    + a[itr]+ ") ");
            }
        }
    }
    if (countPairs <= 0)
        System.out.print("No pairs Found!");
    System.out.println();
}

// Driver function
public static void main(String[] args)
{
    sieve();

    // N, M are size of array a and b respectively
    int N = 5, M = 5;
    int a[] = { 4, 1, 6, 35, 120 };
    int b[] = { 24, 140, 4, 30, 1 };

    // Function that prints the pairs
    // whose product is a perfect square
    printPairs(N, M, a, b);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to print pairs whose
// product is a perfect square
using System;
using System.Collections.Generic;

class GFG{

// Maximum number upto which sieve is performed
static readonly int MAXN = 100001;

// Array to perform Sieve of Eratosthenes
// and store prime numbers
static int []spf = new int[MAXN];

// Function to perform sieve of
// eratosthenes on the array spf.
static void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)
        spf[i] = i;

    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j < MAXN; j += i)

                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to return the product of the
// odd occurring prime factors of a number
static int getProductOddOccuringPrimes(int x)
{
    // Product of 1 with perfect square gives
    // perfect square, 1 is returned for x = 1
    if (x == 1)
        return 1;

    // Temporary container of prime factors
    List<int> ret = new List<int>();
    while (x != 1) {
        ret.Add(spf[x]);
        x = x / spf[x];
    }

    // ans contains the product of primes
    // which occurs odd number of times
    int count = 1, ans = 1;
    for (int i = 0, j = 1; j < ret.Count; ++j, ++i) {
        if (ret[i] != ret[j]) {
            if (count % 2 == 1)
                ans *= ret[i];
            count = 0;
        }
        count++;
    }

    // Checks if count is odd or not
    if (count %2 == 1)
        ans *= ret[ret.Count - 1];

    return ans;
}

// Function to print the pairs whose product is
// a perfect square
static void printPairs(int n, int m, int []a, int []b)
{
    int countPairs = 0;

    // For storing the indicies with same
    // product of odd times occurring Primes as key
    Dictionary<int, List<int>> productOfPrimes =
            new Dictionary<int, List<int>>();

    // Every number from both the array is iterated
    // getProductOddOccuringPrimes function is called
    // and the product of odd occurring primes is
    // stored in the map productOfPrimes.
    // A pair is printed if the product is same
    for (int i = 0; i < n; ++i) {

        // Generating the product of odd times
        // occurring primes
        int productPrimesOfA
            = getProductOddOccuringPrimes(a[i]);

        // Pushing the indices to the to the
        // vector with the product of
        // odd times occurring Primes
        List<int> temp = new List<int>();
        if(productOfPrimes.ContainsKey(productPrimesOfA))
        foreach (int s in productOfPrimes[productPrimesOfA]){
            temp.Add(s);
        }
        temp.Add(i);
        if(productOfPrimes.ContainsKey(productPrimesOfA))
            productOfPrimes[productPrimesOfA] = temp;
        else
            productOfPrimes.Add(productPrimesOfA, temp);
    }

    for (int i = 0; i < m; ++i)
    {

        // Generating the product of odd times
        // occurring Primes
        int productPrimesOfB
            = getProductOddOccuringPrimes(b[i]);

        // Checking if productPrimesOfB
        // lies in the productOfPrimes
        if (productOfPrimes.ContainsKey(productPrimesOfB)) {
            foreach (int itr in productOfPrimes[productPrimesOfB]) {
                countPairs++;
                Console.Write(" (" + b[i]+ ", "
                    + a[itr]+ ") ");
            }
        }
    }
    if (countPairs <= 0)
        Console.Write("No pairs Found!");
    Console.WriteLine();
}

// Driver function
public static void Main(String[] args)
{
    sieve();

    // N, M are size of array a and b respectively
    int N = 5, M = 5;
    int []a = { 4, 1, 6, 35, 120 };
    int []b = { 24, 140, 4, 30, 1 };

    // Function that prints the pairs
    // whose product is a perfect square
    printPairs(N, M, a, b);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
(24, 6)  (140, 35)  (4, 4)  (4, 1)  (30, 120)  (1, 4)  (1, 1)
```

**时间复杂度:** O(Klog(K))，其中 K = max(N，M)