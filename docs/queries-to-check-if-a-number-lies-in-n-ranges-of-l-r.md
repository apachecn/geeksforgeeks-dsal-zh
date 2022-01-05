# 查询一个数字是否在 L-R 的 N 个范围内

> 原文:[https://www . geesforgeks . org/query-to-check-a-number-in-n-ranges-l-r/](https://www.geeksforgeeks.org/queries-to-check-if-a-number-lies-in-n-ranges-of-l-r/)

给定 N 个范围和由数字组成的 Q 个查询。每个范围由 L 和 r 组成。任务是检查每个查询的给定数字是否在任何给定范围内。
**注:**无重叠范围。
**示例:**

> **输入:**范围[] = { {5，6}，{1，3}，{8，10}
> Q = 4
> 第一次查询:2
> 第二次查询:3
> 第三次查询:4
> 第四次查询:7
> **输出:**
> 是
> 是
> 否
> 否
> 第一次查询:2 位于范围 1-3
> 第二次查询:3 位于范围 1-3【T0
> 第四次查询:7 不在任何给定范围内。

**方法:**下面是解决这个问题的分步算法:

1.  将每个范围的 L 散列为 1，将每个范围的 R 散列为 2。
2.  将左侧和右侧分别推入容器。
3.  对容器中的元素进行排序，所有范围 L 和 R 将彼此相邻，因为它们不重叠。
4.  对于每个查询，使用二分搜索法查找第一次出现的等于或大于它的数字。这可以使用[下限](https://www.geeksforgeeks.org/lower_bound-in-cpp/)函数来完成。
5.  如果有任何值等于该查询，则该数字与该范围重叠。
6.  如果没有与查询相等的值，则检查较大的元素是否被散列为 1 或 2。
7.  如果它被散列为 1，则该数字不会重叠，否则它会重叠。

**以下是上述方法的实施:**

## C++

```
// C++ program to check if the
// number lies in given range
#include <bits/stdc++.h>

using namespace std;

// Function that answers every query
void answerQueries(int a[][2], int n, int queries[], int q)
{

    // container to store all range
    vector<int> v;

    // hash the L and R
    unordered_map<int, int> mpp;

    // Push the element to container
    // and hash the L and R
    for (int i = 0; i < n; i++) {

        v.push_back(a[i][0]);
        mpp[a[i][0]] = 1;
        v.push_back(a[i][1]);
        mpp[a[i][1]] = 2;
    }

    // sort the elements in container
    sort(v.begin(), v.end());
    for (int i = 0; i < q; i++) {

        // each query
        int num = queries[i];

        // get the number same or greater than integer
        int ind = lower_bound(v.begin(), v.end(), num) - v.begin();

        // if it lies
        if (v[ind] == num) {
            cout << "Yes\n";
        }

        else {

            // check if greater is hashed as 2
            if (mpp[v[ind]] == 2)
                cout << "Yes\n";

            else // check if greater is hashed as 1
                cout << "No\n";
        }
    }
}

// Driver code
int main()
{
    int a[][2] = { { 5, 6 }, { 1, 3 }, { 8, 10 } };

    int n = 3;

    int queries[] = { 2, 3, 4, 7 };

    int q = sizeof(queries) / sizeof(queries[0]);

    // function call to answer queries
    answerQueries(a, n, queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the
// number lies in given range
import java.io.*;
import java.util.*;

class GFG
{

    // Function that answers every query
    static void answerQueries(int[][] a, int n,
                               int[] queries, int q)
    {

        // container to store all range
        Vector<Integer> v = new Vector<>();

        // hash the L and R
        HashMap<Integer, Integer> mpp = new HashMap<>();

        // Push the element to container
        // and hash the L and R
        for (int i = 0; i < n; i++)
        {
            v.add(a[i][0]);
            mpp.put(a[i][0], 1);
            v.add(a[i][1]);
            mpp.put(a[i][1], 2);
        }

        // sort the elements in container
        Collections.sort(v);
        for (int i = 0; i < q; i++)
        {

            // each query
            int num = queries[i];

            // get the number same or greater than integer
            int ind = lowerBound(v, num);

            // if it lies
            if (ind >= 0 && v.elementAt(ind) == num)
                System.out.println("Yes");

            else
            {

                // check if greater is hashed as 2
                if (ind >= 0 && mpp.get(v.elementAt(ind)) == 2)
                    System.out.println("Yes");

                else // check if greater is hashed as 1
                    System.out.println("No");
            }
        }
    }

    // Lower bound implementation
    static int lowerBound(Vector<Integer> array, int value)
    {
        int low = 0;
        int high = array.size();
        while (low < high)
        {
            final int mid = (low + high) / 2;
            if (value <= array.elementAt(mid))
            {
                high = mid;
            }
            else
            {
                low = mid + 1;
            }
        }
        return low;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[][] a = {{ 5, 6 }, { 1, 3 }, { 8, 10 }};
        int n = 3;
        int[] queries = {2, 3, 4, 7};
        int q = queries.length;

        // function call to answer queries
        answerQueries(a, n, queries, q);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python program to check if the
# number lies in given range
from bisect import bisect_left as lower_bound

# Function that answers every query
def answerQueries(a: list, n, queries: list, q):

    # container to store all range
    v = list()

    # hash the L and R
    mpp = dict()

    # Push the element to container
    # and hash the L and R
    for i in range(n):
        v.append(a[i][0])
        mpp[a[i][0]] = 1
        v.append(a[i][1])
        mpp[a[i][1]] = 2

    # sort the elements in container
    v.sort()
    for i in range(q):

        # each query
        num = queries[i]

        # get the number same or greater than integer
        ind = lower_bound(v, num)

        # if it lies
        if v[ind] == num:
            print("Yes")
        else:

            # check if greater is hashed as 2
            if mpp[v[ind]] == 2:
                print("Yes")

            # check if greater is hashed as 1
            else:
                print("No")

# Driver Code
if __name__ == "__main__":
    a = [[5, 6], [1, 3], [8, 10]]
    n = 3
    queries = [2, 3, 4, 7]
    q = len(queries)

    # function call to answer queries
    answerQueries(a, n, queries, q)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check if the
// number lies in given range
using System;
using System.Collections.Generic;

class GFG
{

    // Function that answers every query
    static void answerQueries(int[,] a, int n,
                            int[] queries, int q)
    {

        // container to store all range
        List<int> v = new List<int>();

        // hash the L and R
        Dictionary<int, int> mpp = new Dictionary<int, int>();

        // Push the element to container
        // and hash the L and R
        for (int i = 0; i < n; i++)
        {
            v.Add(a[i, 0]);
            if(!mpp.ContainsKey(a[i, 0]))
                mpp.Add(a[i, 0], 1);
            v.Add(a[i, 1]);
            if(!mpp.ContainsKey(a[i, 1]))
                mpp.Add(a[i, 1], 2);
        }

        // sort the elements in container
        v.Sort();
        for (int i = 0; i < q; i++)
        {

            // each query
            int num = queries[i];

            // get the number same or greater than integer
            int ind = lowerBound(v, num);

            // if it lies
            if (ind >= 0 && v[ind] == num)
                Console.WriteLine("Yes");

            else
            {

                // check if greater is hashed as 2
                if (ind >= 0 && mpp[v[ind]] == 2)
                    Console.WriteLine("Yes");

                else // check if greater is hashed as 1
                    Console.WriteLine("No");
            }
        }
    }

    // Lower bound implementation
    static int lowerBound(List<int> array, int value)
    {
        int low = 0;
        int high = array.Count;
        while (low < high)
        {
            int mid = (low + high) / 2;
            if (value <= array[mid])
            {
                high = mid;
            }
            else
            {
                low = mid + 1;
            }
        }
        return low;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        int[,] a = {{ 5, 6 }, { 1, 3 }, { 8, 10 }};
        int n = 3;
        int[] queries = {2, 3, 4, 7};
        int q = queries.Length;

        // function call to answer queries
        answerQueries(a, n, queries, q);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to check if the
// number lies in given range

// Function that answers every query
function answerQueries(a, n, queries, q)
{

    // container to store all range
        let v = [];

        // hash the L and R
        let mpp = new Map();

        // Push the element to container
        // and hash the L and R
        for (let i = 0; i < n; i++)
        {
            v.push(a[i][0]);
            mpp.set(a[i][0], 1);
            v.push(a[i][1]);
            mpp.set(a[i][1], 2);
        }

        // sort the elements in container
        v.sort(function(a,b){return a-b;});
        for (let i = 0; i < q; i++)
        {

            // each query
            let num = queries[i];

            // get the number same or greater than integer
            let ind = lowerBound(v, num);

            // if it lies
            if (ind >= 0 && v[ind] == num)
                document.write("Yes<br>");

            else
            {

                // check if greater is hashed as 2
                if (ind >= 0 && mpp.get(v[ind]) == 2)
                    document.write("Yes<br>");

                else // check if greater is hashed as 1
                    document.write("No<br>");
            }
        }
}

// Lower bound implementation
function lowerBound(array,value)
{
    let low = 0;
        let high = array.length;
        while (low < high)
        {
            let mid = Math.floor((low + high) / 2);
            if (value <= array[mid])
            {
                high = mid;
            }
            else
            {
                low = mid + 1;
            }
        }
        return low;
}

// Driver Code
let a=[[ 5, 6 ], [ 1, 3 ], [ 8, 10 ]];
let n = 3;
let queries=[2, 3, 4, 7];
let q = queries.length;

// function call to answer queries
answerQueries(a, n, queries, q);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Yes
Yes
No
No
```