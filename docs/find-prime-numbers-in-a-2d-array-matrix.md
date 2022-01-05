# 在 2D 阵列(矩阵)中寻找素数

> 原文:[https://www . geesforgeks . org/find-质数-in-a-2d-array-matrix/](https://www.geeksforgeeks.org/find-prime-numbers-in-a-2d-array-matrix/)

给定一个 2d 数组 **mat[][]** ，任务是查找并打印 [**质数**](https://www.geeksforgeeks.org/prime-numbers/) 以及它们在这个 2d 数组中的**位置**(基于 1 的索引)。

**示例:**

> **输入:** mat[][] = {{1，2}，{2，1}}
> 
> **输出:**
> 
> 1 2 2
> 
> 2 1 2
> 
> **说明:**第一个质数在第 1 行第 2 列的位置，数值为 2
> 
> 第二个质数位于第 2 行和第 1 列的位置，值为 2
> 
> **输入:** mat[][] = {{1，1}，{1，1}}
> 
> **输出:** -1
> 
> **说明:**这个 2d 数组中没有质数

**天真法:**基本思路是遍历 2d 数组，对于每个数，检查是否是素数。如果是质数，打印每个找到的质数的位置和值。
**时间复杂度:** O(NM*sqrt(X))，其中 N*M 是矩阵的大小，X 是矩阵中最大的元素
**辅助空间:** O(1)

**高效方法:**我们可以使用筛子高效地检查数字是否是质数。然后遍历 2d 数组，简单地检查这个数是否在 O(1)中是质数。

按照以下步骤实施此方法:

*   从矩阵中找到[最大元素，并将其存储在变量**最大值**中。](https://www.geeksforgeeks.org/program-to-find-the-maximum-element-in-a-matrix/)
*   现在使用埃拉托斯特尼 的 [**筛子找到从 **1 到 maxNum** 的质数，并将结果存储在数组**质数[]** 中。**](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   现在遍历矩阵，使用**素数[]** 数组检查每个数是否是素数。
*   对于矩阵中的每个质数，打印其位置(行、列)和值。

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

#define MAXN 100001
bool prime[MAXN];

// Function to find prime numbers using sieve
void SieveOfEratosthenes()
{
    int n = MAXN - 1;

    // Create a boolean array
    // "prime[0..n]" and initialize
    // all entries it as true.
    // A value in prime[i] will
    // finally be false if i is
    // Not a prime, else true.
    memset(prime, true, sizeof(prime));
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
            // Update all multiples
            // of p greater than or
            // equal to the square of it
            // numbers which are multiple
            // of p and are less than p^2
            // are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to print the position and
// value of the primes in given matrix
void printPrimes(vector<vector<int> >& arr, int n)
{
    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // Check if the element is prime
            // or not in O(1)
            if (prime[arr[i][j]] == true) {
                // Print the position and value
                // if found true
                cout << i + 1 << " " << j + 1 << " "
                     << arr[i][j] << endl;
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 2;
    vector<vector<int> > arr;
    vector<int> temp(N, 2);
    temp[0] = 1;
    temp[1] = 2;
    arr.push_back(temp);
    temp[0] = 2;
    temp[1] = 1;
    arr.push_back(temp);

    // Precomputing prime numbers using sieve
    SieveOfEratosthenes();

    // Find and print prime numbers
    // present in the matrix
    printPrimes(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    static int MAXN = 100001;
    static boolean prime[] = new boolean[MAXN];

    // Function to find prime numbers using sieve
    static void SieveOfEratosthenes()
    {
        int n = MAXN - 1;
        Arrays.fill(prime, true);

        // Create a boolean array
        // "prime[0..n]" and initialize
        // all entries it as true.
        // A value in prime[i] will
        // finally be false if i is
        // Not a prime, else true.
        prime[0] = false;
        prime[1] = false;

        for (int p = 2; p * p <= n; p++) {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {
                // Update all multiples
                // of p greater than or
                // equal to the square of it
                // numbers which are multiple
                // of p and are less than p^2
                // are already been marked.
                for (int i = p * p; i <= n; i = i + p)
                    prime[i] = false;
            }
        }
    }

    // Function to print the position and
    // value of the primes in given matrix
    static void printPrimes(int[][] arr, int n)
    {
        // Traverse the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // Check if the element is prime
                // or not in O(1)
                if (prime[arr[i][j]] == true) {
                    // Print the position and value
                    // if found true
                    System.out.print((i + 1));
                    System.out.print(" ");
                    System.out.print(j + 1);
                    System.out.print(" ");
                    System.out.print(arr[i][j]);
                    System.out.println();
                }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;
        int arr[][] = new int[N][N];

        arr[0][0] = 1;
        arr[0][1] = 2;
        arr[1][0] = 2;
        arr[1][1] = 1;

        // Precomputing prime numbers using sieve
        SieveOfEratosthenes();

        // Find and print prime numbers
        // present in the matrix
        printPrimes(arr, N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python code to implement the above approach
import math
MAXN = 100001
prime = [True for _ in range(MAXN)]

# Function to find prime numbers using sieve
def SieveOfEratosthenes():
    global prime

    n = MAXN - 1

    # Create a boolean array
    # "prime[0..n]" and initialize
    # all entries it as true.
    # A value in prime[i] will
    # finally be false if i is
    # Not a prime, else true.
    prime[0] = False
    prime[1] = False

    for p in range(2, int(math.sqrt(n)) + 1):

                # If prime[p] is not changed,
                # then it is a prime
        if (prime[p] == True):

           # Update all multiples
           # of p greater than or
           # equal to the square of it
           # numbers which are multiple
           # of p and are less than p^2
           # are already been marked.
            for i in range(p*p, n+1, p):
                prime[i] = False

# Function to print the position and
# value of the primes in given matrix
def printPrimes(arr, n):

        # Traverse the matrix
    for i in range(0, n):
        for j in range(0, n):

                        # Check if the element is prime
                        # or not in O(1)
            if (prime[arr[i][j]] == True):

                # Print the position and value
                # if found true
                print(f"{i + 1} {j + 1} {arr[i][j]}")

# Driver Code
if __name__ == "__main__":

    N = 2
    arr = []
    temp = [2 for _ in range(N)]

    temp[0] = 1
    temp[1] = 2
    arr.append(temp.copy())
    temp[0] = 2
    temp[1] = 1
    arr.append(temp.copy())

    # Precomputing prime numbers using sieve
    SieveOfEratosthenes()

    # Find and print prime numbers
    # present in the matrix
    printPrimes(arr, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    static int MAXN = 100001;
    static bool[] prime = new bool[MAXN];

    // Function to find prime numbers using sieve
    static void SieveOfEratosthenes()
    {
        int n = MAXN - 1;
        Array.Fill(prime, true);

        // Create a boolean array
        // "prime[0..n]" and initialize
        // all entries it as true.
        // A value in prime[i] will
        // finally be false if i is
        // Not a prime, else true.
        prime[0] = false;
        prime[1] = false;

        for (int p = 2; p * p <= n; p++) {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {
                // Update all multiples
                // of p greater than or
                // equal to the square of it
                // numbers which are multiple
                // of p and are less than p^2
                // are already been marked.
                for (int i = p * p; i <= n; i = i + p)
                    prime[i] = false;
            }
        }
    }

    // Function to print the position and
    // value of the primes in given matrix
    static void printPrimes(int[,] arr, int n)
    {
        // Traverse the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // Check if the element is prime
                // or not in O(1)
                if (prime[arr[i,j]] == true) {
                    // Print the position and value
                    // if found true
                    Console.Write((i + 1));
                    Console.Write(" ");
                    Console.Write(j + 1);
                    Console.Write(" ");
                    Console.Write(arr[i,j]);
                    Console.WriteLine();
                }
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 2;
        int[,] arr = new int[N,N];

        arr[0,0] = 1;
        arr[0,1] = 2;
        arr[1,0] = 2;
        arr[1,1] = 1;

        // Precomputing prime numbers using sieve
        SieveOfEratosthenes();

        // Find and print prime numbers
        // present in the matrix
        printPrimes(arr, N);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       let MAXN = 100001
       let prime = new Array(MAXN).fill(true);

       // Function to find prime numbers using sieve
       function SieveOfEratosthenes() {
           let n = MAXN - 1;

           // Create a boolean array
           // "prime[0..n]" and initialize
           // all entries it as true.
           // A value in prime[i] will
           // finally be false if i is
           // Not a prime, else true.

           prime[0] = false;
           prime[1] = false;

           for (let p = 2; p * p <= n; p++) {
               // If prime[p] is not changed,
               // then it is a prime
               if (prime[p] == true) {
                   // Update all multiples
                   // of p greater than or
                   // equal to the square of it
                   // numbers which are multiple
                   // of p and are less than p^2
                   // are already been marked.
                   for (let i = p * p; i <= n; i = i + p)
                       prime[i] = false;
               }
           }
       }

       // Function to print the position and
       // value of the primes in given matrix
       function printPrimes(arr, n) {
           // Traverse the matrix
           for (let i = 0; i < n; i++) {
               for (let j = 0; j < n; j++) {

                   // Check if the element is prime
                   // or not in O(1)
                   if (prime[arr[i][j]] == true) {
                       // Print the position and value
                       // if found true
                       document.write((i + 1) + " " + (j + 1) + " "
                           + (arr[i][j]) + "<br>");
                   }
               }
           }
       }

       // Driver Code

       let N = 2;
       let arr = new Array(N);
       let temp = [1, 2]
       arr[0] = temp;
       let temp1 = [2, 1]
       arr[1] = temp1;

       // Precomputing prime numbers using sieve
       SieveOfEratosthenes();

       // Find and print prime numbers
       // present in the matrix
       printPrimes(arr, N);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
1 2 2
2 1 2
```

**时间复杂度:** O(N*M)，其中 N*M 为矩阵的大小。
**辅助空间:** O(maxNum)其中 maxNum 是矩阵中最大的元素。