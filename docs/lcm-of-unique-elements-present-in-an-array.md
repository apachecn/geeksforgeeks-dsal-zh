# 阵列中存在的独特元素的 LCM

> 原文:[https://www . geesforgeks . org/LCM-of-unique-elements-in-a-array/](https://www.geeksforgeeks.org/lcm-of-unique-elements-present-in-an-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到给定数组所有唯一元素的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。如果数组不包含任何唯一元素，则打印**-1**。

**示例:**

> **输入:** arr[] = {1，2，1，3，3，4}
> **输出:** 4
> **解释:**
> 给定数组的唯一元素是:2 和 4。因此，(2，4)的 LCM 为 4。
> 
> **输入:** arr[] = {1，1，2，2，3，3}
> **输出:** -1

**天真方法:**解决给定问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 为每个数组元素 **arr[i]** 并检查 **arr[i]** 是否唯一。如果发现是真的，那么把它存储在另一个数组中。遍历所有元素后，打印新创建的数组中存在的元素的 [LCM。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)

***时间复杂度:** O(N <sup>2</sup> + N * log(M))，其中 M 是数组* [*最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) ***arr[]** 。*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来寻找数组中的唯一元素来优化。按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 为 **1** 来存储数组唯一元素的 LCM。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将各元素的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   现在，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，如果任一元素的计数等于 **1** ，则将 **ans** 的值更新为 **ans** 和当前元素的 [LCM。](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)
*   完成以上步骤后，如果 **ans** 的值为 **1** ，则打印**-1”**。否则，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find GCD of two numbers
int findGCD(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Recursively find the GCD
    return findGCD(b, a % b);
}

// Function to find LCM of two numbers
int findLCM(int a, int b)
{
    return (a * b) / findGCD(a, b);
}

// Function to find LCM of unique elements
// present in the array
int uniqueElementsLCM(int arr[], int N)
{
    // Stores the frequency of each
    // number of the array
    unordered_map<int, int> freq;

    // Store the frequency of each
    // element of the array
    for (int i = 0; i < N; i++) {
        freq[arr[i]]++;
    }

    // Store the required result
    int lcm = 1;

    // Traverse the map freq
    for (auto i : freq) {

        // If the frequency of the
        // current element is 1, then
        // update ans
        if (i.second == 1) {
            lcm = findLCM(lcm, i.first);
        }
    }

    // If there is no unique element,
    // set lcm to -1
    if (lcm == 1)
        lcm = -1;

    // Print the result
    cout << lcm;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 3, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    uniqueElementsLCM(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
import java.util.Map.Entry;

class GFG{

// Function to find GCD of two numbers
static int findGCD(int a, int b)
{

    // Base Case
    if (b == 0)
        return a;

    // Recursively find the GCD
    return findGCD(b, a % b);
}

// Function to find LCM of two numbers
static int findLCM(int a, int b)
{
    return (a * b) / findGCD(a, b);
}

// Function to find LCM of unique elements
// present in the array
static void uniqueElementsLCM(int arr[], int N)
{

    // Stores the frequency of each
    // number of the array
    HashMap<Integer,
            Integer> freq = new HashMap<Integer,
                                        Integer>();

    // Store the frequency of each
    // element of the array
    for(int i = 0; i < N; i++)
    {
        freq.put(arr[i],
                 freq.getOrDefault(arr[i], 0) + 1);
    }

    // Store the required result
    int lcm = 1;

    // Traverse the map freq
    for(Entry<Integer, Integer> i : freq.entrySet())
    {

        // If the frequency of the
        // current element is 1, then
        // update ans
        if (i.getValue() == 1)
        {
            lcm = findLCM(lcm, i.getKey());
        }
    }

    // If there is no unique element,
    // set lcm to -1
    if (lcm == 1)
        lcm = -1;

    // Print the result
    System.out.print(lcm);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 1, 3, 3, 4 };
    int N = arr.length;

    // Function Call
    uniqueElementsLCM(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find GCD of two numbers
def findGCD(a, b):

    # Base Case
    if (b == 0):
        return a

    # Recursively find the GCD
    return findGCD(b, a % b)

# Function to find LCM of two numbers
def findLCM(a, b):

    return (a * b) // findGCD(a, b)

# Function to find LCM of unique elements
# present in the array
def uniqueElementsLCM(arr, N):

    # Stores the frequency of each
    # number of the array
    freq = defaultdict(int)

    # Store the frequency of each
    # element of the array
    for i in range(N):
        freq[arr[i]] += 1

    # Store the required result
    lcm = 1

    # Traverse the map freq
    for i in freq:

        # If the frequency of the
        # current element is 1, then
        # update ans
        if (freq[i] == 1):
            lcm = findLCM(lcm, i)

    # If there is no unique element,
    # set lcm to -1
    if (lcm == 1):
        lcm = -1

    # Print the result
    print(lcm)

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 1, 3, 3, 4 ]
    N = len(arr)

    # Function Call
    uniqueElementsLCM(arr, N)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

  // Function to find GCD of two numbers
static int findGCD(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Recursively find the GCD
    return findGCD(b, a % b);
}

// Function to find LCM of two numbers
static int findLCM(int a, int b)
{
    return (a * b) / findGCD(a, b);
}

// Function to find LCM of unique elements
// present in the array
static void uniqueElementsLCM(int []arr, int N)
{
    // Stores the frequency of each
    // number of the array
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Store the frequency of each
    // element of the array
    for (int i = 0; i < N; i++) {
        if(freq.ContainsKey(arr[i]))
          freq[arr[i]]++;
        else
            freq.Add(arr[i],1);
    }

    // Store the required result
    int lcm = 1;

    // Traverse the map freq
    foreach(KeyValuePair<int, int> kvp in freq) {

        // If the frequency of the
        // current element is 1, then
        // update ans
        if (kvp.Value == 1) {
            lcm = findLCM(lcm, kvp.Key);
        }
    }

    // If there is no unique element,
    // set lcm to -1
    if (lcm == 1)
        lcm = -1;

    // Print the result
    Console.Write(lcm);
}

// Driver Code
public static void Main()
{
    int []arr = {1, 2, 1, 3, 3, 4 };
    int N = arr.Length;

    // Function Call
    uniqueElementsLCM(arr, N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find GCD of two numbers
function findGCD(a, b)
{
    // Base Case
    if (b == 0)
        return a;

    // Recursively find the GCD
    return findGCD(b, a % b);
}

// Function to find LCM of two numbers
function findLCM(a, b)
{
    return (a * b) / findGCD(a, b);
}

// Function to find LCM of unique elements
// present in the array
function uniqueElementsLCM(arr, N)
{
    // Stores the frequency of each
    // number of the array
    var freq = new Map();

    // Store the frequency of each
    // element of the array
    for (var i = 0; i < N; i++) {

        if(freq.has(arr[i]))
        {
            freq.set(arr[i], freq.get(arr[i])+1);
        }
        else
        {
            freq.set(arr[i], 1);
        }
    }

    // Store the required result
    var lcm = 1;

    // Traverse the map freq
    freq.forEach((value, key) => {
        // If the frequency of the
        // current element is 1, then
        // update ans
        if (value == 1) {
            lcm = findLCM(lcm, key);
        }
    });

    // If there is no unique element,
    // set lcm to -1
    if (lcm == 1)
        lcm = -1;

    // Print the result
    document.write( lcm);
}

// Driver Code
var arr = [1, 2, 1, 3, 3, 4];
var N = arr.length;
// Function Call
uniqueElementsLCM(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log(M))，其中 M 是数组中最大的* [*元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)***arr[]***
***辅助空间:** O(N)*