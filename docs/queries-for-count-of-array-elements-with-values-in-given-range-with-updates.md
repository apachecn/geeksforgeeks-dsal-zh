# 通过更新查询给定范围内值的数组元素的计数

> 原文:[https://www . geesforgeks . org/query-for-count-of-of-array-of-elements-with-values-in-给定范围-with-updates/](https://www.geeksforgeeks.org/queries-for-count-of-array-elements-with-values-in-given-range-with-updates/)

给定大小为 **N** 的数组 **arr[]** 和由以下两种类型的查询组成的矩阵 **Q** :

*   **1 L R :** 打印位于[L，R]范围内的元素数量。
*   **2 i x :** 设置 arr[i] = x

**示例:**

> **输入:** arr[] = {1，2，2，3，4，4，5，6}，Q = {{1，{3，5}}，{1，{2，4}}，{1，{1，2}，{1，7}}，{1，{1，2 } }
> T3】输出:4 5 3 2
> T6】解释:
> 范围内的数组元素为{3，4，4 2}
> 将 arr[1]替换为 7 会将数组修改为{1，7，2，3，4，4，5，6}
> 范围[1，2]内的元素是{1，2}
> 
> **输入:** arr = {5，5，1，3，4，4，2，3}，Q = {{1，{3，6}}，{1，{2，4}}，{1，{10，20 } }
> T3】输出:6 5 0
> T6】解释:
> 范围内的数组元素是【3，6】范围内的数组元素{3，3，4，4，5，5}
> 范围内的数组元素

**天真的方法:**
解决这个问题最简单的方法如下:

*   对于类型为 **(1 L R)** 的查询，迭代整个数组并计算数组中的元素数量，使得 **L ≤ arr[i] ≤ R** 。最后，打印计数。
*   对于类型 **(2 i x)** 的查询，将**arr【I】**替换为 **x** 。

下面是上述方法的实现:

## C++

```
// C++ code for queries for number
// of elements that lie in range
// [l, r] (with updates)
#include <bits/stdc++.h>
using namespace std;

// Function to set arr[index] = x
void setElement(int* arr, int n,
                int index, int x)
{
    arr[index] = x;
}

// Function to get count of elements
// that lie in range [l, r]
int getCount(int* arr, int n,
            int l, int r)
{
    int count = 0;

    // Traverse array
    for (int i = 0; i < n; i++) {

        // If element lies in the
        // range [L, R]
        if (arr[i] >= l
            && arr[i] <= r) {

            // Increase count
            count++;
        }
    }
    return count;
}

// Function to solve each query
void SolveQuery(int arr[], int n,
                vector<pair<int,
                            pair<int, int> > >
                    Q)
{
    int x;

    for (int i = 0; i < Q.size(); i++) {
        if (Q[i].first == 1) {
            x = getCount(arr, n,
                        Q[i].second.first,
                        Q[i].second.second);

            cout << x << " ";
        }
        else {
            setElement(arr, n,
                    Q[i].second.first,
                    Q[i].second.second);
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 3, 4, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    vector<pair<int, pair<int, int> > > Q
        = { { 1, { 3, 5 } },
            { 1, { 2, 4 } },
            { 1, { 1, 2 } },
            { 2, { 1, 7 } },
            { 1, { 1, 2 } } };
    SolveQuery(arr, n, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for queries for number
// of elements that lie in range
// [l, r] (with updates)
import java.util.*;
import java.lang.*;

class GFG{

// Function to set arr[index] = x
static void setElement(int[] arr, int n,
                       int index, int x)
{
    arr[index] = x;
}

// Function to get count of elements
// that lie in range [l, r]
static int getCount(int[] arr, int n,
                    int l, int r)
{
    int count = 0;

    // Traverse array
    for(int i = 0; i < n; i++)
    {

        // If element lies in the
        // range [L, R]
        if (arr[i] >= l && arr[i] <= r)
        {
            // Increase count
            count++;
        }
    }
    return count;
}

// Function to solve each query
static void SolveQuery(int arr[], int n,
                       ArrayList<List<Integer>> Q)
{
    int x;

    for(int i = 0; i < Q.size(); i++)
    {
        if (Q.get(i).get(0) == 1)
        {
            x = getCount(arr, n,
                         Q.get(i).get(1),
                         Q.get(i).get(2));

            System.out.print(x + " ");
        }
        else
        {
            setElement(arr, n,
                       Q.get(i).get(1),
                       Q.get(i).get(2));
        }
    }
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 2, 3, 4, 4, 5, 6 };
    int n = arr.length;

    ArrayList<List<Integer>> Q = new ArrayList<>();
    Q.add(Arrays.asList(1, 3, 5));
    Q.add(Arrays.asList(1, 2, 4)); 
    Q.add(Arrays.asList(1, 1, 2));
    Q.add(Arrays.asList(2, 1, 7));
    Q.add(Arrays.asList(1, 1, 2));

    SolveQuery(arr, n, Q);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 code for queries for number
# of elements that lie in range
# [l, r] (with updates)
from typing import Generic, List, TypeVar

T = TypeVar('T')
V = TypeVar('V')

class Pair(Generic[V, T]):

    def __init__(self, first: V, second: T) -> None:

        self.first = first
        self.second = second

# Function to set arr[index] = x
def setElement(arr: List[int], n: int,
                   index: int, x: int) -> None:

    arr[index] = x

# Function to get count of elements
# that lie in range [l, r]
def getCount(arr: List[int], n: int,
                     l: int, r: int) -> int:

    count = 0

    # Traverse array
    for i in range(n):

        # If element lies in the
        # range [L, R]
        if (arr[i] >= l and arr[i] <= r):

            # Increase count
            count += 1

    return count

# Function to solve each query
def SolveQuery(arr: List[int], n: int,
            Q: List[Pair[int, Pair[int, int]]]):

    x = 0

    for i in range(len(Q)):
        if (Q[i].first == 1):
            x = getCount(arr, n, Q[i].second.first,
                                 Q[i].second.second)
            print(x, end = " ")
        else:
            setElement(arr, n, Q[i].second.first,
                               Q[i].second.second)

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 2, 3, 4, 4, 5, 6 ]
    n = len(arr)

    Q = [ Pair(1, Pair(3, 5)),
          Pair(1, Pair(2, 4)),
          Pair(1, Pair(1, 2)),
          Pair(2, Pair(1, 7)),
          Pair(1, Pair(1, 2)) ]

    SolveQuery(arr, n, Q)

# This code is contributed by sanjeev2552
```

## C#

```
// C# code for queries for number
// of elements that lie in range
// [l, r] (with updates)
using System;
using System.Collections.Generic;

class GFG{

// Function to set arr[index] = x
static void setElement(int[] arr, int n,
                       int index, int x)
{
    arr[index] = x;
}

// Function to get count of elements
// that lie in range [l, r]
static int getCount(int[] arr, int n,
                    int l, int r)
{
    int count = 0;

    // Traverse array
    for(int i = 0; i < n; i++)
    {

        // If element lies in the
        // range [L, R]
        if (arr[i] >= l && arr[i] <= r)

            // Increase count
            count += 1;
    }
    return count;
}

// Function to solve each query
static void SolveQuery(int[] arr, int n,
             List<List<int>> Q)
{
    int x;

    for(int i = 0; i < Q.Count; i++)
    {
        if (Q[i][0] == 1)
        {
            x = getCount(arr, n,
                         Q[i][1],
                         Q[i][2]);

            Console.Write(x + " ");
        }
        else
        {
            setElement(arr, n,
                       Q[i][1],
                       Q[i][2]);
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = { 1, 2, 2, 3, 4, 4, 5, 6 };
    int n = arr.Length;

    List<List<int>> myList = new List<List<int>>();
    myList.Add(new List<int>{ 1, 3, 5 });
    myList.Add(new List<int>{ 1, 2, 4 });
    myList.Add(new List<int>{ 1, 1, 2 });
    myList.Add(new List<int>{ 2, 1, 7 });
    myList.Add(new List<int>{ 1, 1, 2 });

    SolveQuery(arr, n, myList);
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>
// Javascript code for queries for number
// of elements that lie in range
// [l, r] (with updates)

// Function to set arr[index] = x
function setElement(arr, n, index, x)
{
    arr[index] = x;
}

// Function to get count of elements
// that lie in range [l, r]
function getCount(arr, n, l, r)
{
    let count = 0;

    // Traverse array
    for (let i = 0; i < n; i++) {

        // If element lies in the
        // range [L, R]
        if (arr[i] >= l
            && arr[i] <= r) {

            // Increase count
            count++;
        }
    }
    return count;
}

// Function to solve each query
function SolveQuery(arr, n, Q) {
    let x;

    for (let i = 0; i < Q.length; i++) {
        if (Q[i][0] == 1) {
            x = getCount(arr, n,
                Q[i][1][0],
                Q[i][1][1]);

            document.write(x + " ");
        }
        else {
            setElement(arr, n,
                Q[i][1][0],
                Q[i][1][1]);
        }
    }
}

// Driver Code
let arr = [ 1, 2, 2, 3, 4, 4, 5, 6 ];
let n = arr.length;

let Q
    = [[1, [3, 5]],
    [1, [2, 4]],
    [1, [1, 2]],
    [2, [1, 7]],
    [1, [1, 2]]];
SolveQuery(arr, n, Q);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
4 5 3 2
```

***时间复杂度:** O(Q * N)*
***辅助空间:** O(1)*

**高效方法:**
使用[芬威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)可以优化上述方法。按照以下步骤解决问题:

*   从给定的数组中构建一个[分支树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)。
*   Fenwick 树将被表示为一个大小等于数组中[最大元素的数组，这样数组元素就可以作为索引(思路类似于](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)[这个](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)的做法)。
*   遍历数组，通过调用芬威克树的**更新**方法增加每个元素的出现频率。
*   对于每一个类型为 **(1 L R)** 的查询，调用分威克树的 **getSum** 方法。类型 1 查询的答案是:

> getsum(r)-getsum(l–1)

*   对于每一个类型为 **(2 i x)** 的查询，调用分威克树的**更新**方法，增加添加元素的频率，减少要替换元素的数量。

下面是上述方法的实现:

## C++

```
// C++ code for queries for number
// of elements that lie in range
// [l, r] (with updates)
#include <bits/stdc++.h>
using namespace std;

class FenwickTree {
public:
    int* BIT;
    int N;

    FenwickTree(int N)
    {
        this->N = N;
        BIT = new int[N];
        for (int i = 0; i < N; i++) {
            BIT[i] = 0;
        }
    }

    // Traverse all ancestors and
    // increase frequency of index
    void update(int index, int increment)
    {
        while (index < N) {

            // Increase count of the current
            // node of BIT Tree
            BIT[index] += increment;

            // Update index to that of parent
            // in update View
            index += (index & -index);
        }
    }
    // Function to return the
    // sum of arr[0..index]
    int getSum(int index)
    {
        int sum = 0;

        // Traverse ancestors of
        // BITree[index]
        while (index > 0) {

            // Add current element of
            // BITree to sum
            sum += BIT[index];

            // Move index to parent node in
            // getSum View
            index -= (index & -index);
        }
        return sum;
    }
};

// Function to set arr[index] = x
void setElement(int* arr, int n,
                int index, int x,
                FenwickTree* fenTree)
{
    int removedElement = arr[index];
    fenTree->update(removedElement, -1);
    arr[index] = x;
    fenTree->update(x, 1);
}

// Function to get count of
// elements that lie in
// range [l, r]
int getCount(int* arr, int n,
            int l, int r,
            FenwickTree* fenTree)
{
    int count = fenTree->getSum(r)
                - fenTree->getSum(l - 1);
    return count;
}

// Function to solve each query
void SolveQuery(int arr[], int n,
                vector<pair<int,
                            pair<int, int> > >
                    Q)
{
    int N = 100001;

    FenwickTree* fenTree = new FenwickTree(N);

    for (int i = 0; i < n; i++) {
        fenTree->update(arr[i], 1);
    }

    int x;

    for (int i = 0; i < Q.size(); i++) {
        if (Q[i].first == 1) {
            x = getCount(arr, n,
                        Q[i].second.first,
                        Q[i].second.second,
                        fenTree);

            cout << x << " ";
        }
        else {
            setElement(arr, n,
                    Q[i].second.first,
                    Q[i].second.second,
                    fenTree);
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 3,
                4, 4, 5, 6 };

    int n = sizeof(arr) / sizeof(arr[0]);
    vector<pair<int, pair<int, int> > > Q
        = { { 1, { 3, 5 } },
            { 1, { 2, 4 } },
            { 1, { 1, 2 } },
            { 2, { 1, 7 } },
            { 1, { 1, 2 } } };

    SolveQuery(arr, n, Q);

    return 0;
}
```

**Output:** 

```
4 5 3 2
```

***时间复杂度:**O(N * log(N)+Q * log(N))*
***辅助空间:** O(maxm)，其中 maxm 是数组中存在的最大元素。*