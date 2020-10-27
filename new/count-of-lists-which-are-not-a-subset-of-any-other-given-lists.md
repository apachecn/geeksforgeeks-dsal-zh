# 不是任何其他给定列表的子集的列表计数

给定 **N** 个字符串列表，任务是查找不是任何其他给定列表的子列表的列表计数。

**示例：**

> **输入：** [[“嘿”，“嗨”，“你好”]，[“嘿”，“再见”]，[“嘿”，“嗨”]]
> **输出 ：** 2
> **解释**
> 第三列表是第一列表的子集，因此第一和第二列表是必需列表。
> 
> **输入：** [[“ geeksforgeeks”，“ geeks”]，[“ geeks”，“ geeksforgeeks”]]
> **输出：** 0
> **说明：[** 这两个列表都包含相同的字符串集。

**方法**
请按照以下步骤解决问题：

1.  首先，列举所有向量中所有可能的字符串，即为它们分配一个整数。
2.  然后，对所有单个列表使用[位集](https://www.geeksforgeeks.org/c-bitset-and-its-application/)来存储其中存在的字符串。
3.  比较位集。 如果其中一个位集是另一个位集的子集，请忽略该列表。 否则，将该列表的索引插入集合中。
4.  打印集中的所有索引。

下面的代码是上述方法的实现：

## C++

```cpp

// C++ program to find all lists 
// which are not a subset of any 
// other given lists 
#include <bits/stdc++.h> 
using namespace std; 

#define N 50005 

// Function to print all lists which 
// are not a subset of any other lists 
void findNonSubsets(vector<vector<string> >& v, 
                    vector<int>& ans) 
{ 
    unordered_map<string, int> mp; 
    int id = 1; 
    // Enumerate all strings 
    // present in all lists 
    for (int i = 0; i < v.size(); i++) { 
        for (int j = 0; j < v[i].size(); j++) { 
            if (mp.count(v[i][j]) > 0) 
                continue; 

            mp[v[i][j]] = id++; 
        } 
    } 

    // Compute and store bitsets 
    // of all strings in lists 
    vector<bitset<N> > v1; 

    for (int i = 0; i < v.size(); i++) { 
        bitset<N> b; 
        for (int j = 0; j < v[i].size(); j++) { 
            b[mp[v[i][j]]] = 1; 
        } 
        v1.push_back(b); 
    } 
    for (int i = 0; i < v.size(); i++) { 
        bool flag = false; 
        for (int j = 0; !flag and j < v.size(); j++) { 
            if (i != j) { 
                // If one of the bitsets is 
                // a subset of another, the 
                // logical AND is equal to the 
                // subset(intersection operation) 
                if ((v1[i] & v1[j]) == v1[i]) { 
                    flag = true; 
                } 
            } 
        } 

        if (!flag) { 
            ans.push_back(i); 
        } 
    } 
    return; 
} 

// Driver Program 
signed main() 
{ 
    vector<vector<string> > v 
        = { { "hey", "hello", "hi" }, 
            { "hey", "bye" }, 
            { "hey", "hi" } }; 

    vector<int> ans; 
    findNonSubsets(v, ans); 

    if (ans.size() == 0) { 
        cout << -1 << endl; 
        return 0; 
    } 

    for (int i = 0; i < ans.size(); i++) { 
        cout << ans[i] << " "; 
    } 

    return 0; 
} 

```

**Output:**

```
0 1

```

***时间复杂度：** O（N * M）*
***辅助空间：** O（N * M）*

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



