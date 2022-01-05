# 找出数值最高的前 K 项

> 原文:[https://www . geesforgeks . org/find-top-k-价值最高的物品/](https://www.geeksforgeeks.org/find-the-top-k-items-with-the-highest-value/)

给定项目及其值的列表。任务是找到价值最高的前 k 项。有可能两个项目具有相同的值，在这种情况下，名字在前的项目(按字典顺序)将被赋予更高的优先级。

**示例:**

> **输入:**物品[] = {球棒、手套、柳条、球}，数值[] = {100、50、200、100}
> k = 2
> 
> **输出:**小门球
> 小门数值最高。
> Bat、Ball 值相同，但按字典顺序，Ball 排第一。

**进场:**这个问题可以根据数值贪婪地挑选物品来解决。我们将按照值的递减顺序使用项目列表进行排序，如果值相同，项目将按照字典顺序递增顺序进行排序。
我们将以向量对的形式存储数据，并将使用内置的排序函数和布尔比较器函数来比较两个项目。

下面是上述方法的实现:

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Boolean Comparator Function
// to compare two pairs of item-value
bool comp(pair<string, int> A, pair<string, int> B)
{
    // Compare the name if the values are equal
    if (A.second == B.second)
        return A.first < B.first;

    // Else compare values
    return A.second > B.second;
}

// Driver code
int main()
{
    int k = 2;
    int n = 3;

    // Store data in a vector of Item-Value Pair
    vector<pair<string, int> > items;

    // inserting items-value pairs in the vector
    items.push_back(make_pair("Bat", 100));
    items.push_back(make_pair("Gloves", 50));
    items.push_back(make_pair("Wickets", 200));
    items.push_back(make_pair("Ball", 100));

    // Sort items using Inbuilt function
    sort(items.begin(), items.end(), comp);

    // Print top k values
    // or if n is less than k
    // Print all n items
    for (int i = 0; i < min(n, k); ++i) {
        cout << items[i].first << '\n';
    }

    return 0;
}
```

**Output:**

```
Wickets
Ball

```

**时间复杂度:** O(NlogN)

进一步优化:我们可以使用[堆数据结构](https://www.geeksforgeeks.org/heap-data-structure/)进一步优化上述解决方案。请参见[数组中 k 个最大的元素](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)。