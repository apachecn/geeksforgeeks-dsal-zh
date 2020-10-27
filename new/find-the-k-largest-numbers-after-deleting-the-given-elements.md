# 删除给定元素后，找出 k 个最大数字

给定一个整数数组，请在删除给定元素后找到 k 个最大数。 如果重复元素，请为包含要删除元素的数组中存在的元素的每个实例删除一个实例。
假定删除 n 个元素后将剩余至少 k 个元素。

**示例：**
输入：array [] = {5，12，33，4，56，12，20}，del [] = {12，56，5}，k = 3
输出：33 20 12
说明：删除后将保留{33，4，12，20}。 从中打印出前 3 个最高的元素。

**方法：**

*   将所有要从数组中删除的数字插入到哈希图中，以便我们可以检查数组元素是否在 O（1）时也出现在 Delete-array 中。
*   遍历数组。 检查元素是否存在于哈希图中。
*   如果存在，请从哈希图中删除它。
*   否则，将其插入 Max 堆中。
*   插入所有要删除的元素（不包括要删除的元素）后，从 Max 堆中弹出 k 个元素。

## C++

```cpp

#include "iostream" 
#include "queue" 
#include "unordered_map" 
using namespace std; 

// Find k maximum element from arr[0..m-1] after deleting 
// elements from del[0..n-1] 
void findElementsAfterDel(int arr[], int m, int del[], 
                                        int n, int k) 
{ 
    // Hash Map of the numbers to be deleted 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; ++i) { 

        // Increment the count of del[i] 
        mp[del[i]]++; 
    } 

    // Initializing the largestElement 
    priority_queue<int> heap; 

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
            heap.push(arr[i]); 
    } 

    // Print top k elements in the heap 
    for (int i = 0; i < k; ++i) { 
        cout << heap.top() << " "; 

        // Pop the top element 
        heap.pop(); 
    } 
} 

int main() 
{ 
    int array[] = { 5, 12, 33, 4, 56, 12, 20 }; 
    int m = sizeof(array) / sizeof(array[0]); 

    int del[] = { 12, 56, 5 }; 
    int n = sizeof(del) / sizeof(del[0]); 

    int k = 3; 

    findElementsAfterDel(array, m, del, n, k); 
    return 0; 
} 

```

## Python3

```py

# Python3 program to find the k maximum  
# number from the array after n deletions 
import math as mt 

# Find k maximum element from arr[0..m-1]  
# after deleting elements from del[0..n-1] 
def findElementsAfterDel(arr, m, dell, n, k): 

    # Hash Map of the numbers to be deleted 
    mp = dict() 
    for i in range(n): 

        # Increment the count of del[i] 
        if dell[i] in mp.keys(): 
            mp[dell[i]] += 1
        else: 
            mp[dell[i]] = 1

    heap = list() 

    for i in range(m): 

        # Search if the element is present 
        if (arr[i] in mp.keys()): 

            # Decrement its frequency 
            mp[arr[i]] -= 1

            # If the frequency becomes 0, 
            # erase it from the map 
            if (mp[arr[i]] == 0): 
                mp.pop(arr[i]) 

        # Else push it  
        else: 
            heap.append(arr[i]) 

    heap.sort() 
    heap = heap[::-1] 
    return heap[:k] 

# Driver code 
array = [5, 12, 33, 4, 56, 12, 20] 
m = len(array) 

dell = [12, 4, 56, 5 ] 
n = len(dell) 
k = 3
print(*findElementsAfterDel(array, m, dell, n, k)) 

# This code is contributed by 
# mohit kumar 29 

```

**Output:**

```
33 20 12

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



