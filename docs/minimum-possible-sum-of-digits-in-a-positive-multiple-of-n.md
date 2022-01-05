# N 的正倍数中数字的最小可能和

> 原文:[https://www . geeksforgeeks . org/最小可能正倍数位数/](https://www.geeksforgeeks.org/minimum-possible-sum-of-digits-in-a-positive-multiple-of-n/)

给定一个数 N，求 N 的正倍数所能得到的最小可能位数和

**约束** : 1 < =N < =10^5.

**示例:**

```
Input :  N = 6
Output : 3
Explanation: 6*2 = 12, sum of digits is 1+2 = 3.

Input : N = 20
Output : 1
20*5 = 100, sum of digits is 1+0+0=1

```

**接近**:问题完全基于观察。对于 N = 6，答案是 12。

因此，我们可以将 12 写成:1-(* 10)–> 10 –(+1)–> 11 –(+1)–> 12。这个序列描述的是，我们可以写出任何> =1 的数字，作为+1 的和和*10 的积，从 1 开始。

另一个观察结果是，当我们将+1 加到数字上时，数字总和会增加+1，除非最后一个数字是 9。
第二个观察是，当我们把数字乘以 10 时，数字的和保持不变。

现在，既然我们想要 N 的倍数，那么 N % N 的任何倍数都将是 0。

所以，采取上面的分析，我们可以构建一个 K 个顶点的图，对于任意一个顶点 X，从 X 到 X+1 的节点权重为 1，从 X 到(X*10)%N 的节点权重为 0。我们取模 N，因为顶点在 0 到 N-1 之间。

答案将是从 1 到 0 的最短距离，因为(N 的任意倍数)mod N = 0。

我们可以利用 Dijkstra 定理求出 1 和 0 之间的最短距离。假设它是 d，答案将是 1+d，因为我们还必须考虑边 0 到 1。

这个解的时间复杂度将是 O(E+VLogV) = O(N+NLogN) = O(NlogN)，因为我们将在最多 N 个顶点和边上行进。

还有一件事需要注意，因为，在 xyz 之后..9，下一个数字将是 abc..0，但不会影响我们的回答。

**证明**:以 N = 11 为例，答案为 2。它从 11*1 = 11 到 11*10 = 110。
既然 110 是 N 的 10 的倍数，也是一个答案，要么我们已经找到了答案，因为如果 110 是 N 的某个 10 的倍数，那么在我们的答案中一定存在一个小于这个的数字，并且没有前导 0，那就是 11。
所以如果不是答案，要么我们会超过 10 的 N 的倍数，要么如果答案中有 10 的 N 的倍数，我们就已经命中了答案。

下面是上述方法的实现:

```
#include <bits/stdc++.h>
using namespace std;

const int Maxx = 100005;
int N;
vector<pair<int, int> > Graph[Maxx];

/// Dijkartas algorithm to find the shortest distance
void Dijkartas(int source)
{
    priority_queue<pair<int, int>, vector<pair<int, int> >, 
                                  greater<pair<int, int> > > PQ;

    // Initialize all distances to be infinity
    vector<int> Distance(N + 2, 1e9);

    // Push source in Priority Queue
    PQ.push(make_pair(0, source));
    int src = source;
    Distance[src] = 0;
    while (!PQ.empty()) {
        int current = PQ.top().second;
        PQ.pop();
        for (auto& neighbours : Graph[current]) {
            int v = neighbours.first;
            int weight = neighbours.second;
            if (Distance[v] > Distance[current] + weight) {
                Distance[v] = Distance[current] + weight;
                PQ.push(make_pair(Distance[v], v));
            }
        }
    }

    cout << "Minimum possible sum of digits is " << 
                              1 + Distance[0] << endl;
    return;
}

// Function to calculate the minimum possible sum of digits
void minSumDigits(int N)
{
    // Build a graph of N vertices with edge weight 1
    for (int i = 1; i <= N; ++i) {
        int From = (i) % N;
        int To = (i + 1) % N;
        int Wt = 1;
        Graph[From].push_back(make_pair(To, Wt));
    }

    // In the same graph add weights 0 to 10's multiple of node X
    for (int i = 1; i <= N; ++i) {
        int From = (i) % N;
        int To = (10 * i) % N;
        int Wt = 0;
        Graph[From].push_back(make_pair(To, Wt));
    }

    // Run dijartas to find the shortest  distance from 1 to 0
    Dijkartas(1);
    return;
}

// Driver Code
int main()
{
    N = 19;

    minSumDigits(N);

    return 0;
}
```

**Output:**

```
Minimum possible sum of digits is 2

```