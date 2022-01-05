# 检查 N 个数的所有质因数是否唯一

> 原文:[https://www . geeksforgeeks . org/check-if-all-prime-of-number-n-is-unique-or-not/](https://www.geeksforgeeks.org/check-if-all-prime-factors-of-number-n-are-unique-or-not/)

给定一个数字 **N** 。任务是检查给定的数字 **N** 是否有唯一的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。如果是，则打印**是**否则打印**否**。
**举例:**

> **输入:** N = 30
> **输出:** YES
> **解释:**
> N = 30 = 2*3*5
> 因为 30 的所有质因数都是唯一的。
> **输入:** N = 100
> **输出:** NO
> **解释:**
> N = 100 = 2*2*5*5
> 由于 2 和 5 重复两次，所以 100 的所有素因子都不是唯一的。

**进场:**

1.  使用厄拉多塞的[筛找出给定数字 **N** 的所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。
2.  如果得到的所有质因数的乘积等于 **N** ，那么所有质因数都是唯一的，所以打印 YES。
3.  否则打印**否**。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the all the
// distinct prime factors in a vector
vector<int> primeFactors(int n)
{
    int i, j;
    vector<int> Prime;

    // If n is divisible by 2
    if (n % 2 == 0) {
        Prime.push_back(2);
    }

    // Divide n till all factors of 2
    while (n % 2 == 0) {
        n = n / 2;
    }

    // Check for the prime numbers other
    // than 2
    for (i = 3; i <= sqrt(n); i = i + 2) {

        // Store i in Prime[] i is a
        // factor of n
        if (n % i == 0) {
            Prime.push_back(i);
        }

        // Divide n till all factors of i
        while (n % i == 0) {
            n = n / i;
        }
    }

    // If n is greater than 2, then n is
    // prime number after n divided by
    // all factors
    if (n > 2) {
        Prime.push_back(n);
    }

    // Returns the vector Prime
    return Prime;
}

// Function that check whether N is the
// product of distinct prime factors
// or not
void checkDistinctPrime(int n)
{
    // Returns the vector to store
    // all the distinct prime factors
    vector<int> Prime = primeFactors(n);

    // To find the product of all
    // distinct prime factors
    int product = 1;

    // Find the product
    for (auto i : Prime) {
        product *= i;
    }

    // If product is equals to N,
    // print YES, else print NO
    if (product == n)
        cout << "YES";
    else
        cout << "NO";
}

// Driver Code
int main()
{
    int N = 30;
    checkDistinctPrime(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that returns the all the
// distinct prime factors in a vector
static Vector<Integer> primeFactors(int n)
{
    int i, j;
    Vector<Integer> Prime = new Vector<Integer>();

    // If n is divisible by 2
    if (n % 2 == 0) {
        Prime.add(2);
    }

    // Divide n till all factors of 2
    while (n % 2 == 0) {
        n = n / 2;
    }

    // Check for the prime numbers other
    // than 2
    for (i = 3; i <= Math.sqrt(n); i = i + 2) {

        // Store i in Prime[] i is a
        // factor of n
        if (n % i == 0) {
            Prime.add(i);
        }

        // Divide n till all factors of i
        while (n % i == 0) {
            n = n / i;
        }
    }

    // If n is greater than 2, then n is
    // prime number after n divided by
    // all factors
    if (n > 2) {
        Prime.add(n);
    }

    // Returns the vector Prime
    return Prime;
}

// Function that check whether N is the
// product of distinct prime factors
// or not
static void checkDistinctPrime(int n)
{
    // Returns the vector to store
    // all the distinct prime factors
    Vector<Integer> Prime = primeFactors(n);

    // To find the product of all
    // distinct prime factors
    int product = 1;

    // Find the product
    for (int i : Prime) {
        product *= i;
    }

    // If product is equals to N,
    // print YES, else print NO
    if (product == n)
        System.out.print("YES");
    else
        System.out.print("NO");
}

// Driver Code
public static void main(String[] args)
{
    int N = 30;
    checkDistinctPrime(N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that returns the all the
# distinct prime factors in a vector
def primeFactors(n) :

    Prime = [];

    # If n is divisible by 2
    if (n % 2 == 0) :
        Prime.append(2);

    # Divide n till all factors of 2
    while (n % 2 == 0) :
        n = n // 2;

    # Check for the prime numbers other
    # than 2
    for i in range(3, int(n ** (1/2)),2) :

        # Store i in Prime[] i is a
        # factor of n
        if (n % i == 0) :
            Prime.append(i);

        # Divide n till all factors of i
        while (n % i == 0) :
            n = n // i;

    # If n is greater than 2, then n is
    # prime number after n divided by
    # all factors
    if (n > 2) :
        Prime.append(n);

    # Returns the vector Prime
    return Prime;

# Function that check whether N is the
# product of distinct prime factors
# or not
def checkDistinctPrime(n) :

    # Returns the vector to store
    # all the distinct prime factors
    Prime = primeFactors(n);

    # To find the product of all
    # distinct prime factors
    product = 1;

    # Find the product
    for i in Prime :
        product *= i;

    # If product is equals to N,
    # print YES, else print NO
    if (product == n) :
        print("YES");
    else :
        print("NO");

# Driver Code
if __name__ == "__main__" :

    N = 30;
    checkDistinctPrime(N);

# This code is contributed by Yash_R
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that returns the all the
// distinct prime factors in a vector
static List<int> primeFactors(int n)
{
    int i;
    List<int> Prime = new List<int>();

    // If n is divisible by 2
    if (n % 2 == 0) {
        Prime.Add(2);
    }

    // Divide n till all factors of 2
    while (n % 2 == 0) {
        n = n / 2;
    }

    // Check for the prime numbers other
    // than 2
    for (i = 3; i <= Math.Sqrt(n); i = i + 2) {

        // Store i in Prime[] i is a
        // factor of n
        if (n % i == 0) {
            Prime.Add(i);
        }

        // Divide n till all factors of i
        while (n % i == 0) {
            n = n / i;
        }
    }

    // If n is greater than 2, then n is
    // prime number after n divided by
    // all factors
    if (n > 2) {
        Prime.Add(n);
    }

    // Returns the vector Prime
    return Prime;
}

// Function that check whether N is the
// product of distinct prime factors
// or not
static void checkDistinctPrime(int n)
{
    // Returns the vector to store
    // all the distinct prime factors
    List<int> Prime = primeFactors(n);

    // To find the product of all
    // distinct prime factors
    int product = 1;

    // Find the product
    foreach (int i in Prime) {
        product *= i;
    }

    // If product is equals to N,
    // print YES, else print NO
    if (product == n)
        Console.Write("YES");
    else
        Console.Write("NO");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 30;
    checkDistinctPrime(N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that returns the all the
// distinct prime factors in a vector
function primeFactors(n)
{
    let i, j;
    let Prime = new Array();

    // If n is divisible by 2
    if (n % 2 == 0) {
        Prime.push(2);
    }

    // Divide n till all factors of 2
    while (n % 2 == 0) {
        n = n / 2;
    }

    // Check for the prime numbers other
    // than 2
    for (i = 3; i <= Math.sqrt(n); i = i + 2) {

        // Store i in Prime[] i is a
        // factor of n
        if (n % i == 0) {
            Prime.push(i);
        }

        // Divide n till all factors of i
        while (n % i == 0) {
            n = n / i;
        }
    }

    // If n is greater than 2, then n is
    // prime number after n divided by
    // all factors
    if (n > 2) {
        Prime.push(n);
    }

    // Returns the vector Prime
    return Prime;
}

// Function that check whether N is the
// product of distinct prime factors
// or not
function checkDistinctPrime(n)
{
    // Returns the vector to store
    // all the distinct prime factors
    let Prime = primeFactors(n);

    // To find the product of all
    // distinct prime factors
    let product = 1;

    // Find the product
    for (let i of Prime) {
        product *= i;
    }

    // If product is equals to N,
    // print YES, else print NO
    if (product == n)
        document.write("YES");
    else
        document.write("NO");
}

// Driver Code

let N = 30;
checkDistinctPrime(N);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N*log(log N))，其中 N 为给定数字。

**辅助空间:** O(sqrt(n))