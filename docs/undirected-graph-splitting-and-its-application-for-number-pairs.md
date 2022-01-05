# 无向图分裂及其在数对中的应用

> 原文:[https://www . geesforgeks . org/无向图拆分及其在数字对中的应用/](https://www.geeksforgeeks.org/undirected-graph-splitting-and-its-application-for-number-pairs/)

图形可以用于看似不相关的问题。说一下两边都有数字的卡片的问题，你试图用一边创建一个连续的数字序列。这个问题导致了如何把一个图分成有圈的连通子集和无圈的连通子集的问题。

有已知的算法来检测图形是否包含圆。在这里，我们修改它以找到所有未连接到圆的节点。我们添加了一个布尔数组，其循环起始为全假，这意味着已知没有节点连接到圆。
然后我们循环遍历节点，应用通常的算法来确定在已知与圆相连的节点上跳过的圆。每当我们发现一个新节点连接到一个圆上，我们就将属性传播到所有已连接的节点，跳过已经被指定为再次连接的节点。
主要功能是对文章“[检测无向图](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)中的循环”中的 DFS 算法的修改:

连接到一个周期的所有节点在线性时间内被指定为这样。
将该算法应用于最近[挑战“锗”](https://app.codility.com/programmers/task/max_not_present/)的以下问题，约 3.5%的参与者解决了该问题。
假设我们有 N 张牌(100000 > = N > = 1)，牌的两边都有一个数字(N 是无用的，可以丢弃。本着同样的精神，每辆车(N，m): n N 允许我们向上放 N，并确保它在序列中的存在，而 m 无论如何都是无用的。
如果我们有一张牌(n.n): n < N，它保证 N 总是可以被加到一个到达 n-1 的连续序列中。
如果我们有两张相同的牌(n，m)，如果需要，n，m 总是可以加到一个序列中，只是把它放在相反的一边。
现在我们按照以下方式将卡片编码成图形。图节点应该从 0 到 N-1 编号。每个节点都有一组通向的边，表示为一个向量，从一个空的边开始，整个边集就是一个整数向量的向量——边(N)。
(n，m) : n，m ^ N–丢弃。
(n，m):N N–加到图边(n-1，n-1)
现在很容易理解图中的每个循环都可以用于图的所有节点。一个例子:(1，2) (2，5)，(5，1)–每一个数字都出现在两张牌上，沿着循环传递，把任意一个数字一次向上，一次向下:
(1，2)–1 向上，2 向下
(2，5)–2 向上，5 向下
(5，1)–5 向上，1 向下
如果上面已经放了任意一个数字，那么后面每一张有这个数字的牌都必须把这个数字向下取出，这样就可以在上面显示另一个数字。在图中，它意味着由一条边连接到多个循环的任何数都可以自由显示。连接到连接到循环的卡的卡也是如此。因此，以某种方式连接到任何周期的任何数字/节点都不会带来任何问题。像(1，2)，(1，2)这样的一对相同的卡片也在图中产生一个小圆，双卡也是如此，像 3，3 它是一个节点连接到自身的循环。
图中不与任何循环相连的所有部分都可以拆分成不相连的更小的图。或多或少显而易见的是，任何这样的片段都有一个有问题的数字——片段中最大的。我们使用类似但简单得多的算法来找到这样的片段和片段中的所有最大值。其中最少的是 Q——从最少的数字中不能成为连续覆盖的结束的最小数字，上面的 Q。
除了循环数组，我们再增加一个数组:visitedNonCyclic，意思是这个数在经过一个非循环片段的时候已经满足了。
非循环片段中的最大值是通过反复调用函数提取的:
请参考下面代码中的 findMax()。图形创建在下面代码的解决方案()中完成。
创建图形后，解决方案只调用 isCyclic，然后调用:

```
// the main crux of the solution, see full code below
graph.isCyclic();
int res = 1 + graph.GetAnswer();
```

该解决方案的灵感来自于最近相当艰难的“2018 锗共质挑战赛”，并带来了金牌。

**主要思路:**
1。数字很大，但我们要求从 1 到最后一个数字的连续序列，
但数字不超过 10 万。所以，最大的可能真的是 10 万，把它作为第一个假设
2。出于同样的考虑，最大数量不能大于 N(数量)
3。我们也可以通过整体数字，取最大的是神经网络。结果不能大于 N 或 NN
4。考虑到这一点，我们可以将所有像(x，200，00 0)这样的卡替换为(x，x)。两者都允许向上设置 x，因此 x 不是问题。
5。两个数字都大于 N 或 NN 的牌才被忽略或处理
6。如果两边都有相同号码的牌，这意味着号码总是 OK 的，不可能是最小的问题，所以永远没有答案。
7。如果有两张相同的卡片，如(x，y)和(y，x)，这意味着 x 和 y 都没有问题，不能作为答案
8。现在我们介绍主要的大思想，即我们将一组卡片转换成一个图形。图中的漩涡从 0 到 M-1 编号，其中 M 是最后一个可能的数字(N，NN 中最小的一个)。每个节点都有一些相邻的节点，所以所有边的集合就是整数向量的向量
8。每张像(x，y)这样两个数字都小于或等于 M 的卡片进入边 x-1，y-1，这样第一个节点得到一个额外的相邻节点，反之亦然
9。一些漩涡会因为像(3，3)这样的卡片而与自己相连。这是一个大小为 1 的循环案例。
10。如果有相同的卡片，一些漩涡会被两条或更多的边连接起来。这是一个 2 号的环。
11。大小为 1 和 2 的循环具有不会有任何问题的数字。但是现在我们意识到，任何长度的周期都是如此。例如，卡片是 2，3；3, 4;4, 10;10, 2;他们所有的数字都没有问题，只是把 2，3，4，10 放到上边。下行将有 3，4，10，2。
12。现在，如果我们有一张牌 x，y，并且我们知道 x 已经保证在另一个地方，我们可以把这张牌 x 放下，y 向上，并保证 y 在结果序列中。
12。因此，如果任何卡通过边缘连接到周期，它不会出现问题，因为周期都是正常的，所以这个数字也是正常的。
13。因此，如果有一个包含一个循环的图的节点的互连子集，所有的涡旋不会出现任何问题。
因此，我们可以应用一种已知的算法来寻找循环，就像文章“[在无向图](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)中检测循环”一样，并增加了传播
14。我们还可以指定图中连接到循环的所有节点，循环[]。我们可以传播属性
只需从循环中的某个开始，将其设置为循环，然后跳过它的相邻，跳过循环并在相邻上调用相同的函数。
15。使用已知算法的组合来检测无向图中的循环，其中跳过已经循环的并传播“连接到循环”的属性，我们找到连接到循环的所有节点。所有这样的节点都是安全的，它们不可能是问题
16。但是剩余的节点没有连接到任何循环，它们的问题可以简化，但是切割成没有公共边或节点的分离图。
17。但是怎么处理它们呢？它可以是一个线性分支或相互交叉的分支。所有节点都不同。
18。通过最后的努力，人们可以理解任何这样的集合只有一个有问题的数——集合的最大值。可以证明的是，注意交叉只会让事情变得更好，但最大值保持不变。
19。所以我们把所有非循环的实体切割成相互连接的独立实体，并在每个实体中找到最大值。
20。然后我们找到它们的最小值，这就是最终答案！

示例:

> 输入:A = [1，2，4，3] B = [1，3，2，3]
> 输出:5。
> 因为现在的卡提供 1、2、3、4 而不是 5。
> 
> 输入:A = [4，2，1，6，5] B = [3，2，1，7，7]，
> 输出:4。
> 因为你可以通过第一张牌显示 3 或 4，但不能同时显示 3 和 4。所以，放 3，而 1 和 2 在下面的牌旁边。
> 
> 输入:A = [2，3]，B = [2，3]
> 输出:1。因为 1 根本就不见了。

复杂性:

*   预期最坏情况时间复杂度为 O(N)；
*   预期最坏情况空间复杂度为 O(N)；

**最终实施**

## C++

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

                // there was return true originally
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