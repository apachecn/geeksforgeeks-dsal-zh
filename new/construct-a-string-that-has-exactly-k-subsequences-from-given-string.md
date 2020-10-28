# 根据给定的字符串

构造一个具有完全 K 个子序列的字符串

给定字符串 **str** 和整数 **K** ，任务是找到字符串 **S** ，使其具有给定的 **K** 子序列 字符串 **str** 。

**范例**：

> **输入**：str =“ gfg”，K = 10
> **输出**：gggggffg
> **说明**：。
> 可能有 10 个子序列 给定字符串“ gggggffg”。 它们是：
> 1\. **g** gggg **f** f **g** 2\. [g **g** ggg **f [** f **g** 3\. [gg **g** gg **f** f **g**
> 4\. ggg **g** g **f** f **g** 5 [gggg **gf** f **g**
> 6\. **g** ggggf **fg** [
> 7\. g **g** gggf **fg**
> 8\. g ]
> 9\. ggg **g** gf **fg**
> 10\. ggggg **g** f **fg** 。
> **输入**：str =“代码”，K = 20
> **输出**：cccccoodde
> **说明**：
> 有 20 种可能 字符串“ cccccoodde”的子序列。

**方法**：

要解决上述问题，我们必须遵循以下步骤：

*   这个想法是找到 K 的[主要因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)并存储这些主要因子（例如 ***因素*** ）。

*   创建给定字符串大小的空数组 ***计数*** ，以将每个字符的计数存储在结果字符串 **s** 中。 用 1 初始化数组。

*   现在，从列表*中弹出元素*，并以循环的方式乘以数组的每个位置，直到列表为空。 最后，我们获得了数组中 str 每个字符的数量。

*   在数组 ***count []*** 中进行迭代，并将每个字符 **ch** 的字符数附加到结果字符串 **s** 中。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function that computes the string s
void printSubsequenceString(string str,
                            long long k)
{
    // Length of the given string str
    int n = str.size();
    int i;

    // List that stores all the prime
    // factors of given k
    vector<long long> factors;

    // Find the prime factors
    for (long long i = 2;
         i <= sqrt(k); i++) {

        while (k % i == 0) {
            factors.push_back(i);
            k /= i;
        }
    }
    if (k > 1)
        factors.push_back(k);

    // Initialize the count of each
    // character position as 1
    vector<long long> count(n, 1);

    int index = 0;

    // Loop until the list
    // becomes empty
    while (factors.size() > 0) {

        // Increase the character
        // count by multiplying it
        // with the prime factor
        count[index++] *= factors.back();
        factors.pop_back();

        // If we reach end then again
        // start from beginning
        if (index == n)
            index = 0;
    }

    // Store the output
    string s;

    for (i = 0; i < n; i++) {
        while (count[i]-- > 0) {
            s += str[i];
        }
    }

    // Print the string
    cout << s;
}

// Driver code
int main()
{
    // Given String
    string str = "code";

    long long k = 20;

    // Function Call
    printSubsequenceString(str, k);
    return 0;
}

```

## Java

```java

// Java program for the above approach 
import java.util.*;
class GFG{ 

// Function that computes the String s 
static void printSubsequenceString(String str, 
                                      int k) 
{ 
    // Length of the given String str 
    int n = str.length(); 
    int i; 

    // List that stores all the prime 
    // factors of given k 
    Vector<Integer> factors = new Vector<Integer>(); 

    // Find the prime factors 
    for (i = 2; i <= Math.sqrt(k); i++) 
    { 
        while (k % i == 0) 
        { 
            factors.add(i); 
            k /= i; 
        } 
    } 
    if (k > 1) 
        factors.add(k); 

    // Initialize the count of each 
    // character position as 1 
    int []count = new int[n]; 
    Arrays.fill(count, 1);
    int index = 0; 

    // Loop until the list 
    // becomes empty 
    while (factors.size() > 0) 
    { 

        // Increase the character 
        // count by multiplying it 
        // with the prime factor 
        count[index++] *= factors.get(factors.size() - 1); 
        factors.remove(factors.get(factors.size() - 1)); 

        // If we reach end then again 
        // start from beginning 
        if (index == n) 
            index = 0; 
    } 

    // Store the output 
    String s = ""; 

    for (i = 0; i < n; i++) 
    { 
        while (count[i]-- > 0) 
        { 
            s += str.charAt(i); 
        } 
    } 

    // Print the String 
    System.out.print(s); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Given String 
    String str = "code"; 

    int k = 20; 

    // Function Call 
    printSubsequenceString(str, k); 
}
} 

// This code is contributed by sapnasingh4991

```

## Python3

```py

# Python3 program for 
# the above approach
import math

# Function that computes 
# the string s
def printSubsequenceString(st, k):
    # Length of the given 
    # string str
    n = len(st)

    # List that stores 
    # all the prime
    # factors of given k
    factors = []

    # Find the prime factors
    sqt = (int(math.sqrt(k)))
    for i in range (2, sqt + 1):

        while (k % i == 0):
            factors.append(i)
            k //= i

    if (k > 1):
        factors.append(k)

    # Initialize the count of each
    # character position as 1
    count = [1] * n

    index = 0

    # Loop until the list
    # becomes empty
    while (len(factors) > 0):

        # Increase the character
        # count by multiplying it
        # with the prime factor
        count[index] *= factors[-1]
        factors.pop()
        index += 1

        # If we reach end then again
        # start from beginning
        if (index == n):
            index = 0

    # store output
    s = ""
    for i in range (n):
        while (count[i] > 0):
            s += st[i]
            count[i] -= 1 

    # Print the string
    print (s)

# Driver code
if __name__ == "__main__":

    # Given String
    st = "code"

    k = 20

    # Function Call
    printSubsequenceString(st, k)

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the above approach 
using System;
using System.Collections.Generic;

class GFG{ 

// Function that computes the String s 
static void printSubsequenceString(String str, 
                                      int k) 
{ 
    // Length of the given String str 
    int n = str.Length; 
    int i; 

    // List that stores all the prime 
    // factors of given k 
    List<int> factors = new List<int>(); 

    // Find the prime factors 
    for (i = 2; i <= Math.Sqrt(k); i++) 
    { 
        while (k % i == 0) 
        { 
            factors.Add(i); 
            k /= i; 
        } 
    } 
    if (k > 1) 
        factors.Add(k); 

    // Initialize the count of each 
    // character position as 1 
    int []count = new int[n]; 
    for (i = 0; i < n; i++) 
        count[i] = 1;
    int index = 0; 

    // Loop until the list 
    // becomes empty 
    while (factors.Count > 0) 
    { 

        // Increase the character 
        // count by multiplying it 
        // with the prime factor 
        count[index++] *= factors[factors.Count - 1]; 
        factors.Remove(factors[factors.Count - 1]); 

        // If we reach end then again 
        // start from beginning 
        if (index == n) 
            index = 0; 
    } 

    // Store the output 
    String s = ""; 

    for (i = 0; i < n; i++) 
    { 
        while (count[i]-- > 0) 
        { 
            s += str[i]; 
        } 
    } 

    // Print the String 
    Console.Write(s); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // Given String 
    String str = "code"; 

    int k = 20; 

    // Function Call 
    printSubsequenceString(str, k); 
}
} 

// This code is contributed by sapnasingh4991

```

**Output:** 

```
cccccoodde

```

**时间复杂度**：*O（N * log <sub>2</sub> （log <sub>2</sub> （N）））*

**辅助空间**：**O（K）**



* * *

* * *



