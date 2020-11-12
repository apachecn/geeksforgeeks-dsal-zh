# 通过将每个元素的首次出现增加`K`来修改给定数组

> 原文：[https://www.geeksforgeeks.org/modify-given-array-by-incrementing-first-occurrence-of-every-element-by-k/](https://www.geeksforgeeks.org/modify-given-array-by-incrementing-first-occurrence-of-every-element-by-k/)



给定由`N`整数组成的数组`arr[]`，依次读取数组的每个元素并执行 以下操作：

*   如果当前元素`arr[i]`先前在数组中出现过，则将其第一次出现增加`K`。

*   否则，将`arr[i]`插入序列。

该任务是打印通过执行上述操作获得的整数的最终序列。

**示例**：

> **输入**：`arr[] = {1, 2, 3, 2, 3}, K = 1`
>
> **输出**：`[1, 4, 3, 2, 3] `
>
> **说明**：
> 
> 到达：1。
>
> 由于 1 是流中的第一个元素，因此只需将其插入解决方案即可。
>
> 因此，`b[] = [1]`。
> 
> 到达：2。
>
> 由于数组中不存在 2，因此只需将其插入解决方案即可。
>
> 因此，`b[] = [1, 2]`。
> 
> 到达：3。
>
> 由于数组中不存在 3，因此只需将其插入解决方案即可。
>
> 因此，`b[] = [1, 2, 3]`。
> 
> 到达：2
>
> 由于 2 已经存在，因此将其首次出现增加`K = 1`会将数组`b[]`修改为`[1, 3, 3, 2]`。
> 
> 到达：3
>
> 由于 3 已经存在，因此将其首次出现增加`K = 1`会将数组`b[]`修改为`[1, 4, 3, 2, 3]`。
> 
> **输入**：`arr [] = {1, 4, 1, 1, 4}, K = 6`
>
> **输出**：`[7, 10, 7, 1, 4]`

**朴素的方法**：解决问题的最简单方法是遍历数组，并且对于每个数组元素`arr[i]`，遍历范围`[0, i – 1]`检查数组中是否已经存在`arr[i]`。 如果发现是真的，则将`arr[i]`的首次出现增加`K`。

**时间复杂度**：`O(N ^ 2)`。

**辅助空间**：`O(1)`。

**有效方法**：可以使用[**散列**](http://www.geeksforgeeks.org/hashing-data-structure/)优化上述方法。 请按照以下步骤解决问题：

*   遍历数组并将每个数组元素的出现都存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，并按升序将其出现的索引配对。

*   如果发现**映射**中已经存在`arr[i]`，请从**映射**中删除首次出现的`arr[i]`。将与`arr[i] + K`配对的索引插入到**映射**中。

*   对所有数组元素重复上述步骤。 一旦遍历整个数组，请从**映射**获得整数序列并打印最终序列。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Print the required final sequence 
void printSequence(vector<int>& A, 
                   int n, int k) 
{ 
    // Stores the array element-index pairs 
    unordered_map<int, set<int> > mp; 

    // Stores the required sequence 
    vector<int> sol; 

    // Insert all array elements 
    for (int x : A) 
        sol.push_back(x); 

    for (int i = 0; i < n; i++) { 
        // If current element has 
        // not occurred previously 
        if (mp.find(sol[i]) == mp.end() 
            || mp[sol[i]].size() == 0) { 
            mp[sol[i]].insert(i); 
        } 

        // Otherwise 
        else { 

            // Iterator to the first index 
            // containing sol[i] 
            auto idxx = mp[sol[i]].begin(); 

            int idx = *idxx; 

            // Remove that occurrence 
            mp[sol[i]].erase(idxx); 

            // Increment by K 
            sol[idx] += k; 

            // Insert the incremented 
            // element at that index 
            mp[sol[idx]].insert(idx); 
            mp[sol[i]].insert(i); 
        } 
    } 

    // Print the final sequence 
    for (int x : sol) { 
        cout << x << " "; 
    } 
} 

// Driver Code 
int main() 
{ 
    int N = 5; 
    int K = 6; 
    vector<int> A = { 1, 4, 1, 1, 4 }; 
    printSequence(A, N, K); 
}

```

**输出**：

```
7 10 7 1 4

```

**时间复杂度**：`O(NlogN)`。

**辅助空间**：`O(n)`。



* * *

* * *



