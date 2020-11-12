# 在删除给定元素之后查找最小的元素

> 原文：[https://www.geeksforgeeks.org/find-the-smallest-after-deleting-given-elements/](https://www.geeksforgeeks.org/find-the-smallest-after-deleting-given-elements/)

给定一个整数数组，请在删除给定元素后找到最小的数字。 在重复元素的情况下，我们为包含要删除元素的数组中存在的每个实例删除一个实例（从原始数组中删除）。

**示例**：

> 输入：`arr = {5, 12, 33, 4, 56, 12, 20}, del = {12, 4, 56, 5}`
>
> 输出：12
>
> 删除给定元素后，数组变为`{33, 12, 20}`，最小元素变为 12。请注意，有两次出现 12，我们将其中之一删除。
> 
> 输入：`arr = {1, 20, 3, 4, 10}, del = {1, 4, 10}`
>
> 输出：3

**方法**：

*   将所有要从数组中删除的数字插入到哈希映射中，以便我们可以检查数组元素是否在`O(1)`时也出现在删除数组中。

*   将最小的最小值`min`初始化为`INT_MAX`。

*   遍历数组。 检查元素是否存在于哈希映射中。

*   如果存在，则将其从哈希映射中删除，否则，将其与`min`变量进行比较，如果元素的值小于`min`值，则更改其值。

## C++

```cpp

// C++ program to find the smallest number 
// from the array after  n deletions 
#include "climits" 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

// Returns minimum element from arr[0..m-1] after deleting 
// elements from del[0..n-1] 
int findSmallestAfterDel(int arr[], int m, int del[], int n) 
{ 
    // Hash Map of the numbers to be deleted 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; ++i) { 

        // Increment the count of del[i] 
        mp[del[i]]++; 
    } 

    // Initializing the smallestElement 
    int smallestElement = INT_MAX; 

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

        // Else compare it smallestElement 
        else
            smallestElement = min(smallestElement, arr[i]); 
    } 

    return smallestElement; 
} 

int main() 
{ 
    int array[] = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = sizeof(array) / sizeof(array[0]); 

    int del[] = { 12, 4, 56, 5 }; 
    int n = sizeof(del) / sizeof(del[0]); 

    cout << findSmallestAfterDel(array, m, del, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find the smallest number 
// from the array after n deletions 
import java.util.*; 

class GFG 
{ 

// Returns minimum element from arr[0..m-1]  
// after deleting elements from del[0..n-1] 
static int findSmallestAfterDel(int arr[], int m, 
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

    // Initializing the smallestElement 
    int smallestElement = Integer.MAX_VALUE; 

    for (int i = 0; i < m; ++i)  
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

        // Else compare it smallestElement 
        else
            smallestElement = Math.min(smallestElement,  
                                               arr[i]); 
    } 

    return smallestElement; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int array[] = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = array.length; 

    int del[] = { 12, 4, 56, 5 }; 
    int n = del.length; 

    System.out.println(findSmallestAfterDel(array, m,  
                                            del, n)); 
} 
}  

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to find the smallest 
# number from the array after n deletions 
import math as mt 

# Returns maximum element from arr[0..m-1]  
# after deleting elements from del[0..n-1] 
def findSmallestAfterDel(arr, m, dell, n): 

    # Hash Map of the numbers  
    # to be deleted 
    mp = dict() 
    for i in range(n): 

        # Increment the count of del[i] 
        if dell[i] in mp.keys(): 
            mp[dell[i]] += 1
        else: 
            mp[dell[i]] = 1

    # Initializing the SmallestElement 
    SmallestElement = 10**9

    for i in range(m): 

        # Search if the element is present 
        if (arr[i] in mp.keys()): 

            # Decrement its frequency 
            mp[arr[i]] -= 1

            # If the frequency becomes 0, 
            # erase it from the map 
            if (mp[arr[i]] == 0): 
                mp.pop(arr[i]) 

        # Else compare it SmallestElement 
        else: 
            SmallestElement = min(SmallestElement,  
                                           arr[i]) 

    return SmallestElement 

# Driver code 
array = [5, 12, 33, 4, 56, 12, 20] 
m = len(array) 

dell = [12, 4, 56, 5] 
n = len(dell) 

print(findSmallestAfterDel(array, m, dell, n)) 

# This code is contributed 
# by mohit kumar 29 

```

## C#

```cs

// C# program to find the smallest number 
// from the array after n deletions 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// Returns minimum element from arr[0..m-1]  
// after deleting elements from del[0..n-1] 
static int findSmallestAfterDel(int []arr, int m, 
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
            mp[del[i]] = mp[del[i]] + 1; 
        } 
        else
        { 
            mp.Add(del[i], 1); 
        } 
    } 

    // Initializing the smallestElement 
    int smallestElement = int.MaxValue; 
    for (int i = 0; i < m; ++i)  
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

        // Else compare it smallestElement 
        else
            smallestElement = Math.Min(smallestElement,  
                                               arr[i]); 
    } 
    return smallestElement; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []array = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = array.Length; 

    int []del = { 12, 4, 56, 5 }; 
    int n = del.Length; 

    Console.WriteLine(findSmallestAfterDel(array, m,  
                                           del, n)); 
} 
}  

// This code is contributed by Princi Singh 

```

**输出**：

```
12

```

**时间复杂度**：`O(n)`



* * *

* * *



