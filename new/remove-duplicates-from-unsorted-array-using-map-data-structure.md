# 使用 Map 数据结构

> 原文：[https://www.geeksforgeeks.org/remove-duplicates-from-unsorted-array-using-map-data-structure/](https://www.geeksforgeeks.org/remove-duplicates-from-unsorted-array-using-map-data-structure/)

从未排序的数组中删除重复项

给定一个未排序的整数数组，请从中删除重复的元素后再打印该数组。 我们需要根据它们的首次出现来打印不同的数组元素。

**示例**：

```
Input : arr[] = { 1, 2, 5, 1, 7, 2, 4, 2}
Output : 1 2 5 7 4
Explanation : {1, 2} appear more than one time.

```

**方法**：

*   拿一个哈希图，其中将存储之前出现的所有元素。

*   遍历数组。

*   检查元素是否存在于哈希图中。

*   如果是，请继续遍历数组。

*   其他打印元素。

## C++

```cpp

// C++ program to remove the duplicates from the array. 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void removeDups(int arr[], int n) 
{ 
    // Hash map which will store the 
    // elements which has appeared previously. 
    unordered_map<int, bool> mp; 

    for (int i = 0; i < n; ++i) { 

        // Print the element if it is not 
        // there in the hash map 
        if (mp.find(arr[i]) == mp.end()) { 
            cout << arr[i] << " "; 
        } 

        // Insert the element in the hash map 
        mp[arr[i]] = true; 
    } 
} 

int main(int argc, char const* argv[]) 
{ 
    int arr[] = { 1, 2, 5, 1, 7, 2, 4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    removeDups(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to remove 
// the duplicates from the array. 
import java.util.HashMap; 

class GFG  
{ 
    static void removeDups(int[] arr, int n)  
    { 

        // Hash map which will store the 
        // elements which has appeared previously. 
        HashMap<Integer,  
                Boolean> mp = new HashMap<>(); 

        for (int i = 0; i < n; ++i) 
        { 

            // Print the element if it is not 
            // there in the hash map 
            if (mp.get(arr[i]) == null) 
                System.out.print(arr[i] + " "); 

            // Insert the element in the hash map 
            mp.put(arr[i], true); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int[] arr = { 1, 2, 5, 1, 7, 2, 4, 2 }; 
        int n = arr.length; 
        removeDups(arr, n); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python 3 program to remove the 
# duplicates from the array  
def removeDups(arr, n): 

    # dict to store every element 
    # one time 
    mp = {i : 0 for i in arr} 

    for i in range(n): 

        if mp[arr[i]] == 0: 
            print(arr[i], end = " ") 
            mp[arr[i]] = 1

# Driver code 
arr = [ 1, 2, 5, 1, 7, 2, 4, 2 ] 

# len of array 
n = len(arr) 

removeDups(arr,n) 

# This code is contributed 
# by Mohit Kumar 

```

## C#

```cs

// C# program to remove 
// the duplicates from the array. 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    static void removeDups(int[] arr, int n)  
    { 

        // Hash map which will store the 
        // elements which has appeared previously. 
        Dictionary<int,  
                Boolean> mp = new Dictionary<int, Boolean>(); 

        for (int i = 0; i < n; ++i) 
        { 

            // Print the element if it is not 
            // there in the hash map 
            if (!mp.ContainsKey(arr[i])) 
                Console.Write(arr[i] + " "); 

            // Insert the element in the hash map 
            mp[arr[i]] = true; 
        } 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 1, 2, 5, 1, 7, 2, 4, 2 }; 
        int n = arr.Length; 
        removeDups(arr, n); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
1 2 5 7 4

```

**时间复杂度–** O（N）



* * *

* * *



