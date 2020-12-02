# 两个城市之间的单一来源最短路径

> 原文： [https://www.geeksforgeeks.org/single-source-shortest-path-between-two-cities/](https://www.geeksforgeeks.org/single-source-shortest-path-between-two-cities/)

给定 **N** 个节点和 **E** 边的图，形式为 **{U，V，W}** ，这样在 **U 和 V 之间存在边** 的重量为 **W** 。 给您一个整数 **K** 以及源 **src** 和目标 **dst** 。 任务是找到从 **K** 停靠点到给定源到目的地的最便宜成本路径。

**示例：**

> **输入：** N = 3，边线= [[0，1，100]，[1,2,100]，[0，2，500]]，src = 0，dst = 2，k = 1
> **输出：** 200
> **解释：**
> 最便宜的价格是从城市 0 到城市 2。只需一站，它的价格为 200，这是我们的 输出。
> 
> **输入：** N = 3，边线= [[0，1，100]，[1,2,100]，[0，2，500]]，src = 0，dst = 2，k = 0
> **输出：** 500

**方法 1：使用** [**深度优先搜索**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

1.  探索当前节点，并继续探索其子节点。
2.  使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以成对的形式存储访问的节点，并以停靠点和距离作为值。
3.  如果键存在于地图中，则打破递归树。
4.  找到每个递归树的答案（最低成本）并将其返回。

下面是我们方法的实现：

## C ++

```

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure to implement hashing to 
// stores pairs in map 
struct pair_hash { 
    template <class T1, class T2> 
    std::size_t
    operator()(const std::pair<T1, T2>& pair) const
    { 
        return std::hash<T1>()(pair.first) 
               ^ std::hash<T2>()(pair.second); 
    } 
}; 

// DFS memoization 
vector<vector<int> > adjMatrix; 
typedef std::pair<int, int> pair1; 
unordered_map<pair1, int, pair_hash> mp; 

// Function to implement DFS Traversal 
long DFSUtility(int node, int stops, 
                int dst, int cities) 
{ 
    // Base Case 
    if (node == dst) 
        return 0; 

    if (stops < 0) { 
        return INT_MAX; 
    } 

    pair<int, int> key(node, stops); 

    // Find value with key in a map 
    if (mp.find(key) != mp.end()) { 
        return mp[key]; 
    } 

    long ans = INT_MAX; 

    // Traverse adjacency matrix of 
    // source node 
    for (int neighbour = 0; 
         neighbour < cities; 
         ++neighbour) { 

        long weight 
            = adjMatrix[node][neighbour]; 

        if (weight > 0) { 

            // Recursive DFS call for 
            // child node 
            long minVal 
                = DFSUtility(neighbour, 
                             stops - 1, 
                             dst, cities); 

            if (minVal + weight > 0) 
                ans = min(ans, 
                          minVal 
                              + weight); 
        } 
    } 

    mp[key] = ans; 

    // Return ans 
    return ans; 
} 

// Function to find the cheapest price 
// from given source to destination 
int findCheapestPrice(int cities, 
                      vector<vector<int> >& flights, 
                      int src, int dst, int stops) 
{ 

    // Resize Adjacency Marix 
    adjMatrix.resize(cities + 1, 
                     vector<int>(cities + 1, 0)); 

    // Traverse flight[][] 
    for (auto item : flights) { 
        // Create Adjacency Matrix 
        adjMatrix[item[0]][item[1]] = item[2]; 
    } 

    // DFS Call to find shortest path 
    long ans = DFSUtility(src, stops, 
                          dst, cities); 

    // Return the cost 
    return ans >= INT_MAX ? -1 : (int)ans; 
    ; 
} 

// Driver Code 
int main() 
{ 
    // Input flight : {Source, 
    // Destination, Cost} 
    vector<vector<int> > flights 
        = { { 4, 1, 1 }, { 1, 2, 3 }, { 0, 3, 2 }, { 0, 4, 10 }, { 3, 1, 1 }, { 1, 4, 3 } }; 

    // vec, n, stops, src, dst 
    int stops = 2; 
    int totalCities = 5; 
    int sourceCity = 0; 
    int destCity = 4; 

    // Function Call 
    long ans = findCheapestPrice( 
        totalCities, flights, 
        sourceCity, destCity, 
        stops); 

    cout << ans; 
    return 0; 
} 

```

**Output:**

```
6

```

**时间复杂度：** O（V + E），其中 V 是节点数，E 是边缘。
**辅助空间：** O（V）

**方法 2：使用** [广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)

1.  这个想法是使用[队列](http://www.geeksforgeeks.org/queue-data-structure/)执行 BFS 遍历。
2.  从当前节点执行遍历，并将根节点插入队列。
3.  遍历队列并浏览当前节点及其同级节点。 然后将节点的同级节点插入队列。
4.  在探索每个同级时，如果成本较低，则继续在队列中推送条目，并更新最低成本。
5.  经过上述遍历后，打印最低成本。

下面是我们方法的实现：

## C ++

```

// C++ program of the above approach 
#include <bits/stdc++.h> 
#include <iostream> 
#include <queue> 
#include <tuple> 
#include <unordered_map> 

using namespace std; 
// BSF Memoization 
typedef tuple<int, int, int> tupl; 

// Function to implement BFS 
int findCheapestPrice(int cities, 
                      vector<vector<int> >& flights, 
                      int src, int dst, int stops) 
{ 
    unordered_map<int, 
                  vector<pair<int, int> > > 
        adjList; 

    // Traverse flight[][] 
    for (auto flight : flights) { 

        // Create Adjacency Matrix 
        adjList[flight[0]].push_back( 
            { flight[1], flight[2] }); 
    } 

    // < city, distancefromsource > pair 
    queue<pair<int, int> > 
        q; 
    q.push({ src, 0 }); 

    // Store the Result 
    int srcDist = INT_MAX; 

    // Traversing the Matrix 
    while (!q.empty() && stops-- >= 0) { 

        int qSize = q.size(); 

        for (int i = 0; i < qSize; i++) { 
            pair<int, int> curr = q.front(); 
            q.pop(); 

            for (auto next : adjList[curr.first]) { 

                // If source distance is already 
                // least the skip this iteration 
                if (srcDist < curr.second 
                                  + next.second) 
                    continue; 

                q.push({ next.first, 
                         curr.second 
                             + next.second }); 

                if (dst == next.first) { 
                    srcDist = min( 
                        srcDist, curr.second 
                                     + next.second); 
                } 
            } 
        } 
    } 

    // Returning the Answer 
    return srcDist == INT_MAX ? -1 : srcDist; 
} 

// Driver Code 
int main() 
{ 
    // Input flight : {Source, 
    // Destination, Cost} 
    vector<vector<int> > flights 
        = { { 4, 1, 1 }, { 1, 2, 3 }, { 0, 3, 2 }, { 0, 4, 10 }, { 3, 1, 1 }, { 1, 4, 3 } }; 

    // vec, n, stops, src, dst 
    int stops = 2; 
    int totalCities = 5; 

    // Given source and destination 
    int sourceCity = 0; 
    int destCity = 4; 

    // Function Call 
    long ans = findCheapestPrice( 
        totalCities, flights, 
        sourceCity, destCity, 
        stops); 
    cout << ans; 
    return 0; 
} 

```

**Output:**

```
6

```

**时间复杂度：** O（Stops * N * N），其中 N 是队列中城市和规模的乘积
**辅助空间：** O（N）

**方法 3：使用** [Dijkstra 算法](https://www.geeksforgeeks.org/c-program-for-dijkstras-shortest-path-algorithm-greedy-algo-7/)

1.  更新所有顶点到源的距离。
2.  未从源直接连接的顶点将标记为无穷大，并且将以正确的距离更新直接连接的顶点。
3.  从源开始，然后提取下一个最小顶点。 这样可以确保最低的成本。
4.  在每个步骤进行边缘松弛： ***D 表示距离**， **w 表示权重***
    1.  如果 D [u] + w（u，z）
    2.  D [z] = D [u] + w（u，z）

这是我们方法的实现：

## C ++

```

// C++ program for the above approach 
#include <bits/stdc++.h> 
#include <tuple> 
using namespace std; 

typedef tuple<int, int, int> tupl; 
long findCheapestPrice(int cities, 
                       vector<vector<int> >& flights, 
                       int src, int dst, int stops) 
{ 
    // Adjacency Matrix 
    vector<vector<pair<int, int> > > adjList(cities); 

    // Traverse flight[][] 
    for (auto flight : flights) { 
        // Create Adjacency Matrix 
        adjList[flight[0]].push_back( 
            { flight[1], flight[2] }); 
    } 

    // Implementing Priority Queue 
    priority_queue<tupl, vector<tupl>, 
                   greater<tupl> > 
        pq; 

    tupl t = make_tuple(0, src, stops); 
    pq.push(t); 

    // While PQ is not empty 
    while (!pq.empty()) { 
        tupl t = pq.top(); 
        pq.pop(); 

        if (src == dst) 
            return 0; 

        int cost = get<0>(t); 
        int current = get<1>(t); 
        int stop = get<2>(t); 

        if (current == dst) 

            // Return the Answer 
            return cost; 

        if (stop >= 0) { 
            for (auto next : adjList[current]) { 

                tupl t = make_tuple((cost 
                                     + next.second), 
                                    next.first, 
                                    stop - 1); 
                pq.push(t); 
            } 
        } 
    } 
    return -1; 
} 

int main() 
{ 
    // Input flight : {Source, 
    // Destination, Cost} 
    vector<vector<int> > flights 
        = { { 4, 1, 1 }, { 1, 2, 3 }, { 0, 3, 2 }, { 0, 4, 10 }, { 3, 1, 1 }, { 1, 4, 3 } }; 

    // vec, n, stops, src, dst 
    int stops = 2; 
    int totalCities = 5; 

    // Given source and destination 
    int sourceCity = 0; 
    int destCity = 4; 

    // Function Call 
    long ans = findCheapestPrice( 
        totalCities, flights, 
        sourceCity, destCity, stops); 
    cout << ans; 
    return 0; 
} 

```

**Output:**

```
6

```

**时间复杂度：** O（E + V log V）其中 V 是节点数，E 是边。
**辅助空间：** O（V）

**方法 4：使用** [Bellmon Ford](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

 **1.  初始化从源到所有顶点的距离为无穷远，到源本身的距离为 0。
2.  在每个步骤进行边缘松弛：D 表示距离，w 表示权重
    *   如果 D [u] + w（u，z）
3.  对该算法进行了修改以解决给定的问题，而不是放宽图表 V-1 的次数，我们将针对给定的停止次数进行处理。

下面是上述方法的实现

## C ++

```

// C++ program of the above Approach 
#include <bits/stdc++.h> 
#include <vector> 
using namespace std; 

// Function to find the cheapest cost 
// from source to destination using K stops 
int findCheapestPrice(int cities, 
                      vector<vector<int> >& flights, 
                      int src, int dst, int stops) 
{ 
    // Dstance from source to all other nodes 
    vector<int> dist(cities, INT_MAX); 
    dist[src] = 0; 

    // Do relaxation for V-1 vertices 
    // here we need for K stops so we 
    // will do relaxation for k+1 stops 
    for (int i = 0; i <= stops; i++) { 

        vector<int> intermediate(dist); 

        for (auto flight : flights) { 

            if (dist[flight[0]] != INT_MAX) { 
                intermediate[flight[1]] 
                    = min(intermediate[flight[1]], 
                          dist[flight[0]] 
                              + flight[2]); 
            } 
        } 

        // Update the distance vector 
        dist = intermediate; 
    } 

    // Return the final cost 
    return dist[dst] == INT_MAX ? -1 : dist[dst]; 
} 

// Driver Code 
int main() 
{ 
    // Input flight : {Source, Destination, Cost} 
    vector<vector<int> > flights 
        = { { 4, 1, 1 }, { 1, 2, 3 }, { 0, 3, 2 }, { 0, 4, 10 }, { 3, 1, 1 }, { 1, 4, 3 } }; 

    // vec, n, stops, src, dst 
    int stops = 2; 
    int totalCities = 5; 

    // Given source and destination 
    int sourceCity = 0; 
    int destCity = 4; 

    // Function Call 
    long ans = findCheapestPrice( 
        totalCities, flights, sourceCity, 
        destCity, stops); 
    cout << ans; 
    return 0; 
} 

```

**Output:**

```
6

```

**时间复杂度：** O（E * V）其中 V 是节点数，E 是边。
**辅助空间：** O（V）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。**