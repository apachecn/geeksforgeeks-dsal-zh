# 数组范围查询频率与值相同的元素

> 原文： [https://www.geeksforgeeks.org/array-range-queries-elements-frequency-value/](https://www.geeksforgeeks.org/array-range-queries-elements-frequency-value/)

给定一个由`N`个数字组成的数组，任务是回答以下类型的`Q`个查询：

```
query(start, end) = Number of times a 
number x occurs exactly x times in a 
subarray from start to end

```

**示例**：

> 输入: `arr = {1, 2, 2, 3, 3, 3}`
> 
> 查询 1: `start = 0`, `end = 1`, 
> 
> 查询 2: `start = 1`, `end = 1`, 
> 
> 查询 3: `start = 0`, `end = 2`, 
> 
> 查询 4: `start = 1,` `end = 3`, 
> 
> 查询 5: `start = 3`,` end = 5`, 
> 
> 查询 6: `start = 0`, `end = 5`
> 
> 输出: `1 0 2 1 1 3`

**说明**：

在查询 1 中，元素 1 在子数组`[1, 2]`中出现一次；

在查询 2 中，没有元素满足子数组`[2]`的条件。

在查询 3 中，元素 1 在子数组`[1, 2, 2]`中出现一次，而元素 2 出现两次；

在查询 4 中，元素 2 在子数组`[2, 2, 3]`中出现两次；

在查询 5 中，元素 3 在子数组`[3, 3, 3]`中发生三次。

在查询 6 中，元素 1 在子数组`[1, 2, 2, 3, 3, 3]`中发生一次，2 发生两次，3 发生三次。



**方法 1（暴力）**：

计算每个查询下子数组中每个元素的频率。 如果在每个查询覆盖的子数组中任何数字`x`的频率为`x`，我们将增加计数器。

## C++ 

```cpp

/* C++ Program to answer Q queries to  
   find number of times an element x  
   appears x times in a Query subarray */
#include <bits/stdc++.h> 
using namespace std; 

/* Returns the count of number x with 
   frequency x in the subarray from  
   start to end */
int solveQuery(int start, int end, int arr[]) 
{ 
    // map for frequency of elements 
    unordered_map<int, int> frequency; 

    // store frequency of each element  
    // in arr[start; end] 
    for (int i = start; i <= end; i++)  
        frequency[arr[i]]++;     

    // Count elements with same frequency 
    // as value 
    int count = 0; 
    for (auto x : frequency)  
        if (x.first == x.second)  
            count++;     
    return count; 
} 

int main() 
{ 
    int A[] = { 1, 2, 2, 3, 3, 3 }; 
    int n = sizeof(A) / sizeof(A[0]); 

    // 2D array of queries with 2 columns 
    int queries[][3] = { { 0, 1 }, 
                         { 1, 1 }, 
                         { 0, 2 }, 
                         { 1, 3 }, 
                         { 3, 5 }, 
                         { 0, 5 } }; 

    // calculating number of queries 
    int q = sizeof(queries) / sizeof(queries[0]); 

    for (int i = 0; i < q; i++) { 
        int start = queries[i][0]; 
        int end = queries[i][1]; 
        cout << "Answer for Query " << (i + 1) 
             << " = " << solveQuery(start, 
             end, A) << endl; 
    } 

    return 0; 
} 

```