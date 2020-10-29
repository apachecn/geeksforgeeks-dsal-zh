# 删除给定元素后找到最大的

> 原文：[https://www.geeksforgeeks.org/find-the-largest-after-deleting-the-given-elements/](https://www.geeksforgeeks.org/find-the-largest-after-deleting-the-given-elements/)

给定一个整数数组，请在删除给定元素后找到最大的数字。 如果重复元素，请为包含要删除元素的数组中存在的元素的每个实例删除一个实例。

**示例**：

> 输入：array [] = {5，12，33，4，56，12，20}
> del [] = {12，33，56，5}
> 输出：20
> 说明：我们得到 删除给定元素后的{12，20}。 其余元素中最大的是 20

**方法**：

*   将所有要从数组中删除的数字插入到哈希映射中，以便我们可以检查数组元素是否在`O(1)`时也出现在 Delete-array 中。

*   初始化最大值 max 为 INT_MIN。

*   遍历数组。 检查元素是否存在于哈希映射中。

*   如果存在，则将其从哈希映射中删除；否则，将其与 max 变量进行比较，如果元素的值大于最大值，则将其值更改。

## C++

```cpp

// C++ program to find the largest number 
// from the array after  n deletions 
#include "climits" 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

// Returns maximum element from arr[0..m-1] after deleting 
// elements from del[0..n-1] 
int findlargestAfterDel(int arr[], int m, int del[], int n) 
{ 
    // Hash Map of the numbers to be deleted 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; ++i) { 

        // Increment the count of del[i] 
        mp[del[i]]++; 
    } 

    // Initializing the largestElement 
    int largestElement = INT_MIN; 

    for (int i = 0; i < m; ++i) { 

        // Search if the element is present 
        if (mp.find(arr[i]) != mp.end()) { 

            // Decrement its frequency 
            mp[arr[i]]--; 

            // If the frequency becomes 0, 
            // erase it from the map 
            if (mp[arr[i]] == 0) 
                mp.erase(arr[i]); 
        } 

        // Else compare it largestElement 
        else
            largestElement = max(largestElement, arr[i]); 
    } 

    return largestElement; 
} 

int main() 
{ 
    int array[] = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = sizeof(array) / sizeof(array[0]); 

    int del[] = { 12, 33, 56, 5 }; 
    int n = sizeof(del) / sizeof(del[0]); 

    cout << findlargestAfterDel(array, m, del, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find the largest number 
// from the array after n deletions 
import java.util.*; 

class GFG  
{ 

// Returns maximum element from arr[0..m-1] after deleting 
// elements from del[0..n-1] 
static int findlargestAfterDel(int arr[], int m, 
                               int del[], int n) 
{ 
    // Hash Map of the numbers to be deleted 
    HashMap<Integer, 
            Integer> mp = new HashMap<Integer, 
                                      Integer>(); 
    for (int i = 0; i < n; ++i)  
    { 

        // Increment the count of del[i] 
        if(mp.containsKey(del[i])) 
        { 
            mp.put(del[i], mp.get(del[i]) + 1); 
        } 
        else
        { 
            mp.put(del[i], 1); 
        } 
    } 

    // Initializing the largestElement 
    int largestElement = Integer.MIN_VALUE; 

    for (int i = 0; i < m; i++)  
    { 

        // Search if the element is present 
        if (mp.containsKey(arr[i]))  
        { 

            // Decrement its frequency 
            mp.put(arr[i], mp.get(arr[i]) - 1); 

            // If the frequency becomes 0, 
            // erase it from the map 
            if (mp.get(arr[i]) == 0) 
                mp.remove(arr[i]); 
        } 

        // Else compare it largestElement 
        else
            largestElement = Math.max(largestElement, arr[i]); 
    } 
    return largestElement; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    int array[] = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = array.length; 

    int del[] = { 12, 33, 56, 5 }; 
    int n = del.length; 

    System.out.println(findlargestAfterDel(array, m, del, n));     
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to find the largest  
# number from the array after n deletions 
import math as mt 

# Returns maximum element from arr[0..m-1]  
# after deleting elements from del[0..n-1] 
def findlargestAfterDel(arr, m, dell, n): 

    # Hash Map of the numbers 
    # to be deleted 
    mp = dict() 
    for i in range(n): 

        # Increment the count of del[i] 
        if dell[i] in mp.keys(): 
            mp[dell[i]] += 1
        else: 
            mp[dell[i]] = 1

    # Initializing the largestElement 
    largestElement = -10**9

    for i in range(m): 

        # Search if the element is present 
        if (arr[i] in mp.keys()): 

            # Decrement its frequency 
            mp[arr[i]] -= 1

            # If the frequency becomes 0, 
            # erase it from the map 
            if (mp[arr[i]] == 0): 
                mp.pop(arr[i]) 

        # Else compare it largestElement 
        else: 
            largestElement = max(largestElement,  
                                         arr[i]) 

    return largestElement 

# Driver code 
array = [5, 12, 33, 4, 56, 12, 20] 
m = len(array) 

dell = [12, 33, 56, 5] 
n = len(dell) 

print(findlargestAfterDel(array, m, dell, n)) 

# This code is contributed  
# by mohit kumar 29 

```

## C#

```cs

// C# program to find the largest number 
// from the array after n deletions 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// Returns maximum element from arr[0..m-1]  
// after deleting elements from del[0..n-1] 
static int findlargestAfterDel(int []arr, int m, 
                               int []del, int n) 
{ 
    // Hash Map of the numbers to be deleted 
    Dictionary<int,  
               int> mp = new Dictionary<int, 
                                        int>(); 
    for (int i = 0; i < n; ++i)  
    { 

        // Increment the count of del[i] 
        if(mp.ContainsKey(del[i])) 
        { 
            mp[arr[i]] = mp[arr[i]] + 1; 
        } 
        else
        { 
            mp.Add(del[i], 1); 
        } 
    } 

    // Initializing the largestElement 
    int largestElement = int.MinValue; 

    for (int i = 0; i < m; i++)  
    { 

        // Search if the element is present 
        if (mp.ContainsKey(arr[i]))  
        { 

            // Decrement its frequency 
            mp[arr[i]] = mp[arr[i]] - 1; 

            // If the frequency becomes 0, 
            // erase it from the map 
            if (mp[arr[i]] == 0) 
                mp.Remove(arr[i]); 
        } 

        // Else compare it largestElement 
        else
            largestElement = Math.Max(largestElement,  
                                             arr[i]); 
    } 
    return largestElement; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    int []array = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = array.Length; 

    int []del = { 12, 33, 56, 5 }; 
    int n = del.Length; 

    Console.WriteLine(findlargestAfterDel(array, m, del, n));  
} 
} 

// This code is contributed by Princi Singh 

```

**输出**：

```
20
```

**时间复杂度** –`O(n)`



* * *

* * *



