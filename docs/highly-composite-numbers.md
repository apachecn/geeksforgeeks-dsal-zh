# 高复合数

> 原文:[https://www.geeksforgeeks.org/highly-composite-numbers/](https://www.geeksforgeeks.org/highly-composite-numbers/)

如果一个数 N 的除数比任何小于 N 的数都多，则称之为高度复合数。

> 1, 2, 4, 6, 12, 24, 36, 48, 60, 120….

### 检查 N 是否为高复合数

给定一个数字 **N** ，任务是检查 **N** 是否为**高复合数**。如果 **N** 是比打印**高的复合数，“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 60
> **输出:**是的
> 60 是一个高度复合的数，因为它有 12 个除数
> 并且 59 以下的数都没有 12 个或更多的除数。
> 
> **输入:**N = 18
> T3】输出:否

**进场:**

1.  求 N 的除数
2.  现在，在从 1 到小于 N 的循环中，检查每个 I，如果 I 的除数大于 N 的除数，则返回 false
3.  否则，最后还真。

下面是上述方法的实现:

## C++

```
// C++ implementation for checking
// Highly Composite Number

#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of divisors of the N
int divCount(int n)
{
    // sieve method for prime calculation
    bool hash[n + 1];
    memset(hash, true, sizeof(hash));
    for (int p = 2; p * p < n; p++)
        if (hash[p] == true)
            for (int i = p * 2; i < n; i += p)
                hash[i] = false;

    // Traversing through
    // all prime numbers
    int total = 1;
    for (int p = 2; p <= n; p++) {
        if (hash[p]) {

            // calculate number of divisor
            // with formula total div =
            // (p1+1) * (p2+1) *.....* (pn+1)
            // where n = (a1^p1)*(a2^p2)....
            // *(an^pn) ai being prime divisor
            // for n and pi are their respective
            // power in factorization
            int count = 0;
            if (n % p == 0) {
                while (n % p == 0) {
                    n = n / p;
                    count++;
                }
                total = total * (count + 1);
            }
        }
    }
    return total;
}

// Function to check if a number
// is a highly composite number
bool isHighlyCompositeNumber(int N)
{
    // count number of factors of N
    int NdivCount = divCount(N);

    // loop to count number of factors of
    // every number less than N
    for (int i = 1; i < N; i++) {
        int idivCount = divCount(i);

        // If any number less than N has
        // more factors than N,
        // then return false
        if (idivCount >= NdivCount)
            return false;
    }

    return true;
}

// Driver code
int main()
{
    // Given Number N
    int N = 12;

    // Function Call
    if (isHighlyCompositeNumber(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for checking
// Highly Composite Number
import java.util.*;
class GFG{

// Function to count the number
// of divisors of the N
static int divCount(int n)
{
    // sieve method for prime calculation
    boolean []hash = new boolean[n + 1];
    Arrays.fill(hash, true);
    for (int p = 2; p * p < n; p++)
        if (hash[p] == true)
            for (int i = p * 2; i < n; i += p)
                hash[i] = false;

    // Traversing through
    // all prime numbers
    int total = 1;
    for (int p = 2; p <= n; p++)
    {
        if (hash[p])
        {

            // calculate number of divisor
            // with formula total div =
            // (p1+1) * (p2+1) *.....* (pn+1)
            // where n = (a1^p1)*(a2^p2)....
            // *(an^pn) ai being prime divisor
            // for n and pi are their respective
            // power in factorization
            int count = 0;
            if (n % p == 0)
            {
                while (n % p == 0)
                {
                    n = n / p;
                    count++;
                }
                total = total * (count + 1);
            }
        }
    }
    return total;
}

// Function to check if a number
// is a highly composite number
static boolean isHighlyCompositeNumber(int N)
{
    // count number of factors of N
    int NdivCount = divCount(N);

    // loop to count number of factors of
    // every number less than N
    for (int i = 1; i < N; i++)
    {
        int idivCount = divCount(i);

        // If any number less than N has
        // more factors than N,
        // then return false
        if (idivCount >= NdivCount)
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    // Given Number N
    int N = 12;

    // Function Call
    if (isHighlyCompositeNumber(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation for checking
# Highly Composite Number

# Function to count the number
# of divisors of the N
def divCount(n):

    # Sieve method for prime calculation
    Hash = [True for i in range(n + 1)]

    p = 2
    while ((p * p) < n):
        if bool(Hash[p]):
            i = p * 2

            while i < n:
                Hash[i] = False
                i += p

        p += 1

    # Traversing through
    # all prime numbers
    total = 1

    for P in range(2, n + 1):
        if (bool(Hash[P])):

            # Calculate number of divisor
            # with formula total div =
            # (p1+1) * (p2+1) *.....* (pn+1)
            # where n = (a1^p1)*(a2^p2)....
            # *(an^pn) ai being prime divisor
            # for n and pi are their respective
            # power in factorization
            count = 0
            if (n % P == 0):
                while (n % P == 0):
                    n = n // P
                    count += 1

                total = total * (count + 1)

    return total

# Function to check if a number
# is a highly composite number
def isHighlyCompositeNumber(N):

    # Count number of factors of N
    NdivCount = divCount(N)

    # Loop to count number of factors of
    # every number less than N
    for i in range(N):
        idivCount = divCount(i)

        # If any number less than N has
        # more factors than N,
        # then return false
        if (idivCount >= NdivCount):
            return bool(False)

    return bool(True)

# Driver code

# Given Number N
N = 12

# Function Call
if (bool(isHighlyCompositeNumber(N))):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation for checking
// Highly Composite Number
using System;
class GFG{

// Function to count the number
// of divisors of the N
static int divCount(int n)
{
    // sieve method for prime calculation
    bool []hash = new bool[n + 1];
    for(int i = 0; i < n + 1; i++)
        hash[i] = true;
    for (int p = 2; p * p < n; p++)
        if (hash[p] == true)
            for (int i = p * 2; i < n; i += p)
                hash[i] = false;

    // Traversing through
    // all prime numbers
    int total = 1;
    for (int p = 2; p <= n; p++)
    {
        if (hash[p])
        {

            // calculate number of divisor
            // with formula total div =
            // (p1+1) * (p2+1) *.....* (pn+1)
            // where n = (a1^p1)*(a2^p2)....
            // *(an^pn) ai being prime divisor
            // for n and pi are their respective
            // power in factorization
            int count = 0;
            if (n % p == 0)
            {
                while (n % p == 0)
                {
                    n = n / p;
                    count++;
                }
                total = total * (count + 1);
            }
        }
    }
    return total;
}

// Function to check if a number
// is a highly composite number
static bool isHighlyCompositeNumber(int N)
{
    // count number of factors of N
    int NdivCount = divCount(N);

    // loop to count number of factors of
    // every number less than N
    for (int i = 1; i < N; i++)
    {
        int idivCount = divCount(i);

        // If any number less than N has
        // more factors than N,
        // then return false
        if (idivCount >= NdivCount)
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    // Given Number N
    int N = 12;

    // Function Call
    if (isHighlyCompositeNumber(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation for checking
// Highly Composite Number

    // Function to count the number
    // of divisors of the N
    function divCount( n) {
        // sieve method for prime calculation
        let hash = Array(n+1).fill(true);

        for ( let p = 2; p * p < n; p++)
            if (hash[p] == true)
                for ( i = p * 2; i < n; i += p)
                    hash[i] = false;

        // Traversing through
        // all prime numbers
        let total = 1;
        for ( p = 2; p <= n; p++) {
            if (hash[p]) {

                // calculate number of divisor
                // with formula total div =
                // (p1+1) * (p2+1) *.....* (pn+1)
                // where n = (a1^p1)*(a2^p2)....
                // *(an^pn) ai being prime divisor
                // for n and pi are their respective
                // power in factorization
                let count = 0;
                if (n % p == 0) {
                    while (n % p == 0) {
                        n = n / p;
                        count++;
                    }
                    total = total * (count + 1);
                }
            }
        }
        return total;
    }

    // Function to check if a number
    // is a highly composite number
    function isHighlyCompositeNumber( N) {
        // count number of factors of N
        let NdivCount = divCount(N);

        // loop to count number of factors of
        // every number less than N
        for ( let i = 1; i < N; i++) {
            let idivCount = divCount(i);

            // If any number less than N has
            // more factors than N,
            // then return false
            if (idivCount >= NdivCount)
                return false;
        }
        return true;
    }

    // Driver code

        // Given Number N
        let N = 12;

        // Function Call
        if (isHighlyCompositeNumber(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n)*
T5】参考:[http://www.numbersaplenty.com/set/highly_composite_number/](http://www.numbersaplenty.com/set/highly_composite_number/)