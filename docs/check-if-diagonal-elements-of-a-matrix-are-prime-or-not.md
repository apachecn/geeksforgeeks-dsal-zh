# 检查矩阵的对角元素是否为素数

> 原文:[https://www . geeksforgeeks . org/check-如果矩阵的对角元素是质数或非质数/](https://www.geeksforgeeks.org/check-if-diagonal-elements-of-a-matrix-are-prime-or-not/)

给定维度为 **N*N** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **M[][]** ，任务是检查矩阵主对角线和交叉对角线上的所有元素是否都是[素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果发现属实，则打印**“是”**。否则打印**“否”。**

**示例:**

> **输入:** M[][] = {{1，2，3，13}，{5，3，7，8}，{1，2，3，4}，{5，6，7，7}}
> **输出:**是
> **说明:**
> 主对角线上的元素是{1，5，3，7}，都是素数。
> 交叉对角线上的元素是{13，7，2，5}，都是素数。
> 因此，矩阵满足所有必要条件。
> 
> **输入:** M[][] = {{1，2，3}，{5，3，7}，{5，6，4 } }
> T3】输出:否

**方法:**思路是用厄拉多塞的[筛去](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[检查一个数是否是质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。按照以下步骤解决问题:

*   使用厄拉多塞的[筛预计算并存储质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   使用变量 **i** 在范围**【0，N–1】**内迭代循环，并执行以下操作:
    *   检查 M[i][i]，即主对角线上的元素，是否是素数。
    *   检查 M[I][N–1–I]，即交叉对角线上的元素，是否是素数。
    *   如果不满足以上两个条件中的任何一个，打印**“否”**[断开](https://www.geeksforgeeks.org/break-statement-cc/)。
*   否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores if a number is prime or not
bool prime[1000005];

// Function to generate and store
// primes using Sieve Of Eratosthenes
void SieveOfEratosthenes(int N)
{
    // Set all numbers as prime
    memset(prime, true, sizeof(prime));

    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= N; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Set all its multiples
            // as non-prime
            for (int i = p * p;
                 i <= N; i += p)

                prime[i] = false;
        }
    }
}

// Function to check if all diagonal
// elements are prime or not
void checkElementsOnDiagonal(
    vector<vector<int> > M, int N)
{
    // Stores if all diagonal
    // elements are prime or not
    int flag = 1;

    // Precompute primes
    SieveOfEratosthenes(1000000);

    // Traverse the range [0, N-1]
    for (int i = 0; i < N; i++) {

        // Check if numbers on the cross
        // diagonal and main diagonal
        // are primes or not
        flag &= (prime[M[i][i]]
                 && prime[M[i][N - 1 - i]]);
    }

    // If true, then print "Yes"
    if (flag)
        cout << "Yes" << endl;

    // Otherwise, print "No"
    else
        cout << "No";
}

// Driver Code
int main()
{
    vector<vector<int> > M = {
        { 1, 2, 3, 13 },
        { 5, 3, 7, 8 },
        { 1, 2, 3, 4 },
        { 5, 6, 7, 7 }
    };
    int N = M.size();

    // Function Call
    checkElementsOnDiagonal(M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

// Stores if a number is prime or not
static boolean[] prime = new boolean[1000005];

// Function to generate and store
// primes using Sieve Of Eratosthenes
static void SieveOfEratosthenes(int N)
{

    // Set all numbers as prime
    Arrays.fill(prime, true);

    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= N; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Set all its multiples
            // as non-prime
            for (int i = p * p;
                 i <= N; i += p)

                prime[i] = false;
        }
    }
}

// Function to check if all diagonal
// elements are prime or not
static void checkElementsOnDiagonal(int[][] M, int N)
{

    // Stores if all diagonal
    // elements are prime or not
    int flag = 1;

    // Precompute primes
    SieveOfEratosthenes(1000000);

    // Traverse the range [0, N-1]
    for (int i = 0; i < N; i++) {

        // Check if numbers on the cross
        // diagonal and main diagonal
        // are primes or not
        boolean flg = (boolean)(prime[M[i][i]]
                && prime[M[i][N - 1 - i]]);
        int val = (flg) ? 1 : 0;
        flag &= val;
    }

    // If true, then print "Yes"
    if (flag != 0)
        System.out.print("Yes");

    // Otherwise, print "No"
    else
        System.out.print("No");
}

// Driver Code
public static void main (String[] args)
{

    int[][] M = {
        { 1, 2, 3, 13 },
        { 5, 3, 7, 8 },
        { 1, 2, 3, 4 },
        { 5, 6, 7, 7 }
    };
    int N = M.length;

    // Function Call
    checkElementsOnDiagonal(M, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores if a number is prime or not
prime = [True]*1000005

# Function to generate and store
# primes using Sieve Of Eratosthenes
def SieveOfEratosthenes(N):

    # Set all numbers as prime
    # memset(prime, true, sizeof(prime))
    prime[0] = False
    prime[1] = False

    for p in range(2, N + 1):
        if p * p > N:
            break

        # If p is a prime
        if (prime[p] == True):

            # Set all its multiples
            # as non-prime
            for i in range(p * p, N + 1, p):
                prime[i] = False

# Function to check if all diagonal
# elements are prime or not
def checkElementsOnDiagonal(M, N):

    # Stores if all diagonal
    # elements are prime or not
    flag = 1

    # Precompute primes
    SieveOfEratosthenes(1000000)

    # Traverse the range [0, N-1]
    for i in range(N):

        # Check if numbers on the cross
        # diagonal and main diagonal
        # are primes or not
        flag &= (prime[M[i][i]] and prime[M[i][N - 1 - i]])

    # If true, then pr"Yes"
    if (flag):
        print("Yes")

    # Otherwise, pr"No"
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    M = [[ 1, 2, 3, 13 ],
        [ 5, 3, 7, 8 ],
        [ 1, 2, 3, 4 ],
        [ 5, 6, 7, 7 ]]
    N = len(M)

    # Function Call
    checkElementsOnDiagonal(M, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Stores if a number is prime or not
  static bool[] prime = new bool[1000005];

  // Function to generate and store
  // primes using Sieve Of Eratosthenes
  static void SieveOfEratosthenes(int N)
  {

    // Set all numbers as prime
    Array.Fill(prime, true);
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= N; p++) {

      // If p is a prime
      if (prime[p] == true) {

        // Set all its multiples
        // as non-prime
        for (int i = p * p; i <= N; i += p)

          prime[i] = false;
      }
    }
  }

  // Function to check if all diagonal
  // elements are prime or not
  static void checkElementsOnDiagonal(int[, ] M, int N)
  {

    // Stores if all diagonal
    // elements are prime or not
    int flag = 1;

    // Precompute primes
    SieveOfEratosthenes(1000000);

    // Traverse the range [0, N-1]
    for (int i = 0; i < N; i++) {

      // Check if numbers on the cross
      // diagonal and main diagonal
      // are primes or not
      bool flg = (bool)(prime[M[i, i]]
                        && prime[M[i, N - 1 - i]]);
      int val = (flg) ? 1 : 0;
      flag &= val;
    }

    // If true, then print "Yes"
    if (flag != 0)
      Console.Write("Yes");

    // Otherwise, print "No"
    else
      Console.Write("No");
  }

  // Driver Code
  public static void Main(string[] args)
  {

    int[, ] M = { { 1, 2, 3, 13 },
                 { 5, 3, 7, 8 },
                 { 1, 2, 3, 4 },
                 { 5, 6, 7, 7 } };
    int N = M.GetLength(0);

    // Function Call
    checkElementsOnDiagonal(M, N);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores if a number is prime or not
var prime = Array(1000005).fill(true);

// Function to generate and store
// primes using Sieve Of Eratosthenes
function SieveOfEratosthenes(N)
{
    // Set all numbers as prime

    prime[0] = false;
    prime[1] = false;

    for (var p = 2; p * p <= N; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Set all its multiples
            // as non-prime
            for (var i = p * p;
                 i <= N; i += p)

                prime[i] = false;
        }
    }
}

// Function to check if all diagonal
// elements are prime or not
function checkElementsOnDiagonal( M, N)
{
    // Stores if all diagonal
    // elements are prime or not
    var flag = 1;

    // Precompute primes
    SieveOfEratosthenes(1000000);

    // Traverse the range [0, N-1]
    for (var i = 0; i < N; i++) {

        // Check if numbers on the cross
        // diagonal and main diagonal
        // are primes or not
        flag &= (prime[M[i][i]]
                 && prime[M[i][N - 1 - i]]);
    }

    // If true, then print "Yes"
    if (flag)
        document.write( "Yes" );

    // Otherwise, print "No"
    else
        document.write( "No");
}

// Driver Code
var M = [
    [ 1, 2, 3, 13 ],
    [ 5, 3, 7, 8 ],
    [ 1, 2, 3, 4 ],
    [ 5, 6, 7, 7 ]
];
var N = M.length;

// Function Call
checkElementsOnDiagonal(M, N);

// This code is contributed by noob2000.
</script>
```

**Output**

```
No
```

***时间复杂度:**O(N * log(log N))*
***辅助空间:** O(N)*