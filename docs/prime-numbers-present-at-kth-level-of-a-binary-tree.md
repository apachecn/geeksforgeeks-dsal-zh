# 二叉树第 k 层出现的素数

> 原文:[https://www . geeksforgeeks . org/素数-二进制树的第 k 层出现/](https://www.geeksforgeeks.org/prime-numbers-present-at-kth-level-of-a-binary-tree/)

给定一个数字 **K** ，任务是打印在该级别出现的[素数](https://www.geeksforgeeks.org/prime-numbers/)，给定所有素数都以[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)的形式表示。

**示例:**

```
Input: K = 3
        2
       / \
      3   5
     /\  / \
    7 11 13 17
Output :7, 11, 13, 17
Explanation:
        2
       / \
      3   5
     /\  / \
    7 11 13 17
So primes present at level 3 : 7, 11, 13, 17

Input :K = 2
        2
       / \
      3   5
Output :3 5
```

**天真方法:**天真方法是构建一个素数的二叉树，然后获取特定级别 k 的元素。
对于大数来说效果不好，因为花费的时间太多。

**高效的方法:**假设有 n 个元素，任务是使用这 n 个元素构建一个二叉树，然后可以使用 log <sub>2</sub> n 个级别来构建它们。
因此，给定一个 k 级，如果所有质数都出现在一个 1D 数组中，这里出现的元素是从 2 <sup>k-1</sup> 到 2 <sup>k</sup> -1。

因此，以下是算法:

1.  使用厄拉多塞的[筛找出最大尺寸的质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2.  计算该级别的左指数和右指数为左指数= 2 <sup>k-1</sup> ，右指数= 2<sup>k</sup>1。
3.  从素数数组的左索引到右索引输出素数。

## C++

```
// CPP program of the approach
#include <bits/stdc++.h>
using namespace std;

// initializing the max value
#define MAX_SIZE 1000005

// To store all prime numbers
vector<int> primes;

// Function to generate N prime numbers using
// Sieve of Eratosthenes
void SieveOfEratosthenes(vector<int>& primes)
{
    // Create a boolean array "IsPrime[0..MAX_SIZE]" and
    // initialize all entries it as true. A value in
    // IsPrime[i] will finally be false if i is
    // Not a IsPrime, else true.
    bool IsPrime[MAX_SIZE];
    memset(IsPrime, true, sizeof(IsPrime));

    for (int p = 2; p * p < MAX_SIZE; p++) {
        // If IsPrime[p] is not changed, then it is a prime
        if (IsPrime[p] == true) {
            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            primes.push_back(p);
}

void printLevel(int level)
{

    cout << "primes at level " << level << ": ";
    int left_index = pow(2, level - 1);
    int right_index = pow(2, level) - 1;
    for (int i = left_index; i <= right_index; i++) {

        cout << primes[i - 1] << " ";
    }
    cout << endl;
}

// Driver Code
int main()
{
    // Function call
    SieveOfEratosthenes(primes);

    printLevel(1);
    printLevel(2);
    printLevel(3);
    printLevel(4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the approach
import java.util.*;

class GFG
{

    // initializing the max value
    static final int MAX_SIZE = 1000005;

    // To store all prime numbers
    static Vector<Integer> primes = new Vector<Integer>();

    // Function to generate N prime numbers using
    // Sieve of Eratosthenes
    static void SieveOfEratosthenes(Vector<Integer> primes)
    {

        // Create a boolean array "IsPrime[0..MAX_SIZE]" and
        // initialize all entries it as true. A value in
        // IsPrime[i] will finally be false if i is
        // Not a IsPrime, else true.
        boolean[] IsPrime = new boolean[MAX_SIZE];
        for (int i = 0; i < MAX_SIZE; i++)
            IsPrime[i] = true;

        for (int p = 2; p * p < MAX_SIZE; p++)
        {

            // If IsPrime[p] is not changed, then it is a prime
            if (IsPrime[p] == true)
            {

                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (int i = p * p; i < MAX_SIZE; i += p)
                    IsPrime[i] = false;
            }
        }

        // Store all prime numbers
        for (int p = 2; p < MAX_SIZE; p++)
            if (IsPrime[p])
                primes.add(p);
    }

    static void printLevel(int level)
    {

        System.out.print("primes at level " + level + ": ");
        int left_index = (int) Math.pow(2, level - 1);
        int right_index = (int) (Math.pow(2, level) - 1);
        for (int i = left_index; i <= right_index; i++)
        {

            System.out.print(primes.get(i - 1) + " ");
        }
        System.out.println();
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Function call
        SieveOfEratosthenes(primes);

        printLevel(1);
        printLevel(2);
        printLevel(3);
        printLevel(4);

    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program of the approach
MAX_SIZE = 1000005
primes = []

# Function to generate N prime numbers using
# Sieve of Eratosthenes
def SieveOfEratosthenes():

    # Create a boolean array "IsPrime[0..MAX_SIZE]" and
    # initialize all entries it as True. A value in
    # IsPrime[i] will finally be false if i is
    # Not a IsPrime, else True.
    IsPrime = [True] * MAX_SIZE
    p = 2

    while p * p < MAX_SIZE:

        # If IsPrime[p] is not changed, then it is a prime
        if (IsPrime[p] == True):

            # Update all multiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(p * p, MAX_SIZE, p):
                IsPrime[i] = False
        p += 1

    # Store all prime numbers
    for p in range(2, MAX_SIZE):
        if (IsPrime[p]):
            primes.append(p)

def printLevel(level):

    print("primes at level ", level, ":", end=" ")
    left_index = pow(2, level - 1)
    right_index = pow(2, level) - 1
    for i in range(left_index, right_index + 1):

        print(primes[i - 1], end=" ")
    print()

# Driver Code

# Function call
SieveOfEratosthenes()

printLevel(1)
printLevel(2)
printLevel(3)
printLevel(4)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // initializing the max value
    static readonly int MAX_SIZE = 1000005;

    // To store all prime numbers
    static List<int> primes = new List<int>();

    // Function to generate N prime numbers using
    // Sieve of Eratosthenes
    static void SieveOfEratosthenes(List<int> primes)
    {

        // Create a bool array "IsPrime[0..MAX_SIZE]" and
        // initialize all entries it as true. A value in
        // IsPrime[i] will finally be false if i is
        // Not a IsPrime, else true.
        bool[] IsPrime = new bool[MAX_SIZE];
        for (int i = 0; i < MAX_SIZE; i++)
            IsPrime[i] = true;

        for (int p = 2; p * p < MAX_SIZE; p++)
        {

            // If IsPrime[p] is not changed, then it is a prime
            if (IsPrime[p] == true)
            {

                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (int i = p * p; i < MAX_SIZE; i += p)
                    IsPrime[i] = false;
            }
        }

        // Store all prime numbers
        for (int p = 2; p < MAX_SIZE; p++)
            if (IsPrime[p])
                primes.Add(p);
    }

    static void printLevel(int level)
    {

        Console.Write("primes at level " + level + ": ");
        int left_index = (int) Math.Pow(2, level - 1);
        int right_index = (int) (Math.Pow(2, level) - 1);
        for (int i = left_index; i <= right_index; i++)
        {

            Console.Write(primes[i - 1] + " ");
        }
        Console.WriteLine();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Function call
        SieveOfEratosthenes(primes);

        printLevel(1);
        printLevel(2);
        printLevel(3);
        printLevel(4);

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program of the approach

// Initializing the max value
let MAX_SIZE = 1000005

// To store all prime numbers
let primes = new Array();

// Function to generate N prime numbers using
// Sieve of Eratosthenes
function SieveOfEratosthenes(primes)
{

    // Create a boolean array "IsPrime[0..MAX_SIZE]" and
    // initialize all entries it as true. A value in
    // IsPrime[i] will finally be false if i is
    // Not a IsPrime, else true.
    let IsPrime = new Array(MAX_SIZE).fill(true);

    for(let p = 2; p * p < MAX_SIZE; p++)
    {

        // If IsPrime[p] is not changed,
        // then it is a prime
        if (IsPrime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for(let i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all prime numbers
    for(let p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            primes.push(p);
}

function printLevel(level)
{
    document.write("primes at level " +
                   level + ": ");
    let left_index = Math.pow(2, level - 1);
    let right_index = Math.pow(2, level) - 1;

    for(let i = left_index; i <= right_index; i++)
    {
        document.write(primes[i - 1] + " ");
    }
    document.write("<br>");
}

// Driver Code

// Function call
SieveOfEratosthenes(primes);

printLevel(1);
printLevel(2);
printLevel(3);
printLevel(4);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
primes at level 1: 2 
primes at level 2: 3 5 
primes at level 3: 7 11 13 17 
primes at level 4: 19 23 29 31 37 41 43 47 
```