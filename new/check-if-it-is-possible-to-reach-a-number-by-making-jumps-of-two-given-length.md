# 检查是否可以通过跳转两个给定长度来达到数字

> 原文： [https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-a-number-by-making-jumps-of-two-given-length/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-a-number-by-making-jumps-of-two-given-length/)

给定起始位置`k`和两个跳跃大小`d1`和`d2`，我们的任务是找到可能的达到`x`的最小跳跃次数。

在任何位置`P`，我们都可以跳到位置：

*   `P + d1`和`P – d1`

*   `P + d2`和`P – d2`

**示例**：

```
Input : k = 10, d1 = 4, d2 = 6 and x = 8 
Output : 2
1st step 10 + d1 = 14
2nd step 14 - d2 = 8

Input : k = 10, d1 = 4, d2 = 6 and x = 9
Output : -1
-1 indicates it is not possible to reach x.

```

在[的上一篇文章](https://www.geeksforgeeks.org/reach-the-numbers-by-making-jumps-of-two-given-lengths/)中，我们讨论了一种通过跳两个给定长度来检查`K`是否可到达数字列表的策略。

在这里，我们没有给出数字列表，而是给我们一个整数`x`，如果可以从`k`到达整数，则任务是找到所需的最小步数或跳跃数。

我们将使用**广度优先搜索**：

**方法**解决此问题：

*   从`k`检查`x`是否可达。 如果满足`(x – k) % gcd(d1, d2) = 0`，则可以从`k`获得数字`x`。

*   如果`x`可达：

    1.  维护哈希表以存储已访问的位置。

    2.  从位置`k`开始应用 bfs 算法。

    3.  如果您以`stp`步长到达位置`P`，则可以以`stp + 1`步长到达`p + d1`位置。

    4.  如果位置`P`是要求的位置`x`，那么达到`P`的步骤就是答案

下图描述了算法如何找出达到`k = 10`，`d1 = 4`，`d2 = 6`，`x = 8`时所需的步数。

![Algo Example](https://docs.google.com/drawings/d/e/2PACX-1vQNc-ChldajMUiKj_gyuUb4IrdhU7cCl-CLDSnA_slb_nU47DBOWqvE-ME35jMpaU6-vF4Jj1abOrrH/pub?w=1440&h=1080)

下面是上述方法的实现：

## C++

```cpp

#include <bits/stdc++.h> 
using namespace std; 

// Function to perform BFS traversal to 
// find minimum number of step needed 
// to reach x from K 
int minStepsNeeded(int k, int d1, int d2, int x) 
{ 
    // Calculate GCD of d1 and d2 
    int gcd = __gcd(d1, d2); 

    // If position is not reachable 
    // return -1 
    if ((k - x) % gcd != 0) 
        return -1; 

    // Queue for BFS 
    queue<pair<int, int> > q; 

    // Hash Table for marking 
    // visited positions 
    unordered_set<int> visited; 

    // we need 0 steps to reach K 
    q.push({ k, 0 }); 

    // Mark starting position 
    // as visited 
    visited.insert(k); 

    while (!q.empty()) { 

        int s = q.front().first; 

        // stp is the number of steps 
        // to reach position s 
        int stp = q.front().second; 

        if (s == x) 
            return stp; 

        q.pop(); 

        if (visited.find(s + d1) == visited.end()) { 

            // if position not visited 
            // add to queue and mark visited 
            q.push({ s + d1, stp + 1 }); 

            visited.insert(s + d1); 
        } 

        if (visited.find(s + d2) == visited.end()) { 
            q.push({ s + d2, stp + 1 }); 
            visited.insert(s + d2); 
        } 

        if (visited.find(s - d1) == visited.end()) { 
            q.push({ s - d1, stp + 1 }); 
            visited.insert(s - d1); 
        } 
        if (visited.find(s - d2) == visited.end()) { 
            q.push({ s - d2, stp + 1 }); 
            visited.insert(s - d2); 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    int k = 10, d1 = 4, d2 = 6, x = 8; 

    cout << minStepsNeeded(k, d1, d2, x); 

    return 0; 
} 

```