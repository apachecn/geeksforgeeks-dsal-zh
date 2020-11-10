# 从数组中删除出现`k`次以上的元素

> 原文：[https://www.geeksforgeeks.org/remove-elements-from-the-array-which-appear-more-than-k-times/](https://www.geeksforgeeks.org/remove-elements-from-the-array-which-appear-more-than-k-times/)

给定一个整数数组，请删除所有出现在数组中严格超过`k`次的元素。

**示例**：

```
Input : arr[] = {1, 2, 2, 3, 2, 3, 4}
        k = 2
Output : 1 3 3 4

Input : arr[] = {2, 5, 5, 7}
        k = 1
Output : 2 7

```

**方法**：

*   拿一个哈希映射，它将存储数组中所有元素的频率。

*   现在，再次遍历。

*   打印出现少于或等于 k 次的元素。

## C++

```cpp

// C++ program to remove the elements which 
// appear more than k times from the array. 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void RemoveElements(int arr[], int n, int k) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    unordered_map<int, int> mp; 

    for (int i = 0; i < n; ++i) { 
        // Incrementing the frequency 
        // of the element by 1\. 
        mp[arr[i]]++; 
    } 

    for (int i = 0; i < n; ++i) { 
        // Print the element which appear 
        // less than or equal to k times. 
        if (mp[arr[i]] <= k) { 
            cout << arr[i] << " "; 
        } 
    } 
} 

int main(int argc, char const* argv[]) 
{ 
    int arr[] = { 1, 2, 2, 3, 2, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int k = 2; 

    RemoveElements(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to remove the elements which 
// appear more than k times from the array. 
import java.util.HashMap; 
import java.util.Map; 

class GFG  
{  

static void RemoveElements(int arr[], int n, int k) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    Map<Integer,Integer> mp = new HashMap<>(); 

    for (int i = 0; i < n; ++i) 
    { 
        // Incrementing the frequency 
        // of the element by 1\. 
        mp.put(arr[i],mp.get(arr[i]) == null?1:mp.get(arr[i])+1); 

    } 

    for (int i = 0; i < n; ++i)  
    { 
        // Print the element which appear 
        // less than or equal to k times. 
        if (mp.containsKey(arr[i]) && mp.get(arr[i]) <= k) 
        { 
            System.out.print(arr[i] + " "); 
        } 
    } 
} 

// Driver code  
public static void main(String[] args)  
{ 
    int arr[] = { 1, 2, 2, 3, 2, 3, 4 }; 
    int n = arr.length; 

    int k = 2; 

    RemoveElements(arr, n, k); 

} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python 3 program to remove the elements which 
# appear more than k times from the array. 
def RemoveElements(arr, n, k): 

    # Hash map which will store the 
    # frequency of the elements of the array. 
    mp = {i:0 for i in range(len(arr))} 

    for i in range(n): 

        # Incrementing the frequency 
        # of the element by 1\. 
        mp[arr[i]] += 1

    for i in range(n): 

        # Print the element which appear 
        # less than or equal to k times. 
        if (mp[arr[i]] <= k): 
            print(arr[i], end = " ") 

# Driver Code     
if __name__ == '__main__': 
    arr = [1, 2, 2, 3, 2, 3, 4] 
    n = len(arr) 

    k = 2

    RemoveElements(arr, n, k) 

# This code is contributed by 
# Sahil_Shelangia 

```

## C#

```cs

// C# program to remove the elements which 
// appear more than k times from the array. 
using System; 
using System.Collections.Generic; 

class GFG  
{  
static void RemoveElements(int [] arr,  
                           int n, int k) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    Dictionary<int,  
               int> mp = new Dictionary<int, 
                                        int>(); 

    for (int i = 0; i < n; ++i) 
    { 
        // Incrementing the frequency 
        // of the element by 1\. 
        if(mp.ContainsKey(arr[i])) 
            mp[arr[i]]++; 
        else
            mp[arr[i]] = 1; 
    } 

    for (int i = 0; i < n; ++i)  
    { 
        // Print the element which appear 
        // less than or equal to k times. 
        if (mp.ContainsKey(arr[i]) && mp[arr[i]] <= k) 
        { 
            Console.Write(arr[i] + " "); 
        } 
    } 
} 

// Driver code  
static public void Main()  
{ 
    int [] arr = { 1, 2, 2, 3, 2, 3, 4 }; 
    int n = arr.Length; 

    int k = 2; 

    RemoveElements(arr, n, k); 
} 
} 

// This code is contributed by Mohit kumar 29 

```

**输出**：

```
1 3 3 4

```

**时间复杂度** –`O(n)`



* * *

* * *



