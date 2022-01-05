# 检查是否存在一个恰好有 N 个因子和 K 个素因子的数

> 原文:[https://www . geesforgeks . org/check-if-a-number-exists-with-n-factors-and-k-prime-factors/](https://www.geeksforgeeks.org/check-if-a-number-exists-having-exactly-n-factors-and-k-prime-factors/)

给定两个数字 **N** 和 **K** ，任务是找出一个整数 **X** 是否存在，使得它正好有 N 个因子，并且其中的 K 是素数。
**示例:**

> **输入:** N = 4，K = 2
> **输出:**是
> **说明:**
> X 的一个可能数字是 6。
> 数字 6 共有 4 个因素:1、2、3 & 6。
> 也正好有 2 个素因子:2 & 3。
> **输入:** N = 3，K = 1
> **输出:**是
> **解释:**
> X 的一个可能的数字是 49。
> 数字 49 共有 3 个因素:1、7、& 49。
> 也正好有 1 个质因数:7。

**进场:**思路是用以下身份。

*   对于任何数字 X，如果该数字有 **N** 个因子，其中 **K** 为质数:

```
X = k1a + k2b + k3c + ... + knn
```

*   因子 N 的总数等于:

```
N = (a + 1) * (b + 1) * (c + 1) .. (n + 1)
```

*   因此，想法是检查 **N** 是否可以表示为大于 1 的 **K** 整数的乘积。这可以通过[找到数字 **N** 的除数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)来实现。
*   如果这个的计数小于 K，那么答案是不可能的。否则，是有可能的。

下面是上述方法的实现:

## C++

```
// C++ program to check if it
// is possible to make a number
// having total N factors and
// K prime factors

#include <bits/stdc++.h>
using namespace std;

// Function to compute the
// number of factors of
// the given number
bool factors(int n, int k)
{
    // Vector to store
    // the prime factors
    vector<int> v;

    // While there are no
    // two multiples in
    // the number, divide
    // it by 2
    while (n % 2 == 0) {
        v.push_back(2);
        n /= 2;
    }

    // If the size is already
    // greater than K,
    // then return true
    if (v.size() >= k)
        return true;

    // Computing the remaining
    // divisors of the number
    for (int i = 3; i * i <= n;
         i += 2) {

        // If n is divisible by i,
        // then it is a divisor
        while (n % i == 0) {
            n = n / i;
            v.push_back(i);
        }

        // If the size is already
        // greater than K, then
        // return true
        if (v.size() >= k)
            return true;
    }

    if (n > 2)
        v.push_back(n);

    // If the size is already
    // greater than K,
    // then return true
    if (v.size() >= k)
        return true;

    // If none of the above
    // conditions satisfies,
    // then return false
    return false;
}

// Function to check if it is
// possible to make a number
// having total N factors and
// K prime factors
void operation(int n, int k)
{
    bool answered = false;

    // If total divisors are
    // less than the number
    // of prime divisors,
    // then print No
    if (n < k) {
        answered = true;
        cout << "No"
             << "\n";
    }

    // Find the number of
    // factors of n
    bool ok = factors(n, k);

    if (!ok && !answered) {
        answered = true;
        cout << "No"
             << "\n";
    }

    if (ok && !answered)
        cout << "Yes"
             << "\n";
}

// Driver Code
int main()
{
    int n = 4;
    int k = 2;

    operation(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it
// is possible to make a number
// having total N factors and
// K prime factors
import java.io.*;
import java.util.*;

class GFG{

// Function to compute the
// number of factors of
// the given number
static boolean factors(int n, int k)
{

    // Vector to store
    // the prime factors
    ArrayList<Integer> v = new ArrayList<Integer>();

    // While there are no
    // two multiples in
    // the number, divide
    // it by 2
    while (n % 2 == 0)
    {
        v.add(2);
        n /= 2;
    }

    // If the size is already
    // greater than K,
    // then return true
    if (v.size() >= k)
        return true;

    // Computing the remaining
    // divisors of the number
    for(int i = 3; i * i <= n; i += 2)
    {

       // If n is divisible by i,
       // then it is a divisor
       while (n % i == 0)
       {
           n = n / i;
           v.add(i);
       }

       // If the size is already
       // greater than K, then
       // return true
       if (v.size() >= k)
           return true;
    }

    if (n > 2)
        v.add(n);

    // If the size is already
    // greater than K,
    // then return true
    if (v.size() >= k)
        return true;

    // If none of the above
    // conditions satisfies,
    // then return false
    return false;
}

// Function to check if it is
// possible to make a number
// having total N factors and
// K prime factors
static void operation(int n, int k)
{
    boolean answered = false;

    // If total divisors are
    // less than the number
    // of prime divisors,
    // then print No
    if (n < k)
    {
        answered = true;
        System.out.println("No");
    }

    // Find the number of
    // factors of n
    boolean ok = factors(n, k);

    if (!ok && !answered)
    {
        answered = true;
        System.out.println("No");
    }
    if (ok && !answered)
        System.out.println("Yes");
}

// Driver code
public static void main(String[] args)
{
    int n = 4;
    int k = 2;

    //Function call
    operation(n, k);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to check if it
# is possible to make a number
# having total N factors and
# K prime factors

# Function to compute the
# number of factors of
# the given number
def factors(n, k):

    # Vector to store
    # the prime factors
    v = [];

    # While there are no
    # two multiples in
    # the number, divide
    # it by 2
    while (n % 2 == 0):
        v.append(2);
        n //= 2;

    # If the size is already
    # greater than K,
    # then return true
    if (len(v) >= k):
        return True;

    # Computing the remaining
    # divisors of the number
    for i in range(3, int(n ** (1 / 2)), 2):

        # If n is divisible by i,
        # then it is a divisor
        while (n % i == 0):
            n = n // i;
            v.append(i);

        # If the size is already
        # greater than K, then
        # return true
        if (len(v) >= k):
            return True;

    if (n > 2):
        v.append(n);

    # If the size is already
    # greater than K,
    # then return true
    if (len(v) >= k):
        return True;

    # If none of the above
    # conditions satisfies,
    # then return false
    return False;

# Function to check if it is
# possible to make a number
# having total N factors and
# K prime factors
def operation(n, k):
    answered = False;

    # If total divisors are
    # less than the number
    # of prime divisors,
    # then print No
    if (n < k):
        answered = True;
        print("No");

    # Find the number of
    # factors of n
    ok = factors(n, k);

    if (not ok and not answered):
        answered = True;
        print("No");

    if (ok and not answered):
        print("Yes");

# Driver Code
if __name__ == "__main__":

    n = 4;
    k = 2;
    operation(n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to check if it
// is possible to make a number
// having total N factors and
// K prime factors
using System;
using System.Collections.Generic;

class GFG{

// Function to compute the
// number of factors of
// the given number
static bool factors(int n, int k)
{

    // Vector to store
    // the prime factors
    List<int> v = new List<int>();

    // While there are no
    // two multiples in
    // the number, divide
    // it by 2
    while (n % 2 == 0)
    {
        v.Add(2);
        n /= 2;
    }

    // If the size is already
    // greater than K,
    // then return true
    if (v.Count >= k)
        return true;

    // Computing the remaining
    // divisors of the number
    for(int i = 3; i * i <= n; i += 2)
    {

        // If n is divisible by i,
        // then it is a divisor
        while (n % i == 0)
        {
            n = n / i;
            v.Add(i);
        }

        // If the size is already
        // greater than K, then
        // return true
        if (v.Count >= k)
            return true;
    }

    if (n > 2)
        v.Add(n);

    // If the size is already
    // greater than K,
    // then return true
    if (v.Count >= k)
        return true;

    // If none of the above
    // conditions satisfies,
    // then return false
    return false;
}

// Function to check if it is
// possible to make a number
// having total N factors and
// K prime factors
static void operation(int n, int k)
{
    bool answered = false;

    // If total divisors are
    // less than the number
    // of prime divisors,
    // then print No
    if (n < k)
    {
        answered = true;
        Console.WriteLine("No");
    }

    // Find the number of
    // factors of n
    bool ok = factors(n, k);

    if (!ok && !answered)
    {
        answered = true;
        Console.WriteLine("No");
    }
    if (ok && !answered)
        Console.WriteLine("Yes");
}

// Driver code
public static void Main()
{
    int n = 4;
    int k = 2;

    // Function call
    operation(n, k);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to check if it
// is possible to make a number
// having total N factors and
// K prime factors

// Function to compute the
// number of factors of
// the given number
function factors(n, k)
{
    // Vector to store
    // the prime factors
    let v = [];

    // While there are no
    // two multiples in
    // the number, divide
    // it by 2
    while (n % 2 == 0) {
        v.push(2);
        n = parseInt(n/2);
    }

    // If the size is already
    // greater than K,
    // then return true
    if (v.length >= k)
        return true;

    // Computing the remaining
    // divisors of the number
    for (let i = 3; i * i <= n;
         i += 2) {

        // If n is divisible by i,
        // then it is a divisor
        while (n % i == 0) {
            n = parseInt(n / i);
            v.push(i);
        }

        // If the size is already
        // greater than K, then
        // return true
        if (v.length >= k)
            return true;
    }

    if (n > 2)
        v.push(n);

    // If the size is already
    // greater than K,
    // then return true
    if (v.length >= k)
        return true;

    // If none of the above
    // conditions satisfies,
    // then return false
    return false;
}

// Function to check if it is
// possible to make a number
// having total N factors and
// K prime factors
function operation(n, k)
{
    let answered = false;

    // If total divisors are
    // less than the number
    // of prime divisors,
    // then print No
    if (n < k) {
        answered = true;
        document.write("No<br>");
    }

    // Find the number of
    // factors of n
    let ok = factors(n, k);

    if (!ok && !answered) {
        answered = true;
        document.write("No<br>");
    }

    if (ok && !answered)
        document.write("Yes<br>");
}

// Driver Code
let n = 4;
let k = 2;

operation(n, k);

</script>
```

**Output:** 

```
Yes
```

时间复杂度:O(n <sup>1/2</sup> )

辅助空间:O(n <sup>1/2</sup> )