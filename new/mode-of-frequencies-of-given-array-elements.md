# 给定数组元素的频率模式

给定数组 **arr []** ，任务是找到给定数组的元素的[频率的](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[模式](https://www.geeksforgeeks.org/mode/)。

**示例**：

> **输入**：arr [] = {6，10，3，10，8，3，6，4}，N = 8
> **输出**：2
> **说明**：
> 此处（3、10 和 6）具有频率 2，而（4 和 8）具有频率 1。
> 三个数字具有频率 2，而两个数字具有频率 1。
> 因此，频率的模式为 2。
> 
> **输入**：arr [] = {5、9、2、9、7、2、5、3、1}，N = 9
> **输出**：1

**方法**：想法是找到所有阵列元素的频率。 最后，计算频率的[模式。](https://www.geeksforgeeks.org/mode/)

下面是上述方法的实现：

## C++

```cpp

// C++ program of the 
// above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the mode of the 
// frequency of the array 
int countFreq(int arr[], int n) 
{ 

    // Stores the frequencies 
    // of array elements 
    unordered_map<int, int> mp1; 

    // Traverse through array 
    // elements and 
    // count frequencies 
    for (int i = 0; i < n; ++i) { 
        mp1[arr[i]]++; 
    } 

    // Stores the frequencies's of 
    // frequencies of array elements 
    unordered_map<int, int> mp2; 

    for (auto it : mp1) { 
        mp2[it.second]++; 
    } 

    // Stores teh minimum value 
    int M = INT_MIN; 

    // Find the Mode in 2nd map 
    for (auto it : mp2) { 
        M = max(M, it.second); 
    } 

    // search for this Mode 
    for (auto it : mp2) { 
        // When mode is find then return 
        // to main function. 
        if (M == it.second) { 
            return it.first; 
        } 
    } 

    // If mode is not found 
    return 0; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 6, 10, 3, 10, 8, 3, 6, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << countFreq(arr, n); 
    return 0; 
}

```

## Java

```java

// Java program of the 
// above approach 
import java.util.*; 

class GFG{ 

// Function to find the mode of the 
// frequency of the array 
static int countFreq(int arr[], int n) 
{ 

    // Stores the frequencies 
    // of array elements 
    HashMap<Integer, 
            Integer> mp1 = new HashMap<Integer, 
                                       Integer>(); 

    // Traverse through array 
    // elements and 
    // count frequencies 
    for(int i = 0; i < n; ++i) 
    { 
        if (mp1.containsKey(arr[i])) 
        { 
            mp1.put(arr[i], mp1.get(arr[i]) + 1); 
        } 
        else
        { 
            mp1.put(arr[i], 1); 
        } 
    } 

    // Stores the frequencies's of 
    // frequencies of array elements 
    HashMap<Integer, 
            Integer> mp2 = new HashMap<Integer, 
                                       Integer>(); 

    for(Map.Entry<Integer, 
                  Integer> it : mp1.entrySet()) 
    { 
        if (mp2.containsKey(it.getValue())) 
        { 
            mp2.put(it.getValue(), 
            mp2.get(it.getValue()) + 1); 
        } 
        else
        { 
            mp2.put(it.getValue(), 1); 
        } 
    } 

    // Stores teh minimum value 
    int M = Integer.MIN_VALUE; 

    // Find the Mode in 2nd map 
    for(Map.Entry<Integer, 
                  Integer> it : mp2.entrySet()) 
    { 
        M = Math.max(M, it.getValue()); 
    } 

    // Search for this Mode 
    for(Map.Entry<Integer, 
                  Integer> it : mp2.entrySet()) 
    { 

        // When mode is find then return 
        // to main function. 
        if (M == it.getValue())  
        { 
            return it.getKey(); 
        } 
    } 

    // If mode is not found 
    return 0; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int arr[] = { 6, 10, 3, 10, 8, 3, 6, 4 }; 
    int n = arr.length; 

    System.out.print(countFreq(arr, n)); 
} 
} 

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program of the 
# above approach 
from collections import defaultdict 
import sys 

# Function to find the mode of the 
# frequency of the array 
def countFreq(arr, n): 

  # Stores the frequencies 
  # of array elements 
  mp1 = defaultdict (int) 

  # Traverse through array 
  # elements and 
  # count frequencies 
  for i in range (n): 
    mp1[arr[i]] += 1

    # Stores the frequencies's of 
    # frequencies of array elements 
    mp2 = defaultdict (int) 

    for it in mp1: 
      mp2[mp1[it]] += 1

      # Stores teh minimum value 
      M = -sys.maxsize - 1

      # Find the Mode in 2nd map 
      for it in mp2: 
        M = max(M, mp2[it]) 

        # search for this Mode 
        for it in mp2: 

          # When mode is find then return 
          # to main function. 

          if (M == mp2[it]): 
            return it 

          # If mode is not found 
          return 0

# Driver Code 
if __name__ == "__main__": 

  arr = [6, 10, 3, 10, 
         8, 3, 6, 4] 
  n = len(arr) 
  print (countFreq(arr, n)) 

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program of the 
// above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the mode of the 
// frequency of the array 
static int countFreq(int []arr, int n) 
{ 

    // Stores the frequencies 
    // of array elements 
    Dictionary<int, 
               int> mp1 = new Dictionary<int, 
                                         int>(); 

    // Traverse through array 
    // elements and 
    // count frequencies 
    for(int i = 0; i < n; ++i) 
    { 
        if (mp1.ContainsKey(arr[i])) 
        { 
            mp1[arr[i]] = mp1[arr[i]] + 1; 
        } 
        else
        { 
            mp1.Add(arr[i], 1); 
        } 
    } 

    // Stores the frequencies's of 
    // frequencies of array elements 
    Dictionary<int, 
               int> mp2 = new Dictionary<int, 
                                         int>(); 

    foreach(KeyValuePair<int, int> it in mp1) 
    { 
        if (mp2.ContainsKey(it.Value)) 
        { 
            mp2[it.Value] = 
            mp2[it.Value] + 1; 
        } 
        else
        { 
            mp2.Add(it.Value, 1); 
        } 
    } 

    // Stores teh minimum value 
    int M = int.MinValue; 

    // Find the Mode in 2nd map 
    foreach(KeyValuePair<int, int> it in mp2) 
    { 
        M = Math.Max(M, it.Value); 
    } 

    // Search for this Mode 
    foreach(KeyValuePair<int, int> it in mp2) 
    { 

        // When mode is find then return 
        // to main function. 
        if (M == it.Value)  
        { 
            return it.Key; 
        } 
    } 

    // If mode is not found 
    return 0; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 6, 10, 3, 10, 8, 3, 6, 4 }; 
    int n = arr.Length; 

    Console.Write(countFreq(arr, n)); 
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



