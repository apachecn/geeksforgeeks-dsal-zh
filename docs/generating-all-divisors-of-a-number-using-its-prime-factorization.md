# 利用一个数的素因子分解生成它的所有除数

> 原文:[https://www . geeksforgeeks . org/利用素数分解生成一个数的所有除数/](https://www.geeksforgeeks.org/generating-all-divisors-of-a-number-using-its-prime-factorization/)

给定一个整数 **N** ，任务是利用它的素分解找到它的所有除数。

**示例:**

> **输入:**N = 6
> T3】输出: 1 2 3 6
> 
> **输入:**N = 10
> T3】输出: 1 2 5 10

**方法:**由于每个大于 1 的数在其素分解中都可以表示为 p<sub>1</sub><sup>a</sup><sub><sup>1</sup></sub>* p<sub>2</sub>T12】a<sub>T15】2T17 *……* p<sub>k</sub>T20】a<sub>T23】k</sub>，其中 p<sub>I【T29
现在，如果 n 的每个素因子的出现次数已知，所有可能的除数都可以递归生成。对于每个质因数 p <sub>i</sub> ，可以包含 x 次，其中 0 ≤ x ≤ a <sub>i</sub> 。首先，使用[这个](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)方法找到 n 的素因子分解，对于每个素因子，用它出现的次数来存储它。
以下是上述方法的实施:</sub></sub>

## C++

```
// C++ implementation of the approach
#include "iostream"
#include "vector"
using namespace std;

struct primeFactorization {

    // to store the prime factor
    // and its highest power
    int countOfPf, primeFactor;
};

// Recursive function to generate all the
// divisors from the prime factors
void generateDivisors(int curIndex, int curDivisor,
                      vector<primeFactorization>& arr)
{

    // Base case i.e. we do not have more
    // primeFactors to include
    if (curIndex == arr.size()) {
        cout << curDivisor << ' ';
        return;
    }

    for (int i = 0; i <= arr[curIndex].countOfPf; ++i) {
        generateDivisors(curIndex + 1, curDivisor, arr);
        curDivisor *= arr[curIndex].primeFactor;
    }
}

// Function to find the divisors of n
void findDivisors(int n)
{

    // To store the prime factors along
    // with their highest power
    vector<primeFactorization> arr;

    // Finding prime factorization of n
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            int count = 0;
            while (n % i == 0) {
                n /= i;
                count += 1;
            }

            // For every prime factor we are storing
            // count of it's occurenceand itself.
            arr.push_back({ count, i });
        }
    }

    // If n is prime
    if (n > 1) {
        arr.push_back({ 1, n });
    }

    int curIndex = 0, curDivisor = 1;

    // Generate all the divisors
    generateDivisors(curIndex, curDivisor, arr);
}

// Driver code
int main()
{
    int n = 6;

    findDivisors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

static class primeFactorization
{

    // to store the prime factor
    // and its highest power
    int countOfPf, primeFactor;

    public primeFactorization(int countOfPf,
                              int primeFactor)
    {
        this.countOfPf = countOfPf;
        this.primeFactor = primeFactor;
    }
}

// Recursive function to generate all the
// divisors from the prime factors
static void generateDivisors(int curIndex, int curDivisor,
                           Vector<primeFactorization> arr)
{

    // Base case i.e. we do not have more
    // primeFactors to include
    if (curIndex == arr.size())
    {
        System.out.print(curDivisor + " ");
        return;
    }

    for (int i = 0; i <= arr.get(curIndex).countOfPf; ++i)
    {
        generateDivisors(curIndex + 1, curDivisor, arr);
        curDivisor *= arr.get(curIndex).primeFactor;
    }
}

// Function to find the divisors of n
static void findDivisors(int n)
{

    // To store the prime factors along
    // with their highest power
    Vector<primeFactorization> arr = new Vector<>();

    // Finding prime factorization of n
    for (int i = 2; i * i <= n; ++i)
    {
        if (n % i == 0)
        {
            int count = 0;
            while (n % i == 0)
            {
                n /= i;
                count += 1;
            }

            // For every prime factor we are storing
            // count of it's occurenceand itself.
            arr.add(new primeFactorization(count, i ));
        }
    }

    // If n is prime
    if (n > 1)
    {
        arr.add(new primeFactorization( 1, n ));
    }

    int curIndex = 0, curDivisor = 1;

    // Generate all the divisors
    generateDivisors(curIndex, curDivisor, arr);
}

// Driver code
public static void main(String []args)
{
    int n = 6;

    findDivisors(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to generate all the
# divisors from the prime factors
def generateDivisors(curIndex, curDivisor, arr):

    # Base case i.e. we do not have more
    # primeFactors to include
    if (curIndex == len(arr)):
        print(curDivisor, end = ' ')
        return

    for i in range(arr[curIndex][0] + 1):
        generateDivisors(curIndex + 1, curDivisor, arr)
        curDivisor *= arr[curIndex][1]

# Function to find the divisors of n
def findDivisors(n):

    # To store the prime factors along
    # with their highest power
    arr = []

    # Finding prime factorization of n
    i = 2
    while(i * i <= n):
        if (n % i == 0):
            count = 0
            while (n % i == 0):
                n //= i
                count += 1

            # For every prime factor we are storing
            # count of it's occurenceand itself.
            arr.append([count, i])

    # If n is prime
    if (n > 1):
        arr.append([1, n])

    curIndex = 0
    curDivisor = 1

    # Generate all the divisors
    generateDivisors(curIndex, curDivisor, arr)

# Driver code
n = 6
findDivisors(n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

public class primeFactorization
{

    // to store the prime factor
    // and its highest power
    public int countOfPf, primeFactor;

    public primeFactorization(int countOfPf,
                              int primeFactor)
    {
        this.countOfPf = countOfPf;
        this.primeFactor = primeFactor;
    }
}

// Recursive function to generate all the
// divisors from the prime factors
static void generateDivisors(int curIndex, int curDivisor,
                             List<primeFactorization> arr)
{

    // Base case i.e. we do not have more
    // primeFactors to include
    if (curIndex == arr.Count)
    {
        Console.Write(curDivisor + " ");
        return;
    }

    for (int i = 0; i <= arr[curIndex].countOfPf; ++i)
    {
        generateDivisors(curIndex + 1, curDivisor, arr);
        curDivisor *= arr[curIndex].primeFactor;
    }
}

// Function to find the divisors of n
static void findDivisors(int n)
{

    // To store the prime factors along
    // with their highest power
    List<primeFactorization> arr = new List<primeFactorization>();

    // Finding prime factorization of n
    for (int i = 2; i * i <= n; ++i)
    {
        if (n % i == 0)
        {
            int count = 0;
            while (n % i == 0)
            {
                n /= i;
                count += 1;
            }

            // For every prime factor we are storing
            // count of it's occurenceand itself.
            arr.Add(new primeFactorization(count, i ));
        }
    }

    // If n is prime
    if (n > 1)
    {
        arr.Add(new primeFactorization( 1, n ));
    }

    int curIndex = 0, curDivisor = 1;

    // Generate all the divisors
    generateDivisors(curIndex, curDivisor, arr);
}

// Driver code
public static void Main(String []args)
{
    int n = 6;

    findDivisors(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Recursive function to generate all the
// divisors from the prime factors
function generateDivisors(curIndex, curDivisor, arr)
{

    // Base case i.e. we do not have more
    // primeFactors to include
    if (curIndex == arr.length) {
        document.write(curDivisor + " ");
        return;
    }

    for (var i = 0; i <= arr[curIndex][0]; ++i) {
        generateDivisors(curIndex + 1, curDivisor, arr);
        curDivisor *= arr[curIndex][1];
    }
}

// Function to find the divisors of n
function findDivisors(n)
{

    // To store the prime factors along
    // with their highest power
    arr = [];

    // Finding prime factorization of n
    for (var i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            var count = 0;
            while (n % i == 0) {
                n /= i;
                count += 1;
            }

            // For every prime factor we are storing
            // count of it's occurenceand itself.
            arr.push([ count, i ]);
        }
    }

    // If n is prime
    if (n > 1) {
        arr.push([ 1, n ]);
    }

    var curIndex = 0, curDivisor = 1;

    // Generate all the divisors
    generateDivisors(curIndex, curDivisor, arr);
}

// driver code
var n = 6;
findDivisors(n);
// This code contributed by shubhamsingh10
</script>
```

**Output:** 

```
1 3 2 6
```