# 使用分支定界实现 0/1 背包

> 原文:[https://www . geesforgeks . org/实现-0-1-背包-使用分支和绑定/](https://www.geeksforgeeks.org/implementation-of-0-1-knapsack-using-branch-and-bound/)

我们强烈建议将以下帖子作为先决条件。

[分支定界|集合 1(带 0/1 背包的介绍)](https://www.geeksforgeeks.org/branch-and-bound-set-1-introduction-with-01-knapsack/)

我们讨论了解决上述问题的不同方法，发现当项目权重不是整数时，分支定界法是最合适的方法。

本文讨论了 0/1 背包问题分支定界法的实现。

**0/1 背包如何求每个节点的界？**
的想法是利用[贪婪方法](https://www.geeksforgeeks.org/fractional-knapsack-problem/)为分数背包问题提供了最佳解决方案的事实。
为了检查特定节点是否能给我们更好的解决方案，我们使用贪婪方法计算最优解(通过节点)。如果贪婪方法本身计算的解超过了目前为止的最佳解，那么我们就不能通过节点得到更好的解。

**完整算法:**

1.  按照单位重量价值比的递减顺序对所有项目进行排序，以便使用贪婪方法计算上限。
2.  初始化最大利润，最大利润= 0
3.  创建一个空队列，q。
4.  创建一个决策树的伪节点，并将其入队到 q，伪节点的利润和权重为 0。
5.  当 Q 不为空时，执行以下操作。
    *   从 q 中提取一个项目，让提取的项目为 u。
    *   计算下一级节点的利润。如果利润大于最大利润，那么更新最大利润。
    *   计算下一级节点的界限。如果绑定大于 max 利润，那么在 q 上增加下一级节点。
    *   考虑下一级节点不被视为解决方案的一部分的情况，并添加一个节点到队列中，级别为下一级，但权重和利润不考虑下一级节点。

插图:

```
Input:
// First thing in every pair is weight of item
// and second thing is value of item
Item arr[] = {{2, 40}, {3.14, 50}, {1.98, 100},
              {5, 95}, {3, 30}};
Knapsack Capacity W = 10

Output:
The maximum possible profit = 235

Below diagram shows illustration. Items are 
considered sorted by value/weight.

Note :  The image doesn't strictly follow the 
algorithm/code as there is no dummy node in the
image.

```

以下是上述思想的 C++实现。

```
// C++ program to solve knapsack problem using
// branch and bound
#include <bits/stdc++.h>
using namespace std;

// Structure for Item which store weight and corresponding
// value of Item
struct Item
{
    float weight;
    int value;
};

// Node structure to store information of decision
// tree
struct Node
{
    // level  --> Level of node in decision tree (or index
    //             in arr[]
    // profit --> Profit of nodes on path from root to this
    //            node (including this node)
    // bound ---> Upper bound of maximum profit in subtree
    //            of this node/
    int level, profit, bound;
    float weight;
};

// Comparison function to sort Item according to
// val/weight ratio
bool cmp(Item a, Item b)
{
    double r1 = (double)a.value / a.weight;
    double r2 = (double)b.value / b.weight;
    return r1 > r2;
}

// Returns bound of profit in subtree rooted with u.
// This function mainly uses Greedy solution to find
// an upper bound on maximum profit.
int bound(Node u, int n, int W, Item arr[])
{
    // if weight overcomes the knapsack capacity, return
    // 0 as expected bound
    if (u.weight >= W)
        return 0;

    // initialize bound on profit by current profit
    int profit_bound = u.profit;

    // start including items from index 1 more to current
    // item index
    int j = u.level + 1;
    int totweight = u.weight;

    // checking index condition and knapsack capacity
    // condition
    while ((j < n) && (totweight + arr[j].weight <= W))
    {
        totweight    += arr[j].weight;
        profit_bound += arr[j].value;
        j++;
    }

    // If k is not n, include last item partially for
    // upper bound on profit
    if (j < n)
        profit_bound += (W - totweight) * arr[j].value /
                                         arr[j].weight;

    return profit_bound;
}

// Returns maximum profit we can get with capacity W
int knapsack(int W, Item arr[], int n)
{
    // sorting Item on basis of value per unit
    // weight.
    sort(arr, arr + n, cmp);

    // make a queue for traversing the node
    queue<Node> Q;
    Node u, v;

    // dummy node at starting
    u.level = -1;
    u.profit = u.weight = 0;
    Q.push(u);

    // One by one extract an item from decision tree
    // compute profit of all children of extracted item
    // and keep saving maxProfit
    int maxProfit = 0;
    while (!Q.empty())
    {
        // Dequeue a node
        u = Q.front();
        Q.pop();

        // If it is starting node, assign level 0
        if (u.level == -1)
            v.level = 0;

        // If there is nothing on next level
        if (u.level == n-1)
            continue;

        // Else if not last node, then increment level,
        // and compute profit of children nodes.
        v.level = u.level + 1;

        // Taking current level's item add current
        // level's weight and value to node u's
        // weight and value
        v.weight = u.weight + arr[v.level].weight;
        v.profit = u.profit + arr[v.level].value;

        // If cumulated weight is less than W and
        // profit is greater than previous profit,
        // update maxprofit
        if (v.weight <= W && v.profit > maxProfit)
            maxProfit = v.profit;

        // Get the upper bound on profit to decide
        // whether to add v to Q or not.
        v.bound = bound(v, n, W, arr);

        // If bound value is greater than profit,
        // then only push into queue for further
        // consideration
        if (v.bound > maxProfit)
            Q.push(v);

        // Do the same thing,  but Without taking
        // the item in knapsack
        v.weight = u.weight;
        v.profit = u.profit;
        v.bound = bound(v, n, W, arr);
        if (v.bound > maxProfit)
            Q.push(v);
    }

    return maxProfit;
}

// driver program to test above function
int main()
{
    int W = 10;   // Weight of knapsack
    Item arr[] = {{2, 40}, {3.14, 50}, {1.98, 100},
                  {5, 95}, {3, 30}};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Maximum possible profit = "
         << knapsack(W, arr, n);

    return 0;
}
```

输出:

```
Maximum possible profit = 235
```

本文由乌特卡尔什·特里维迪供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并将你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。