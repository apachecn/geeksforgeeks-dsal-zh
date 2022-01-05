# 线性搜索中 m 个查询每个方向的比较次数

> 原文:[https://www . geeksforgeeks . org/线性搜索中 m 个查询每个方向的比较次数/](https://www.geeksforgeeks.org/number-of-comparisons-in-each-direction-for-m-queries-in-linear-search/)

给定一个包含 **N** 个不同元素的数组。有 **M** 个查询，每个查询包含一个整数 **X** 并要求数组中 **X** 的索引。对于每个查询，任务是从左到右执行线性搜索 **X** ，并计算找到 **X** 所需的比较次数，然后从右到左执行相同的操作。最后，打印所有查询中双向比较的总数。
**示例:**

> **输入:** arr[] = {1，2}，q[] = {1，2}
> **输出:** 3，3
> 对于基于 1 的索引
> 对于第一次查询:从左到右的比较数为 1，从右到左的比较数为 2
> 对于第二次查询:从左到右的比较数为 2，从右到左的比较数为 1
> **输入:** arr[] = {-1，2，4，5，1}，q[] = {-1

**方法:**找到数组中出现 **X** 的索引比如说 **i** (基于 1 的索引)，从左到右的比较次数是 **i** ，从右到左的比较次数是**(n–I+1)**。我们需要做的就是快速找到索引。这可以通过使用一个映射来实现，其中键是元素的值，值是索引。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of comparisons from left to right
// and right to left in linear search among m queries
pair<int, int> countCamparisions(int n, int arr[], int m, int qry[])
{
    int i;
    unordered_map<int, int> index;
    for (i = 1; i <= n; i++) {

        // arr[i] occurs at i
        index[arr[i]] = i;
    }

    // Count of comparisons for left to right and right to left
    int ltr = 0, rtl = 0;
    for (i = 1; i <= m; i++) {
        int x = qry[i];
        ltr += index[x];
        rtl += n - index[x] + 1;
    }
    return make_pair(ltr, rtl);
}

// Driver Code
int main()
{
    // -1 will be ignored as it is 1-based indexing
    int arr[] = { -1, 2, 4, 5, 1 };
    int n = (sizeof(arr) / sizeof(arr[0])) - 1;

    int q[] = { -1, 4, 2 };
    int m = (sizeof(q) / sizeof(q[0])) - 1;

    pair<int, int> res = countCamparisions(n, arr, m, q);
    cout << res.first << " " << res.second;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;
import java.util.Map;

class GFG
{

// Function to return the count of
// comparisons from left to right
// and right to left in linear
// search among m queries
static Pair<Integer, Integer> countCamparisions(int n,
                            int arr[], int m, int qry[])
{
    int i;
    HashMap<Integer,Integer> index = new HashMap<>();
    for (i = 1; i <= n; i++)
    {

        // arr[i] occurs at i
        index.put(arr[i], i);
    }

    // Count of comparisons for left
    // to right and right to left
    int ltr = 0, rtl = 0;
    for (i = 1; i <= m; i++)
    {
        int x = qry[i];
        ltr += index.get(x);
        rtl += n - index.get(x) + 1;
    }

    Pair<Integer, Integer> ans = new Pair<>(ltr, rtl);
    return ans;
}

    // Driver Code
    public static void main(String []args)
    {

        // -1 will be ignored as it is 1-based indexing
        int arr[] = { -1, 2, 4, 5, 1 };
        int n = arr.length - 1;

        int q[] = { -1, 4, 2 };
        int m = q.length - 1;

        Pair<Integer, Integer> res = countCamparisions(n, arr, m, q);
        System.out.println(res.first + " " + res.second);
    }
}

class Pair<A, B>
{
    A first;
    B second;

    public Pair(A first, B second)
    {
        this.first = first;
        this.second = second;
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function to return the count of
# comparisons from left to right
# and right to left in linear search
# among m queries
def countCamparisions(n, arr, m, qry) :

    index = {}
    for i in range(1, n + 1) :

        # arr[i] occurs at i
        index[arr[i]] = i

    # Count of comparisons for left to
    # right and right to left
    ltr, rtl = 0, 0
    for i in range(1, m + 1) :
        x = qry[i]
        ltr += index[x]
        rtl += n - index[x] + 1

    return (ltr, rtl)

# Driver Code
if __name__ == "__main__" :

    # -1 will be ignored as it
    # is 1-based indexing
    arr = [ -1, 2, 4, 5, 1 ]
    n = len(arr) - 1

    q = [ -1, 4, 2 ]
    m = len(q) - 1

    res = countCamparisions(n, arr, m, q)
    print(res[0], res[1])

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count of
// comparisons from left to right
// and right to left in linear
// search among m queries
static Pair<int,
            int> countCamparisions(int n, int []arr,
                                   int m, int []qry)
{
    int i;
    Dictionary<int,
               int> index = new Dictionary<int,
                                           int>();
    for (i = 1; i <= n; i++)
    {

        // arr[i] occurs at i
        index.Add(arr[i], i);
    }

    // Count of comparisons for left
    // to right and right to left
    int ltr = 0, rtl = 0;
    for (i = 1; i <= m; i++)
    {
        int x = qry[i];
        ltr += index[x];
        rtl += n - index[x] + 1;
    }

    Pair<int,
         int> ans = new Pair<int,
                             int>(ltr, rtl);
    return ans;
}

// Driver Code
public static void Main(String []args)
{

    // -1 will be ignored as
    // it is 1-based indexing
    int []arr = { -1, 2, 4, 5, 1 };
    int n = arr.Length - 1;

    int []q = { -1, 4, 2 };
    int m = q.Length - 1;

    Pair<int, int> res = countCamparisions(n, arr, m, q);
    Console.WriteLine(res.first + " " + res.second);
}
}

class Pair<A, B>
{
    public A first;
    public B second;

    public Pair(A first, B second)
    {
        this.first = first;
        this.second = second;
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of comparisons from left to right
// and right to left in linear search among m queries
function countCamparisions(n, arr, m, qry)
{
    var i;
    var index = new Map();
    for (i = 1; i <= n; i++) {

        // arr[i] occurs at i
        index.set(arr[i], i);
    }

    // Count of comparisons for left to right and right to left
    var ltr = 0, rtl = 0;
    for (i = 1; i <= m; i++) {
        var x = qry[i];
        ltr += index.get(x);
        rtl += n - index.get(x) + 1;
    }
    return [ltr, rtl];
}

// Driver Code
// -1 will be ignored as it is 1-based indexing
var arr = [-1, 2, 4, 5, 1];
var n = arr.length - 1;
var q = [-1, 4, 2];
var m = q.length - 1;
var res = countCamparisions(n, arr, m, q);
document.write( res[0] + " " + res[1]);

// This code is contributed by famously.
</script>
```

**Output:** 

```
3 7
```

**时间复杂度:**O(N+M)
T3】辅助空间: O(N)