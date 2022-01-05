# 对于 Q 查询，在给定数组中将给定元素的第一次出现移动到结束后打印数组

> 原文:[https://www . geeksforgeeks . org/print-array-move-first-occurrence-of-给定元素-to-end-in-给定数组-for-q-query/](https://www.geeksforgeeks.org/print-array-after-moving-first-occurrence-of-given-element-to-end-in-given-array-for-q-queries/)

给定一个由 **N** 个整数组成的[数组 **arr[]** 和一个具有 **Q** 个整数的数组**查询[]** ，任务是在将第一个出现的**查询【I】**移动到数组 **arr[]** 的末尾后，为范围**【0，Q】**中的每个 **i** 打印数组 **arr[]**](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {1，3，1，3}，查询[] = {3，1}
> **输出:** 1 3 3 1
> **解释:**在第一次迭代中，将查询[0]的第一次出现发送到末尾，即，将 3 的第一次出现发送到末尾。
> 因此，数组变成 arr[] = {1，1，3，3}。
> 在第二次迭代中，将查询[1]的第一次出现发送到最后。
> 因此，数组 arr[] = {1，3，3，1}是必需的数组。
> 
> **输入:** arr[] = {1，2，3，4，5}，查询[] = {4，3}
> **输出:** 1 2 5 4 3

**方法:**给定的问题可以使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)来解决。其思想是将每个整数的索引列表存储在[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，对于当前整数的操作，从表示当前整数第一次出现的索引的集合中移除第一个索引，并将最后一个索引的索引插入到集合中。以下是要遵循的步骤:

*   创建一个[无序地图](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **m** ，存储每个索引的索引集。
*   [迭代数组](https://www.geeksforgeeks.org/range-based-loop-c/) **arr[]** ，并将所有索引插入到地图 **m** 中各自的集合中。
*   使用变量 I 迭代数组**查询[]** ，并执行以下操作:
    *   从集合**m[查询[i]]** 中移除代表第一个出现的第一个元素。
    *   将最后一个元素的索引，即 **N+i** 插入到集合 **m【查询[I]】**中。
*   按照最终索引的递增顺序打印元素，这是必需的答案。

下面是上述方法的实现:

## C++14

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array after
// performing the given operations
void sendToLast(vector<int> arr, 
                vector<int> query)
{
    // Stores index of present
    // integers in a set
    unordered_map<int, set<int> > m;

    // Loop to insert indices
    // into the given map
    for (int i = 0; i < arr.size(); i++) {
        m[arr[i]].insert(i);
    }

    // Loop to iterate the
    // query array
    for (int i = 0; i < query.size(); i++) {

        // Erase the index of current
        // element from the map
        m[query[i]].erase(*m[query[i]].begin());

        // Insert new location
        m[query[i]].insert(arr.size() + i);
    }

    // Vector of pair to store index
    // value pair
    vector<pair<int, int> > v;

    // Insert all index value pair
    // into the vector v
    for (auto x : m) {
        for (auto y : x.second) {
            v.push_back({ y, x.first });
        }
    }

    // Sort v in increasing order
    // of the index
    sort(v.begin(), v.end());

    // Print array
    for (int i = 0; i < v.size(); i++) {
        cout << v[i].second << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr{ 1, 3, 1, 3 };
    vector<int> query{ 3, 1 };

    sendToLast(arr, query);
    return 0;
}
```

**Output**

```
1 3 3 1 
```

***时间复杂度:** O(Q * log N)*
***辅助空间:** O(N)*