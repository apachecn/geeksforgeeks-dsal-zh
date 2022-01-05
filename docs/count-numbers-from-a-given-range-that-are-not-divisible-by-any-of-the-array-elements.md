# 计算给定范围内不能被任何数组元素整除的数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-给定范围内不能被任何数组元素整除的数字/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-that-are-not-divisible-by-any-of-the-array-elements/)

给定一个由 **N** 正整数和 **L** 和 **R** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出**【L，R】**范围内不能被任何数组元素整除的数字的个数。

**示例:**

> **输入:** arr[] = {2，3，4，5，6}，L = 1，R = 20
> **输出:** 6
> **解释:**
> 范围内不能被任何数组元素整除的 6 个数字是 1，7，11，13，17 和 19。
> 
> **输入:** arr[] = {1，2，3}，L = 75，R = 1000000
> **输出:** 0
> **解释:**
> 由于所有的数字都可以被 1 整除，所以，答案是 0。

**天真方法:**简单的方法是[迭代给定范围内的所有数字](https://www.geeksforgeeks.org/iterating-arraylists-java/)**【L，R】****，对于每个数字，检查它是否可以被任何数组元素整除。如果它不能被任何数组元素整除，则增加计数。检查所有数字后，打印计数。**

*****时间复杂度:**O((R–L+1)* N)*
***辅助空间:** O(N)***

****高效方法:**上述方法可以通过使用厄拉多塞的[筛进行优化，标记一个数的所有倍数并将其存储在高效的数据结构中，比如](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) [Set](https://www.geeksforgeeks.org/set-in-cpp-stl/) ，它提供了几乎恒定时间的查找操作。按照以下步骤解决问题:**

*   **首先，对于每个数组元素，说**arr【I】**，使用厄拉多塞的[筛，将其所有小于 **R** 的倍数存储在](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。**
*   **在范围**【1，R】**中不能被给定数组中的任何数字整除的整数数量将等于**(R–集合的大小)**。就这样吧 **A** 。**
*   **同样，找出范围**【1，L】**中不能被给定数组中任何数字整除的数字。让它成为 **B** 。**
*   **完成上述步骤后，打印**(A–B)**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the non-multiples
// till k
int findNonMultiples(int arr[],
                     int n, int k)
{
    // Stores all unique multiples
    set<int> multiples;

    // Iterate the array
    for (int i = 0; i < n; ++i) {

        // For finding duplicates
        // only once
        if (multiples.find(arr[i])
            == multiples.end()) {

            // Inserting all multiples
            // into the set
            for (int j = 1;
                 j <= k / arr[i]; j++) {
                multiples.insert(arr[i] * j);
            }
        }
    }

    // Returning only the count of
    // numbers that are not divisible
    // by any of the array elements
    return k - multiples.size();
}

// Function to count the total values
// in the range [L, R]
int countValues(int arr[], int N,
                int L, int R)
{
    // Count all values in the range
    // using exclusion principle
    return findNonMultiples(arr, N, R)
           - findNonMultiples(arr, N, L - 1);
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int L = 1, R = 20;

    // Function Call
    cout << countValues(arr, N, L, R);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the non-multiples
// till k
public static int findNonMultiples(int[] arr, int n,
                                   int k)
{

    // Stores all unique multiples
    Set<Integer> multiples = new HashSet<Integer>();

    // Iterate the array
    for(int i = 0; i < n; ++i)
    {

        // For finding duplicates
        // only once
        if (!multiples.contains(arr[i]))
        {

            // Inserting all multiples
            // into the set
            for(int j = 1; j <= k / arr[i]; j++)
            {
                multiples.add(arr[i] * j);
            }
        }
    }

    // Returning only the count of
    // numbers that are not divisible
    // by any of the array elements
    return k - multiples.size();
}

// Function to count the total values
// in the range [L, R]
public static int countValues(int[] arr, int N,
                              int L, int R)
{

    // Count all values in the range
    // using exclusion principle
    return findNonMultiples(arr, N, R) -
           findNonMultiples(arr, N, L - 1);
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 4, 5, 6 };
    int N = arr.length;
    int L = 1;
    int R = 20;

    // Function Call
    System.out.println(countValues(arr, N, L, R));
}
}

// This code is contributed by rohitsingh07052
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the non-multiples
# till k
def findNonMultiples(arr, n, k):

    # Stores all unique multiples
    multiples = set([])

    # Iterate the array
    for i in range(n):

        # For finding duplicates
        # only once
        if (arr[i] not in multiples):

            # Inserting all multiples
            # into the set
            for j in range(1, k // arr[i] + 1):
                multiples.add(arr[i] * j)

    # Returning only the count of
    # numbers that are not divisible
    # by any of the array elements
    return k - len(multiples)

# Function to count the total values
# in the range [L, R]
def countValues(arr, N, L, R):

    # Count all values in the range
    # using exclusion principle
    return (findNonMultiples(arr, N, R) -
            findNonMultiples(arr, N, L - 1))

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 3, 4, 5, 6 ]
    N = len(arr)
    L = 1
    R = 20

    # Function Call
    print( countValues(arr, N, L, R))

# This code is contributed by chitranayal
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to find the non-multiples
// till k
public static int findNonMultiples(int[] arr, int n,
                                   int k)
{

    // Stores all unique multiples
    HashSet<int> multiples = new HashSet<int>();

    // Iterate the array
    for(int i = 0; i < n; ++i)
    {

        // For finding duplicates
        // only once
        if (!multiples.Contains(arr[i]))
        {

            // Inserting all multiples
            // into the set
            for(int j = 1; j <= k / arr[i]; j++)
            {
                multiples.Add(arr[i] * j);
            }
        }
    }

    // Returning only the count of
    // numbers that are not divisible
    // by any of the array elements
    return k - multiples.Count;
}

// Function to count the total values
// in the range [L, R]
public static int countValues(int[] arr, int N,
                              int L, int R)
{

    // Count all values in the range
    // using exclusion principle
    return findNonMultiples(arr, N, R) -
           findNonMultiples(arr, N, L - 1);
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 2, 3, 4, 5, 6 };
    int N = arr.Length;
    int L = 1;
    int R = 20;

    // Function Call
    Console.WriteLine(countValues(arr, N, L, R));
}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to find the non-multiples
// till k
function findNonMultiples(arr, n, k)
{
    // Stores all unique multiples
    let multiples = new Set();

    // Iterate the array
    for (let i = 0; i < n; ++i) {

        // For finding duplicates
        // only once
        if (!multiples.has(arr[i])) {

            // Inserting all multiples
            // into the set
            for (let j = 1;
                j <= k / arr[i]; j++) {
                multiples.add(arr[i] * j);
            }
        }
    }

    // Returning only the count of
    // numbers that are not divisible
    // by any of the array elements

    return k - multiples.size;
}

// Function to count the total values
// in the range [L, R]
function countValues(arr, N, L, R)
{
    // Count all values in the range
    // using exclusion principle
    return findNonMultiples(arr, N, R)
        - findNonMultiples(arr, N, L - 1);
}

// Driver Code

    let arr = [ 2, 3, 4, 5, 6 ];
    let N = arr.length;
    let L = 1, R = 20;

    // Function Call
    document.write(countValues(arr, N, L, R));

 // This code is contributed by _saurabh_jaiswal

 </script>
```

****Output:** 

```
6
```** 

*****时间复杂度:**O(N * log(log N))*
***辅助空间:** O(N)***