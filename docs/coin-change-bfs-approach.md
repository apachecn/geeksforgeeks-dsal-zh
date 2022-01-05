# 硬币兑换| BFS 进场

> 原文:[https://www.geeksforgeeks.org/coin-change-bfs-approach/](https://www.geeksforgeeks.org/coin-change-bfs-approach/)

给定一个整数 **X** 和一个由正整数组成的长度为 **N** 的数组**arr【】**，任务是从数组中选取最小数量的整数，使它们的总和达到 **N** 。任何数字都可以选择无限次。如果没有答案，则打印 **-1** 。
**示例:**

> **输入:** X = 7，arr[] = {3，5，4}
> **输出:** 2
> 最小元素数为 2，因为
> 3 和 4 可以选择达到 7。
> 
> **输入:** X = 4，arr[] = {5}
> **输出:** -1

**方法:**在这篇[文章](https://www.geeksforgeeks.org/coin-change-dp-7/)中，我们已经看到了如何使用动态规划方法来解决这个问题。
在这里，我们将看到使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 解决这个问题的稍微不同的方法。
在此之前，我们先来定义一个状态。一个状态 **S <sub>X</sub>** 可以定义为我们需要从数组中取的整数的最小数量，以得到总共 **X** 。
现在，如果我们开始将每个状态视为图中的一个节点，使得每个节点都连接到**(S<sub>X–arr[0]</sub>、S<sub>X–arr[1]</sub>、…S<sub>X–arr[N–1]</sub>)**。
因此，我们必须以未加权的方式找到从状态 **N** 到 **0** 的最短路径，这可以使用 BFS 来完成。BFS 在这里工作，因为这个图表没有加权。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of integers required
int minNumbers(int x, int* arr, int n)
{
    // Queue for BFS
    queue<int> q;

    // Base value in queue
    q.push(x);

    // Boolean array to check if a number has been
    // visited before
    unordered_set<int> v;

    // Variable to store depth of BFS
    int d = 0;

    // BFS algorithm
    while (q.size()) {

        // Size of queue
        int s = q.size();
        while (s--) {

            // Front most element of the queue
            int c = q.front();

            // Base case
            if (!c)
                return d;
            q.pop();
            if (v.find(c) != v.end() or c < 0)
                continue;

            // Setting current state as visited
            v.insert(c);

            // Pushing the required states in queue
            for (int i = 0; i < n; i++)
                q.push(c - arr[i]);
        }

        d++;
    }

    // If no possible solution
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 4 };
    int n = sizeof(arr) / sizeof(int);
    int x = 7;

    cout << minNumbers(x, arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the minimum number
// of integers required
static int minNumbers(int x, int []arr, int n)
{
    // Queue for BFS
    Queue<Integer> q = new LinkedList<>();

    // Base value in queue
    q.add(x);

    // Boolean array to check if
    // a number has been visited before
    HashSet<Integer> v = new HashSet<Integer>();

    // Variable to store depth of BFS
    int d = 0;

    // BFS algorithm
    while (q.size() > 0)
    {

        // Size of queue
        int s = q.size();
        while (s-- > 0)
        {

            // Front most element of the queue
            int c = q.peek();

            // Base case
            if (c == 0)
                return d;
            q.remove();
            if (v.contains(c) || c < 0)
                continue;

            // Setting current state as visited
            v.add(c);

            // Pushing the required states in queue
            for (int i = 0; i < n; i++)
                q.add(c - arr[i]);
        }
        d++;
    }

    // If no possible solution
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 3, 4 };
    int n = arr.length;
    int x = 7;

    System.out.println(minNumbers(x, arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the minimum number
# of integers required
def minNumbers(x, arr, n) :

    q = []

    # Base value in queue
    q.append(x)

    v = set([])

    d = 0

    while (len(q) > 0) :

        s = len(q)
        while (s) :
            s -= 1
            c = q[0]
            #print(q)
            if (c == 0) :
                return d
            q.pop(0)
            if ((c in v) or c < 0) :
                continue

            # Setting current state as visited
            v.add(c)

            # Pushing the required states in queue
            for i in range(n) :
                q.append(c - arr[i])            

        d += 1
        #print()
        #print(d,c)

    # If no possible solution
    return -1

arr = [ 1, 4,6 ]
n = len(arr)
x = 20
print(minNumbers(x, arr, n))

# This code is contributed by divyeshrabadiya07
# Improved by nishant.k108
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the minimum number
// of integers required
static int minNumbers(int x, int []arr, int n)
{
    // Queue for BFS
    Queue<int> q = new Queue<int>();

    // Base value in queue
    q.Enqueue(x);

    // Boolean array to check if
    // a number has been visited before
    HashSet<int> v = new HashSet<int>();

    // Variable to store depth of BFS
    int d = 0;

    // BFS algorithm
    while (q.Count > 0)
    {

        // Size of queue
        int s = q.Count;
        while (s-- > 0)
        {

            // Front most element of the queue
            int c = q.Peek();

            // Base case
            if (c == 0)
                return d;
            q.Dequeue();
            if (v.Contains(c) || c < 0)
                continue;

            // Setting current state as visited
            v.Add(c);

            // Pushing the required states in queue
            for (int i = 0; i < n; i++)
                q.Enqueue(c - arr[i]);
        }
        d++;
    }

    // If no possible solution
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 3, 4 };
    int n = arr.Length;
    int x = 7;

    Console.WriteLine(minNumbers(x, arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the minimum number
// of integers required
function minNumbers(x, arr, n)
{
    // Queue for BFS
    var q = [];

    // Base value in queue
    q.push(x);

    // Boolean array to check if a number has been
    // visited before
    var v = new Set();

    // Variable to store depth of BFS
    var d = 0;

    // BFS algorithm
    while (q.length!=0) {

        // Size of queue
        var s = q.length;
        while (s--) {

            // Front most element of the queue
            var c = q[0];

            // Base case
            if (!c)
                return d;
            q.shift();
            if (v.has(c) || c < 0)
                continue;

            // Setting current state as visited
            v.add(c);

            // Pushing the required states in queue
            for (var i = 0; i < n; i++)
                q.push(c - arr[i]);
        }

        d++;
    }

    // If no possible solution
    return -1;
}

// Driver code
var arr = [3, 3, 4];
var n = arr.length;
var x = 7;
document.write(minNumbers(x, arr, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N * X)
T3】辅助空间: O(N)