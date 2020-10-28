# 大小为 3 的 GP（几何级数）子序列的数量

> 原文：[https://www.geeksforgeeks.org/number-gp-geometric-progression-subsequences-size-3/](https://www.geeksforgeeks.org/number-gp-geometric-progression-subsequences-size-3/)

给定 n 个元素和一个比率 r，求 G.P. 子序列的长度为 3。子序列被视为 GP，长度为 3，比率为 r。

**范例**：

```
Input : arr[] = {1, 1, 2, 2, 4}
            r = 2
Output : 4 
Explanation: Any of the two 1s can be chosen 
as the first element, the second element can 
be any of the two 2s, and the third element 
of the subsequence must be equal to 4.

Input : arr[] = {1, 1, 2, 2, 4}
            r = 3
Output : 0

```

**天真的方法**是使用三个嵌套的 for 循环，并检查每个长度为 3 的子序列，并保留这些子序列的计数。 复杂度为 O（n <sup>3</sup> ）。

**有效方法**是要解决进度的固定中间元素的问题。 这意味着如果将元素 a [i]固定为中间，则它必须是 r 的倍数，并且必须存在 a [i] / r 和 a [i] * r。 我们计算 a [i] / r 和 a [i] * r 的出现次数，然后将其相乘。 为此，我们可以使用哈希的概念，将所有可能元素的计数存储在两个哈希图中，一个表示左侧的元素数量，另一个表示右侧的元素数量。

下面是上述方法的实现

## C++

```cpp

// C++ program to count GP subsequences of size 3.
#include <bits/stdc++.h>
using namespace std;

// Returns count of G.P. subseqeunces
// with length 3 and common ratio r
long long subsequences(int a[], int n, int r)
{
    // hashing to maintain left and right array
    // elements to the main count
    unordered_map<int, int> left, right;

    // stores the answer
    long long ans = 0;

    // traverse through the elements
    for (int i = 0; i < n; i++)
        right[a[i]]++; // keep the count in the hash

    // traverse through all elements
    // and find out the number of elements as k1*k2
    for (int i = 0; i < n; i++) {

        // keep the count of left and right elements
        // left is a[i]/r and right a[i]*r
        long long c1 = 0, c2 = 0;

        // if the current element is divisible by k,
        // count elements in left hash.
        if (a[i] % r == 0)
            c1 = left[a[i] / r];

        // decrease the count in right hash
        right[a[i]]--;

        // number of right elements 
        c2 = right[a[i] * r];

        // calculate the answer
        ans += c1 * c2;

        left[a[i]]++; // left count of a[i]
    }

    // returns answer
    return ans;
}

// driver program 
int main()
{
    int a[] = { 1, 2, 6, 2, 3, 6, 9, 18, 3, 9 };
    int n = sizeof(a) / sizeof(a[0]);
    int r = 3;
    cout << subsequences(a, n, r);
    return 0;
}

```

## Java

```java

// Java program to count GP subsequences
// of size 3\. 
import java.util.*;
import java.lang.*;

class GFG{

// Returns count of G.P. subseqeunces 
// with length 3 and common ratio r 
static long subsequences(int a[], int n, int r) 
{ 

    // Hashing to maintain left and right array 
    // elements to the main count 
    Map<Integer, Integer> left = new HashMap<>(),
                         right = new HashMap<>(); 

    // Stores the answer 
    long ans = 0; 

    // Traverse through the elements 
    for(int i = 0; i < n; i++) 

        // Keep the count in the hash 
        right.put(a[i],
        right.getOrDefault(a[i], 0) + 1); 

    // Traverse through all elements 
    // and find out the number of 
    // elements as k1*k2 
    for(int i = 0; i < n; i++)
    { 

        // Keep the count of left and right 
        // elements left is a[i]/r and 
        // right a[i]*r 
        long c1 = 0, c2 = 0; 

        // If the current element is divisible 
        // by k, count elements in left hash. 
        if (a[i] % r == 0) 
            c1 = left.getOrDefault(a[i] / r, 0); 

        // Decrease the count in right hash 
        right.put(a[i],
        right.getOrDefault(a[i], 0) - 1); 

        // Number of right elements 
        c2 = right.getOrDefault(a[i] * r, 0); 

        // Calculate the answer 
        ans += c1 * c2; 

        // left count of a[i] 
        left.put(a[i],
        left.getOrDefault(a[i], 0) + 1); 
    } 

    // Returns answer 
    return ans; 
}

// Driver Code
public static void main (String[] args)
{
    int a[] = { 1, 2, 6, 2, 3, 
                6, 9, 18, 3, 9 }; 
    int n = a.length; 
    int r = 3; 

    System.out.println(subsequences(a, n, r)); 
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program to count GP subsequences 
# of size 3\. 
from collections import defaultdict

# Returns count of G.P. subseqeunces 
# with length 3 and common ratio r 
def subsequences(a, n, r): 

    # hashing to maintain left and right
    # array elements to the main count 
    left = defaultdict(lambda:0)
    right = defaultdict(lambda:0)

    # stores the answer 
    ans = 0

    # traverse through the elements 
    for i in range(0, n): 
        right[a[i]] += 1 # keep the count in the hash 

    # traverse through all elements and 
    # find out the number of elements as k1*k2 
    for i in range(0, n): 

        # keep the count of left and right elements 
        # left is a[i]/r and right a[i]*r 
        c1, c2 = 0, 0

        # if the current element is divisible 
        # by k, count elements in left hash. 
        if a[i] % r == 0: 
            c1 = left[a[i] // r] 

        # decrease the count in right hash 
        right[a[i]] -= 1

        # number of right elements 
        c2 = right[a[i] * r] 

        # calculate the answer 
        ans += c1 * c2 

        left[a[i]] += 1 # left count of a[i] 

    return ans 

# Driver Code
if __name__ == "__main__": 

    a = [1, 2, 6, 2, 3, 6, 9, 18, 3, 9] 
    n = len(a) 
    r = 3
    print(subsequences(a, n, r)) 

# This code is contributed by 
# Rituraj Jain

```

## C#

```cs

// C# program to count GP subsequences
// of size 3\. 
using System;
using System.Collections.Generic;

class GFG{

// Returns count of G.P. subseqeunces 
// with length 3 and common ratio r 
static long subsequences(int []a, int n, int r) 
{ 

    // Hashing to maintain left and right array 
    // elements to the main count 
    Dictionary<int, int> left = new Dictionary<int, int>(),
                        right = new Dictionary<int, int>(); 

    // Stores the answer 
    long ans = -1; 

    // Traverse through the elements 
    for(int i = 0; i < n; i++) 

        // Keep the count in the hash 
        if (right.ContainsKey(a[i]))
            right[a[i]] = right[a[i]] + 1; 
        else
            right.Add(a[i], 1);

    // Traverse through all elements 
    // and find out the number of 
    // elements as k1*k2 
    for(int i = 0; i < n; i++)
    { 

        // Keep the count of left and right 
        // elements left is a[i]/r and 
        // right a[i]*r 
        long c1 = 0, c2 = 0; 

        // If the current element is divisible 
        // by k, count elements in left hash. 
        if (a[i] % r == 0) 
            if (left.ContainsKey(a[i] / r))
                c1 =  right[a[i] / r]; 
        else

            c1 =  0; 

        // Decrease the count in right hash
        if (right.ContainsKey(a[i]))
            right[a[i]] = right[a[i]]; 
        else
            right.Add(a[i], -1);

        // Number of right elements 
        if (right.ContainsKey(a[i] * r))
            c2 = right[a[i] * r]; 
        else
            c2 = 0;

        // Calculate the answer 
        ans += (c1 * c2); 

        // left count of a[i] 
        if (left.ContainsKey(a[i]))
            left[a[i]] = 0; 
        else
            left.Add(a[i], 1);
    } 

    // Returns answer 
    return ans - 1; 
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 1, 2, 6, 2, 3, 
                6, 9, 18, 3, 9 }; 
    int n = a.Length; 
    int r = 3; 

    Console.WriteLine(subsequences(a, n, r)); 
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
6

```

**时间复杂度**：O（n）

**上述解决方案不适用于 r 为 1 的情况**：例如，对于 input = {1,1,1,1， 1}，GP 有 10 种可能 可以通过使用 <sup>5</sup> C <sub>3</sub> 计算出长度 3 的子序列。 在 r = 1 的所有情况下都应实施这样的过程。下面是处理此问题的修改代码。

## C++

```cpp

// C++ program to count GP subsequences of size 3.
#include <bits/stdc++.h>
using namespace std;

// to calculate nCr
// DP approach
int binomialCoeff(int n, int k) {
  int C[k + 1];
  memset(C, 0, sizeof(C));
  C[0] = 1; // nC0 is 1
  for (int i = 1; i <= n; i++) {

    // Compute next row of pascal triangle using
    // the previous row
    for (int j = min(i, k); j > 0; j--)
      C[j] = C[j] + C[j - 1];
  }
  return C[k];
}

// Returns count of G.P. subseqeunces
// with length 3 and common ratio r
long long subsequences(int a[], int n, int r)
{
    // hashing to maintain left and right array
    // elements to the main count
    unordered_map<int, int> left, right;

    // stores the answer
    long long ans = 0;

    // traverse through the elements
    for (int i = 0; i < n; i++)
        right[a[i]]++; // keep the count in the hash

    // IF RATIO IS ONE
    if (r == 1){

        // traverse the count in hash
        for (auto i : right) {

             // calculating nC3, where 'n' is
             // the number of times each number is
             // repeated in the input
             ans += binomialCoeff(i.second, 3);
        }

        return ans;
    }

    // traverse through all elements
    // and find out the number of elements as k1*k2
    for (int i = 0; i < n; i++) {

        // keep the count of left and right elements
        // left is a[i]/r and right a[i]*r
        long long c1 = 0, c2 = 0;

        // if the current element is divisible by k,
        // count elements in left hash.
        if (a[i] % r == 0)
            c1 = left[a[i] / r];

        // decrease the count in right hash
        right[a[i]]--;

        // number of right elements 
        c2 = right[a[i] * r];

        // calculate the answer
        ans += c1 * c2;

        left[a[i]]++; // left count of a[i]
    }

    // returns answer
    return ans;
}

// driver program 
int main()
{
    int a[] = { 1, 2, 6, 2, 3, 6, 9, 18, 3, 9 };
    int n = sizeof(a) / sizeof(a[0]);
    int r = 3;
    cout << subsequences(a, n, r);
    return 0;
}

```

## Python3

```py

# Python3 program to count 
# GP subsequences of size 3.
from collections import defaultdict

# To calculate nCr
# DP approach
def binomialCoeff(n, k):

  C = [0] * (k + 1)

  # nC0 is 1
  C[0] = 1 

  for  i in range (1, n + 1):

    # Compute next row of pascal 
    # triangle using the previous row
    for j in range (min(i, k), -1, -1):
      C[j] = C[j] + C[j - 1]
  return C[k]

# Returns count of G.P. subseqeunces
# with length 3 and common ratio r
def subsequences(a, n, r):

    # hashing to maintain left
    # and right array elements 
    # to the main count
    left = defaultdict (int)
    right = defaultdict (int)

    # Stores the answer
    ans = 0

    # Traverse through 
    # the elements
    for i in range (n):

        # Keep the count 
        # in the hash
        right[a[i]] += 1

    # IF RATIO IS ONE
    if (r == 1):

        # Traverse the count 
        # in hash
        for  i in right:

             # calculating nC3, where 'n' is
             # the number of times each number is
             # repeated in the input
             ans += binomialCoeff(right[i], 3)

        return ans

    # traverse through all elements
    # and find out the number 
    # of elements as k1*k2
    for i in range (n):

        # Keep the count of left 
        # and right elements left 
        # is a[i]/r and right a[i]*r
        c1 = 0
        c2 = 0;

        # if the current element 
        # is divisible by k, count 
        # elements in left hash.
        if (a[i] % r == 0):
            c1 = left[a[i] // r]

        # Decrease the count 
        # in right hash
        right[a[i]] -= 1

        # Number of right elements 
        c2 = right[a[i] * r]

        # Calculate the answer
        ans += c1 * c2

        # left count of a[i]
        left[a[i]] += 1

    # returns answer
    return ans

# Driver code
if __name__ == "__main__":

    a = [1, 2, 6, 2, 3, 
         6, 9, 18, 3, 9]
    n = len(a) 
    r = 3
    print ( subsequences(a, n, r))

# This code is contributed by Chitranayal

```

**Output:** 

```
6

```



* * *

* * *



