# 两市单源最短路径

> 原文:[https://www . geesforgeks . org/单源-两个城市间最短路径/](https://www.geeksforgeeks.org/single-source-shortest-path-between-two-cities/)

给定一个 **N** 节点和 **E** 边的图形，其形式为 **{U，V，W}** ，使得在 **U 和 V** 之间存在一条边，权重为 **W** 。给你一个整数 **K** 和源 **src** 和目的地 **dst** 。任务是从 **K** 站找到从给定源到目的地最便宜的成本路径。
**例:**

> **输入:** N = 3，边= [[0，1，100]，[1，2，100]，[0，2，500]]，src = 0，dst = 2，k = 1
> **输出:** 200
> **说明:**
> 最便宜的价格是从城市 0 到城市 2。只需一站，只需 200 英镑，这就是我们的产量。
> **输入:** N = 3，边= [[0，1，100]，[1，2，100]，[0，2，500]]，src = 0，dst = 2，k = 0
> **输出:** 500

**方法一:使用** [**深度优先搜索**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

1.  探索当前节点并继续探索其子节点。
2.  使用[地图](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以停靠点和距离为值成对存储访问节点。
3.  如果该键存在于映射中，则断开递归树。
4.  找到每个递归树的答案(最小成本)并返回。

下面是我们方法的实现。

## C++

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

    // Resize Adjacency Matrix
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

## 蟒蛇 3

```
# Python3 program for the above approach

# DFS memoization
adjMatrix=[]
mp=dict()

# Function to implement DFS Traversal
def DFSUtility(node, stops, dst, cities):
    # Base Case
    if (node == dst):
        return 0

    if (stops < 0) :
        return 1e9

    key=(node, stops)

    # Find value with key in a map
    if key in mp:
        return mp[key]

    ans = 1e9

    # Traverse adjacency matrix of
    # source node
    for neighbour in range(cities):
        weight = adjMatrix[node][neighbour]

        if (weight > 0) :

            # Recursive DFS call for
            # child node
            minVal = DFSUtility(neighbour, stops - 1, dst, cities)

            if (minVal + weight > 0):
                ans = min(ans, minVal + weight)

    mp[key] = ans

    # Return ans
    return ans

# Function to find the cheapest price
# from given source to destination
def findCheapestPrice(cities, flights, src, dst, stops):
    global adjMatrix
    # Resize Adjacency Matrix
    adjMatrix=[[0]*(cities + 1) for _ in range(cities + 1)]

    # Traverse flight[][]
    for item in flights:
        # Create Adjacency Matrix
        adjMatrix[item[0]][item[1]] = item[2]

    # DFS Call to find shortest path
    ans = DFSUtility(src, stops, dst, cities)

    # Return the cost
    return -1 if ans >= 1e9 else int(ans)

# Driver Code
if __name__ == '__main__':
    # Input flight : :Source,
    # Destination, Cost
    flights = [[ 4, 1, 1 ],[ 1, 2, 3] , [ 0, 3, 2] , [ 0, 4, 10] , [ 3, 1, 1] , [ 1, 4, 3]] 

    # vec, n, stops, src, dst
    stops = 2
    totalCities = 5
    sourceCity = 0
    destCity = 4

    # Function Call
    ans = findCheapestPrice(
        totalCities, flights,
        sourceCity, destCity,
        stops)

    print(ans)
```

**Output:** 

```
6
```

**时间复杂度:** O(V + E)，其中 V 为节点数，E 为边数。
**辅助空间:** O(V)

**方法二:使用** [广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)

1.  想法是使用[队列](http://www.geeksforgeeks.org/queue-data-structure/)执行 BFS 遍历。
2.  从当前节点执行遍历，并在队列中插入根节点。
3.  遍历队列并浏览当前节点及其同级节点。然后在队列中插入该节点的兄弟节点。
4.  同时探索每个兄弟，如果开销较小，则继续推送队列中的条目，并更新最小开销。
5.  打印上述遍历后的最小成本。

下面是我们方法的实现:

## C++

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

## 蟒蛇 3

```
# Python3 program of the above approach

from queue import Queue as Q
# Function to implement BFS
def findCheapestPrice(cities, flights, src, dst, stops):
    adjList=dict()

    # Traverse flight[][]
    for flight in flights :

        # Create Adjacency Matrix
        if flight[0] in adjList:
            adjList[flight[0]].append(
                (flight[1], flight[2]))
        else:
            adjList[flight[0]]=[(flight[1], flight[2])]

    q=Q()
    q.put((src, 0))

    # Store the Result
    srcDist = 1e9
    # Traversing the Matrix
    while (not q.empty() and stops >= 0) :
        stops-=1

        for i in range(q.qsize()) :
            curr = q.get()

            for nxt in adjList[curr[0]]:

                # If source distance is already
                # least the skip this iteration
                if (srcDist < curr[1] + nxt[1]):
                    continue

                q.put((nxt[0],curr[1] + nxt[1]))

                if (dst == nxt[0]):
                    srcDist = min( srcDist, curr[1] + nxt[1])

    # Returning the Answer
    return -1 if srcDist == 1e9 else srcDist

# Driver Code
if __name__ == '__main__':
    # Input flight : :Source,
    # Destination, Cost
    flights= [[ 4, 1, 1 ],[ 1, 2, 3] , [ 0, 3, 2] , [ 0, 4, 10] , [ 3, 1, 1] , [ 1, 4, 3]] 

    # vec, n, stops, src, dst
    stops = 2
    totalCities = 5

    # Given source and destination
    sourceCity = 0
    destCity = 4

    # Function Call
    ans = findCheapestPrice(
        totalCities, flights,
        sourceCity, destCity,
        stops)
    print(ans)
```

**Output:** 

```
6
```

**时间复杂度:** O(停靠点* N * N)其中 N 是排队的城市和规模的乘积
T3】辅助空间: O(N)

**方法三:使用** [迪克斯特拉算法](https://www.geeksforgeeks.org/c-program-for-dijkstras-shortest-path-algorithm-greedy-algo-7/)

1.  更新所有顶点与源的距离。
2.  与源没有直接连接的顶点用无穷大标记，直接连接的顶点用正确的距离更新。
3.  从源开始，提取下一个最小顶点。这将确保最低成本。
4.  每一步做边缘放松: ***D 表示距离****w 表示重量***
    1.  如果 D[u] + w(u，z) < D[z]，那么
    2.  D[z] = D[u] + w(u，z)

下面是我们方法的实现:

## C++

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

## 蟒蛇 3

```
# Python3 program for the above approach
import heapq as hq

def findCheapestPrice(cities, flights, src, dst, stops):
    # Adjacency Matrix
    adjList = [[] for _ in range(cities)]
    # Traverse flight[][]
    for flight in flights:
        # Create Adjacency Matrix
        adjList[flight[0]].append((flight[1], flight[2]))

    # Implementing Priority Queue
    pq = []

    t = (0, src, stops)
    hq.heappush(pq, t)

    # While PQ is not empty
    while (pq):
        t = hq.heappop(pq)

        if (src == dst):
            return 0

        cost, current, stop = t

        if (current == dst):

            # Return the Answer
            return cost

        if (stop >= 0):
            for nxt in adjList[current]:

                t = ((cost + nxt[1]), nxt[0], stop - 1)
                hq.heappush(pq, t)
    return -1

if __name__ == '__main__':
    # Input flight : :Source,
    # Destination, Cost
    flights = [[4, 1, 1], [1, 2, 3], [0, 3, 2],
               [0, 4, 10], [3, 1, 1], [1, 4, 3]]

    # vec, n, stops, src, dst
    stops = 2
    totalCities = 5

    # Given source and destination
    sourceCity = 0
    destCity = 4

    # Function Call
    ans = findCheapestPrice(
        totalCities, flights,
        sourceCity, destCity, stops)
    print(ans)
```

**Output:** 

```
6
```

**时间复杂度:** O(E+V log V)，其中 V 为节点数，E 为边数。
**辅助空间:** O(V)

**方法四:使用** [贝尔蒙福特](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

1.  将从源到所有顶点的距离初始化为无穷大，到源本身的距离初始化为 0。
2.  在每一步做边缘放松:D 表示距离，w 表示重量
    *   如果 D[u] + w(u，z) < D[z]，那么 D[z] = D[u] + w(u，z)
3.  该算法已被修改，以解决给定的问题，而不是放松图 V-1 次，我们将为给定的停止次数。

以下是上述方法的实施

## C++

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
    // Distance from source to all other nodes
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

## 蟒蛇 3

```
# Python3 program of the above Approach

# Function to find the cheapest cost
# from source to destination using K stops
def findCheapestPrice(cities, flights, src, dst, stops):
    # Distance from source to all other nodes
    dist=[1e9]*cities
    dist[src] = 0

    # Do relaxation for V-1 vertices
    # here we need for K stops so we
    # will do relaxation for k+1 stops
    for i in range(stops):

        intermediate=dist

        for flight in flights:

            if (dist[flight[0]] != 1e9) :
                intermediate[flight[1]] = min(intermediate[flight[1]], dist[flight[0]] + flight[2])

        # Update the distance vector
        dist = intermediate

    # Return the final cost
    return -1 if dist[dst] == 1e9 else dist[dst]

# Driver Code
if __name__ == '__main__':
    # Input flight : :Source, Destination, Cost
    flights = [[4, 1, 1], [1, 2, 3], [0, 3, 2],
               [0, 4, 10], [3, 1, 1], [1, 4, 3]]

    # vec, n, stops, src, dst
    stops = 2
    totalCities = 5

    # Given source and destination
    sourceCity = 0
    destCity = 4

    # Function Call
    ans = findCheapestPrice(
        totalCities, flights,
        sourceCity, destCity, stops)
    print(ans)
```

**Output:** 

```
6
```

**时间复杂度:** O(E*V)，其中 V 为节点数，E 为边数。
**辅助空间:** O(V)