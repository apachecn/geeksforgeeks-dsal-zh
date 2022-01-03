# 无向图拆分及其在数字对中的应用

> 原文： [https://www.geeksforgeeks.org/undirected-graph-splitting-and-its-application-for-number-pairs/](https://www.geeksforgeeks.org/undirected-graph-splitting-and-its-application-for-number-pairs/)

图可以用于看似无关的问题。 假设卡片两面都有数字的问题，然后尝试使用一侧创建连续的数字序列。 此问题导致如何将图形分为带周期的连通子集和无周期的连通子集的问题。

有已知的算法可以检测图形是否包含圆。 在这里，我们对其进行修改以查找所有未连接到圆的节点。 我们添加了一个循环数组布尔值数组，将其初始化为全 false，这意味着没有节点与圆连接。

然后，我们循环遍历节点，并应用常规算法来确定在已知连接到圆上的节点上跳过圆。 每当我们找到连接到圆的新节点时，我们都会将该属性传播到所有已连接节点，并跳过已经指定为再次连接的节点。

主要功能是对“ [检测无向图](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)”中的循环的 DFS 算法的修改：

这样连接到一个循环的所有节点都在线性时间内指定。

该算法被应用于来自最近[挑战“锗”](https://app.codility.com/programmers/task/max_not_present/) 的以下问题，大约 3.5％的参与者解决了该问题。

假设我们有 N 张卡（100000 > = N > = 1），并且卡的两边都有一个数字（N 是无用的，可以丢弃。以同样的精神，每辆​​车（n ，m）：n N 允许我们向上放置 n 并确保其在序列中的存在，而 m 仍然无用。

如果我们有卡（nn）：n < N，则它确保 n 可以始终

如果我们有两张相同的卡片（n，m）都为 n，则可以将 m 始终添加到一个序列中（如果需要），只需将其放在相反的一侧即可。

现在，我们通过以下方式将卡编码为图形：图形节点的编号应从 0 到 N-1 编号，每个节点都有一组通向的边表示为矢量，起始为空且 整个边集是一个整数向量的向量–边（N）。

（n，m）：n，m N –丢弃

（n，m）：n N –添加到图的边 （n-1，n-1）

现在很容易理解 该图可用于该图的所有节点。 样本：（1、2）（2、5），（5、1）–每个数字出现在两张牌上，只是沿循环进行，将任意数字一次向上一次，一次向下一次：

（1、2 ）– 1 向上，2 向下

（2，5）– 2 向上，5 向下

（5，1）– 5 向上，1 向下

如果上面已经有数字，则以后 带有该号码的卡必须向下排列该号码，以便可以在上方显示另一个号码。 在图中，这意味着可以自由显示通过边连接到多个循环的任何数字。 连接到循环的卡上的卡也是如此。 因此，以某种方式连接到任何周期的任何数字/节点都不会带来任何问题。 成对的相同卡（例如（1、2），（1、2））也会在图中产生一个小圆圈，双卡也是如此，例如 3、3，这是一个节点与其自身连接的循环。

可以将未连接到任何周期的图形的所有部分拆分为未连接的较小图形。 或多或少显而易见的是，任何此类片段都有一个有问题的数字-该片段中最大的一个。 我们使用类似但容易得多的算法来查找此类片段和片段中的所有最大值。 最小的是 Q –最小的数字，它不能是连续覆盖的终点，而最小的数字是上面的 Q。

除了循环数组之外，我们还添加了另一个数组：VisitedNonCyclic，这意味着该数字在通过非循环片段时已经满足。

通过循环调用函数来提取非循环片段中的最大值：

请参考以下代码中的 findMax（）。 图形创建在以下代码的 solution（）中完成。

创建图形后，解决方案仅调用 isCyclic，然后调用：

```
// the main crux of the solution, see full code below
graph.isCyclic();
int res = 1 + graph.GetAnswer();

```

该解决方案受到近期相当艰难的“ [Germanium 2018 Codility Challenge](https://app.codility.com/programmers/task/max_not_present/) ”的启发，并获得了金牌。

**主要思想**：

1.数字很大，但是我们需要从 1 到最后一个数字

的连续序列，但是数字不能超过 10 万。 因此，最大可能实际上是 100 000，将其作为第一个假设

2。基于相同的考虑，最大数不能大于 N（数量）

3.我们也可以整体通过 数字并取最大的是 NN。 结果不能大于 N 或 NN

。4.考虑到这一点，我们可以将（x，200 000）之类的所有卡替换为（x，x）。 两者都允许将 x 向上设置，因此 x 并不是问题。

5.两个数字都大于 N 或 NN 的卡只是被忽略或处理了

6.如果两边的卡号相同，则表示该数字始终可以，不能成为最小的问题，因此 从来没有答案。

7.如果有两个相同的卡片，例如（x，y）和（y，x），则意味着 x 和 y 都没有问题，也不能作为答案。

8.现在，我们介​​绍 BIG 的主要思想 我们将一组卡片转换成图表。 图表的漩涡编号从 0 到 M-1，其中 M 是最后一个可能的数字（N，NN 中的最小数）。 每个节点都有一些相邻节点，因此所有边的集合都是整数

8 的向量。每个像（x，y）的两个数字均小于或等于 M 的卡进入边 x-1，y-1 ，因此第一个节点将获得一个额外的相邻节点，反之亦然

9。由于卡（3，3）之类的作用，一些涡旋将连接到其自身。 这是一个大小为 1 的循环情况。

10.如果有相同的卡，则某些涡旋将通过两个或更多个边连接。 它是一个大小为 2 的循环。

11.大小为 1 和 2 的循环具有不会出现任何问题的数字。 但是现在我们意识到，任何长度的循环都是如此。 例如，纸牌为 2、3； 3，4; 4、10； 10，2; 它们的所有数字都没有问题，只需将 2、3、4、10 放在上面。 不利的一面是 3、4、10、2。

12.现在，如果我们有一张 x，y 卡，并且知道 x 已经在其他地方保证了，我们可以将该卡 x 放下，y 放并确保 y 在结果序列中。

12.因此，如果任何卡通过边连接到一个循环，则由于循环一切正常，因此不会出现问题，因此该编号也可以。

13.因此，如果图的节点的互连子集包含一个循环，则所有涡旋都不会出现任何问题。

因此，我们可以应用一种已知算法来查找循环，如文章“ [在无向图](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)中检测循环”中所述，并添加传播

14。我们还可以指定所有节点 在图中连接到一个循环 cycle []。 而且，我们可以传播

属性，只需从一个循环中开始，将其设置为循环，然后跳过该循环并在相邻位置调用相同的函数，就可以跳过该属性。

15.通过使用已知算法的组合来检测无向图中的循环，并跳过已经循环的循环并传播“连接到循环”的属性，我们发现所有连接到循环的节点。 所有这些节点都是安全的，它们不会成为问题

16。但是，保持节点未连接任何周期，可以简化它们的问题，但可以切成没有公共边或节点的分离图。

17.但是如何处理它们？ 它可以是线性分支，也可以是彼此交叉的分支。 所有节点都不同。

18.经过最后的努力，人们可以理解，任何这样的集合只有一个有问题的编号-该集合的最大值。 可以证明，注意交叉只会使事情变得更好，但最大值保持不变。

19.因此，我们将所有非循环实体都切成相连的分离实体，并在每个实体中找到最大值。

20.然后，我们找到其中的最小值，这是最终答案！

例子：

> 输入：A = [1、2、4、3] B = [1、3、2、3]
> 输出：5。
> 因为所提供的卡提供了 1、2、3、4，但没有提供 5，
> 
> 输入：A = [4，2，1，6，5] B = [3，2，1，7，7]，
> 输出：4。
> 因为您可以在第一张牌上显示 3 或 4 但不能同时包含 3 和 4。因此，放置 3，而 1 和 2 由以下卡片组成。
> 
> 输入：A = [2，3]，B = [2，3]
> 输出：1.因为根本没有 1。

复杂：

*   预期最坏情况下的时间复杂度为`O(N)`；

*   预期的最坏情况下的空间复杂度为`O(N)`；

**最终实现**

```

#include <algorithm> 
#include <vector> 
using namespace std; 

class Graph { 
private: 
    int V; // No. of vertices 
    vector<vector<int> > edges; // edges grouped by nodes 
    bool isCyclicUtil(int v, vector<bool>& visited, int parent); 
    vector<bool> cyclic; 
    vector<int> maxInNonCyclicFragments; 
    int findMax(int v); 
    vector<bool> visitedNonCyclic; 
    void setPropagateCycle(int v); 

public: 
    Graph(int V); // Constructor 
    void addEdge(int v, int w); // to add an edge to graph 

    // returns true if there is a cycle and 
    // also designates all connected to a cycle 
    bool isCyclic();  
    int getSize() const { return V; } 
    int GetAnswer(); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    edges = vector<vector<int> >(V, vector<int>()); 
    visitedNonCyclic = cyclic = vector<bool>(V, false); 
} 

void Graph::addEdge(int v, int w) 
{ 
    edges[v].push_back(w); 
    edges[w].push_back(v); 
} 

void Graph::setPropagateCycle(int v) 
{ 
    if (cyclic[v]) 
        return; 
    cyclic[v] = true; 
    for (auto i = edges[v].begin(); i != edges[v].end(); ++i) { 
        setPropagateCycle(*i); 
    } 
} 

bool Graph::isCyclicUtil(int v, vector<bool>& visited, int parent) 
{ 
    if (cyclic[v]) 
        return true; 

    // Mark the current node as visited 
    visited[v] = true; 

    // Recur for all the vertices edgesacent to this vertex 
    vector<int>::iterator i; 
    for (i = edges[v].begin(); i != edges[v].end(); ++i) { 

        // If an edgesacent is not visited, then  
        // recur for that edgesacent 
        if (!visited[*i]) { 
            if (isCyclicUtil(*i, visited, v)) { 
                setPropagateCycle(v); 
                return true; 
            } 
        } 

        // If an edgesacent is visited and not parent 
        //  of current vertex, then there is a cycle. 
        else if (*i != parent) { 
            setPropagateCycle(v); 
            return true; 
        } 
        if (cyclic[*i]) { 
            setPropagateCycle(v); 
            return true; 
        } 
    } 
    return false; 
} 

bool Graph::isCyclic() 
{ 
    // Mark all the vortices as not visited  
    // and not part of recursion stack 
    vector<bool> visited(V, false); 

    // Call the recursive helper function  
    // to detect cycle in different DFS trees 
    bool res = false; 
    for (int u = 0; u < V; u++) 

        // Don't recur for u if it is already visited{ 
        if (!visited[u] && !cyclic[u]) {  
            if (isCyclicUtil(u, visited, -1)) { 
                res = true; 

                // there was retur true originally 
                visited = vector<bool>(V, false);  
            } 
        } 
    return res; 
} 

int Graph::findMax(int v) 
{ 
    if (cyclic[v]) 
        return -1; 
    if (visitedNonCyclic.at(v)) 
        return -1; 
    int res = v; 
    visitedNonCyclic.at(v) = true; 
    for (auto& u2 : edges.at(v)) { 
        res = max(res, findMax(u2)); 
    } 
    return res; 
} 

int Graph::GetAnswer() 
{ 
    // cannot be less than, after extract must add 1 
    int res = V;  

    for (int u = 0; u < V; u++) { 
        maxInNonCyclicFragments.push_back(findMax(u)); 
    } 
    for (auto& u : maxInNonCyclicFragments) { 
        if (u >= 0) 
            res = min(res, u); 
    } 
    return res; 
} 

int solution(vector<int>& A, vector<int>& B) 
{ 
    const int N = (int)A.size(); 

    const int MAX_AMOUNT = 100001; 
    vector<bool> present(MAX_AMOUNT, false); 

    for (auto& au : A) { 
        if (au <= N) { 
            present.at(au) = true; 
        } 
    } 
    for (auto& au : B) { 
        if (au <= N) { 
            present.at(au) = true; 
        } 
    } 
    int MAX_POSSIBLE = N; 
    for (int i = 1; i <= N; i++) { 
        if (false == present.at(i)) { 
            MAX_POSSIBLE = i - 1; 
            break; 
        } 
    } 

    Graph graph(MAX_POSSIBLE); 

    for (int i = 0; i < N; i++) { 
        if (A.at(i) > MAX_POSSIBLE && B.at(i) > MAX_POSSIBLE) { 
            continue; 
        } 
        int mi = min(A.at(i), B.at(i)); 
        int ma = max(A.at(i), B.at(i)); 
        if (A.at(i) > MAX_POSSIBLE || B.at(i) > MAX_POSSIBLE) { 
            graph.addEdge(mi - 1, mi - 1); 
        } 
        else { 
            graph.addEdge(mi - 1, ma - 1); 
        } 
    } 
    graph.isCyclic(); 
    int res = 1 + graph.GetAnswer(); 
    return res; 
} 
// Test and driver 
#include <iostream> 
void test(vector<int>& A, vector<int>& B, int expected,  
                                 bool printAll = false) 
{ 
    int res = solution(A, B); 
    if (expected != res || printAll) { 
        for (size_t i = 0; i < A.size(); i++) { 
            cout << A.at(i) << " "; 
        } 
        cout << endl; 
        for (size_t i = 0; i < B.size(); i++) { 
            cout << B.at(i) << " "; 
        } 
        cout << endl; 
        if (expected != res) 
            cout << "Error! Expected: " << expected << "  "; 
        else
            cout << "Expected: " << expected << "  "; 
    } 
    cout << " Result: " << res << endl; 
} 
int main() 
{ 
    vector<int> VA; 
    vector<int> VB; 

    int A4[] = { 1, 1, 1, 1, 1 }; 
    int B4[] = { 2, 3, 4, 5, 6 }; 
    VA = vector<int>(A4, A4 + 1); 
    VB = vector<int>(B4, B4 + 1); 
    test(VA, VB, 2, true); 

    int A0[] = { 1, 1 }; 
    int B0[] = { 2, 2 }; 
    VA = vector<int>(A0, A0 + 2); 
    VB = vector<int>(B0, B0 + 2); 
    test(VA, VB, 3); 

    int A[] = { 1, 2, 4, 3 }; 
    int B[] = { 1, 3, 2, 3 }; 
    VA = vector<int>(A, A + 4); 
    VB = vector<int>(B, B + 4); 
    test(VA, VB, 5); 

    int A2[] = { 4, 2, 1, 6, 5 }; 
    int B2[] = { 3, 2, 1, 7, 7 }; 
    VA = vector<int>(A2, A2 + 5); 
    VB = vector<int>(B2, B2 + 5); 
    test(VA, VB, 4); 

    int A3[] = { 2, 3 }; 
    int B3[] = { 2, 3 }; 
    VA = vector<int>(A3, A3 + 2); 
    VB = vector<int>(B3, B3 + 2); 
    test(VA, VB, 1); 
    return 0; 
} 

```

**Output:**

```
1 
2 
Expected: 2   Result: 2
 Result: 3
 Result: 5
 Result: 4
 Result: 1

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。