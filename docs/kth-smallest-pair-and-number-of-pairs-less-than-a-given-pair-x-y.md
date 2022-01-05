# 第 Kt 个最小对和少于给定对(x，y)的对的数量

> 原文:[https://www . geesforgeks . org/kth-最小对和对数-小于给定对-x-y/](https://www.geeksforgeeks.org/kth-smallest-pair-and-number-of-pairs-less-than-a-given-pair-x-y/)

给定 **N 个**对，任务是找到 **K 个<sup>第</sup>个**最小对，且对的数量少于给定对 **(x，y)** 。

**示例:**

> **输入:** pairs[][] = {{23，20}，{23，10}，{23，30}，{12，35}，{12，22}}，K = 3，(x，y) = (23，20)
> T3】输出:T5】{ 23，10}
> 3
> 
> **输入:** pairs[][] = {{23，20}，{23，10}，{23，30}，{12，35}，{12，22}}，K = 2，(x，y) = (12，35)
> T3】输出:T5】{ 12，35}
> 1

**天真法:**上述问题可以通过从数组中找出所有对，然后分别打印第 k 个最小对和小于(x，y)的对的个数来解决。

**基于策略的数据结构方法:**以下是将[基于策略的数据结构显示为 MAP](https://www.geeksforgeeks.org/map-policy-based-data-structure-in-g/) 的代码。它可以添加/移除元素对，可以在 O(log N)时间内找到小于(x，y)的元素对数量、第 k 个最小的元素对等。这张地图的特别之处在于，我们可以访问这一对元素在有序的 2D 数组中的索引。如果这一对没有出现在地图上，我们就得到这一对在地图上的位置。

```
// C++ implementation of the approach
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <functional>
#include <iostream>
using namespace __gnu_pbds;
using namespace std;

// A new data structure is defined
// Please refer https:// goo.gl/WVDL6g
typedef tree<pair<int, int>, null_type,
             less<pair<int, int> >,
             rb_tree_tag, tree_order_statistics_node_update>
    ordered_map;

// Driver code
int main()
{
    ordered_map om;

    om.insert({ 23, 20 });
    om.insert({ 23, 10 });
    om.insert({ 23, 30 });
    om.insert({ 12, 35 });
    om.insert({ 12, 22 });

    int K = 2, x = 12, y = 35;

    cout << "{" << om.find_by_order(K - 1)->first << ", "
         << om.find_by_order(K - 1)->second << "}\n";

    cout << om.order_of_key({ x, y }) << endl;

    return 0;
}
```

**Output:**

```
{12, 35}
1

```