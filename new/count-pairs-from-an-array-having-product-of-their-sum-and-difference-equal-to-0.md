# 来自其和与差之积等于 0 的数组的计数对

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，任务是计算可能的成对数组元素**（arr [i]，arr [j ]）**，使得**（arr [i] + arr [j]）*（arr [i] – arr [j]）**为 **0** 。

**示例**：

> **输入**：arr [] = {2，-2，1，1}
> **输出**：2
> **说明**：
> （arr [0] + arr [1]）*（arr [0] – arr [1]）= 0
> （arr [3] + arr [4]）*（arr [3] – arr [4]）= 0
> 
> **输入**：arr [] = {5，9，-9，-9}
> **输出**：3

**方法**：可以看出，方程**（arr [i] + arr [j]）*（arr [i] – arr [j]）= 0** 可简化为 **arr [i] <sup>2</sup> = arr [j] <sup>2</sup>** 。 因此，任务减少到对具有[绝对值](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)相等的对进行计数。 请按照以下步骤解决问题：

*   初始化数组 **hash []** ，以存储每个数组元素的绝对值的频率。

*   通过为每个数组不同的绝对值相加**（hash [x] *（hash [x] – 1））/ 2 2** ，计算对数。

下面是上述方法的实现：

## C++ 14

```

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define MAXN 100005

// Function to count required
// number of pairs
int countPairs(int arr[], int N)
{
    // Stores count of pairs
    int desiredPairs = 0;

    // Initialize hash with 0
    int hash[MAXN] = { 0 };

    // Count frequency of each element
    for (int i = 0; i < N; i++) {
        hash[abs(arr[i])]++;
    }

    // Calculate desired number of pairs
    for (int i = 0; i < MAXN; i++) {
        desiredPairs
            += ((hash[i]) * (hash[i] - 1)) / 2;
    }

    // Print desired pairs
    cout << desiredPairs;
}

// Driver Code
int main()
{
    // Given arr[]
    int arr[] = { 2, -2, 1, 1 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, N);

    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.io.*;
import java.util.Arrays; 

class GFG{

static int MAXN = 100005;

// Function to count required
// number of pairs
static void countPairs(int arr[], int N)
{

    // Stores count of pairs
    int desiredPairs = 0;

    // Initialize hash with 0
    int hash[] = new int[MAXN];
    Arrays.fill(hash, 0);

    // Count frequency of each element
    for(int i = 0; i < N; i++) 
    {
        hash[Math.abs(arr[i])]++;
    }

    // Calculate desired number of pairs
    for(int i = 0; i < MAXN; i++)
    {
        desiredPairs += ((hash[i]) * 
                         (hash[i] - 1)) / 2;
    }

    // Print desired pairs
    System.out.print(desiredPairs);
}   

// Driver Code
public static void main (String[] args) 
{

    // Given arr[]
    int arr[] = { 2, -2, 1, 1 };

    // Size of the array
    int N = arr.length;

    // Function call
    countPairs(arr, N);
}
}

// This code is contributed by code_hunt

```

## Python3

```py

# Python3 program for 
# the above approach
MAXN = 100005

# Function to count required
# number of pairs
def countPairs(arr, N):

    # Stores count of pairs
    desiredPairs = 0

    # Initialize hash with 0
    hash = [0] * MAXN

    # Count frequency of 
    # each element
    for i in range(N):
        hash[abs(arr[i])] += 1

    # Calculate desired number 
    # of pairs
    for i in range(MAXN):
        desiredPairs += ((hash[i]) *
                         (hash[i] - 1)) // 2

    # Print desired pairs
    print (desiredPairs)

# Driver Code
if __name__ == "__main__":

    # Given arr[]
    arr = [2, -2, 1, 1]

    # Size of the array
    N = len(arr)

    # Function Call
    countPairs(arr, N)

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the above approach
using System;

class GFG{

static int MAXN = 100005;

// Function to count required
// number of pairs
static void countPairs(int []arr, int N)
{

    // Stores count of pairs
    int desiredPairs = 0;

    // Initialize hash with 0
    int []hash = new int[MAXN];

    // Count frequency of each element
    for(int i = 0; i < N; i++) 
    {
        hash[Math.Abs(arr[i])]++;
    }

    // Calculate desired number of pairs
    for(int i = 0; i < MAXN; i++)
    {
        desiredPairs += ((hash[i]) * 
                         (hash[i] - 1)) / 2;
    }

    // Print desired pairs
    Console.Write(desiredPairs);
}   

// Driver Code
public static void Main(String[] args) 
{

    // Given []arr
    int []arr = { 2, -2, 1, 1 };

    // Size of the array
    int N = arr.Length;

    // Function call
    countPairs(arr, N);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
2

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*



* * *

* * *



