# 在给定的树的普鲁弗序列中打印具有素数度的节点

> 原文:[https://www . geesforgeks . org/print-the-nodes-with-prime-degree-in-给定-prufer-sequence-of-a-tree/](https://www.geeksforgeeks.org/print-the-nodes-with-a-prime-degree-in-given-prufer-sequence-of-a-tree/)

给定一个树的 [Prufer 序列](https://www.geeksforgeeks.org/prufer-code-tree-creation/)，任务是打印该树中具有素数度的节点。
**例:**

```
Input: arr[] = {4, 1, 3, 4} 
Output: 1 3 4
Explanation:
The tree is:
2----4----3----1----5
     |
     6 
Hence, the degree of 1, 3 and 4
are 2, 2 and 3 respectively
which are prime.

Input: a[] = {1, 2, 2} 
Output: 1 2
```

**进场:**

1.  因为如果 **N** 是节点数，那么 prufer 序列的长度是**N–2**。因此，创建一个比普鲁弗序列长度大 2 倍的数组**度[]** 。
2.  最初，用 **1** 填充度数数组。
3.  迭代普鲁弗序列，增加每个元素在度表中的出现频率。这种方法之所以有效，是因为普鲁弗序列中一个节点的频率比树中的度数少一个。
4.  此外，为了检查节点度是否为素数，我们将使用埃拉托斯特尼的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。创建一个筛子，它将帮助我们识别度在 O(1)时间内是否是质数。
5.  如果一个节点有质数，则打印节点号。

以下是上述方法的实现:

## C++

```
// C++ implementation to print the
// nodes with prime degree from the
// given prufer sequence

#include <bits/stdc++.h>

using namespace std;

// Function to create Sieve
// to check primes
void SieveOfEratosthenes(
       bool prime[], int p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= p_size;
                                      i += p)
                prime[i] = false;
        }
    }
}

// Function to print the nodes with
// prime degree in the tree
// whose Prufer sequence is given
void PrimeDegreeNodes(int prufer[], int n)
{
    int nodes = n + 2;

    bool prime[nodes + 1];
    memset(prime, true, sizeof(prime));

    SieveOfEratosthenes(prime, nodes + 1);

    // Hash-table to mark the
    // degree of every node
    int degree[n + 2 + 1];

    // Initially let all the degrees be 1
    for (int i = 1; i <= nodes; i++)
        degree[i] = 1;

    // Increase the count of the degree
    for (int i = 0; i < n; i++)
        degree[prufer[i]]++;

    // Print the nodes with prime degree
    for (int i = 1; i <= nodes; i++) {
        if (prime[degree[i]]) {
            cout << i << " ";
        }
    }
}

// Driver Code
int main()
{
    int a[] = { 4, 1, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    PrimeDegreeNodes(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the
// nodes with prime degree from the
// given prufer sequence

import java.util.*;

class GFG{

// Function to create Sieve
// to check primes
static void SieveOfEratosthenes(
       boolean prime[], int p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= p_size;
                                      i += p)
                prime[i] = false;
        }
    }
}

// Function to print the nodes with
// prime degree in the tree
// whose Prufer sequence is given
static void PrimeDegreeNodes(int prufer[], int n)
{
    int nodes = n + 2;

    boolean []prime = new boolean[nodes + 1];
    Arrays.fill(prime, true);

    SieveOfEratosthenes(prime, nodes + 1);

    // Hash-table to mark the
    // degree of every node
    int []degree = new int[n + 2 + 1];

    // Initially let all the degrees be 1
    for (int i = 1; i <= nodes; i++)
        degree[i] = 1;

    // Increase the count of the degree
    for (int i = 0; i < n; i++)
        degree[prufer[i]]++;

    // Print the nodes with prime degree
    for (int i = 1; i <= nodes; i++) {
        if (prime[degree[i]]) {
            System.out.print(i+ " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 4, 1, 3, 4 };
    int n = a.length;

    PrimeDegreeNodes(a, n);

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to print the
# nodes with prime degree from the
# given prufer sequence

# Function to create Sieve
# to check primes
def SieveOfEratosthenes(prime, p_size):

    # False here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False
    p = 2
    while (p * p <= p_size):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, p_size + 1, p):
                prime[i] = False
        p += 1

# Function to print the nodes with
# prime degree in the tree
# whose Prufer sequence is given
def PrimeDegreeNodes(prufer, n):

    nodes = n + 2
    prime = [True] * (nodes + 1)
    SieveOfEratosthenes(prime, nodes + 1)

    # Hash-table to mark the
    # degree of every node
    degree = [0] * (n + 2 + 1);

    # Initially let all the degrees be 1
    for i in range(1, nodes + 1):
        degree[i] = 1;

    # Increase the count of the degree
    for i in range(0, n):
        degree[prufer[i]] += 1

    # Print the nodes with prime degree
    for i in range(1, nodes + 1):
        if prime[degree[i]]:
            print(i, end = ' ')

# Driver Code
if __name__=='__main__':

    a = [ 4, 1, 3, 4 ]
    n = len(a)

    PrimeDegreeNodes(a, n)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to print the
// nodes with prime degree from the
// given prufer sequence
using System;

class GFG{

// Function to create Sieve
// to check primes
static void SieveOfEratosthenes(bool []prime,
                                int p_size)
{

    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

       // If prime[p] is not changed,
       // then it is a prime
       if (prime[p])
       {

           // Update all multiples of p,
           // set them to non-prime
           for(int i = p * 2; i <= p_size;
                                    i += p)
              prime[i] = false;
        }
    }
}

// Function to print the nodes with
// prime degree in the tree
// whose Prufer sequence is given
static void PrimeDegreeNodes(int []prufer, int n)
{
    int nodes = n + 2;
    bool []prime = new bool[nodes + 1];

    for(int i = 0; i < prime.Length; i++)
       prime[i] = true;

    SieveOfEratosthenes(prime, nodes + 1);

    // Hash-table to mark the
    // degree of every node
    int []degree = new int[n + 2 + 1];

    // Initially let all the degrees be 1
    for(int i = 1; i <= nodes; i++)
       degree[i] = 1;

    // Increase the count of the degree
    for(int i = 0; i < n; i++)
       degree[prufer[i]]++;

    // Print the nodes with prime degree
    for(int i = 1; i <= nodes; i++)
    {
       if (prime[degree[i]])
       {
           Console.Write(i + " ");
       }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 4, 1, 3, 4 };
    int n = a.Length;

    PrimeDegreeNodes(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation to print the
// nodes with prime degree from the
// given prufer sequence

// Function to create Sieve
// to check primes
function SieveOfEratosthenes(prime, p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (let p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (let i = p * 2; i <= p_size;
                                    i += p)
                prime[i] = false;
        }
    }
}

// Function to print the nodes with
// prime degree in the tree
// whose Prufer sequence is given
function PrimeDegreeNodes(prufer, n)
{
    let nodes = n + 2;

    let prime = new Array(nodes + 1);
    prime.fill(true);

    SieveOfEratosthenes(prime, nodes + 1);

    // Hash-table to mark the
    // degree of every node
    let degree = new Array(n + 2 + 1);

    // Initially let all the degrees be 1
    for (let i = 1; i <= nodes; i++)
        degree[i] = 1;

    // Increase the count of the degree
    for (let i = 0; i < n; i++)
        degree[prufer[i]]++;

    // Print the nodes with prime degree
    for (let i = 1; i <= nodes; i++) {
        if (prime[degree[i]]) {
            document.write(i + " ");
        }
    }
}

// Driver Code

let a = [ 4, 1, 3, 4 ];
let n = a.length

PrimeDegreeNodes(a, n);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
1 3 4
```