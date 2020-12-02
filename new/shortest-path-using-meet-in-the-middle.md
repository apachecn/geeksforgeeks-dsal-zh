# 使用中间开会的最短路径

> 原文： [https://www.geeksforgeeks.org/shortest-path-using-meet-in-the-middle/](https://www.geeksforgeeks.org/shortest-path-using-meet-in-the-middle/)

给定一个排列 **P = p <sub>1</sub> ，p <sub>2</sub> ，…。，第一个`n`自然的 p <sub>n</sub>** 数字**（1≤n≤10）**。 一个人可以交换任意两个连续的元素 **p <sub>i</sub>** 和 **p <sub>i + 1</sub>** **（1≤i < n）** 。 任务是找到将`P`更改为另一个排列 **P'= p' <sub>1</sub> ，p' <sub>2</sub> 等的最小交换次数。 ，p' <sub>n</sub>** 。

**示例**：

> **输入**：P =“ 213”，P'=“ 321”
> **输出**：2
> 213 <-> 231 <-> 321
> ![](img/59af6c0b7b39cd3f34f68fefce2f906f.png)
> 
> **输入**：P =“ 1234”，P'=“ 4123”
> **输出**：3

**方法**：可以使用 [Dijkstra 最短路径算法解决。](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/) 语句中似乎没有与图形相关的内容。 但是假设一个排列是一个顶点，那么排列元素的每次交换都是一条边，该边将该顶点与另一个顶点连接起来。 因此，现在找到最小交换数成为一个简单的 BFS /最短路径问题。
现在，我们来分析时间复杂度。 我们有 **n！** 顶点，每个顶点具有 **n – 1** 个相邻顶点。 我们还必须存储通过地图访问过的顶点，因为它们的表示很难被普通数组存储。 因此，总时间复杂度为 **O（N log（N！）* N！）**。 [中间开会](https://www.geeksforgeeks.org/meet-in-the-middle/)技术可用于加快解决方案的速度。
中间相遇解决方案与 Dijkstra 的解决方案类似，但有所修改。

*   令`P`为起始顶点， **P'**为终点。
*   让起点和终点都扎根。 我们从两个根目录开始 BFS，同时开始和结束，但仅使用一个队列。
*   将开始和结束推送到队列的后方，**已访问<sub>开始</sub> =已访问<sub>完成</sub> = true** 。
*   令 **src <sub>u</sub>** 成为 BFS 进程中顶点 u 的根。 因此， **src <sub>开始</sub> =开始，而 src <sub>完成</sub> =完成**。
*   假设 **D <sub>u</sub>** 是顶点`u`到树根的最短距离。 因此 **D <sub>开始</sub> = D <sub>完成</sub> = 0** 。
*   当队列不为空时，弹出队列的前端为`u`，然后推入所有与`u`相邻但尚未访问过的顶点`v`]（访问过 <sub>v</sub> =否）进入队列的后面，然后让 **D <sub>v</sub> = D <sub>u</sub> + 1** ， **src <sub>v</sub> = src <sub>u</sub>** 和**访问过 <sub>v</sub> = true** 。 特别是，如果访问了`v`，并且 **src <sub>v</sub> ！= src <sub>u</sub>** ，那么我们可以立即返回 **D <sub>u</sub> + D <sub>v</sub> +1** 。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find minimum number of 
// swaps to make another permutation 
int ShortestPath(int n, string start, string finish) 
{ 
    unordered_map<string, bool> visited; 
    unordered_map<string, int> D; 
    unordered_map<string, string> src; 

    visited[start] = visited[finish] = true; 
    D[start] = D[finish] = 0; 
    src[start] = start; 
    src[finish] = finish; 

    queue<string> q; 
    q.push(start); 
    q.push(finish); 

    while (!q.empty()) { 

        // Take top vertex of the queue 
        string u = q.front(); 
        q.pop(); 

        // Generate n - 1 of it's permutations 
        for (int i = 1; i < n; i++) { 

            // Generate next permutation 
            string v = u; 
            swap(v[i], v[i - 1]); 

            // If v is not visited 
            if (!visited[v]) { 

                // Set it visited 
                visited[v] = true; 

                // Make root of u and root of v equal 
                src[v] = src[u]; 

                // Increment it's distance by 1 
                D[v] = D[u] + 1; 

                // Push this vertex into queue 
                q.push(v); 
            } 

            // If it is already visited 
            // and roots are different 
            // then answer is found 
            else if (src[u] != src[v]) 
                return D[u] + D[v] + 1; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    string p1 = "1234", p2 = "4123"; 
    int n = p1.length(); 
    cout << ShortestPath(n, p1, p2); 

    return 0; 
} 

```