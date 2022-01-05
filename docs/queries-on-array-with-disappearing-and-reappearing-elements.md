# 查询具有消失和重现元素的数组

> 原文:[https://www . geeksforgeeks . org/带有消失和重新出现元素的数组查询/](https://www.geeksforgeeks.org/queries-on-array-with-disappearing-and-reappearing-elements/)

给定一个数组，大小为 **N** 的 **arr[]** 。每一秒钟，一个整数消失 **N** 秒钟，在 **N** 秒钟后，它重新出现在原来的位置。整数从左到右依次消失 **arr[0]，arr[1]，…，arr[N–1]**。所有整数消失后，它们开始重新出现，直到所有整数重新出现。一旦 **N** 元素再次出现，过程再次开始。
现在给出 **Q** 查询，每个查询由两个整数 **t** 和 **M** 组成。任务是在第二个**t<sup>t</sup>处从左侧确定 **M <sup>第</sup>T22】元素。如果在 **M 之前数组不存在，**则打印 **-1** 。****

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，Q = {{1，4}，{6，1}，{3，5}}
> **输出:**
> 5
> 1
> -1
> 在时间，
> t1 - > {2，3，4，5}
> t2 - > {3，4，5}
> t3 - > {4，5}
> 
> **输入:** arr[] = {5，4，3，4，5}，Q = {{2，3}，{100000000，2}}
> **输出:**
> 5
> 4

**方式:**主要的方式是要求检查数组是空的还是满的，用圈数除以数组的大小就可以看出来。如果余数为 0，则它可以是两种情况之一(空或满)。
通过观察，可以看到在奇数圈时数组在减少，在偶数圈时数组在扩大，利用这个观察，可以检查 M 是在索引之外还是在数组之内。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the queries
void PerformQueries(vector<int>& a,
                    vector<pair<long long, int> >& vec)
{

    vector<int> ans;

    // Size of the array with
    // 1-based indexing
    int n = (int)a.size() - 1;

    // Number of queries
    int q = (int)vec.size();

    // Iterating through the queries
    for (int i = 0; i < q; ++i) {

        long long t = vec[i].first;
        int m = vec[i].second;

        // If m is more than the
        // size of the array
        if (m > n) {
            ans.push_back(-1);
            continue;
        }

        // Count of turns
        int turn = t / n;

        // Find the remainder
        int rem = t % n;

        // If the remainder is 0 and turn is
        // odd then the array is empty
        if (rem == 0 and turn % 2 == 1) {
            ans.push_back(-1);
            continue;
        }

        // If the remainder is 0 and turn is
        // even then array is full and
        // is in its initial state
        if (rem == 0 and turn % 2 == 0) {
            ans.push_back(a[m]);
            continue;
        }

        // If the remainder is not 0
        // and the turn is even
        if (turn % 2 == 0) {

            // Current size of the array
            int cursize = n - rem;

            if (cursize < m) {
                ans.push_back(-1);
                continue;
            }
            ans.push_back(a[m + rem]);
        }
        else {

            // Current size of the array
            int cursize = rem;
            if (cursize < m) {
                ans.push_back(-1);
                continue;
            }
            ans.push_back(a[m]);
        }
    }

    // Print the result
    for (int i : ans)
        cout << i << "\n";
}

// Driver code
int main()
{

    // The initial array, -1 is for
    // 1 base indexing
    vector<int> a = { -1, 1, 2, 3, 4, 5 };

    // Queries in the form of the pairs of (t, M)
    vector<pair<long long, int> > vec = {
        { 1, 4 },
        { 6, 1 },
        { 3, 5 }
    };

    PerformQueries(a, vec);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

class GFG
{

    // Function to perform the queries
    static void PerformQueries(int[] a, int[][] vec)
    {

        Vector<Integer> ans = new Vector<>();

        // Size of the array with
        // 1-based indexing
        int n = (int) a.length - 1;

        // Number of queries
        int q = (int) vec.length;

        // Iterating through the queries
        for (int i = 0; i < q; ++i)
        {

            long t = vec[i][0];
            int m = vec[i][1];

            // If m is more than the
            // size of the array
            if (m > n)
            {
                ans.add(-1);
                continue;
            }

            // Count of turns
            int turn = (int) (t / n);

            // Find the remainder
            int rem = (int) (t % n);

            // If the remainder is 0 and turn is
            // odd then the array is empty
            if (rem == 0 && turn % 2 == 1)
            {
                ans.add(-1);
                continue;
            }

            // If the remainder is 0 and turn is
            // even then array is full and
            // is in its initial state
            if (rem == 0 && turn % 2 == 0)
            {
                ans.add(a[m]);
                continue;
            }

            // If the remainder is not 0
            // and the turn is even
            if (turn % 2 == 0)
            {

                // Current size of the array
                int cursize = n - rem;

                if (cursize < m)
                {
                    ans.add(-1);
                    continue;
                }
                ans.add(a[m + rem]);
            }
            else
            {

                // Current size of the array
                int cursize = rem;
                if (cursize < m)
                {
                    ans.add(-1);
                    continue;
                }
                ans.add(a[m]);
            }
        }

        // Print the result
        for (int i : ans)
            System.out.print(i + "\n");
    }

    // Driver code
    public static void main(String[] args)
    {

        // The initial array, -1 is for
        // 1 base indexing
        int[] a = { -1, 1, 2, 3, 4, 5 };

        // Queries in the form of the pairs of (t, M)
        int[][] vec = { { 1, 4 }, { 6, 1 }, { 3, 5 } };

        PerformQueries(a, vec);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to perform the queries
def PerformQueries(a, vec) :

    ans = [];

    # Size of the array with
    # 1-based indexing
    n = len(a) - 1;

    # Number of queries
    q = len(vec);

    # Iterating through the queries
    for i in range(q) :

        t = vec[i][0];
        m = vec[i][1];

        # If m is more than the
        # size of the array
        if (m > n) :
            ans.append(-1);
            continue;

        # Count of turns
        turn = t // n;

        # Find the remainder
        rem = t % n;

        # If the remainder is 0 and turn is
        # odd then the array is empty
        if (rem == 0 and turn % 2 == 1) :
            ans.append(-1);
            continue;

        # If the remainder is 0 and turn is
        # even then array is full and
        # is in its initial state
        if (rem == 0 and turn % 2 == 0) :
            ans.append(a[m]);
            continue;

        # If the remainder is not 0
        # and the turn is even
        if (turn % 2 == 0) :

            # Current size of the array
            cursize = n - rem;

            if (cursize < m) :
                ans.append(-1);
                continue;

            ans.append(a[m + rem]);

        else :

            # Current size of the array
            cursize = rem;

            if (cursize < m) :
                ans.append(-1);
                continue;

            ans.append(a[m]);

    # Print the result
    for i in ans :
        print(i) ;

# Driver code
if __name__ == "__main__" :

    # The initial array, -1 is for
    # 1 base indexing
    a = [ -1, 1, 2, 3, 4, 5 ];

    # Queries in the form of the pairs of (t, M)
    vec = [
        [ 1, 4 ],
        [ 6, 1 ],
        [ 3, 5 ]
    ];

    PerformQueries(a, vec);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to perform the queries
    static void PerformQueries(int[] a, int[,] vec)
    {

        List<int> ans = new List<int>();

        // Size of the array with
        // 1-based indexing
        int n = (int) a.Length - 1;

        // Number of queries
        int q = (int) vec.GetLength(0);

        // Iterating through the queries
        for (int i = 0; i < q; ++i)
        {

            long t = vec[i, 0];
            int m = vec[i, 1];

            // If m is more than the
            // size of the array
            if (m > n)
            {
                ans.Add(-1);
                continue;
            }

            // Count of turns
            int turn = (int) (t / n);

            // Find the remainder
            int rem = (int) (t % n);

            // If the remainder is 0 and turn is
            // odd then the array is empty
            if (rem == 0 && turn % 2 == 1)
            {
                ans.Add(-1);
                continue;
            }

            // If the remainder is 0 and turn is
            // even then array is full and
            // is in its initial state
            if (rem == 0 && turn % 2 == 0)
            {
                ans.Add(a[m]);
                continue;
            }

            // If the remainder is not 0
            // and the turn is even
            if (turn % 2 == 0)
            {

                // Current size of the array
                int cursize = n - rem;

                if (cursize < m)
                {
                    ans.Add(-1);
                    continue;
                }
                ans.Add(a[m + rem]);
            }
            else
            {

                // Current size of the array
                int cursize = rem;
                if (cursize < m)
                {
                    ans.Add(-1);
                    continue;
                }
                ans.Add(a[m]);
            }
        }

        // Print the result
        foreach (int i in ans)
            Console.Write(i + "\n");
    }

    // Driver code
    public static void Main(String[] args)
    {

        // The initial array, -1 is for
        // 1 base indexing
        int[] a = { -1, 1, 2, 3, 4, 5 };

        // Queries in the form of the pairs of (t, M)
        int[,] vec = { { 1, 4 }, { 6, 1 }, { 3, 5 } };

        PerformQueries(a, vec);

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to perform the queries
function PerformQueries(a, vec) {

    let ans = new Array();

    // Size of the array with
    // 1-based indexing
    let n = a.length - 1;

    // Number of queries
    let q = vec.length;

    // Iterating through the queries
    for (let i = 0; i < q; ++i) {

        let t = vec[i][0];
        let m = vec[i][1];

        // If m is more than the
        // size of the array
        if (m > n) {
            ans.push(-1);
            continue;
        }

        // Count of turns
        let turn = Math.floor(t / n);

        // Find the remainder
        let rem = t % n;

        // If the remainder is 0 and turn is
        // odd then the array is empty
        if (rem == 0 && turn % 2 == 1) {
            ans.push(-1);
            continue;
        }

        // If the remainder is 0 and turn is
        // even then array is full and
        // is in its initial state
        if (rem == 0 && turn % 2 == 0) {
            ans.push(a[m]);
            continue;
        }

        // If the remainder is not 0
        // and the turn is even
        if (turn % 2 == 0) {

            // Current size of the array
            let cursize = n - rem;

            if (cursize < m) {
                ans.push(-1);
                continue;
            }
            ans.push(a[m + rem]);
        }
        else {

            // Current size of the array
            let cursize = rem;
            if (cursize < m) {
                ans.push(-1);
                continue;
            }
            ans.push(a[m]);
        }
    }

    // Print the result
    for (let i of ans)
        document.write(i + "<br>");
}

// Driver code

// The initial array, -1 is for
// 1 base indexing
let a = [-1, 1, 2, 3, 4, 5];

// Queries in the form of the pairs of (t, M)
let vec = [
    [1, 4],
    [6, 1],
    [3, 5]];

PerformQueries(a, vec);
</script>
```

**Output:** 

```
5
1
-1
```