# 从数组

> 原文：[https://www.geeksforgeeks.org/print-all-repeating-adjacent-pairs-in-sorted-order-from-an-array/](https://www.geeksforgeeks.org/print-all-repeating-adjacent-pairs-in-sorted-order-from-an-array/)

中按排序顺序打印所有重复的相邻对

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，该数组由 **N** 个整数组成，任务是从该数组中打印出所有相邻的整数对，这些对在给定数组中出现多次 。 如果数组包含多个这样的对，请按排序顺序打印所有对。

**示例**：

> **输入**：arr [] = {1、2、5、1、2}
> **输出**：
> 1 2
> **说明**：
> 1 2 是数组中唯一重复的整数对。
> 
> **输入**：arr [] = {1、2、3、4、1、2、3、4、1、2}
> **输出**：
> 1 2
> 2 3
> 3 4
> 4 1
> **说明**：
> 由于数组具有多个重复对，因此所有对均按排序顺序打印。

**方法**：最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将每个相邻对存储在 [Map](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 中。 打印频率大于 **1** 的所有此类对。 请按照以下步骤解决问题：

1.  创建一个映射 **M** 以将所有相邻对存储在数组中。

2.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将每个相邻对存储在 Map **M** 中。

3.  完成上述步骤后，[遍历图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，如果任意一对频率至少为一个，则将其插入向量 **V** 中。

4.  [以升序](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)对向量 **v** 进行排序，并打印存储在其中的所有对。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to print adjacent pairs 
// in sorted order 
void repeated_pairs(int arr[], int N) 
{ 
    // Store the frequency of all 
    // the adjacent pairs 
    map<pair<int, int>, int> m; 

    // Stores the resultant pairs 
    vector<pair<int, int> > v; 
    int i, j; 

    // Stores the count of all 
    // adjacent pairs 
    for (i = 0; i < N - 1; i++) { 

        pair<int, int> p 
            = { arr[i], arr[i + 1] }; 

        // Increment the count of pair 
        m[p]++; 
    } 

    // Store pairs that appears more 
    // than once 
    for (auto i = m.begin(); 
         i != m.end(); i++) { 

        // If frequency is at least 1 
        if (i->second > 1) { 
            pair<int, int> p = i->first; 

            // Insert pair into vector 
            v.push_back(p); 
        } 
    } 

    // Sort the vector 
    sort(v.begin(), v.end()); 

    // Print the pairs 
    for (i = 0; i < v.size(); i++) { 

        pair<int, int> p = v[i]; 

        // Print the pair 
        cout << p.first << " "
             << p.second << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given arr[] 
    int arr[] = { 1, 2, 3, 4, 1, 
                  2, 3, 4, 1, 2 }; 

    int N = sizeof(arr) / sizeof(arr[0]); 

    // Function call 
    repeated_pairs(arr, N); 

    return 0; 
} 

```

**Output:**

```
1 2
2 3
3 4
4 1

```

***时间复杂度**：O（N * log N）*

***辅助空间**：O（N）*



* * *

* * *



