# 找出两个其和可以表示为 N 的斐波那契数

> 原文:[https://www . geesforgeks . org/find-two-Fibonacci-numbers-其和可以表示为-n/](https://www.geeksforgeeks.org/find-two-fibonacci-numbers-whose-sum-can-be-represented-as-n/)

给定一个偶数 **N** ，任务是找到两个斐波那契数，它们的和可以表示为 **N** 。可能有几种可能的组合。只打印第一对这样的。如果没有解决方案，则打印 **-1** 。
**举例:**

> **输入:** N = 90
> **输出:** 1，89
> **说明:**
> 第一对和等于 90 的为{1，89}
> **输入:** N = 74
> **输出:** -1

**方法:**思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，然后在 O(1)时间内检查一对是否为斐波那契值。
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find two
// Fibonacci numbers whose
// sum can be represented as N

#include <bits/stdc++.h>
using namespace std;

// Function to create hash table
// to check Fibonacci numbers
void createHash(set<int>& hash,
                int maxElement)
{

    // Storing the first two numbers
    // in the hash
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {
        int temp = curr + prev;
        hash.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the Fibonacci pair
// with the given sum
void findFibonacciPair(int n)
{
    // creating a set containing
    // all fibonacci numbers
    set<int> hash;
    createHash(hash, n);

    // Traversing all numbers
    // to find first pair
    for (int i = 0; i < n; i++) {

        // If both i and (N - i) are Fibonacci
        if (hash.find(i) != hash.end()
            && hash.find(n - i) != hash.end()) {

            // Printing the pair because
            // i + (N - i) = N
            cout << i << ", "
                 << (n - i) << endl;
            return;
        }
    }

    // If no fibonacci pair is found
    // whose sum is equal to n
    cout << "-1\n";
}

// Driven code
int main()
{
    int N = 90;

    findFibonacciPair(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find two
// Fibonacci numbers whose
// sum can be represented as N
import java.util.*;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<Integer> hash,
                int maxElement)
{

    // Storing the first two numbers
    // in the hash
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {
        int temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the Fibonacci pair
// with the given sum
static void findFibonacciPair(int n)
{
    // creating a set containing
    // all fibonacci numbers
    HashSet<Integer> hash = new HashSet<Integer>();
    createHash(hash, n);

    // Traversing all numbers
    // to find first pair
    for (int i = 0; i < n; i++) {

        // If both i and (N - i) are Fibonacci
        if (hash.contains(i)
            && hash.contains(n - i)) {

            // Printing the pair because
            // i + (N - i) = N
            System.out.print(i+ ", "
                + (n - i) +"\n");
            return;
        }
    }

    // If no fibonacci pair is found
    // whose sum is equal to n
    System.out.print("-1\n");
}

// Driven code
public static void main(String[] args)
{
    int N = 90;

    findFibonacciPair(N);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3  program to find two
# Fibonacci numbers whose
# sum can be represented as N

# Function to create hash table
# to check Fibonacci numbers
def createHash(hash1,maxElement):

    # Storing the first two numbers
    # in the hash
    prev , curr = 0 , 1
    hash1.add(prev)
    hash1.add(curr)

    # Finding Fibonacci numbers up to N
    # and storing them in the hash
    while (curr < maxElement):
        temp = curr + prev
        hash1.add(temp)
        prev = curr
        curr = temp

# Function to find the Fibonacci pair
# with the given sum
def findFibonacciPair( n):

    # creating a set containing
    # all fibonacci numbers
    hash1 = set()
    createHash(hash1, n)

    # Traversing all numbers
    # to find first pair
    for i in range(n):

        # If both i and (N - i) are Fibonacci
        if (i in hash1 and (n - i) in hash1):

            # Printing the pair because
            # i + (N - i) = N
            print(i , ", ", (n - i))
            return

    # If no fibonacci pair is found
    # whose sum is equal to n
    print("-1")

# Driven code
if __name__ == "__main__":
    N = 90
    findFibonacciPair(N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find two
// Fibonacci numbers whose
// sum can be represented as N
using System;
using System.Collections.Generic;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<int> hash,
                int maxElement)
{

    // Storing the first two numbers
    // in the hash
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {
        int temp = curr + prev;
        hash.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the Fibonacci pair
// with the given sum
static void findFibonacciPair(int n)
{
    // creating a set containing
    // all fibonacci numbers
    HashSet<int> hash = new HashSet<int>();
    createHash(hash, n);

    // Traversing all numbers
    // to find first pair
    for (int i = 0; i < n; i++) {

        // If both i and (N - i) are Fibonacci
        if (hash.Contains(i)
            && hash.Contains(n - i)) {

            // Printing the pair because
            // i + (N - i) = N
            Console.Write(i+ ", "
                + (n - i) +"\n");
            return;
        }
    }

    // If no fibonacci pair is found
    // whose sum is equal to n
    Console.Write("-1\n");
}

// Driven code
public static void Main(String[] args)
{
    int N = 90;

    findFibonacciPair(N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find two
// Fibonacci numbers whose
// sum can be represented as N

// Function to create hash table
// to check Fibonacci numbers
function createHash(hash, maxElement)
{

    // Storing the first two numbers
    // in the hash
    let prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {
        let temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the Fibonacci pair
// with the given sum
function findFibonacciPair(n)
{
    // creating a set containing
    // all fibonacci numbers
    let hash = new Set();
    createHash(hash, n);

    // Traversing all numbers
    // to find first pair
    for (let i = 0; i < n; i++) {

        // If both i and (N - i) are Fibonacci
        if (hash.has(i)
            && hash.has(n - i)) {

            // Printing the pair because
            // i + (N - i) = N
            document.write(i+ ", "
                + (n - i) + "<br/>");
            return;
        }
    }

    // If no fibonacci pair is found
    // whose sum is equal to n
    document.write("-1" + "<br/>");
}

// Driver code

      let N = 90;

    findFibonacciPair(N);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
1, 89
```

***时间复杂度:** O(N)*

***辅助空间:** O(N)*