# 根据给定条件删除的字符索引总和，以获得空字符串

> 原文：[https://www.geeksforgeeks.org/sum-of-indices-of-characters-removed-to-obtain-an-empty-string-based-on-given-conditions/](https://www.geeksforgeeks.org/sum-of-indices-of-characters-removed-to-obtain-an-empty-string-based-on-given-conditions/)

给定由小写英文字母组成的字符串`str`，任务是通过以下操作来计算所删除字符的索引总和（从 1 开始的索引），以获得空字符串：

*   删除字符串中最小的字母。

*   对于多次出现的最小字母，请删除索引最小的那个字母。

*   删除每个字符后，其右边所有字符的索引都会减少 1。

**示例**：

> **输入**：`str = "aba"`
>
> **输出**：4
>
> **说明**：`"aba" -> "ba"`，总和为 1
>
> `"ba" -> "b"`，总和为`1 + 2 = 3`
>
> `"b" -> ""`，总和为`3 + 1 = 4`
> 
> **输入**：`str = "geeksforgeeks"`
>
> **输出**：41

**朴素的方法**：

请按照以下步骤解决问题：

*   查找具有最小索引的最小字符。

*   从字符串中删除该字符，并将所有字符向右移一个索引。

*   重复上述步骤，直到字符串为空。

***时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`*

**高效方法**：可以使用[分段树](http://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)和[哈希优化上述方法。](https://www.geeksforgeeks.org/hashing-data-structure/) 请按照以下步骤解决问题：

*   可以观察到，仅删除字符右侧的索引受到影响，也就是说，它们需要移动一个位置。

*   将字符的索引存储在 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中

*   处理`HashMap`中的字符。

*   使用段树，找到留在字符当前索引中的元素数，这些元素已从字符串中删除。

*   提取已删除字符的索引，并在分段树中的`[0, 提取元素的索引]`范围内搜索，并在分段树中存在的范围内找到索引的**计数**。

*   将已提取元素的**索引添加到答案中–将**计数，然后将当前已删除元素的索引插入到分段树中。

*   重复上述步骤，直到字符串为空。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to add index of the deleted character 
void add_seg(int seg[], int start, int end, int current, 
             int index) 
{ 

    // If index is beyond the range 
    if (index > end or index < start) 
        return; 

    // Insert the index of the deleted 
    // characeter 
    if (start == end) { 
        seg[current] = 1; 
        return; 
    } 
    int mid = (start + end) / 2; 

    // Search over the subtrees to find the 
    // desired index 
    add_seg(seg, start, mid, 2 * current + 1, index); 
    add_seg(seg, mid + 1, end, 2 * current + 2, index); 
    seg[current] 
        = seg[2 * current + 1] + seg[2 * current + 2]; 
} 

// Function to return count of deleted indices 
// which are to the left of the current index 
int deleted(int seg[], int l, int r, int start, int end, 
            int current) 
{ 
    if (end < l or start > r) 
        return 0; 
    if (start >= l and end <= r) 
        return seg[current]; 
    int mid = (start + end) / 2; 
    return deleted(seg, l, r, start, mid, 2 * current + 1) 
           + deleted(seg, l, r, mid + 1, end, 
                     2 * current + 2); 
} 

// Function to generate the  
// sum of indices  
void sumOfIndices(string s) 
{ 
    int N = s.size(); 
    int x = int(ceil(log2(N))); 
    int seg_size = 2 * (int)pow(2, x) - 1; 
    int segment[seg_size] = { 0 }; 

    int count = 0; 

    // Stores the original index of the 
    // characters in sorted order of key 
    map<int, queue<int> > fre; 
    for (int i = 0; i < N; i++) { 
        fre[s[i]].push(i); 
    } 

    // Traverse the map 
    while (fre.empty() == false) { 

        // Extract smallest index 
        // of smallest characetr 
        auto it = fre.begin(); 

        // Delete the character from the map 
        // if it has no remaining occurrence 
        if (it->second.empty() == true) 
            fre.erase(it->first); 
        else { 

            // Stores the original index 
            int original_index 
                = it->second.front(); 

            // Count of elements removed to 
            // the left of current character 
            int curr_index 
                = deleted(segment, 0, original_index - 1, 
                          0, N - 1, 0); 

            // Current index of the current character 
            int new_index 
                = original_index - curr_index; 

            // For 1-based indexing 
            count += new_index + 1; 

            // Insert the deleted index 
            // in the segment tree 
            add_seg(segment, 0, N - 1, 
                    0, original_index); 
            it->second.pop(); 
        } 
    } 

    // Final answer 
    cout << count << endl; 
} 

// Driver Code 
int main() 
{ 
    string s = "geeksforgeeks"; 
    sumOfIndices(s); 
}

```

**Output:**

```
41

```

**时间复杂度**：`O(n Log n)`

**辅助空间**：`O(n)`



* * *

* * *



