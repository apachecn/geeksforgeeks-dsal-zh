# 寻找`N!`中任意数字`P`的幂

> 原文：[https://www.geeksforgeeks.org/finding-powers-of-any-number-p-in-n/](https://www.geeksforgeeks.org/finding-powers-of-any-number-p-in-n/)

前提条件：[打印所有质数及其幂](http://Print all prime factors and their powers)

给定自然数`N`和`P`，任务是在`N!`的因数中找到`P`的幂。

**示例**：

> **输入**：`N = 4, P = 2`
> **输出**：3
> **说明**：
> `4 != 24`的素因数中的 2 的幂是 3
> **输入**：`N = 24, P = 4`
> **输出**：11

**朴素的方法**：这个想法是为从 1 到`N`的每个数字找到`P`的幂，并在相乘幂时将它们相加。

**时间复杂度**：`O(N * P)`

**有效方法**：

求`N!`中`P`的幂，执行以下操作：

1.  通过使用[本文章中讨论的方法](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)，找到所有`P`的[素因数](http://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)及其频率。 将[素因子](http://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)及其频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

2.  在`N!`的因式分解中找到`P`的每个质因数的幂，[通过使用本文中讨论的方法](http://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。

3.  将上述步骤中获得的每个幂除以[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中的相应频率。

4.  将上述步骤的结果存储在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，这些元素中的最小值将提供`N!`的分解的`P`的幂。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the power
// of P in N!
#include <bits/stdc++.h>
using namespace std;

// Map to store all the prime
// factors of P
unordered_map<int, int> Map;

// Function to find the prime
// factors of N im Map
void findPrimeFactors(int N)
{
    int i;

    // Clear map
    Map.clear();

    // Check for factors of 2
    while (N % 2 == 0) {
        Map[2] += 1;
        N /= 2;
    }

    // Find all the prime factors
    for (i = 3; i <= sqrt(N); i += 2) {

        // If i is a factors
        // then increase the
        // frequency of i
        while (N % i == 0) {
            Map[i] += 1;
            N /= i;
        }
    }

    if (N > 2) {
        Map[N] += 1;
    }
}

// Function to find the power
// of prime number P in N!
int PowInFactN(int N, int P)
{
    int ans = 0;
    int temp = P;

    // Loop until temp <= N
    while (temp <= N) {

        // Add the number of
        // numbers divisible
        // by N
        ans += N / temp;

        // Each time multiply
        // temp by P
        temp = temp * P;
    }

    // Returns ans
    return ans;
}

// Function that find the
// powers of any P in N!
int findPowers(int N, int P)
{

    // Find all prime factors
    // of number P
    findPrimeFactors(P);

    // To store the powers of
    // all prime factors
    vector<int> Powers;

    // Traverse the map
    for (auto& it : Map) {

        // Prime factor and
        // corres. powers
        int primeFac = it.first;
        int facPow = it.second;

        // Find power of prime
        // factor primeFac
        int p = PowInFactN(N,
                           primeFac);

        // Divide frequency by
        // facPow
        p /= facPow;

        // Store the power of
        // primeFac^facPow
        Powers.push_back(p);
    }

    // Return the minimum
    // element in Power array
    return *min_element(Powers.begin(),
                        Powers.end());
}

// Driver's Code
int main()
{
    int N = 24, P = 4;

    // Function to find power of
    // P in N!
    cout << findPowers(N, P);
    return 0;
}

```

## Java

```java

// Java program to find the power
// of P in N!
import java.util.*;

class GFG{

// Map to store all the prime
// factors of P
static HashMap<Integer,Integer> Map = new HashMap<Integer,Integer>();

// Function to find the prime
// factors of N im Map
static void findPrimeFactors(int N)
{
    int i;

    // Clear map
    Map.clear();

    // Check for factors of 2
    while (N % 2 == 0) {
        if(Map.containsKey(2))
            Map.put(2, Map.get(2) + 1);
        else
            Map.put(2, 1);
        N /= 2;
    }

    // Find all the prime factors
    for (i = 3; i <= Math.sqrt(N); i += 2) {

        // If i is a factors
        // then increase the
        // frequency of i
        while (N % i == 0) {
            if(Map.containsKey(i))
                Map.put(i, Map.get(i) + 1);
            else
                Map.put(i, 1);
            N /= i;
        }
    }

    if (N > 2) {
        if(Map.containsKey(N))
            Map.put(N, Map.get(N) + 1);
        else
            Map.put(N, 1);
    }
}

// Function to find the power
// of prime number P in N!
static int PowInFactN(int N, int P)
{
    int ans = 0;
    int temp = P;

    // Loop until temp <= N
    while (temp <= N) {

        // Add the number of
        // numbers divisible
        // by N
        ans += N / temp;

        // Each time multiply
        // temp by P
        temp = temp * P;
    }

    // Returns ans
    return ans;
}

// Function that find the
// powers of any P in N!
static int findPowers(int N, int P)
{

    // Find all prime factors
    // of number P
    findPrimeFactors(P);

    // To store the powers of
    // all prime factors
    Vector<Integer> Powers = new Vector<Integer>();

    // Traverse the map
    for (Map.Entry<Integer, Integer> it : Map.entrySet()) {

        // Prime factor and
        // corres. powers
        int primeFac = it.getKey();
        int facPow = it.getValue();

        // Find power of prime
        // factor primeFac
        int p = PowInFactN(N,
                           primeFac);

        // Divide frequency by
        // facPow
        p /= facPow;

        // Store the power of
        // primeFac^facPow
        Powers.add(p);
    }

    // Return the minimum
    // element in Power array
    return Collections.min(Powers);
}

// Driver's Code
public static void main(String[] args)
{
    int N = 24, P = 4;

    // Function to find power of
    // P in N!
    System.out.print(findPowers(N, P));
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program to find the power 
# of P in N! 
import math

# Map to store all 
# the prime factors of P 
Map = {} 

# Function to find the prime 
# factors of N im Map 
def findPrimeFactors(N): 

    # Clear map 
    Map.clear() 

    # Check for factors of 2 
    while (N % 2 == 0):
        if 2 in Map:
            Map[2] += 1
        else:
            Map[2] = 1
        N = N // 2

    # Find all the prime factors 
    for i in range(3, int(math.sqrt(N)) + 1, 2):

        # If i is a factors 
        # then increase the 
        # frequency of i 
        while (N % i == 0):
            if i in Map:
                Map[i] += 1
            else:
                Map[i] = 1

            N = N // i

    if (N > 2):
        if N in Map:
            Map[N] += 1
        else:
            Map[N] = 1

# Function to find the power 
# of prime number P in N! 
def PowInFactN(N, P): 

    ans = 0
    temp = P 

    # Loop until temp <= N 
    while (temp <= N): 

        # Add the number of 
        # numbers divisible 
        # by N 
        ans = ans + (N // temp) 

        # Each time multiply 
        # temp by P 
        temp = temp * P 

    # Returns ans 
    return ans

# Function that find the 
# powers of any P in N! 
def findPowers(N, P): 

    # Find all prime factors 
    # of number P 
    findPrimeFactors(P) 

    # To store the powers of 
    # all prime factors 
    Powers = []

    # Traverse the map 
    for it1, it2 in Map.items(): 

        # Prime factor and 
        # corres. powers 
        primeFac = it1
        facPow = it2 

        # Find power of prime 
        # factor primeFac 
        p = PowInFactN(N, primeFac) 

        # Divide frequency by 
        # facPow 
        p = p // facPow 

        # Store the power of 
        # primeFac^facPow 
        Powers.append(p)

    # Return the minimum 
    # element in Power array 
    return min(Powers)

N, P = 24, 4

# Driver code
if __name__ == "__main__":

  # Function to find 
  # power of P in N! 
  print(findPowers(N, P))

# This code is contriibuted by divyeshrabadiya07

```

## C#

```cs

// C# program to find the power
// of P in N!
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Map to store all the prime
// factors of P
static Dictionary<int,int> Map = new Dictionary<int,int>();

// Function to find the prime
// factors of N im Map
static void findPrimeFactors(int N)
{
    int i;

    // Clear map
    Map.Clear();

    // Check for factors of 2
    while (N % 2 == 0) {
        if(Map.ContainsKey(2))
            Map[2] = Map[2] + 1;
        else
            Map.Add(2, 1);
        N /= 2;
    }

    // Find all the prime factors
    for (i = 3; i <= Math.Sqrt(N); i += 2) {

        // If i is a factors
        // then increase the
        // frequency of i
        while (N % i == 0) {
            if(Map.ContainsKey(i))
                Map[i] = Map[i] + 1;
            else
                Map.Add(i, 1);
            N /= i;
        }
    }

    if (N > 2) {
        if(Map.ContainsKey(N))
            Map[N] =Map[N] + 1;
        else
            Map.Add(N, 1);
    }
}

// Function to find the power
// of prime number P in N!
static int PowInFactN(int N, int P)
{
    int ans = 0;
    int temp = P;

    // Loop until temp <= N
    while (temp <= N) {

        // Add the number of
        // numbers divisible
        // by N
        ans += N / temp;

        // Each time multiply
        // temp by P
        temp = temp * P;
    }

    // Returns ans
    return ans;
}

// Function that find the
// powers of any P in N!
static int findPowers(int N, int P)
{

    // Find all prime factors
    // of number P
    findPrimeFactors(P);

    // To store the powers of
    // all prime factors
    List<int> Powers = new List<int>();

    // Traverse the map
    foreach (KeyValuePair<int, int> it in Map) {

        // Prime factor and
        // corres. powers
        int primeFac = it.Key;
        int facPow = it.Value;

        // Find power of prime
        // factor primeFac
        int p = PowInFactN(N,
                        primeFac);

        // Divide frequency by
        // facPow
        p /= facPow;

        // Store the power of
        // primeFac^facPow
        Powers.Add(p);
    }

    // Return the minimum
    // element in Power array
    return Powers.Min();
}

// Driver's Code
public static void Main(String[] args)
{
    int N = 24, P = 4;

    // Function to find power of
    // P in N!
    Console.Write(findPowers(N, P));
}
}

// This code is contributed by sapnasingh4991

```

**Output:** 

```
11

```

**时间复杂度**：`O(sqrt(P) * log(P, N))`



* * *

* * *



