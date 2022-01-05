# 将数组划分为最小数量的由单个不同值组成的等长子集

> 原文:[https://www . geeksforgeeks . org/partition-array-in-minimum-number-of-single-distinct-value/](https://www.geeksforgeeks.org/partition-array-into-minimum-number-of-equal-length-subsets-consisting-of-a-single-distinct-value/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是打印最小计数的等长[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)数组可以被划分成这样，每个子集只包含一个不同的元素

**示例:**

> **输入:** arr[] = { 1，2，3，4，4，3，2，1 }
> **输出:** 4
> **解释:**
> 数组的可能分区为{ {1，1 }、{2，2}、{3，3}、{4，4} }。
> 因此，要求输出为 4。
> 
> **输入:** arr[] = { 1，1，1，2，2，3，3 }
> **输出:** 8
> **解释:**
> 数组的可能分区为{ {1}、{1}、{1}、{2}、{2}、{2}、{3}、{3} }。
> 因此，要求的输出是 8。

**天真方法:**解决问题最简单的方法是[存储每个不同数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率，使用变量 **i** 迭代范围**【N，1】**，检查数组中所有不同元素的频率是否可以被 **i** 整除。如果发现为真，则打印**(不适用)**的值。

***时间复杂度:** O(N <sup>2</sup> )。*
***辅助空间:** O(N)*

**高效方法:**优化上述方法的思路是使用 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 的概念。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如**频率**，来存储数组中每个不同元素的频率。
*   初始化一个变量，比如说**频率 GCD** ，来存储数组中每个不同元素的频率的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)找到**频率**的值。
*   最后打印 **(N) % FreqGCD** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of subsets
// by partitioning the array with given conditions
int CntOfSubsetsByPartitioning(int arr[], int N)
{
    // Store frequency of each
    // distinct element of the array
    unordered_map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        freq[arr[i]]++;
    }

    // Stores GCD of frequency of
    // each distinct element of the array
    int freqGCD = 0;
    for (auto i : freq) {

        // Update freqGCD
        freqGCD = __gcd(freqGCD, i.second);
    }

    return (N) / freqGCD;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 4, 3, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << CntOfSubsetsByPartitioning(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the minimum count of subsets
// by partitioning the array with given conditions
static int CntOfSubsetsByPartitioning(int arr[], int N)
{
    // Store frequency of each
    // distinct element of the array
    HashMap<Integer,Integer> freq = new HashMap<>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        if(freq.containsKey(arr[i])){
            freq.put(arr[i], freq.get(arr[i])+1);
        }
        else{
            freq.put(arr[i], 1);
        }
    }

    // Stores GCD of frequency of
    // each distinct element of the array
    int freqGCD = 0;
    for (Map.Entry<Integer,Integer> i : freq.entrySet()) {

        // Update freqGCD
        freqGCD = __gcd(freqGCD, i.getValue());
    }

    return (N) / freqGCD;
}

// Recursive function to return gcd of a and b 
static int __gcd(int a, int b) 
{ 
 return b == 0? a:__gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 4, 3, 2, 1 };
    int N = arr.length;
    System.out.print(CntOfSubsetsByPartitioning(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import gcd

# Function to find the minimum count
# of subsets by partitioning the array
# with given conditions
def CntOfSubsetsByPartitioning(arr, N):

    # Store frequency of each
    # distinct element of the array
    freq = {}

    # Traverse the array
    for i in range(N):

        # Update frequency
        # of arr[i]
        freq[arr[i]] = freq.get(arr[i], 0) + 1

    # Stores GCD of frequency of
    # each distinct element of the array
    freqGCD = 0

    for i in freq:

        # Update freqGCD
        freqGCD = gcd(freqGCD, freq[i])

    return (N) // freqGCD

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 4, 3, 2, 1 ]
    N = len(arr)

    print(CntOfSubsetsByPartitioning(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum count of subsets
// by partitioning the array with given conditions
static int CntOfSubsetsByPartitioning(int []arr, int N)
{
    // Store frequency of each
    // distinct element of the array
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        if(freq.ContainsKey(arr[i])){
            freq[arr[i]] = freq[arr[i]]+1;
        }
        else{
            freq.Add(arr[i], 1);
        }
    }

    // Stores GCD of frequency of
    // each distinct element of the array
    int freqGCD = 0;
    foreach (KeyValuePair<int,int> i in freq) {

        // Update freqGCD
        freqGCD = __gcd(freqGCD, i.Value);
    }

    return (N) / freqGCD;
}

// Recursive function to return gcd of a and b 
static int __gcd(int a, int b) 
{ 
 return b == 0? a:__gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 4, 3, 2, 1 };
    int N = arr.Length;
    Console.Write(CntOfSubsetsByPartitioning(arr, N));
}
}

 // This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the minimum count of subsets
// by partitioning the array with given conditions
function CntOfSubsetsByPartitioning(arr, N)
{
    // Store frequency of each
    // distinct element of the array
    var freq = {};

    // Traverse the array
    for(var i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        if (freq.hasOwnProperty(arr[i]))
        {
            freq[arr[i]] = freq[arr[i]] + 1;
        }
        else
        {
            freq[arr[i]] = 1;
        }
    }

    // Stores GCD of frequency of
    // each distinct element of the array
    var freqGCD = 0;
    for(const [key, value] of Object.entries(freq))
    {

        // Update freqGCD
        freqGCD = __gcd(freqGCD, value);
    }
    return parseInt(N / freqGCD);
}

// Recursive function to return gcd of a and b
function __gcd(a, b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Driver Code
var arr = [ 1, 2, 3, 4, 4, 3, 2, 1 ];
var N = arr.length;

document.write(CntOfSubsetsByPartitioning(arr, N));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log(M))，其中 M 是数组中最小的元素*
***辅助空间:** O(N)*