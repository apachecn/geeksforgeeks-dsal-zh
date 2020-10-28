# 出现多次的数组元素

> 原文：[https://www.geeksforgeeks.org/array-elements-that-appear-more-than-once/](https://www.geeksforgeeks.org/array-elements-that-appear-more-than-once/)

给定一个整数数组，请打印该数组中所有重复的元素（出现多次的元素）。 输出应包含根据其首次出现的元素。

**示例**：

```
Input: arr[] = {12, 10, 9, 45, 2, 10, 10, 45}
Output: 10 45

Input: arr[] = {1, 2, 3, 4, 2, 5}
Output: 2

Input: arr[] = {1, 1, 1, 1, 1}
Output: 1
```

这个想法是**使用[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)** 来平均解决`O(n)`时间。 我们将元素及其计数存储在哈希表中。 存储完计数后，我们再次遍历输入数组并打印计数不止一次的那些元素。 为了确保每个输出元素仅打印一次，我们在打印元素后将`count`设置为 0。

## C++

```cpp

// C++ program to print all repeating elements 
#include <bits/stdc++.h> 
using namespace std; 

void printRepeating(int arr[], int n) 
{ 
    // Store elements and their counts in 
    // hash table 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; i++) 
        mp[arr[i]]++; 

    // Since we want elements in same order, 
    // we traverse array again and print 
    // those elements that appear more than 
    // once. 
    for (int i = 0; i < n; i++) { 
        if (mp[arr[i]] > 1) { 
            cout << arr[i] << " "; 

            // This is tricky, this is done 
            // to make sure that the current 
            // element is not printed again 
            mp[arr[i]] = 0; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 12, 10, 9, 45, 2, 10, 10, 45 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to print all repeating elements 

import java.util.*; 
import java.util.Map.Entry; 
import java.io.*; 
import java.lang.*; 

public class GFG { 

    static void printRepeating(int arr[], int n) 
    { 

        // Store elements and their counts in 
        // hash table 
        Map<Integer, Integer> map 
            = new LinkedHashMap<Integer, Integer>(); 
        for (int i = 0; i < n; i++) { 
            try { 
                map.put(arr[i], map.get(arr[i]) + 1); 
            } 
            catch (Exception e) { 
                map.put(arr[i], 1); 
            } 
        } 

        // Since we want elements in the same order, 
        // we traverse array again and print 
        // those elements that appear more than once. 

        for (Entry<Integer, Integer> e : map.entrySet()) { 
            if (e.getValue() > 1) { 
                System.out.print(e.getKey() + " "); 
            } 
        } 
    } 

    // Driver code 
    public static void main(String[] args) throws IOException 
    { 
        int arr[] = { 12, 10, 9, 45, 2, 10, 10, 45 }; 
        int n = arr.length; 
        printRepeating(arr, n); 
    } 
} 

// This code is contributed by Wrick 

```

## Python3

```py

# Python3 program to print 
# all repeating elements 
def printRepeating(arr, n): 

    # Store elements and  
    # their counts in 
    # hash table 
    mp = [0] * 100
    for i in range(0, n): 
        mp[arr[i]] += 1

    # Since we want elements  
    # in same order, we  
    # traverse array again  
    # and print those elements  
    # that appear more than once. 
    for i in range(0, n): 
        if (mp[arr[i]] > 1): 
            print(arr[i], end = " ") 

            # This is tricky, this  
            # is done to make sure  
            # that the current element  
            # is not printed again 
            mp[arr[i]] = 0

# Driver code 
arr = [12, 10, 9, 45,  
       2, 10, 10, 45]  
n = len(arr) 
printRepeating(arr, n) 

# This code is contributed  
# by Smita 

```

## C#

```cs

// C# program to print all repeating elements 
using System; 
using System.Collections.Generic;  

class GFG  
{ 
static void printRepeating(int []arr, int n) 
{ 

    // Store elements and their counts in 
    // hash table 
    Dictionary<int,  
               int> map = new Dictionary<int, 
                                         int>(); 
    for (int i = 0 ; i < n; i++) 
    { 
        if(map.ContainsKey(arr[i])) 
        { 
            var val = map[arr[i]]; 
            map.Remove(arr[i]); 
            map.Add(arr[i], val + 1);  
        } 
        else
        { 
            map.Add(arr[i], 1); 
        } 
    } 

    // Since we want elements in the same order, 
    // we traverse array again and print 
    // those elements that appear more than once. 
    foreach(KeyValuePair<int, int> e in map) 
    { 
        if (e.Value > 1)  
        { 
            Console.Write(e.Key + " "); 
        } 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []arr = { 12, 10, 9, 45, 2, 10, 10, 45 }; 
    int n = arr.Length; 
    printRepeating(arr, n); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

**Output:**

```
10 45

```

时间复杂度：在散列插入和搜索功能在`O(1)`时间工作的假设下，`O(n)`。



* * *

* * *



