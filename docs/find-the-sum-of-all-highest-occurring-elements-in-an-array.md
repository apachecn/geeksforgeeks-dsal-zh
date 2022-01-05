# 求数组中所有最高出现元素的和

> 原文:[https://www . geeksforgeeks . org/find-所有出现次数最多的数组元素之和/](https://www.geeksforgeeks.org/find-the-sum-of-all-highest-occurring-elements-in-an-array/)

给定包含重复元素的整数数组。任务是找出给定数组中所有最高出现元素的总和。这是数组中频率最大的所有元素的总和。
**例** :

```
Input : arr[] = {1, 1, 2, 2, 2, 2, 3, 3, 3, 3}
Output : 20
The highest occurring elements are 3 and 2 and their
frequency is 4\. Therefore sum of all 3's and 2's in the 
array = 3+3+3+3+2+2+2+2 = 20.

Input : arr[] = {10, 20, 30, 40, 40}
Output : 80
```

**接近** :

*   遍历数组，用 C++中的[无序 _ map](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)存储数组元素的频率，这样 map 的键就是数组元素，值就是它在数组中的频率。
*   然后，遍历地图以找到最大出现元素的频率。
*   现在，为了找到总和，再次遍历地图，对于所有具有最大频率的元素，找到**frequency _ of _ max _ occuring _ element * max _ occuring _ element**，并找到它们的总和。

以下是上述方法的实现:

## C++

```
// CPP program to find the sum of all maximum
// occurring elements in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all maximum
// occurring elements in an array
int findSum(int arr[], int N)
{
    // Store frequencies of elements
    // of the array
    unordered_map<int, int> mp;
    for (int i = 0; i < N; i++)
        mp[arr[i]]++;

    // Find the max frequency
    int maxFreq = 0;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second > maxFreq) {
            maxFreq = itr->second;
        }
    }

    // Traverse the map again and find the sum
    int sum = 0;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second == maxFreq) {
            sum += itr->first * itr->second;
        }
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 2, 2, 2, 3, 3, 3, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all maximum
// occurring elements in an array
import java.util.*;

class GFG
{

// Function to find the sum of all maximum
// occurring elements in an array
static int findSum(int arr[], int N)
{
    // Store frequencies of elements
    // of the array
    Map<Integer,Integer> mp = new HashMap<>();
    for (int i = 0 ; i < N; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // Find the max frequency
    int maxFreq = 0;
    for (Map.Entry<Integer,Integer> entry : mp.entrySet())
    {
        if (entry.getValue() > maxFreq)
        {
            maxFreq = entry.getValue();
        }
    }

    // Traverse the map again and find the sum
    int sum = 0;
    for (Map.Entry<Integer,Integer> entry : mp.entrySet())
    {
        if (entry.getValue() == maxFreq)
        {
            sum += entry.getKey() * entry.getValue();
        }
    }

    return sum;
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 1, 1, 2, 2, 2, 2, 3, 3, 3, 3 };

    int N = arr.length;
    System.out.println(findSum(arr, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the Sum of all maximum
# occurring elements in an array

# Function to find the Sum of all maximum
# occurring elements in an array
def findSum(arr, N):

    # Store frequencies of elements
    # of the array
    mp = dict()
    for i in range(N):
        mp[arr[i]] = mp.get(arr[i], 0) + 1

    # Find the max frequency
    maxFreq = 0
    for itr in mp:
        if (mp[itr] > maxFreq):
            maxFreq = mp[itr]

    # Traverse the map again and find the Sum
    Sum = 0
    for itr in mp:
        if (mp[itr] == maxFreq):
            Sum += itr* mp[itr]

    return Sum

# Driver Code

arr= [1, 1, 2, 2, 2, 2, 3, 3, 3, 3 ]

N = len(arr)

print(findSum(arr, N))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find the sum of all maximum
// occurring elements in an array
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the sum of all maximum
// occurring elements in an array
static int findSum(int []arr, int N)
{
    // Store frequencies of elements
    // of the array
    Dictionary<int,int> mp = new Dictionary<int,int>();
    for (int i = 0 ; i < N; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            var val = mp[arr[i]];
            mp.Remove(arr[i]);
            mp.Add(arr[i], val + 1);
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Find the max frequency
    int maxFreq = 0;
    foreach(KeyValuePair<int, int> entry in mp)
    {
        if (entry.Value > maxFreq)
        {
            maxFreq = entry.Value;
        }
    }

    // Traverse the map again and find the sum
    int sum = 0;
    foreach(KeyValuePair<int, int> entry in mp)
    {
        if (entry.Value == maxFreq)
        {
            sum += entry.Key * entry.Value;
        }
    }

    return sum;
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 1, 1, 2, 2, 2, 2, 3, 3, 3, 3 };

    int N = arr.Length;
    Console.WriteLine(findSum(arr, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find
// the sum of all maximum
// occurring elements in an array

// Function to find the sum of all maximum
// occurring elements in an array
function findSum(arr,N)
{
    // Store frequencies of elements
    // of the array
    let mp = new Map();
    for (let i = 0 ; i < N; i++)
    {
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // Find the max frequency
    let maxFreq = 0;
    for (let [key, value] of mp.entries())
    {
        if (value > maxFreq)
        {
            maxFreq = value;
        }
    }

    // Traverse the map again and find the sum
    let sum = 0;
    for (let [key, value] of mp.entries())
    {
        if (value == maxFreq)
        {
            sum += key * value;
        }
    }

    return sum;
}

// Driver Code

let arr=[ 1, 1, 2, 2, 2, 2, 3, 3, 3, 3 ];
let N = arr.length;
document.write(findSum(arr, N));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
20
```

**时间复杂度** : O(N)，其中 N 为数组中的元素个数。