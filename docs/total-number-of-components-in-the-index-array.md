# 索引数组中的组件总数

> 原文:[https://www . geesforgeks . org/索引数组中的组件总数/](https://www.geeksforgeeks.org/total-number-of-components-in-the-index-array/)

给定一个从 **0 到 N** 的数值为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算索引数组中的组件数量。

> **索引数组**表示如果我们在**并且**索引，那么它会导致 arr【I】。
> 索引数组的**组件**在形成循环时被计数。如果没有循环持续，或者数组包含单个元素，那么我们也将其视为一个组件。
> 例如:
> 让数组 arr[] = {1，2，0，3}
> {1，2，0}将形成一个组件，因为从索引 0 开始，我们再次到达索引 0，如下所示:
> 1->2(arr[1])->0(arr[2])->1(arr[0])

**示例:**

> **输入:** arr[] = {1，2，3，5，0，4，6}
> **输出:** 2
> **解释:**
> 下面是 2 个组件的遍历:
> 组件 1:从 0 开始遍历，然后遍历的路径由:
> 1->2(arr[1])->3(arr[2])->5(arr[3])->给出
> 组件 2:只有 6 是未访问的，它会再创建一个组件。
> 所以，总成分= 2。
> 
> **输入:** arr[] = {1，2，0，3}
> **输出:** 2
> **解释:**
> 下面是 2 个组件的遍历:
> 组件 1:从 0 开始遍历，然后遍历的路径由下式给出:
> 1->2(arr[1])->0(arr[2])->1(arr[0])
> 组件 2:只有 3 是不变的
> 所以，总成分= 2。

**方法:**思路是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)的概念。以下是步骤:

1.  从第一个未访问的索引开始，该索引将包含整数 0。
2.  在 **DFS 遍历**期间，标记数组中被访问的元素，直到元素形成一个循环。
3.  如果形成了一个循环，那么这意味着我们得到了一个分量，因此增加了分量数。
4.  对数组中所有未访问的索引重复上述所有步骤，并计算给定索引数组中的所有组件。
5.  如果访问了数组的所有索引，则打印连接组件的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// To mark the visited index
// during DFS Traversal
vector<int> visited;

// Function for DFS traversal
void dfs(int i, int a[])
{
    // Check if not visited then
    // recurr for the next index
    if (visited[i] == 0) {
        visited[i] = 1;

        // DFS Traversal for next index
        dfs(a[i], a);
    }

    return;
}

// Function for checking which
// indexes are remaining
int allvisited(int a[], int n)
{
    for (int i = 0; i < n; i++) {

        // Marks that the ith
        // index is not visited
        if (visited[i] == 0)
            return i;
    }
    return -1;
}

// Function for counting components
int count(int a[], int n)
{
    int c = 0;

    // Function call
    int x = allvisited(a, n);

    while (x != -1) {

        // Count number of components
        c++;

        // DFS call
        dfs(x, a);

        x = allvisited(a, n);
    }

    // Print the total count of components
    cout << c << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 4, 3, 5, 0, 2, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

      visited = vector<int>(N+1,0);

    // Function Call
    count(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class Main
{
    // Function for DFS traversal
    static void dfs(int i, int[] a,
                    HashMap<Integer, Integer> m)
    {

        // Check if not visited then
        // recurr for the next index
        if (!m.containsKey(i))
        {
            m.put(i, 1);

            // DFS Traversal for next index
            dfs(a[i], a, m);
        }
        return;
    }

    // Function for checking which
    // indexes are remaining
    static int allvisited(int[] a, int n,
                          HashMap<Integer, Integer> m)
    {
        for(int i = 0; i < n; i++)
        {

            // Marks that the ith
            // index is not visited
            if (!m.containsKey(i))
                return i;
        }
        return -1;
    }

    // Function for counting components
    static void count(int[] a, int n)
    {
        int c = 0;

        // To mark the visited index
        // during DFS Traversal
        HashMap<Integer, Integer> m = new HashMap<>();

        // Function call
        int x = allvisited(a, n, m);

        while (x != -1)
        {

            // Count number of components
            c++;

            // DFS call
            dfs(x, a, m);

            x = allvisited(a, n, m);
        }

        // Print the total count of components
        System.out.print(c);
    }

    public static void main(String[] args)
    {

        // Given array arr[]
        int[] arr = { 1, 4, 3, 5, 0, 2, 6 };

        int N = arr.length;

        // Function Call
        count(arr, N);
    }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for DFS traversal
def dfs(i, a, m):

    # Check if not visited then
    # recurr for the next index
    if i in m:
        if m[i] == 0:
            m[i] = 1

            # DFS Traversal for next index
            dfs(a[i], a, m)
    else:
        m[i] = 1

        # DFS Traversal for next index
        dfs(a[i], a, m)

    return

# Function for checking which
# indexes are remaining
def allvisited(a, n, m):

    for i in range(n):

        # Marks that the ith
        # index is not visited
        if i in m:
            if m[i] == 0:
                return i

        else:
            return i

    return -1

# Function for counting components
def count(a, n):

    c = 0

    # To mark the visited index
    # during DFS Traversal
    m = dict()

    # Function call
    x = allvisited(a, n, m)

    while (x != -1):

        # Count number of components
        c += 1

        # DFS call
        dfs(x, a, m)

        x = allvisited(a, n, m)

    # Print the total count of components
    print(c)

# Driver Code
if __name__=='__main__':

    # Given array arr[]
    arr = [ 1, 4, 3, 5, 0, 2, 6 ]

    N = len(arr)

    # Function Call
    count(arr, N)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function for DFS traversal
static void dfs(int i, int []a,
     Dictionary<int, int> m)
{

    // Check if not visited then
    // recurr for the next index
    if (!m.ContainsKey(i))
    {
        m[i] = 1;

        // DFS Traversal for next index
        dfs(a[i], a, m);
    }
    return;
}

// Function for checking which
// indexes are remaining
static int allvisited(int []a, int n,
               Dictionary<int, int> m)
{
    for(int i = 0; i < n; i++)
    {

        // Marks that the ith
        // index is not visited
        if (!m.ContainsKey(i))
            return i;
    }
    return -1;
}

// Function for counting components
static void count(int []a, int n)
{
    int c = 0;

    // To mark the visited index
    // during DFS Traversal
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // Function call
    int x = allvisited(a, n, m);

    while (x != -1)
    {

        // Count number of components
        c++;

        // DFS call
        dfs(x, a, m);

        x = allvisited(a, n, m);
    }

    // Print the total count of components
    Console.Write(c);
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int []arr = { 1, 4, 3, 5, 0, 2, 6 };

    int N = arr.Length;

    // Function Call
    count(arr, N);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function for DFS traversal
function dfs(i, a, m)
{
    // Check if not visited then
    // recurr for the next index
    if (!m.has(i)) {
        m.set(i, 1);
        m[i] = 1;

        // DFS Traversal for next index
        dfs(a[i], a, m);
    }

    return;
}

// Function for checking which
// indexes are remaining
function allvisited(a, n, m)
{
    for (var i = 0; i < n; i++) {

        // Marks that the ith
        // index is not visited
        if (!m.has(i))
            return i;
    }
    return -1;
}

// Function for counting components
function count(a, n)
{
    var c = 0;

    // To mark the visited index
    // during DFS Traversal
    var m = new Map();

    // Function call
    var x = allvisited(a, n, m);

    while (x != -1) {

        // Count number of components
        c++;

        // DFS call
        dfs(x, a, m);

        x = allvisited(a, n, m);
    }

    // Print the total count of components
    document.write( c );
}

// Driver Code

// Given array arr[]
var arr = [1, 4, 3, 5, 0, 2, 6];
var N = arr.length;

// Function Call
count(arr, N);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*