# 在每个数组元素

> 原文：[https://www.geeksforgeeks.org/count-greater-elements-on-the-left-side-of-every-array-element/](https://www.geeksforgeeks.org/count-greater-elements-on-the-left-side-of-every-array-element/)

的左侧计数更大的元素

给定大小为 **N** 的不同整数的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，任务是在每个数组元素的左侧打印较大元素的计数。

**示例**：

> **输入**：arr [] = {12，1，2，3，0，}
> **输出**：0 1 1 1 4
> **说明**：
> 对于索引 0，左侧不存在更大的元素。
> 对于索引 1，{12}是左侧的较大元素。
> 对于索引 2，{12}是左侧的较大元素。
> 对于索引 3，{12}是左侧的较大元素。
> 对于索引 4，{12，1，2，3}是左侧的较大元素。
> 因此，输出为 0 1 1 1 4。
> 
> **输入**：arr [] = {5，4，3，2，1}
> **输出**：0 1 2 3 4

**天真的方法**：解决该问题的最简单方法是遍历数组，对于每个数组元素，向左遍历，并将每个元素与当前元素进行比较。 最后，为每个数组元素在其左侧打印更多元素的计数。

***时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：`O(1)`*

**有效方法**：可以使用 [Set](https://www.geeksforgeeks.org/set-in-cpp-stl/) 容器解决此问题，这些容器由 [自平衡二进制搜索树](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/) 实现。 请按照以下步骤解决问题。

1.  创建一个空的[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)， **St** 。

2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将每个元素一一插入 **St** 中。

3.  使用 [upper_bound](https://www.geeksforgeeks.org/set-upper_bound-function-in-c-stl/) 函数查找 **arr [i]** 的前一个较大元素。

4.  使用 [distance](https://www.geeksforgeeks.org/stddistance-in-c/) 函数查找集合中的上一个较大元素与最后一个元素之间的距离。

5.  将距离存储在数组 **countLeftGreater []** 中。

6.  打印数组。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to print the count of greater 
// elements on left of each array element 
void display(int countLeftGreater[], int N) 
{ 
    for (int i = 0; i < N; i++) { 
        cout << countLeftGreater[i] 
             << " "; 
    } 
} 

// Function to get the count of greater 
// elements on left of each array element 
void countGreater(int arr[], int N) 
{ 
    // Store distinct array 
    // elements in sorted order 
    set<int> St; 

    // Stores the count of greater 
    // elements on the left side 
    int countLeftGreater[N]; 

    // Traverse the array 
    for (int i = 0; i < N; i++) { 

        // Insert array elements 
        // into the set 
        St.insert(arr[i]); 

        // Find previous greater element 
        auto it = St.upper_bound(arr[i]); 

        // Find the distance between the 
        // previous greater element of arr[i] 
        // and last element of the set 
        countLeftGreater[i] 
            = distance(it, St.end()); 
    } 
    display(countLeftGreater, N); 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 12, 1, 2, 3, 0, 11, 4 }; 
    int N = sizeof(arr) / sizeof(arr[0]); 
    countGreater(arr, N); 
}

```

**Output:**

```
0 1 1 1 4 1 2

```

***时间复杂度**：O（N <sup>2</sup> ），因为距离函数取 **`O(n)`**，但上述实现非常简单，并且比朴素的方法效果更好 一般情况下的算法。

**辅助空间**：`O(n)`*

**注意**：上述方法适用于唯一元素，但对于重复元素，只需将[替换为](https://www.geeksforgeeks.org/set-in-cpp-stl/) [](https://www.geeksforgeeks.org/set-in-cpp-stl/) [多组。](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)



* * *

* * *



