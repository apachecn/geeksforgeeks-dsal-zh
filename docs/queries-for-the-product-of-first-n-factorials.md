# 查询第一个 N 阶乘的乘积

> 原文:[https://www . geeksforgeeks . org/first-n-factories 产品查询/](https://www.geeksforgeeks.org/queries-for-the-product-of-first-n-factorials/)

给定 **Q[]** 查询，其中每个查询由整数 **N** 组成，任务是为每个查询找到第一个 **N** 阶乘的乘积。因为结果可能很大，所以以 **10 <sup>9</sup> + 7** 为模进行计算。
**举例:**

> **输入:** Q[] = {4，5 }
> T3】输出:T5】288
> 34560
> 查询 1: 1！* 2!* 3!* 4!= 1 * 2 * 6 * 24 = 288
> 查询 2: 1！* 2!* 3!* 4!* 5!= 1 * 2 * 6 * 24 * 120 = 34560
> **输入:** Q[] = {500，1000，7890}
> **输出:**
> 976141892
> 560688561
> 793351288

**方法:**创建两个数组**结果[]** 和**事实[]** ，其中**事实[i]** 将存储 **i** 的阶乘，**结果[i]** 将存储第一个 **i** 阶乘的乘积。
初始化**事实[0] = 1** 和**结果[0] = 1** 。现在对于其余的值，循环关系将是:

> 事实[i] =事实[I–1]* I
> 结果[i] =结果[I–1]*事实[i]

现在，可以使用生成的**结果[]** 数组来回答每个查询。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define MAX 1000000

const ll MOD = 1e9 + 7;

// Declare result array globally
ll result[MAX + 1];
ll fact[MAX + 1];

// Function to precompute the product
// of factorials upto MAX
void preCompute()
{

    // Initialize base condition if n = 0
    // then factorial of 0 is equal to 1
    // and answer for n = 0 is 1
    fact[0] = 1;
    result[0] = 1;

    // Iterate loop from 1 to MAX
    for (int i = 1; i <= MAX; i++) {

        // factorial(i) = factorial(i - 1) * i
        fact[i] = ((fact[i - 1] % MOD) * i) % MOD;

        // Result for current n is equal to result[i-1]
        // multiplied by the factorial of i
        result[i] = ((result[i - 1] % MOD) * (fact[i] % MOD)) % MOD;
    }
}

// Function to perform the queries
void performQueries(int q[], int n)
{

    // Precomputing the result till MAX
    preCompute();

    // Perform queries
    for (int i = 0; i < n; i++)
        cout << result[q[i]] << "\n";
}

// Driver code
int main()
{

    int q[] = { 4, 5 };
    int n = sizeof(q) / sizeof(q[0]);

    performQueries(q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{
static int MAX = 1000000;

static int MOD = 10000007;

// Declare result array globally
static int []result = new int [MAX + 1];
static int []fact = new int [MAX + 1];

// Function to precompute the product
// of factorials upto MAX
static void preCompute()
{

    // Initialize base condition if n = 0
    // then factorial of 0 is equal to 1
    // and answer for n = 0 is 1
    fact[0] = 1;
    result[0] = 1;

    // Iterate loop from 1 to MAX
    for (int i = 1; i <= MAX; i++)
    {

        // factorial(i) = factorial(i - 1) * i
        fact[i] = ((fact[i - 1] % MOD) * i) % MOD;

        // Result for current n is equal to result[i-1]
        // multiplied by the factorial of i
        result[i] = ((result[i - 1] % MOD) *
                   (fact[i] % MOD)) % MOD;
    }
}

// Function to perform the queries
static void performQueries(int q[], int n)
{

    // Precomputing the result till MAX
    preCompute();

    // Perform queries
    for (int i = 0; i < n; i++)
        System.out.println (result[q[i]]);
}

// Driver code
public static void main (String[] args)
{
    int q[] = { 4, 5 };
    int n = q.length;

    performQueries(q, n);
}
}

// This code is contributed by tushil.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 1000000
MOD = 10**9 + 7

# Declare result array globally
result = [0 for i in range(MAX + 1)]
fact = [0 for i in range(MAX + 1)]

# Function to precompute the product
# of factorials upto MAX
def preCompute():

    # Initialize base condition if n = 0
    # then factorial of 0 is equal to 1
    # and answer for n = 0 is 1
    fact[0] = 1
    result[0] = 1

    # Iterate loop from 1 to MAX
    for i in range(1, MAX + 1):

        # factorial(i) = factorial(i - 1) * i
        fact[i] = ((fact[i - 1] % MOD) * i) % MOD

        # Result for current n is 
        # equal to result[i-1]
        # multiplied by the factorial of i
        result[i] = ((result[i - 1] % MOD) *
                     (fact[i] % MOD)) % MOD

# Function to perform the queries
def performQueries(q, n):

    # Precomputing the result tiMAX
    preCompute()

    # Perform queries
    for i in range(n):
        print(result[q[i]])

# Driver code
q = [4, 5]
n = len(q)

performQueries(q, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 1000000;

static int MOD = 10000007;

// Declare result array globally
static int []result = new int [MAX + 1];
static int []fact = new int [MAX + 1];

// Function to precompute the product
// of factorials upto MAX
static void preCompute()
{

    // Initialize base condition if n = 0
    // then factorial of 0 is equal to 1
    // and answer for n = 0 is 1
    fact[0] = 1;
    result[0] = 1;

    // Iterate loop from 1 to MAX
    for (int i = 1; i <= MAX; i++)
    {

        // factorial(i) = factorial(i - 1) * i
        fact[i] = ((fact[i - 1] % MOD) * i) % MOD;

        // Result for current n is equal to result[i-1]
        // multiplied by the factorial of i
        result[i] = ((result[i - 1] % MOD) *
                     (fact[i] % MOD)) % MOD;
    }
}

// Function to perform the queries
static void performQueries(int []q, int n)
{

    // Precomputing the result till MAX
    preCompute();

    // Perform queries
    for (int i = 0; i < n; i++)
        Console.WriteLine(result[q[i]]);
}

// Driver code
public static void Main (String[] args)
{
    int []q = { 4, 5 };
    int n = q.Length;

    performQueries(q, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let MAX = 1000000;

    let MOD = 10000007;

    // Declare result array globally
    let result = new Array(MAX + 1);
    result.fill(0);
    let fact = new Array(MAX + 1);
    fact.fill(0);

    // Function to precompute the product
    // of factorials upto MAX
    function preCompute()
    {

        // Initialize base condition if n = 0
        // then factorial of 0 is equal to 1
        // and answer for n = 0 is 1
        fact[0] = 1;
        result[0] = 1;

        // Iterate loop from 1 to MAX
        for (let i = 1; i <= MAX; i++)
        {

            // factorial(i) = factorial(i - 1) * i
            fact[i] = ((fact[i - 1] % MOD) * i) % MOD;

            // Result for current n is equal to result[i-1]
            // multiplied by the factorial of i
            result[i] = ((result[i - 1] % MOD) *
                         (fact[i] % MOD)) % MOD;
        }
    }

    // Function to perform the queries
    function performQueries(q, n)
    {

        // Precomputing the result till MAX
        preCompute();

        // Perform queries
        for (let i = 0; i < n; i++)
            document.write(result[q[i]] + "</br>");
    }

    let q = [ 4, 5 ];
    let n = q.length;

    performQueries(q, n);

</script>
```

**Output:** 

```
288
34560
```