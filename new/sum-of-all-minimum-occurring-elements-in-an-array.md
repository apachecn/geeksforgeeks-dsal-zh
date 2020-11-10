# 数组

> 原文：[https://www.geeksforgeeks.org/sum-of-all-minimum-occurring-elements-in-an-array/](https://www.geeksforgeeks.org/sum-of-all-minimum-occurring-elements-in-an-array/)

中所有最小出现元素的总和

给定包含重复元素的整数数组。 任务是找到给定数组中所有最少出现的元素的总和。 这是其频率在数组中最小的所有此类元素的总和。

**示例**：

```
Input : arr[] = {1, 1, 2, 2, 3, 3, 3, 3}
Output : 2
The least occurring element is 1 and 2 and it's number
of occurrence is 2\. Therefore sum of all 1's and 2's in the 
array = 1+1+2+2 = 6.

Input : arr[] = {10, 20, 30, 40, 40}
Output : 60
Elements with least frequency are 10, 20, 30.
Their sum = 10 + 20 + 30 = 60.

```

**方法**：

*   遍历数组，并在 C++ 中使用[`unordered_map`](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)存储数组元素的频率，`map`的键为数组元素，值为数组中的频率。

*   然后，遍历该图以查找出现最少的元素的频率。

*   现在，要再次找到遍历该映射的总和，对于所有具有最小频率的元素，请找到 **frequency_of_min_occurring_element * min_occurring_element** 并找到其总和。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the sum of all minimum
// occurring elements in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all minimum
// occurring elements in an array
int findSum(int arr[], int N)
{
    // Store frequencies of elements
    // of the array
    unordered_map<int, int> mp;
    for (int i = 0; i < N; i++) 
        mp[arr[i]]++;    

    // Find the min frequency
    int minFreq = INT_MAX;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second < minFreq) {
            minFreq = itr->second;
        }
    }

    // Traverse the map again and find the sum
    int sum = 0;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second == minFreq) {
            sum += itr->first * itr->second;
        }
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 10, 20, 30, 40, 40 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findSum(arr, N);

    return 0;
}

```

## Java

```java

// Java program to find the sum of all minimum
// occurring elements in an array
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

class GFG 
{ 
// Function to find the sum of all minimum
// occurring elements in an array
static int findSum(int arr[], int N)
{
    // Store frequencies of elements
    // of the array
    Map<Integer,Integer> mp = new HashMap<>();
    for (int i = 0; i < N; i++) 
        mp.put(arr[i],mp.get(arr[i])==null?1:mp.get(arr[i])+1);

    // Find the min frequency
    int minFreq = Integer.MAX_VALUE;
    minFreq = Collections.min(mp.entrySet(), 
            Comparator.comparingInt(Map.Entry::getKey)).getValue();

    // Traverse the map again and find the sum
    int sum = 0;
    for (Map.Entry<Integer,Integer> entry : mp.entrySet()) 
    {
        if (entry.getValue() == minFreq)
        {
            sum += entry.getKey() * entry.getValue();
        }
    }

    return sum;
}

// Driver Code
public static void main(String[] args) 
{
    int arr[] = { 10, 20, 30, 40, 40 };

    int N = arr.length;

    System.out.println( findSum(arr, N));
}
}

// This code contributed by Rajput-Ji

```

## Python3

```py

# Python3 program to find theSum of all 
# minimum occurring elements in an array
import math as mt

# Function to find theSum of all minimum
# occurring elements in an array
def findSum(arr, N):

    # Store frequencies of elements
    # of the array
    mp = dict()
    for i in arr:
        if i in mp.keys():
            mp[i] += 1
        else:
            mp[i] = 1

    # Find the min frequency
    minFreq = 10**9
    for itr in mp:
        if mp[itr]< minFreq:
            minFreq = mp[itr]

    # Traverse the map again and 
    # find theSum
    Sum = 0
    for itr in mp:
        if mp[itr]== minFreq:
            Sum += itr * mp[itr]

    return Sum

# Driver Code
arr = [ 10, 20, 30, 40, 40] 

N = len(arr)

print(findSum(arr, N))

# This code is contributed by
# mohit kumar 29

```

## C#

```cs

// C# program to find the sum of all minimum 
// occurring elements in an array 
using System; 
using System.Collections.Generic; 

class GFG{

// Function to find the sum of all minimum 
// occurring elements in an array 
static int findSum(int[] arr, int N) 
{ 

    // Store frequencies of elements 
    // of the array 
    Dictionary<int, 
               int> mp = new Dictionary<int,
                                        int>();  
    for(int i = 0; i < N; i++) 
    {
        if (mp.ContainsKey(arr[i]))
        {
            mp[arr[i]]++;
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Find the min frequency 
    int minFreq = Int32.MaxValue; 
    foreach(KeyValuePair<int, int> itr in mp) 
    { 
        if (itr.Value < minFreq)
        {
            minFreq = itr.Value;
        }
    } 

    // Traverse the map again and find the sum 
    int sum = 0; 
    foreach(KeyValuePair<int, int> itr in mp) 
    { 
        if (itr.Value == minFreq)
        {
            sum += itr.Key * itr.Value; 
        }
    }
    return sum; 
} 

// Driver code
static void Main() 
{
    int[] arr = { 10, 20, 30, 40, 40 }; 

    int N = arr.Length; 

    Console.Write(findSum(arr, N)); 
}
}

// This code is contributed by divyeshrabadiya07

```

**输出**： 

```
60

```

**时间复杂度**：`O(n)`，其中`N`是数组中元素的数量。



* * *

* * *



