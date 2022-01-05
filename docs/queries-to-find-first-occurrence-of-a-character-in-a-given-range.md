# 查找给定范围内第一次出现的字符的查询

> 原文:[https://www . geesforgeks . org/query-to-find-给定范围内第一次出现的字符/](https://www.geeksforgeeks.org/queries-to-find-first-occurrence-of-a-character-in-a-given-range/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个维度为 **M × 3** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**[]**，由类型为 **{L，R，C}** 的查询组成，任务是打印字符 **C** 在范围**【L，R】**内的第一个索引(如果找到的话)。否则，打印 **-1。**

**示例:**

> **输入:**S = " ababc ABC "，Q[][] = { { 0，3，' a' }，{ 0，2，' b' }，{ 2，4，' z ' }
> 输出:0 1-1
> T6】解释:
> 
> *   第一个查询:打印 0，它是字符“a”在[0，3]范围内的第一个索引。
> *   第二个查询:打印 1，这是字符“b”在[0，2]范围内的第一个索引。
> *   第三个查询:Print -1 作为字符“z”不出现在范围[2，4]中。
> 
> **输入:** S= "geeksforgeeks "，Q[][] = { { 0，12，' f' }，{ 0，2，' g' }，{ 6，12，' f ' }
> **输出:** 5 0 -1
> **解释:**
> 
> *   第一个查询:打印 5，这是字符“f”在[0，12]范围内的第一个索引。
> *   第二次查询:打印 0，即【0，2】范围内字符‘g’的第一个索引
>     。
> *   第三个查询:Print -1 作为字符“f”不出现在范围[6，12]中。

**简单方法:**最简单的方法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的索引范围**【L，R】**为每个查询，并打印第一次出现的字符 **C** (如果找到的话)。否则，打印 **-1** 。
***时间复杂度:** O(M * Q)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过在[向量图](https://www.geeksforgeeks.org/map-of-vectors-in-c-stl-with-examples/)中预先存储字符的索引，并使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在字符向量 **C** 中找到范围**【L，R】**中的索引来优化。按照以下步骤解决问题:

*   初始化一个[映射<字符，向量< int > >](https://www.geeksforgeeks.org/map-of-vectors-in-c-stl-with-examples/) ，比如 **V** ，来存储一个字符所有出现的索引。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并更新 **V** 。
*   遍历数组 **Q** :
    *   如果**V【C】**的大小为零，则打印 **-1。**
    *   否则，使用向量**中的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)V【C】**即**下界(V【C】找到索引。begin()，V[C]。end()，L)–V[C]。begin()** 并将其存储在一个变量中，比如 **idx** 。
    *   如果 **idx = N** 或 **idx > R** ，则打印 **-1** 。
    *   否则，打印索引 **idx** 。

下面是上述方法的实现:

## C++

```
// C++ implementation
// for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the first occurence
// for a given range
int firstOccurence(string s,
                   vector<pair<pair<int, int>, char> > Q)
{
    // N = length of string
    int N = s.size();

    // M = length of queries
    int M = Q.size();

    // Stores the indices of a character
    map<char, vector<int> > v;

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // Push the index i
        // into the vector[s[i]]
        v[s[i]].push_back(i);
    }

    // Traverse the query
    for (int i = 0; i < M; i++) {

        // Stores the value L
        int left = Q[i].first.first;

        // Stores the value R
        int right = Q[i].first.second;

        // Stores the character C
        char c = Q[i].second;

        if (v.size() == 0) {
            cout << "-1 ";
            continue;
        }

        // Find index >= L in
        // the vector v
        int idx
            = lower_bound(v.begin(),
                          v.end(), left)
              - v.begin();

        // If there is no index of C >= L
        if (idx == (int)v.size()) {

            cout << "-1 ";
            continue;
        }

        // Stores the value at idx
        idx = v[idx];

        // If idx > R
        if (idx > right) {
            cout << "-1 ";
        }

        // Otherwise
        else {
            cout << idx << " ";
        }
    }
}

// Driver Code
int main()
{
    string S = "abcabcabc";
    vector<pair<pair<int, int>, char> > Q
        = { { { 0, 3 }, 'a' },
            { { 0, 2 }, 'b' },
            { { 2, 4 }, 'z' } };

    firstOccurence(S, Q);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation
# for the above approach
from bisect import bisect_left

# Function to find the first occurence
# for a given range
def firstOccurence(s, Q):

    # N = length of string
    N = len(s)

    # M = length of queries
    M = len(Q)

    # Stores the indices of a character
    v = [[] for i in range(26)]

    # Traverse the string
    for i in range(N):

        # Push the index i
        # into the vector[s[i]]
        v[ord(s[i]) - ord('a')].append(i)

    # Traverse the query
    for i in range(M):

        # Stores the value L
        left = Q[i][0]

        # Stores the value R
        right = Q[i][1]

        # Stores the character C
        c = Q[i][2]

        if (len(v[ord(c) - ord('a')]) == 0):
            print ("-1")
            continue

        # Find index >= L in
        # the vector v
        idx = bisect_left(v[ord(c) - ord('a')], left)

        # If there is no index of C >= L
        if (idx == len(v[ord(c) - ord('a')])):
            print("-1 ")
            continue

        # Stores the value at idx
        idx = v[ord(c) - ord('a')][idx]

        # If idx > R
        if (idx > right):
            print ("-1 ")

        # Otherwise
        else:
            print(idx, end=" ")

# Driver Code
if __name__ == '__main__':
    S = "abcabcabc";
    Q = [ [ 0, 3 , 'a'],[ 0, 2 , 'b' ],[ 2, 4, 'z']]

    firstOccurence(S, Q)

    # This code is contributed by mohit kumar 29.
```

**Output:** 

```
0 1 -1
```

***时间复杂度:** O(M * log(N))*
***辅助空间:** O(N)*