# 用阶乘范围和更新和查询

> 原文:[https://www . geeksforgeeks . org/range-and-update-sum-带有阶乘的查询/](https://www.geeksforgeeks.org/range-and-update-sum-queries-with-factorial/)

给定一个数组**arr[]****N**整数和查询数量 **Q** 。任务是回答三种类型的查询。

1.  **更新【l，r】**–对于范围**【l，r】**内的每个 **i** ，将**arr【I】**增加 **1** 。
2.  **更新【l，val】**–将**arr【l】**的值更改为 **val** 。
3.  **查询【l，r】**–计算**arr【I】之和！% 10<sup>9</sup>T5】适用于范围**【l，r】**内的所有 **i** ，其中**arr【I】！**是**arr【I】**的**因子**。**

**先决条件:** [二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) | [分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

**示例:**

> **输入:** Q = 6，arr[] = { 1，2，1，4，5 }
> 3 1 5
> 1 1 3
> 2 2 4
> 3 2 4
> 1 2 5
> 3 1 5
> **输出:**T11】148
> 50
> 968
> 1<sup>ST</sup>查询，需要的和为(1！+ 2!+ 1!+ 4!+ 5!)% 10<sup>9</sup>= 148
> 2<sup>nd</sup>查询，数组变成 arr[] = { 2，3，2，4，5 }
> 3 <sup>rd</sup> 查询，数组变成 arr[] = { 2，4，2，4，5 }
> 4 <sup>th</sup> 查询，需要的和为(4！+ 2!+ 4!)% 10 <sup>9</sup> = 50
> 5 <sup>第</sup>次查询，数组变成 arr[] = { 2，5，3，5，6 }
> 6 <sup>第</sup>次查询，需要的和为(2！+ 5!+ 3!+ 5!+ 6!)% 10 <sup>9</sup> = 968

**天真方法:**一个简单的解决方案是运行一个从 **l** 到 **r** 的循环，并为 **3 <sup>rd</sup>** 查询计算给定范围内元素的阶乘之和(预先计算的)。对于 **2 <sup>nd</sup>** 查询，要更新一个值，只需将 **arr[i]** 替换为给定值，即 **arr[i] = val** 。对于 **1 <sup>st</sup>** 类型查询，增加 **arr[i]** 的值，即 **arr[i] = arr[i] + 1** 。

**高效进场:**仔细分析可以观察到 **40！**可以被 10 <sup>9</sup> 整除，这意味着大于 **40** 的每个数的阶乘都可以被 **10 <sup>9</sup>** 整除。因此，我们对**3<sup>3</sup>T15】查询的回答为零。其思想是将每次查询和更新操作的时间复杂度降低到 **O(logN)** 。使用[二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) (BIT)或[分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。构造一个 **BIT[]** 数组，有查询和更新操作两个功能。**

*   现在，对于 **1 <sup>st</sup> 类型**的每一次更新操作，关键的观察是给定范围内的数字最多可以更新到 **40** ，因为在那之后就没有关系了，因为它会给我们的最终答案添加零。我们将使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)来仅存储那些小于 10 的数字的索引，并使用二分搜索法来找到更新查询的 l 索引，并递增 l 索引，直到该更新查询范围内的每个元素都被更新。如果 **arr[i]** 在递增 **1** 后变得大于或等于 **40** ，将其从集合中移除，因为即使在任何下一次更新查询后，它也不会影响我们的总和查询答案。
*   对于 **2 <sup>和</sup>类型**的更新操作，用给定值调用更新函数。另外，给定值为 **< 40** ，将要替换的元素的索引插入到集合中，如果给定值为 **≥ 40** ，将其从集合中移除，因为它在求和查询中没有重要性。
*   对于 **3 <sup>rd</sup> 类型**的总和查询，只需做**查询(r)–查询(l–1)**。

以下是上述方法的实现:

## C++

```
// CPP program to calculate sum of
// factorials in an interval and update
// with two types of operations
#include <bits/stdc++.h>
using namespace std;

// Modulus
const int MOD = 1e9;

// Maximum size of input array
const int MAX = 100;

// Size for factorial array
const int SZ = 40;

int BIT[MAX + 1], fact[SZ + 1];

// structure for queries with members type,
// leftIndex, rightIndex of the query
struct queries {
    int type, l, r;
};

// function for updating the value
void update(int x, int val, int n)
{
    for (x; x <= n; x += x & -x)
        BIT[x] += val;
}

// function for calculating the required
// sum between two indexes
int sum(int x)
{
    int s = 0;
    for (x; x > 0; x -= x & -x)
        s += BIT[x];
    return s;
}

// function to return answer to queries
void answerQueries(int arr[], queries que[],
                   int n, int q)
{
    // Precomputing factorials
    fact[0] = 1;
    for (int i = 1; i < 41; i++)
        fact[i] = (fact[i - 1] * i) % MOD;

    // Declaring a Set
    set<int> s;
    for (int i = 1; i < n; i++) {

        // inserting indexes of those
        // numbers which are lesser
        // than 40
        if (arr[i] < 40) {
            s.insert(i);
            update(i, fact[arr[i]], n);
        }
        else
            update(i, 0, n);
    }

    for (int i = 0; i < q; i++) {

        // update query of the 1st type
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
                int val = arr[*it] + 1;

                // update the value of arr[i] to
                // its new value
                update(*it, fact[val] - fact[arr[*it]], n);

                arr[*it]++;

                // if updated value becomes greater
                // than or equal to 40 remove it from
                // the set
                if (arr[*it] >= 40)
                    s.erase(*it);

                // increment the index
                que[i].l++;
            }
        }

        // update query of the 2nd type
        else if (que[i].type == 2) {
            int idx = que[i].l;
            int val = que[i].r;

            // update the value to its new value
            update(idx, fact[val] - fact[arr[idx]], n);

            arr[idx] = val;

            // If the value is less than 40, insert
            // it into set, otherwise remove it
            if (val < 40)
                s.insert(idx);
            else
                s.erase(idx);
        }

        // sum query of the 3rd type
        else
            cout << (sum(que[i].r) - sum(que[i].l - 1))
                 << endl;
    }
}

// Driver Code to test above functions
int main()
{
    int q = 6;

    // input array using 1-based indexing
    int arr[] = { 0, 1, 2, 1, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // declaring array of structure of type queries
    queries que[q + 1];

    que[0].type = 3, que[0].l = 1, que[0].r = 5;
    que[1].type = 1, que[1].l = 1, que[1].r = 3;
    que[2].type = 2, que[2].l = 2, que[2].r = 4;
    que[3].type = 3, que[3].l = 2, que[3].r = 4;
    que[4].type = 1, que[4].l = 2, que[4].r = 5;
    que[5].type = 3, que[5].l = 1, que[5].r = 5;

    // answer the Queries
    answerQueries(arr, que, n, q);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to calculate sum of
# factorials in an interval and update
# with two types of operations
from bisect import bisect_left as lower_bound

# Modulus
MOD = 1e9

# Maximum size of input array
MAX = 100

# Size for factorial array
SZ = 40

BIT = [0] * (MAX + 1)
fact = [0] * (SZ + 1)

# structure for queries with members type,
# leftIndex, rightIndex of the query
class queries:
    def __init__(self, tpe, l, r):
        self.type = tpe
        self.l = l
        self.r = r

# function for updating the value
def update(x, val, n):
    global BIT
    while x <= n:
        BIT[x] += val
        x += x & -x

# function for calculating the required
# sum between two indexes
def summ(x):
    global BIT
    s = 0
    while x > 0:
        s += BIT[x]
        x -= x & -x
    return s

# function to return answer to queries
def answerQueries(arr: list, que: list, 
                       n: int, q: int):
    global fact

    # Precomputing factorials
    fact[0] = 1
    for i in range(1, 41):
        fact[i] = int((fact[i - 1] * i) % MOD)

    # Declaring a Set
    s = set()
    for i in range(1, n):

        # inserting indexes of those
        # numbers which are lesser
        # than 40
        if arr[i] < 40:
            s.add(i)
            update(i, fact[arr[i]], n)
        else:
            update(i, 0, n)

    for i in range(q):

        # update query of the 1st type
        if que[i].type == 1:
            while True:
                s = list(s)
                s.sort()

                # find the left index of query in
                # the set using binary search
                it = lower_bound(s, que[i].l)

                # if it crosses the right index of
                # query or end of set, then break
                if it == len(s) or s[it] > que[i].r:
                    break

                que[i].l = s[it]
                val = arr[s[it]] + 1

                # update the value of arr[i] to
                # its new value
                update(s[it], fact[val] - 
                              fact[arr[s[it]]], n)

                arr[s[it]] += 1

                # if updated value becomes greater
                # than or equal to 40 remove it from
                # the set
                if arr[s[it]] >= 40:
                    s.remove(it)

                # increment the index
                que[i].l += 1

        # update query of the 2nd type
        elif que[i].type == 2:
            s = set(s)
            idx = que[i].l
            val = que[i].r

            # update the value to its new value
            update(idx, fact[val] - fact[arr[idx]], n)

            arr[idx] = val

            # If the value is less than 40, insert
            # it into set, otherwise remove it
            if val < 40:
                s.add(idx)
            else:
                s.remove(idx)

        # sum query of the 3rd type
        else:
            print((summ(que[i].r) - 
                   summ(que[i].l - 1)))

# Driver Code
if __name__ == "__main__":

    q = 6

    # input array using 1-based indexing
    arr = [0, 1, 2, 1, 4, 5]
    n = len(arr)

    # declaring array of structure of type queries
    que = [ queries(3, 1, 5),
            queries(1, 1, 3),
            queries(2, 2, 4),
            queries(3, 2, 4),
            queries(1, 2, 5),
            queries(3, 1, 5) ]

    # answer the Queries
    answerQueries(arr, que, n, q)

# This code is contributed by
# sanjeev2552
```

**Output:**

```
148
50
968

```