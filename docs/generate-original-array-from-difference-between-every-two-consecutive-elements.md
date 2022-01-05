# 根据每两个连续元素之间的差异生成原始数组

> 原文:[https://www . geesforgeks . org/generate-original-array-from-difference-每两个连续元素之间的差异/](https://www.geeksforgeeks.org/generate-original-array-from-difference-between-every-two-consecutive-elements/)

给定包含在 **1 到 N** 范围内的 **N** 个数字的数组的两个连续元素之间的**N–1**个差。任务是使用给定的差异来确定原始数组。如果可能，打印阵列，否则打印 **-1** 。
**举例:**

> **输入:** diff[] = {2，-3，2}
> **输出:** arr[] = {2，4，1，3 }
> 4–2 = 2
> 1–4 =-3
> 3–1 = 2
> **输入:** diff[] = {2，2，2}
> **输出:** -1

**方法:**由于我们想在**【1，n】**范围内生成排列，每个数字应该只出现一次。以
为例

> arr[] = {2，-3，2}
> 这里，**P2–P1 = 2**，**P3–P2 =-3**，**P4–P3 = 2**。
> 让 **P1 = x** 然后 **P2 = x + 2** ，**P3 = P2–3 = x+2–3 = x–1**，P4 = P3+2 = x–1+2 = x+1。
> 所以， **P1 = x** ， **P2 = x + 2** ，**P3 = x–1**， **P4 = x + 1** 。
> 既然我们想要一个从 **1** 到 **n** 的排列，那么我们上面得到的**P[I]**也必须满足这个条件。由于每个 **x** 都必须满足该值，因此为了简单起见，我们取 x = 0。
> 现在，P1 = 0，P2 = 2，P3 = -1，P4 = 1。

我们将对 **p[i]的**进行排序，排序后每个元素之间的连续差必须等于 1。如果在任何一个指数上，我们遇到一个元素 **p[i]** ，那么**p[I]–p[I–1]！= 1** 则不可能产生排列。为了生成最终的排列，我们将跟踪索引，我们可以使用 map 或无序 map 来这样做。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required permutation
void findPerm(int n, vector<int>& differences)
{
    vector<int> ans;
    ans.clear();
    ans.push_back(0);

    // Take x = 0 for simplicity
    int x = 0;

    // Calculate aint the differences
    // and store it in a vector
    for (int i = 0; i <= n - 2; ++i) {
        int diff = differences[i];
        x = x + diff;
        ans.push_back(x);
    }

    // Preserve the original array
    vector<int> anss = ans;
    sort(ans.begin(), ans.end());
    int flag = -1;

    // Check if aint the consecutive elements
    // have difference = 1
    for (int i = 1; i <= n - 1; ++i) {
        int res = ans[i] - ans[i - 1];
        if (res != 1) {
            flag = 0;
        }
    }

    // If consecutive elements don't have
    // difference 1 at any position then
    // the answer is impossible
    if (flag == 0) {
        cout << -1;
        return;
    }

    // Else store the indices and values
    // at those indices in a map
    // and finainty print them
    else {
        unordered_map<int, int> mpp;
        mpp.clear();
        int j = 1;
        vector<int> value_at_index;
        for (auto& x : ans) {
            mpp[x] = j;
            ++j;
        }
        for (auto& x : anss) {
            value_at_index.push_back(mpp[x]);
        }
        for (auto& x : value_at_index) {
            cout << x << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    vector<int> differences;
    differences.push_back(2);
    differences.push_back(-3);
    differences.push_back(2);
    int n = differences.size() + 1;
    findPerm(n, differences);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.*;
class GFG
{

// Function to print the required permutation
static void findPerm(int n, Vector<Integer> differences)
{
    Vector<Integer> ans = new Vector<Integer>();
    ans.clear();
    ans.add(0);

    // Take x = 0 for simplicity
    int x = 0;

    // Calculate aint the differences
    // and store it in a vector
    for (int i = 0; i <= n - 2; ++i)
    {
        int diff = differences.get(i);
        x = x + diff;
        ans.add(x);
    }

    // Preserve the original array
    Vector<Integer> anss = new Vector<Integer>();
    for(Integer obj:ans)
        anss.add(obj);

    Collections.sort(ans);
    int flag = -1;

    // Check if aint the consecutive elements
    // have difference = 1
    for (int i = 1; i <= n - 1; ++i)
    {
        int res = ans.get(i) - ans.get(i - 1);
        if (res != 1)
        {
            flag = 0;
        }
    }

    // If consecutive elements don't have
    // difference 1 at any position then
    // the answer is impossible
    if (flag == 0)
    {
        System.out.print(-1);
        return;
    }

    // Else store the indices and values
    // at those indices in a map
    // and finainty print them
    else
    {
        Map<Integer,Integer> mpp = new HashMap<>();
        mpp.clear();
        int j = 1;
        Vector<Integer> value_at_index = new Vector<Integer>();
        for (Integer x1 : ans)
        {
            mpp.put(x1, j);
            ++j;
        }
        for (Integer x2 : anss)
        {
            value_at_index.add(mpp.get(x2));
        }
        for (Integer x3 : value_at_index)
        {
            System.out.print(x3 + " ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    Vector<Integer> differences = new Vector<Integer>();
    differences.add(2);
    differences.add(-3);
    differences.add(2);
    int n = differences.size() + 1;
    findPerm(n, differences);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the required permutation
def findPerm(n, differences):
    ans = []
    ans.append(0)

    # Take x = 0 for simplicity
    x = 0

    # Calculate athe differences
    # and store it in a vector
    for i in range(n - 1):
        diff = differences[i]
        x = x + diff
        ans.append(x)

    # Preserve the original array
    anss = ans
    ans = sorted(ans)
    flag = -1

    # Check if athe consecutive elements
    # have difference = 1
    for i in range(1, n):
        res = ans[i] - ans[i - 1]
        if (res != 1):
            flag = 0

    # If consecutive elements don't have
    # difference 1 at any position then
    # the answer is impossible
    if (flag == 0):
        print("-1")
        return

    # Else store the indices and values
    # at those indices in a map
    # and finainty print them
    else:
        mpp = dict()
        j = 1
        value_at_index = []
        for x in ans:
            mpp[x] = j
            j += 1

        for x in anss:
            value_at_index.append(mpp[x])

        for x in value_at_index:
            print(x, end = " ")
        print()

# Driver code
differences=[]
differences.append(2)
differences.append(-3)
differences.append(2)
n = len(differences) + 1
findPerm(n, differences)

# This code is contributed by mohit kumar
```

## C#

```
// C# program to implement the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the required permutation
static void findPerm(int n, List<int> differences)
{
    List<int> ans = new List<int>();
    ans.Clear();
    ans.Add(0);

    // Take x = 0 for simplicity
    int x = 0;

    // Calculate aint the differences
    // and store it in a vector
    for(int i = 0; i <= n - 2; ++i)
    {
        int diff = differences[i];
        x = x + diff;
        ans.Add(x);
    }

    // Preserve the original array
    List<int> anss = new List<int>();
    foreach(int obj in ans)
        anss.Add(obj);

    ans.Sort();
    int flag = -1;

    // Check if aint the consecutive elements
    // have difference = 1
    for(int i = 1; i <= n - 1; ++i)
    {
        int res = ans[i] - ans[i - 1];
        if (res != 1)
        {
            flag = 0;
        }
    }

    // If consecutive elements don't have
    // difference 1 at any position then
    // the answer is impossible
    if (flag == 0)
    {
        Console.Write(-1);
        return;
    }

    // Else store the indices and values
    // at those indices in a map
    // and finainty print them
    else
    {
        Dictionary<int,
                   int> mpp = new Dictionary<int,
                                             int>();
        mpp.Clear();
        int j = 1;

        List<int> value_at_index = new List<int>();
        foreach (int x1 in ans)
        {
            mpp.Add(x1, j);
            ++j;
        }

        foreach (int x2 in anss)
        {
            value_at_index.Add(mpp[x2]);
        }

        foreach (int x3 in value_at_index)
        {
            Console.Write(x3 + " ");
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String[] args)
{
    List<int> differences = new List<int>();
    differences.Add(2);
    differences.Add(-3);
    differences.Add(2);

    int n = differences.Count + 1;

    findPerm(n, differences);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to implement the above approach

    // Function to print the required permutation
function findPerm(n,differences)
{
    let ans = [];   
    ans.push(0);

    // Take x = 0 for simplicity
    let x = 0;

    // Calculate aint the differences
    // and store it in a vector
    for (let i = 0; i <= n - 2; ++i)
    {
        let diff = differences[i];
        x = x + diff;
        ans.push(x);
    }

    // Preserve the original array
    let anss = [];
    for(let obj = 0; obj < ans.length; obj++)
        anss.push(ans[obj]);

    ans.sort(function(a,b){return a-b;});
    let flag = -1;

    // Check if aint the consecutive elements
    // have difference = 1
    for (let i = 1; i <= n - 1; ++i)
    {
        let res = ans[i] - ans[i - 1];
        if (res != 1)
        {
            flag = 0;
        }
    }

    // If consecutive elements don't have
    // difference 1 at any position then
    // the answer is impossible
    if (flag == 0)
    {
        document.write(-1);
        return;
    }

    // Else store the indices and values
    // at those indices in a map
    // and finainty print them
    else
    {
        let mpp = new Map();

        let j = 1;
        let value_at_index = [];
        for (let x1 = 0; x1 < ans.length; x1++)
        {
            mpp.set(ans[x1], j);
            ++j;
        }
        for (let x2 = 0; x2 < anss.length; x2++)
        {
            value_at_index.push(mpp.get(anss[x2]));
        }
        for (let x3 = 0; x3 < value_at_index.length; x3++)
        {
            document.write(value_at_index[x3] + " ");
        }
        document.write("<br>");
    }
}

    // Driver code
    let differences =[];
    differences.push(2);
    differences.push(-3);
    differences.push(2);
    let n = differences.length + 1;
    findPerm(n, differences);

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
2 4 1 3
```