# 统一费用搜索（大图为 Dijkstra）

> 原文： [https://www.geeksforgeeks.org/uniform-cost-search-dijkstra-for-large-graphs/](https://www.geeksforgeeks.org/uniform-cost-search-dijkstra-for-large-graphs/)

[统一费用搜索](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm#Practical_optimizations_and_infinite_graphs)是 [Dijikstra 算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)的变体。 在这里，我们没有插入所有顶点到优先级队列中，而是仅插入源，然后在需要时一个接一个地插入。 在每一步中，我们都会检查项目是否已经在优先级队列中（使用访问数组）。 如果是，则执行减少键，否则将其插入。
Dijsktra 的这种变体对于无限图和太大而无法在内存中表示的图很有用。 统一成本搜索主要用于人工智能。

**示例**：

```
Input :

Output :
Minimum cost from S to G is =3

```

统一费用搜索与 Dijikstra 的算法相似。 在此算法中，从开始状态开始，我们将访问相邻状态并选择成本最低的状态，然后从访问状态的所有未访问状态和相邻状态中选择下一个成本最低的状态，这样我们将尝试 达到目标状态（请注意，我们不会继续通过目标状态的路径），即使我们达到目标状态，我们也会继续搜索其他可能的路径（如果有多个目标）。 我们将保留一个优先级队列，该队列将为所有被访问状态的相邻状态提供最廉价的下一个状态。

```

// C++ implemenatation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// graph 
vector<vector<int> > graph; 

// map to store cost of edges 
map<pair<int, int>, int> cost; 

// returns the minimum cost in a vector( if  
// there are multiple goal states) 
vector<int> uniform_cost_search(vector<int> goal, int start) 
{ 
    // minimum cost upto 
    // goal state from starting 
    // state 
    vector<int> answer; 

    // create a priority queue 
    priority_queue<pair<int, int> > queue; 

    // set the answer vector to max value 
    for (int i = 0; i < goal.size(); i++) 
        answer.push_back(INT_MAX); 

    // insert the starting index 
    queue.push(make_pair(0, start)); 

    // map to store visited node 
    map<int, int> visited; 

    // count 
    int count = 0; 

    // while the queue is not empty 
    while (queue.size() > 0) { 

        // get the top element of the  
        // priority queue 
        pair<int, int> p = queue.top(); 

        // pop the element 
        queue.pop(); 

        // get the original value 
        p.first *= -1; 

        // check if the element is part of 
        // the goal list 
        if (find(goal.begin(), goal.end(), p.second) != goal.end()) { 

            // get the position 
            int index = find(goal.begin(), goal.end(),  
                             p.second) - goal.begin(); 

            // if a new goal is reached 
            if (answer[index] == INT_MAX) 
                count++; 

            // if the cost is less 
            if (answer[index] > p.first) 
                answer[index] = p.first; 

            // pop the element 
            queue.pop(); 

            // if all goals are reached 
            if (count == goal.size()) 
                return answer; 
        } 

        // check for the non visited nodes 
        // which are adjacent to present node 
        if (visited[p.second] == 0) 
            for (int i = 0; i < graph[p.second].size(); i++) { 

                // value is multiplied by -1 so that  
                // least priority is at the top 
                queue.push(make_pair((p.first +  
                  cost[make_pair(p.second, graph[p.second][i])]) * -1,  
                  graph[p.second][i])); 
            } 

        // mark as visited 
        visited[p.second] = 1; 
    } 

    return answer; 
} 

// main function 
int main() 
{ 
    // create the graph 
    graph.resize(7); 

    // add edge 
    graph[0].push_back(1); 
    graph[0].push_back(3); 
    graph[3].push_back(1); 
    graph[3].push_back(6); 
    graph[3].push_back(4); 
    graph[1].push_back(6); 
    graph[4].push_back(2); 
    graph[4].push_back(5); 
    graph[2].push_back(1); 
    graph[5].push_back(2); 
    graph[5].push_back(6); 
    graph[6].push_back(4); 

    // add the cost 
    cost[make_pair(0, 1)] = 2; 
    cost[make_pair(0, 3)] = 5; 
    cost[make_pair(1, 6)] = 1; 
    cost[make_pair(3, 1)] = 5; 
    cost[make_pair(3, 6)] = 6; 
    cost[make_pair(3, 4)] = 2; 
    cost[make_pair(2, 1)] = 4; 
    cost[make_pair(4, 2)] = 4; 
    cost[make_pair(4, 5)] = 3; 
    cost[make_pair(5, 2)] = 6; 
    cost[make_pair(5, 6)] = 3; 
    cost[make_pair(6, 4)] = 7; 

    // goal state 
    vector<int> goal; 

    // set the goal 
    // there can be multiple goal states 
    goal.push_back(6); 

    // get the answer 
    vector<int> answer = uniform_cost_search(goal, 0); 

    // print the answer 
    cout << "Minimum cost from 0 to 6 is = " 
         << answer[0] << endl; 

    return 0; 
} 

```

**Output:**

```
Minimum cost from 0 to 6 is = 3

```

**复杂度**：O（m ^（1 + floor（l / e）））
其中，
m 是节点具有的最大邻居数。
l 是节点的长度。 进入目标状态的最短路径
e 是最低的边缘成本



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。