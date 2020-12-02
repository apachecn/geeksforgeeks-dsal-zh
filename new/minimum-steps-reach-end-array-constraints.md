# 在约束

下达到数组末尾的最小步骤

> 原文： [https://www.geeksforgeeks.org/minimum-steps-reach-end-array-constraints/](https://www.geeksforgeeks.org/minimum-steps-reach-end-array-constraints/)

给定一个仅包含一个数字的数组，假设我们站在第一个索引处，我们需要使用最少的步数到达数组末尾，其中一步可以跳转到邻居索引或可以跳到具有相同值的位置 。

换句话说，如果我们在索引 i 处，那么您可以一步一步到达 arr [i-1]或 arr [i + 1]或 arr [K]，从而 arr [K] = arr [i]（ arr [K]的值与 arr [i]相同）

**示例**：

```
Input : arr[] = {5, 4, 2, 5, 0}
Output : 2
Explanation : Total 2 step required.
We start from 5(0), in first step jump to next 5 
and in second step we move to value 0 (End of arr[]).

Input  : arr[] = [0, 1, 2, 3, 4, 5, 6, 7, 5, 4,
                 3, 6, 0, 1, 2, 3, 4, 5, 7]
Output : 5
Explanation : Total 5 step required.
0(0) -> 0(12) -> 6(11) -> 6(6) -> 7(7) ->
(18)                                                          
(inside parenthesis indices are shown)

```

可以使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 解决此问题。 我们可以将给定的数组视为未加权图，其中每个顶点在下一个和上一个数组元素上都有两个边，而在具有相同值的数组元素上有更多边。 现在，为了快速处理第三种类型的边缘，我们保留 10 个[向量](http://quiz.geeksforgeeks.org/vector-sequence-containers-the-c-standard-template-library-stl-set-1/)，这些向量存储所有存在数字 0 至 9 的索引。 在上面的示例中，对应于 0 的向量将存储[0，12]，2 个索引，其中给定数组中发生了 0。
使用了另一个布尔数组，因此我们不会多次访问同一索引。 由于我们正在使用 BFS，并且 BFS 逐级进行，因此可以保证最佳的最小步长。

## C++

```cpp

// C++ program to find minimum jumps to reach end 
// of array 
#include <bits/stdc++.h> 
using namespace std; 

//  Method returns minimum step to reach end of array 
int getMinStepToReachEnd(int arr[], int N) 
{ 
    // visit boolean array checks whether current index 
    // is previously visited 
    bool visit[N]; 

    // distance array stores distance of current 
    // index from starting index 
    int distance[N]; 

    // digit vector stores indices where a 
    // particular number resides 
    vector<int> digit[10]; 

    //  In starting all index are unvisited 
    memset(visit, false, sizeof(visit)); 

    //  storing indices of each number in digit vector 
    for (int i = 1; i < N; i++) 
        digit[arr[i]].push_back(i); 

    //  for starting index distance will be zero 
    distance[0] = 0; 
    visit[0] = true; 

    // Creating a queue and inserting index 0\. 
    queue<int> q; 
    q.push(0); 

    //  loop untill queue in not empty 
    while(!q.empty()) 
    { 
        // Get an item from queue, q. 
        int idx = q.front();        q.pop(); 

        //  If we reached to last index break from loop 
        if (idx == N-1) 
            break; 

        // Find value of dequeued index 
        int d = arr[idx]; 

        // looping for all indices with value as d. 
        for (int i = 0; i<digit[d].size(); i++) 
        { 
            int nextidx = digit[d][i]; 
            if (!visit[nextidx]) 
            { 
                visit[nextidx] = true; 
                q.push(nextidx); 

                //  update the distance of this nextidx 
                distance[nextidx] = distance[idx] + 1; 
            } 
        } 

        // clear all indices for digit d, because all 
        // of them are processed 
        digit[d].clear(); 

        //  checking condition for previous index 
        if (idx-1 >= 0 && !visit[idx - 1]) 
        { 
            visit[idx - 1] = true; 
            q.push(idx - 1); 
            distance[idx - 1] = distance[idx] + 1; 
        } 

        //  checking condition for next index 
        if (idx + 1 < N && !visit[idx + 1]) 
        { 
            visit[idx + 1] = true; 
            q.push(idx + 1); 
            distance[idx + 1] = distance[idx] + 1; 
        } 
    } 

    //  N-1th position has the final result 
    return distance[N - 1]; 
} 

//  driver code to test above methods 
int main() 
{ 
    int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 5, 
                 4, 3, 6, 0, 1, 2, 3, 4, 5, 7}; 
    int N = sizeof(arr) / sizeof(int); 
    cout << getMinStepToReachEnd(arr, N); 
    return 0; 
} 

```