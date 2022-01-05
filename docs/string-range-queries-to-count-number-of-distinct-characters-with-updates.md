# 字符串范围查询，通过更新计算不同字符的数量

> 原文:[https://www . geesforgeks . org/string-range-query-to-count-number-distinct-characters-with-updates/](https://www.geeksforgeeks.org/string-range-queries-to-count-number-of-distinct-characters-with-updates/)

给定一个长度为 N 的字符串 S，以下类型的 Q 个查询:

> **键入 1:** 1 i X
> 用给定的字符 X 更新字符串的第 I 个字符
> 
> **类型 2:** L R
> 计算给定范围内不同性状的数量[L，R]。
> 
> 约束:
> 
> *   1<=N<=500000
> *   1<=Q<20000
> *   |S|=N
> *   字符串仅包含小写字母。

**示例:**

> **输入:**S = " abcdbd " Q = 6
> 2 3 6
> 1 5 z
> 2 1 1
> 1 4a
> 1 7d
> 2 1 7
> T9】输出:
> 3
> 1
> 5
> **解释:**
> 对于查询:
> 1。L = 3，R = 6
> 不同的字符是:c，b，d
> ans = 3。
> 2。查询后的字符串更新为 S="abcdzbd "。
> 3。L = 1，R = 1
> 只有一个不同的字符。
> 等处理所有查询。
> 
> **输入:**S = " aaaaaa "，Q = 2
> 1 2b
> 2 1 4
> T5】输出:
> 2

**天真的方法:**

**查询类型 1:** 用给定字符替换字符串的第 I 个字符。
**查询类型 2:** 从左到右遍历字符串，统计不同字符的数量。

***时间复杂度:** O(N <sup>2</sup> )*

**高效方法:**该方法基于[频率计数](https://www.geeksforgeeks.org/basic/frequency-counting/)算法。
这个想法是使用一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 将字符串中不同的字符映射到一个 [Ordered_set](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/) 中，该集合存储所有出现的索引。之所以使用 Ordered_set，是因为它基于[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)，所以字符的插入和删除会取 O ( log N)。

1.  将字符串的所有字符及其索引插入哈希映射
2.  对于类型 1 的查询，删除索引 I 处出现的字符，并在哈希映射中插入索引 I 处出现的字符 X
3.  对于类型 2 的查询，遍历所有 26 个字符并检查其出现是否在范围[L，R]内，如果是，则增加计数。遍历后打印计数值。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;

#define ordered_set                 \
    tree<int, null_type, less<int>, \
         rb_tree_tag,               \
         tree_order_statistics_node_update>

// Function that returns the lower-
// bound of the element in ordered_set
int lower_bound(ordered_set set1, int x)
{
    // Finding the position of
    // the element
    int pos = set1.order_of_key(x);

    // If the element is not
    // present in the set
    if (pos == set1.size()) {
        return -1;
    }

    // Finding the element at
    // the position
    else {
        int element = *(set1.find_by_order(pos));

        return element;
    }
}

// Utility function to add the
// position of all characters
// of string into ordered set
void insert(
    unordered_map<int, ordered_set>& hMap,
    string S, int N)
{
    for (int i = 0; i < N; i++) {
        hMap[S[i] - 'a'].insert(i);
    }
}

// Utility function for update
// the character at position P
void Query1(
    string& S,
    unordered_map<int, ordered_set>& hMap,
    int pos, char c)
{

    // we delete the position of the
    // previous character as new
    // character is to be replaced
    // at the same position.
    pos--;
    int previous = S[pos] - 'a';
    int current = c - 'a';
    S[pos] = c;
    hMap[previous].erase(pos);
    hMap[current].insert(pos);
}

// Utility function to determine
// number of different characters
// in given range.
void Query2(
    unordered_map<int, ordered_set>& hMap,
    int L, int R)
{
    // Iterate over all 26 alphabets
    // and check if it is in given
    // range using lower bound.
    int count = 0;
    L--;
    R--;
    for (int i = 0; i < 26; i++) {
        int temp = lower_bound(hMap[i], L);
        if (temp <= R and temp != -1)
            count++;
    }
    cout << count << endl;
}

// Driver code
int main()
{
    string S = "abcdbbd";
    int N = S.size();

    unordered_map<int, ordered_set> hMap;

    // Insert all characters with its
    // occurrence in the hash map
    insert(hMap, S, N);

    // Queries for sample input
    Query2(hMap, 3, 6);
    Query1(S, hMap, 5, 'z');
    Query2(hMap, 1, 1);
    Query1(S, hMap, 4, 'a');
    Query1(S, hMap, 7, 'd');
    Query2(hMap, 1, 7);

    return 0;
}
```

**Output:**

```
3
1
5

```

时间复杂度: **O(Q * logN)** 其中 Q 为查询数，N 为字符串大小。