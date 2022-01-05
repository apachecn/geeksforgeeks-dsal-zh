# 范围总和查询和平方根更新

> 原文:[https://www . geesforgeks . org/range-sum-query-and-update-with-平方根/](https://www.geeksforgeeks.org/range-sum-queries-and-update-with-square-root/)

给定一个由 **N** 个整数和查询次数 **Q** 组成的数组 **A** 。你必须回答两种类型的问题。

*   **更新【l，r】**–对于从 **l** 到 **r** 范围内的每个 **i** ，用 **sqrt(A <sub>i</sub> )** 更新**A<sub>I</sub>**，其中 **sqrt(A <sub>i</sub> )** 代表 **A <sub>i</sub>** 的平方根
*   **查询【l，r】**–计算数组 **A** 中所有介于 **l** 和 **r** 之间的数字之和。

**先决条件:** [二元索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) | [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
**示例:**

> **输入:** A[] = { 4，5，1，2，4}，Q = {{2，1，5}，{1，1，2}，{1，2，4 }，{2，1，5}}
> **输出:** 16
> 9
> 考虑基于 1 的索引，第一个查询是计算从 A <sub>1</sub> 到 A <sub>5</sub>
> 的数字之和，即 4 + 5 + 1 + 2 + 4
> 第二次查询是用其平方根将 A <sub>1</sub> 更新为 A <sub>2</sub> 。现在，数组变成了 A[] = { 2，2，1，2，4 }。
> 同样，第三个查询是用平方根将 A <sub>2</sub> 更新为 A <sub>4</sub> 。现在，数组变成了 A[] = { 2，1，1，1，4 }。
> 第四个查询是计算 A <sub>1</sub> 到 A <sub>5</sub> 的数字之和，是 2 + 1 + 1 + 1 + 4 = 9。
> **输入:** A[] = { 4，9，25，36 }，Q = {{1，2，4}，{2，1，4}}
> **输出:** 18

**天真方法:**一个简单的解决方案是运行一个从 **l** 到 **r** 的循环，并计算给定范围内的元素总和。要更新一个值，只需用平方根替换 **arr[i]** ，即 **arr[i] = sqrt[arr[i]]** 。
**高效方法:**思路是将每次查询和更新操作的时间复杂度降低到 **O(logN)** 。使用[二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) (BIT)或[分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。构造一个 **BIT[]** 数组，有查询和更新操作两个功能。现在，对于每个更新操作，关键的观察是数字 **1** 将有 **1** 作为它的平方根，所以如果它存在于更新查询的范围内，就不需要更新。我们将使用一个集合来仅存储那些大于 **1** 的数字的索引，并使用二分搜索法找到更新查询的 **l** 索引，并递增 **l** 索引，直到该更新查询范围内的每个元素都被更新。如果 **arr[i]** 将 **1** 作为其平方根，那么在更新它之后，将其从集合中移除，因为它将始终是 **1** ，即使在任何下一次更新查询之后。求和查询操作，只需做**查询(r)–查询(l–1)**。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to calculate sum
// in an interval and update with
// square root
#include <bits/stdc++.h>
using namespace std;

// Maximum size of input array
const int MAX = 100;

int BIT[MAX + 1];

// structure for queries with members type,
// leftIndex, rightIndex of the query
struct queries {
    int type, l, r;
};

// function for updating the value
void update(int x, int val, int n)
{
    for (x; x <= n; x += x & -x) {
        BIT[x] += val;
    }
}

// function for calculating the required
// sum between two indexes
int sum(int x)
{
    int s = 0;
    for (x; x > 0; x -= x & -x) {
        s += BIT[x];
    }
    return s;
}

// function to return answer to queries
void answerQueries(int arr[], queries que[], int n, int q)
{
    // Declaring a Set
    set<int> s;
    for (int i = 1; i < n; i++) {

        // inserting indexes of those numbers
        // which are greater than 1
        if (arr[i] > 1)
            s.insert(i);
        update(i, arr[i], n);
    }

    for (int i = 0; i < q; i++) {

        // update query
        if (que[i].type == 1) {
            while (true) {

                // find the left index of query in
                // the set using binary search
                auto it = s.lower_bound(que[i].l);

                // if it crosses the right index of
                // query or end of set, then break
                if (it == s.end() || *it > que[i].r)
                    break;

                que[i].l = *it;

                // update the value of arr[i] to
                // its square root
                update(*it, (int)sqrt(arr[*it]) - arr[*it], n);

                arr[*it] = (int)sqrt(arr[*it]);

                // if updated value becomes equal to 1
                // remove it from the set
                if (arr[*it] == 1)
                    s.erase(*it);

                // increment the index
                que[i].l++;
            }
        }

        // sum query
        else {
            cout << (sum(que[i].r) - sum(que[i].l - 1)) << endl;
        }
    }
}

// Driver Code
int main()
{
    int q = 4;

    // input array using 1-based indexing
    int arr[] = { 0, 4, 5, 1, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // declaring array of structure of type queries
    queries que[q + 1];

    que[0].type = 2, que[0].l = 1, que[0].r = 5;
    que[1].type = 1, que[1].l = 1, que[1].r = 2;
    que[2].type = 1, que[2].l = 2, que[2].r = 4;
    que[3].type = 2, que[3].l = 1, que[3].r = 5;

    // answer the Queries
    answerQueries(arr, que, n, q);

    return 0;
}
```

## 蟒蛇 3

```
# Python program to calculate sum
# in an interval and update with
# square root
from typing import List
import bisect
from math import sqrt, floor

# Maximum size of input array
MAX = 100
BIT = [0 for _ in range(MAX + 1)]

# structure for queries with members type,
# leftIndex, rightIndex of the query
class queries:
    def __init__(self, type: int = 0, l: int = 0, r: int = 0) -> None:
        self.type = type
        self.l = l
        self.r = r

# function for updating the value
def update(x: int, val: int, n: int) -> None:
    a = x
    while a <= n:
        BIT[a] += val
        a += a & -a

# function for calculating the required
# sum between two indexes
def sum(x: int) -> int:
    s = 0
    a = x
    while a:
        s += BIT[a]
        a -= a & -a

    return s

# function to return answer to queries
def answerQueries(arr: List[int], que: List[queries], n: int, q: int) -> None:

    # Declaring a Set
    s = set()
    for i in range(1, n):

        # inserting indexes of those numbers
        # which are greater than 1
        if (arr[i] > 1):
            s.add(i)
        update(i, arr[i], n)

    for i in range(q):

        # update query
        if (que[i].type == 1):
            while True:
                ss = list(sorted(s))

                # find the left index of query in
                # the set using binary search
                # auto it = s.lower_bound(que[i].l);
                it = bisect.bisect_left(ss, que[i].l)

                # if it crosses the right index of
                # query or end of set, then break
                if it == len(s) or ss[it] > que[i].r:
                    break
                que[i].l = ss[it]

                # update the value of arr[i] to
                # itss square root
                update(ss[it], floor(sqrt(arr[ss[it]]) - arr[ss[it]]), n)

                arr[ss[it]] = floor(sqrt(arr[ss[it]]))

                # if updated value becomes equal to 1
                # remove it from the set
                if (arr[ss[it]] == 1):
                    s.remove(ss[it])

                # increment the index
                que[i].l += 1

        # sum query
        else:
            print(sum(que[i].r) - sum(que[i].l - 1))

# Driver Code
if __name__ == "__main__":

    q = 4

    # input array using 1-based indexing
    arr = [0, 4, 5, 1, 2, 4]
    n = len(arr)
    # declaring array of structure of type queries
    que = [queries() for _ in range(q + 1)]

    que[0].type, que[0].l, que[0].r = 2, 1, 5
    que[1].type, que[1].l, que[1].r = 1, 1, 2
    que[2].type, que[2].l, que[2].r = 1, 2, 4
    que[3].type, que[3].l, que[3].r = 2, 1, 5

    # answer the Queries
    answerQueries(arr, que, n, q)

# This code is contributed by sanjeev2552
```

**Output:** 

```
16
9
```

**时间复杂度:**每查询 O(logN)
T3】辅助空间: O(N)