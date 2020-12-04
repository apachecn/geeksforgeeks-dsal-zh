# 检查数组是否只能使用给定索引之间的交换进行排序

> 原文： [https://www.geeksforgeeks.org/check-if-the-array-can-be-sorted-using-swaps-between-given-indices-only/](https://www.geeksforgeeks.org/check-if-the-array-can-be-sorted-using-swaps-between-given-indices-only/)

给定大小为`N`的数组`arr[]`，该数组由以随机顺序排列的`[0, N – 1]`范围内的不同整数组成。 还给出了几对，其中每对表示可以交换数组元素的索引。 允许的交换数量没有限制。 任务是查找是否有可能使用这些交换以升序排列数组。 如果可能，请打印`Yes`，否则打印`No`。

**示例**：

> **输入**：`arr[] = {0, 4, 3, 2, 1, 5}, pairs[][] = {{1, 4}, {2, 3}}`
>
> **输出**：`Yes`
>
> `swap(arr[1], arr[4]) -> arr[] = {0, 1, 3, 2, 4, 5}`
>
> `swap(arr[2], arr[3]) -> arr[] = {0, 1, 2, 3, 4, 5}`
> 
> **输入**：`arr[] = {1,2,3,0,4}, pairs[][] = {{2, 3}}`
>
> **输出**：`No`

**方法**：给定的问题可以视为图问题，其中`N`表示图中的节点总数，每个交换对表示图中的无向边。 我们必须找出是否有可能以`{0, 1, 2, 3, …, N – 1}`的形式转换输入数组。

让我们将上面的数组称为`B`。现在找出两个数组的所有连通组件，如果元素至少在一个组件上不同，则答案为`No`否则答案为`Yes`。

下面是上述方法的实现：

## CPP

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function that returns true if the array elements 
// can be sorted with the given operation 
bool canBeSorted(int N, vector<int> a, int P,  
vector<pair<int, int> > vp) 
{ 

    // To create the adjacency list of the graph 
    vector<int> v[N]; 

    // Boolean array to mark the visited nodes 
    bool vis[N] = { false }; 

    // Creating adjacency list for undirected graph 
    for (int i = 0; i < P; i++) { 
        v[vp[i].first].push_back(vp[i].second); 
        v[vp[i].second].push_back(vp[i].first); 
    } 

    for (int i = 0; i < N; i++) { 

        // If not already visited 
        // then apply BFS 
        if (!vis[i]) { 
            queue<int> q; 
            vector<int> v1; 
            vector<int> v2; 

            // Set visited to true 
            vis[i] = true; 

            // Push the node to the queue 
            q.push(i); 

            // While queue is not empty 
            while (!q.empty()) { 
                int u = q.front(); 
                v1.push_back(u); 
                v2.push_back(a[u]); 
                q.pop(); 

                // Check all the adjacent nodes 
                for (auto s : v[u]) { 

                    // If not visited 
                    if (!vis[s]) { 

                        // Set visited to true 
                        vis[s] = true; 
                        q.push(s); 
                    } 
                } 
            } 
            sort(v1.begin(), v1.end()); 
            sort(v2.begin(), v2.end()); 

            // If the connected component does not 
            // contain same elements then return false 
            if (v1 != v2) 
                return false; 
        } 
    } 
    return true; 
} 

// Driver code 
int main() 
{ 
    vector<int> a = { 0, 4, 3, 2, 1, 5 }; 
    int n = a.size(); 
    vector<pair<int, int> > vp = { { 1, 4 }, { 2, 3 } }; 
    int p = vp.size(); 

    if (canBeSorted(n, a, p, vp)) 
        cout << "Yes"; 
    else
        cout << "No"; 

    return 0; 
} 

```