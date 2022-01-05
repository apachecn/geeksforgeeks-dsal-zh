# 检查矩阵是否遵循给定的约束

> 原文:[https://www . geeksforgeeks . org/check-如果矩阵遵循给定的约束或不遵循约束/](https://www.geeksforgeeks.org/check-if-the-matrix-follows-the-given-constraints-or-not/)

给定一个大小为 **N*M** 的矩阵 **A[][]** ，任务是检查给定的矩阵是否满足以下两个条件:

1.  所有元素的总和是质数
2.  如果 **(i + j)** 是素数，则矩阵中的元素 **A[i][j]** 也应该是素数。

**示例:**

> **输入:** N = 4，M = 5
> A[][] = {{ 1，2，3，2，2 }，{ 2，2，7，7，7，7 }，{ 7，7，21，7，10 }，{ 2，2，3，6，7 }}
> **输出:** YES
> **解释:**
> 所有元素之和= 107(质数)
> 所有可能(I， j)使得(i + j)是素数的是:
> (0+2) = 2(素数)和 A[0][2] = 3(素数)
> (0+3) = 3(素数)和 A[0][3] = 2(素数)
> (1+1) = 2(素数)和 A[1][1] = 2(素数)
> (1+2) = 3(素数)和 A[1][2] = 7(素数)
> (1+4) = = 5(质数)和 A[2][3] = 7(质数)
> (3+0) = 3(质数)和 A[3][0] = 2(质数)
> (3+2) = 5(质数)和 A[3][2] = 3(质数)
> (3+4) = 7(质数)和 A[3][4] = 7(质数)
> 因此，两个条件都满足，答案都是肯定的。
> 
> **输入:** N = 3，M = 3
> A[][] = {{7，3，4}，{11，0，6}，{12，16，3}}
> **输出:** NO
> **解释:**
> 所有元素之和= 62(非质数)
> 因此，不满足第一个条件。

**天真方法:**
计算矩阵中所有元素的和，检查是否是素数。如果没有，打印**否**。否则，遍历整个矩阵，对于每(I，j)个(i + j)为素数，检查 A[ i ][ j ]是否为素数。如果(I，j)的所有这些值都满足这两个条件，打印**是**作为输出。否则，打印**否**。一个数字 **K** 的素性测试可以在 O(√K)中使用简单的蛮力进行。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function checks if
// n is prime or not

bool isPrime(int n)
{

    // Corner case

    if (n <= 1)
        return false;

    // Check from 2 to sqrt(n)

    for (int i = 2; i <= sqrt(n);
         i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function returns sum of
// all elements of matrix

int takeSum(int a[4][5])
{
    // Stores the sum of the matrix
    int sum = 0;

    for (int i = 0; i < 4; i++)
        for (int j = 0; j < 5; j++)
            sum += a[i][j];

    return sum;
}

// Function to check if all a[i][j]
// with prime (i+j) are prime
bool checkIndex(int n, int m,
                int a[4][5])
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If index is prime
            if (isPrime(i + j)) {

                // If element not prime
                if (!isPrime(a[i][j]))
                    return false;
            }
        }
    }
    return true;
}

// Driver code
int main()
{

    int n = 4, m = 5;

    int a[4][5] = { { 1, 2, 3, 2, 2 },
                    { 2, 2, 7, 7, 7 },
                    { 7, 7, 21, 7, 10 },
                    { 2, 2, 3, 6, 7 } };

    int sum = takeSum(a);

    // Check for both conditions
    if (isPrime(sum)
        && checkIndex(n, m, a)) {

        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG{

// Function checks if
// n is prime or not
static boolean isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to Math.sqrt(n)
    for(int i = 2; i <= Math.sqrt(n); i++)
       if (n % i == 0)
           return false;

    return true;
}

// Function returns sum of
// all elements of matrix
static int takeSum(int a[][])
{

    // Stores the sum of the matrix
    int sum = 0;

    for(int i = 0; i < 4; i++)
       for(int j = 0; j < 5; j++)
          sum += a[i][j];

    return sum;
}

// Function to check if all a[i][j]
// with prime (i+j) are prime
static boolean checkIndex(int n, int m,
                          int a[][])
{
    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < m; j++)
       {

          // If index is prime
          if (isPrime(i + j))
          {
              // If element not prime
              if (!isPrime(a[i][j]))
                  return false;
          }
       }
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int n = 4, m = 5;

    int a[][] = { { 1, 2, 3, 2, 2 },
                  { 2, 2, 7, 7, 7 },
                  { 7, 7, 21, 7, 10 },
                  { 2, 2, 3, 6, 7 } };

    int sum = takeSum(a);

    // Check for both conditions
    if (isPrime(sum) && checkIndex(n, m, a))
    {
        System.out.print("YES" + "\n");
    }
    else
    {
        System.out.print("NO" + "\n");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
import math

# Function checks if
# n is prime or not
def isPrime(n):

    # Corner case
    if (n <= 1):
        return False

    # Check from 2 to sqrt(n)
    for i in range(2, int(math.sqrt(n)) + 1):
        if (n % i == 0):
            return False

    return True

# Function returns sum of
# all elements of matrix
def takeSum(a, n, m):

    # Stores the sum of the matrix
    sum = 0

    for i in range(0, n):
        for j in range(0, m):
            sum += a[i][j]

    return sum

# Function to check if all a[i][j]
# with prime (i+j) are prime
def checkIndex(n, m, a):

    for i in range(0, n):
        for j in range(0, m):

            # If index is prime
            if (isPrime(i + j)):

                # If element not prime
                if (isPrime(a[i][j]) != True):
                    return False

    return True

# Driver code
n = 4
m = 5

a = [ [ 1, 2, 3, 2, 2 ] ,
      [ 2, 2, 7, 7, 7 ],
      [ 7, 7, 21, 7, 10 ],
      [ 2, 2, 3, 6, 7 ] ]

sum = takeSum(a, n, m)

# Check for both conditions
if (isPrime(sum) and checkIndex(n, m, a)):
    print("YES")
else:
    print("NO")

# This code is contributed by sanjoy_62
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

// Function checks if
// n is prime or not
static bool isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to Math.Sqrt(n)
    for(int i = 2; i <= Math.Sqrt(n); i++)
       if (n % i == 0)
           return false;

    return true;
}

// Function returns sum of
// all elements of matrix
static int takeSum(int[,]a)
{

    // Stores the sum of the matrix
    int sum = 0;

    for(int i = 0; i < 4; i++)
       for(int j = 0; j < 5; j++)
          sum += a[i, j];

    return sum;
}

// Function to check if all a[i,j]
// with prime (i+j) are prime
static bool checkIndex(int n, int m,
                       int[,]a)
{
    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < m; j++)
       {

          // If index is prime
          if (isPrime(i + j))
          {

              // If element not prime
              if (!isPrime(a[i, j]))
                  return false;
          }
       }
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int n = 4, m = 5;

    int[,]a = { { 1, 2, 3, 2, 2 },
                { 2, 2, 7, 7, 7 },
                { 7, 7, 21, 7, 10 },
                { 2, 2, 3, 6, 7 } };

    int sum = takeSum(a);

    // Check for both conditions
    if (isPrime(sum) && checkIndex(n, m, a))
    {
        Console.Write("YES" + "\n");
    }
    else
    {
        Console.Write("NO" + "\n");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Stores true at prime
// indices
let prime = [];

// Function to generate
// the prime numbers
// using Sieve of Eratosthenes
function buildSieve(sum)
{
    prime = Array.from({length: sum + 1}, (_, i) => 1);

    prime[0] = false;
    prime[1] = false;

    for(let p = 2; p * p < (sum + 1); p++)
    {

        // If p is still true
        if (prime[p] == true)
        {

            // Mark all multiples of p
            for(let i = p * 2;
                    i < (sum + 1);
                    i += p)
                prime[i] = false;
        }
    }
}

// Function returns sum of
// all elements of matrix
function getSum(a)
{
    let s = 0;
    for(let i = 0; i < 4; i++)
        for(let j = 0; j < 5; j++)
            s += a[i][j];

    return s;
}

// Function to check if for all
// prime (i+j), a[i][j] is prime
function checkIndex(n, m, a)
{
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m; j++)
        {

            // If index is prime
            if (prime[i + j] &&
               !prime[a[i][j]])
            {
                return false;
            }
        }
    return true;
}

// Driver code

      let n = 4, m = 5;

    let a = [[ 1, 2, 3, 2, 2 ],
                  [ 2, 2, 7, 7, 7 ],
                  [ 7, 7, 21, 7, 10 ],
                  [ 2, 2, 3, 6, 7 ]];

    let sum = getSum(a);

    buildSieve(sum);

    // Check for both conditions
    if (prime[sum] && checkIndex(n, m, a))
    {
        document.write("YES" + "<br/>");
    }
    else{
        document.write("NO" + "<br/>");
    }

    // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(N * M * √K)*
***辅助空间:** O(1)*

**高效方法:**
为了优化上述方法，我们可以使用厄拉多塞的[筛进行素性检验。将质数存储至**和**，表示矩阵元素的和。这将初级测试的计算复杂度降低到了 *O(1)* ，预计算筛子需要 *O(log(log(sum)))* 。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores true at prime
// indices
vector<bool> prime;

// Function to generate
// the prime numbers
// using Sieve of Eratosthenes
void buildSieve(int sum)
{
    prime = vector<bool>(sum + 1,
                         true);

    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p
                    < (sum + 1);
         p++) {

        // If p is still true
        if (prime[p] == true) {

            // Mark all multiples of p
            for (int i = p * 2;
                 i < (sum + 1);
                 i += p)
                prime[i] = false;
        }
    }
}

// Function returns sum of
// all elements of matrix
int getSum(int a[4][5])
{

    int s = 0;
    for (int i = 0; i < 4; i++)
        for (int j = 0; j < 5; j++)
            s += a[i][j];

    return s;
}

// Function to check if for all
// prime (i+j), a[i][j] is prime
bool checkIndex(int n, int m,
                int a[4][5])
{

    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {

            // If index is prime
            if (prime[i + j]
                && !prime[a[i][j]]) {
                return false;
            }
        }
    return true;
}

// Driver Code
int main()
{

    int n = 4, m = 5;

    int a[4][5] = { { 1, 2, 3, 2, 2 },
                    { 2, 2, 7, 7, 7 },
                    { 7, 7, 21, 7, 10 },
                    { 2, 2, 3, 6, 7 } };

    int sum = getSum(a);

    buildSieve(sum);

    // Check for both conditions
    if (prime[sum] && checkIndex(n, m, a)) {
        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Stores true at prime
// indices
static boolean []prime;

// Function to generate
// the prime numbers
// using Sieve of Eratosthenes
static void buildSieve(int sum)
{
    prime = new boolean[sum + 1];
    Arrays.fill(prime, true);

    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p < (sum + 1); p++)
    {

        // If p is still true
        if (prime[p] == true)
        {

            // Mark all multiples of p
            for(int i = p * 2;
                    i < (sum + 1);
                    i += p)
                prime[i] = false;
        }
    }
}

// Function returns sum of
// all elements of matrix
static int getSum(int a[][])
{
    int s = 0;
    for(int i = 0; i < 4; i++)
        for(int j = 0; j < 5; j++)
            s += a[i][j];

    return s;
}

// Function to check if for all
// prime (i+j), a[i][j] is prime
static boolean checkIndex(int n, int m,
                          int a[][])
{
    for(int i = 0; i < n; i++)
        for(int j = 0; j < m; j++)
        {

            // If index is prime
            if (prime[i + j] &&
               !prime[a[i][j]])
            {
                return false;
            }
        }
    return true;
}

// Driver Code
public static void main(String[] args)
{

    int n = 4, m = 5;

    int a[][] = { { 1, 2, 3, 2, 2 },
                  { 2, 2, 7, 7, 7 },
                  { 7, 7, 21, 7, 10 },
                  { 2, 2, 3, 6, 7 } };

    int sum = getSum(a);

    buildSieve(sum);

    // Check for both conditions
    if (prime[sum] && checkIndex(n, m, a))
    {
        System.out.print("YES" + "\n");
    }
    else
        System.out.print("NO" + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Stores true at prime
# indices
prime = []

# Function to generate
# the prime numbers
# using Sieve of Eratosthenes
def buildSieve(sum):

    global prime
    prime = [True for i in range(sum + 1)]

    prime[0] = False
    prime[1] = False

    p = 2

    while(p * p < (sum + 1)):

        # If p is still true
        if (prime[p]):

            # Mark all multiples of p
            for i in range(p * 2, sum + 1, p):
                prime[i] = False

        p += 1

# Function returns sum of
# all elements of matrix
def getSum(a):

    s = 0

    for i in range(4):
        for j in range(5):
            s += a[i][j]

    return s

# Function to check if for all
# prime (i+j), a[i][j] is prime
def checkIndex(n, m, a):

    for i in range(n):
        for j in range(m):

            # If index is prime
            if (prime[i + j] and
            not prime[a[i][j]]):
                return False

    return True

# Driver code
if __name__=="__main__":

    n = 4
    m = 5

    a = [ [ 1, 2, 3, 2, 2 ],
          [ 2, 2, 7, 7, 7 ],
          [ 7, 7, 21, 7, 10 ],
          [ 2, 2, 3, 6, 7 ] ]

    sum = getSum(a)

    buildSieve(sum)

    # Check for both conditions
    if (prime[sum] and checkIndex(n, m, a)):
        print("YES")
    else:
        print("NO")

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

// Stores true at prime
// indices
static bool []prime;

// Function to generate
// the prime numbers
// using Sieve of Eratosthenes
static void buildSieve(int sum)
{
    prime = new bool[sum + 1];
    for(int i = 0; i < prime.Length; i++)
        prime[i] = true;

    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p < (sum + 1); p++)
    {

        // If p is still true
        if (prime[p] == true)
        {

            // Mark all multiples of p
            for(int i = p * 2;
                    i < (sum + 1);
                    i += p)
                prime[i] = false;
        }
    }
}

// Function returns sum of
// all elements of matrix
static int getSum(int[,]a)
{
    int s = 0;
    for(int i = 0; i < 4; i++)
        for(int j = 0; j < 5; j++)
            s += a[i, j];

    return s;
}

// Function to check if for all
// prime (i+j), a[i,j] is prime
static bool checkIndex(int n, int m,
                       int[,]a)
{
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // If index is prime
            if (prime[i + j] &&
               !prime[a[i, j]])
            {
                return false;
            }
        }
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4, m = 5;

    int[,]a = { { 1, 2, 3, 2, 2 },
                { 2, 2, 7, 7, 7 },
                { 7, 7, 21, 7, 10 },
                { 2, 2, 3, 6, 7 } };

    int sum = getSum(a);

    buildSieve(sum);

    // Check for both conditions
    if (prime[sum] && checkIndex(n, m, a))
    {
        Console.Write("YES" + "\n");
    }
    else
        Console.Write("NO" + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Stores true at prime
// indices
var prime = [];

// Function to generate
// the prime numbers
// using Sieve of Eratosthenes
function buildSieve(sum)
{
    prime = Array(sum+1).fill(true);

    prime[0] = false;
    prime[1] = false;

    for (var p = 2; p * p
                    < (sum + 1);
         p++) {

        // If p is still true
        if (prime[p] == true) {

            // Mark all multiples of p
            for (var i = p * 2;
                 i < (sum + 1);
                 i += p)
                prime[i] = false;
        }
    }
}

// Function returns sum of
// all elements of matrix
function getSum(a)
{

    var s = 0;
    for (var i = 0; i < 4; i++)
        for (var j = 0; j < 5; j++)
            s += a[i][j];

    return s;
}

// Function to check if for all
// prime (i+j), a[i][j] is prime
function checkIndex(n, m, a)
{

    for (var i = 0; i < n; i++)
        for (var j = 0; j < m; j++) {

            // If index is prime
            if (prime[i + j]
                && !prime[a[i][j]]) {
                return false;
            }
        }
    return true;
}

// Driver Code
var n = 4, m = 5;
var a = [ [ 1, 2, 3, 2, 2 ],
                [ 2, 2, 7, 7, 7 ],
                [ 7, 7, 21, 7, 10 ],
                [ 2, 2, 3, 6, 7 ] ];
var sum = getSum(a);
buildSieve(sum);
// Check for both conditions
if (prime[sum] && checkIndex(n, m, a)) {
    document.write( "YES" );
}
else
    document.write( "NO" );

// This code is contributed by itsok.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(log(log(sum)) + (N*M))，其中 **sum** 表示矩阵的和。*
***辅助空间:** O(N)*