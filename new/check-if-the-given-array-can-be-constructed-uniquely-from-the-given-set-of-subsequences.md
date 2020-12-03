# 检查给定的数组是否可以从给定的子序列集中唯一地构建

> 原文： [https://www.geeksforgeeks.org/check-if-the-given-array-can-be-constructed-uniquely-from-the-given-set-of-subsequences/](https://www.geeksforgeeks.org/check-if-the-given-array-can-be-constructed-uniquely-from-the-given-set-of-subsequences/)

给定具有不同元素的数组 **arr** 和该数组的子序列**序列**列表，任务是检查给定的数组是否可以从 给定子序列集。

**示例**：

> **输入**：arr [] = {1、2、3、4}，seqs [] [] = {{1、2}，{2、3}，{3、4}}
> **输出**：是
> **说明**：序列[1、2]，[2、3]和[3、4]可以唯一地重建
> 原始数组{ 1，2，3，4}。
> 
> **输入**：arr [] = {1、2、3、4}，seqs [] [] = {{1、2}，{2、3}，{2、4}}
> **输出**：否
> **说明**：序列[1、2]，[2、3]和[2、4]无法唯一地重建
> {1、2 ，3，4}。 可以从给定序列中构造两个可能的序列：
> 1）{1,2,3,4}
> 2）{1,2,4,3}

**方法**：

为了解决此问题，我们需要找到所有数组元素的[拓扑顺序](https://www.geeksforgeeks.org/topological-sorting/)，并检查是否仅存在一个元素的拓扑顺序， 在查找元素的拓扑顺序时，可以通过在每个瞬间仅存在一个源来确认。

下面是上述方法的实现：

## C++

```cpp

// C# program to Check if   
// the given array can be constructed  
// uniquely from the given set of subsequences 

#include <bits/stdc++.h> 
using namespace std; 

bool canConstruct(vector<int> originalSeq, 
                vector<vector<int> > sequences) 
{ 
    vector<int> sortedOrder; 
    if (originalSeq.size() <= 0) { 
        return false; 
    } 

    // Count of incoming edges for every vertex 
    unordered_map<int, int> inDegree; 

    // Adjacency list graph 
    unordered_map<int, vector<int> > graph; 
    for (auto seq : sequences) { 
        for (int i = 0; i < seq.size(); i++) { 
            inDegree[seq[i]] = 0; 
            graph[seq[i]] = vector<int>(); 
        } 
    } 

    // Build the graph 
    for (auto seq : sequences) { 
        for (int i = 1; i < seq.size(); i++) { 
            int parent = seq[i - 1], child = seq[i]; 
            graph[parent].push_back(child); 
            inDegree[child]++; 
        } 
    } 

    // if ordering rules for all the numbers 
    // are not present 
    if (inDegree.size() != originalSeq.size()) { 
        return false; 
    } 

    // Find all sources i.e., all vertices 
    // with 0 in-degrees 
    queue<int> sources; 
    for (auto entry : inDegree) { 
        if (entry.second == 0) { 
            sources.push(entry.first); 
        } 
    } 

    // For each source, add it to the sortedOrder 
    // and subtract one from all of in-degrees 
    // if a child's in-degree becomes zero 
    // add it to the sources queue 
    while (!sources.empty()) { 

        // If there are more than one source 
        if (sources.size() > 1) { 

            // Multiple sequences exist 
            return false; 
        } 

        // If the next source is different from the origin 
        if (originalSeq[sortedOrder.size()] !=  
                                sources.front()) { 
            return false; 
        } 
        int vertex = sources.front(); 
        sources.pop(); 
        sortedOrder.push_back(vertex); 
        vector<int> children = graph[vertex]; 
        for (auto child : children) { 

            // Decrement the node's in-degree 
            inDegree[child]--; 
            if (inDegree[child] == 0) { 
                sources.push(child); 
            } 
        } 
    } 

    // Compare the sizes of sortedOrder 
    // and the original sequence 
    return sortedOrder.size() == originalSeq.size(); 
} 

int main(int argc, char* argv[]) 
{ 
    vector<int> arr = { 1, 2, 6, 7, 3, 5, 4 }; 
    vector<vector<int> > seqs = { { 1, 2, 3 }, 
                                { 7, 3, 5 }, 
                                { 1, 6, 3, 4 }, 
                                { 2, 6, 5, 4 } }; 
    bool result = canConstruct(arr, seqs); 
    if (result) 
        cout << "Yes" << endl; 
    else
        cout << "No" << endl; 
} 

```