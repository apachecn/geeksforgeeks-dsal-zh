# 填充给定的 N 个插槽所需的最短时间

> 原文:[https://www . geeksforgeeks . org/填充给定 n 个插槽所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-fill-given-n-slots/)

给定一个表示槽数的整数 **N** ，以及一个由范围**【1，N】**代表的 **K** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**。数组的每个元素都在范围**【1，N】**内，该范围代表填充槽的索引。在每个时间单位，具有填充槽的索引填充相邻的空槽。任务是找到填满所有 **N** 槽所需的最短时间。

**示例:**

> **输入:** N = 6，K = 2，arr[] = {2，6}
> **输出:** 2
> **解释:**
> 最初有 6 个槽，填充槽的索引为槽[] = {0，2，0，0，0，6}，其中 0 表示未填充。
> 1 个时间单位后，槽[] = {1，2，3，0，5，6 }
> 2 个时间单位后，槽[] = {1，2，3，4，5，6}
> 因此，所需的最小时间为 2。
> 
> **输入:** N = 5，K = 5，arr[] = {1，2，3，4，5 }
> T3】输出: 1

**方法:**为了解决给定的问题，想法是使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)在给定的 **N** 槽上执行[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/) 。按照以下步骤解决问题:

*   初始化一个变量，将**时间**设为 **0** ，辅助数组**访问【】**标记每次迭代中填充的索引。
*   现在，将数组**arr【】**中给定的已填充插槽的索引推送到[队列](https://www.geeksforgeeks.org/queue-data-structure/) **队列**中，并将它们标记为已访问。
*   现在，迭代直到[队列不为空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下步骤:
    *   从[队列](https://www.geeksforgeeks.org/queue-data-structure/)中移除前索引 **i** ，如果相邻插槽**(I–1)**和 **(i + 1)** 在范围**【1，N】**内且未被访问，则将其标记为已访问，[将其推入队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)。
    *   将**时间**增加 **1** 。
*   完成上述步骤后，打印**(时间–1)**的值，作为填满所有插槽所需的最短时间。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to return the minimum
// time to fill all the slots
void minTime(vector<int> arr, int N, int K)
{

    // Stores visited slots
    queue<int> q;

    // Checks if a slot is visited or not
    vector<bool> vis(N + 1, false);

    int time = 0;

    // Insert all filled slots
    for (int i = 0; i < K; i++) {

        q.push(arr[i]);
        vis[arr[i]] = true;
    }

    // Iterate until queue is
    // not empty
    while (q.size() > 0) {

        // Iterate through all slots
        // in the queue
        for (int i = 0; i < q.size(); i++) {

            // Front index
            int curr = q.front();
            q.pop();

            // If previous slot is
            // present and not visited
            if (curr - 1 >= 1 &&
                !vis[curr - 1]) {
                vis[curr - 1] = true;
                q.push(curr - 1);
            }

            // If next slot is present
            // and not visited
            if (curr + 1 <= N &&
                !vis[curr + 1]) {

                vis[curr + 1] = true;
                q.push(curr + 1);
            }
        }

        // Increment the time
        // at each level
        time++;
    }

    // Print the answer
    cout << (time - 1);
}

// Driver Code
int main()
{
    int N = 6;
    vector<int> arr = { 2, 6 };
    int K = arr.size();

    // Function Call
    minTime(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to return the minimum
    // time to fill all the slots
    public static void minTime(int arr[],
                               int N, int K)
    {

        // Stores visited slots
        Queue<Integer> q = new LinkedList<>();

        // Checks if a slot is visited or not
        boolean vis[] = new boolean[N + 1];
        int time = 0;

        // Insert all filled slots
        for (int i = 0; i < K; i++) {

            q.add(arr[i]);
            vis[arr[i]] = true;
        }

        // Iterate until queue is
        // not empty
        while (q.size() > 0) {

            // Iterate through all slots
            // in the queue
            for (int i = 0; i < q.size(); i++) {

                // Front index
                int curr = q.poll();

                // If previous slot is
                // present and not visited
                if (curr - 1 >= 1 &&
                    !vis[curr - 1]) {
                    vis[curr - 1] = true;
                    q.add(curr - 1);
                }

                // If next slot is present
                // and not visited
                if (curr + 1 <= N &&
                    !vis[curr + 1]) {

                    vis[curr + 1] = true;
                    q.add(curr + 1);
                }
            }

            // Increment the time
            // at each level
            time++;
        }

        // Print the answer
        System.out.println(time - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;
        int arr[] = { 2, 6 };
        int K = arr.length;

        // Function Call
        minTime(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the minimum
# time to fill all the slots
def minTime(arr, N, K):

    # Stores visited slots
    q = []

    # Checks if a slot is visited or not
    vis = [False] * (N + 1)

    time = 0

    # Insert all filled slots
    for i in range(K):
        q.append(arr[i])
        vis[arr[i]] = True

    # Iterate until queue is
    # not empty
    while (len(q) > 0):

        # Iterate through all slots
        # in the queue
        for i in range(len(q)):

            # Front index
            curr = q[0]
            q.pop(0)

            # If previous slot is
            # present and not visited
            if (curr - 1 >= 1 and vis[curr - 1] == 0):
                vis[curr - 1] = True
                q.append(curr - 1)

            # If next slot is present
            # and not visited
            if (curr + 1 <= N and vis[curr + 1] == 0):
                vis[curr + 1] = True
                q.append(curr + 1)

        # Increment the time
        # at each level
        time += 1

    # Print the answer
    print(time - 1)

# Driver Code
N = 6
arr = [ 2, 6 ]
K = len(arr)

# Function Call
minTime(arr, N, K)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to return the minimum
// time to fill all the slots
static void minTime(List<int> arr, int N, int K)
{

    // Stores visited slots
    Queue<int> q = new Queue<int>();

    // Checks if a slot is visited or not
    int []vis = new int[N + 1];
    Array.Clear(vis, 0, vis.Length);
    int time = 0;

    // Insert all filled slots
    for (int i = 0; i < K; i++)
    {
        q.Enqueue(arr[i]);
        vis[arr[i]] = 1;
    }

    // Iterate until queue is
    // not empty
    while (q.Count > 0)
    {

        // Iterate through all slots
        // in the queue
        for (int i = 0; i < q.Count; i++)
        {

            // Front index
            int curr = q.Peek();
            q.Dequeue();

            // If previous slot is
            // present and not visited
            if (curr - 1 >= 1 &&
                vis[curr - 1]==0)
            {
                vis[curr - 1] = 1;
                q.Enqueue(curr - 1);
            }

            // If next slot is present
            // and not visited
            if (curr + 1 <= N &&
                vis[curr + 1] == 0)
            {

                vis[curr + 1] = 1;
                q.Enqueue(curr + 1);
            }
        }

        // Increment the time
        // at each level
        time++;
    }

    // Print the answer
    Console.WriteLine(time-1);
}

// Driver Code
public static void Main()
{
    int N = 6;
    List<int> arr = new List<int>() { 2, 6 };
    int K = arr.Count;

    // Function Call
    minTime(arr, N, K);
}
}

// THIS CODE IS CONTRIBUTED BY SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the minimum
// time to fill all the slots
function minTime(arr, N, K)
{

    // Stores visited slots
    var q = [];

    // Checks if a slot is visited or not
    var vis = Array(N + 1).fill(false);

    var time = 0;

    // Insert all filled slots
    for (var i = 0; i < K; i++) {

        q.push(arr[i]);
        vis[arr[i]] = true;
    }

    // Iterate until queue is
    // not empty
    while (q.length > 0) {

        // Iterate through all slots
        // in the queue
        for (var i = 0; i < q.length; i++) {

            // Front index
            var curr = q[0];
            q.pop();

            // If previous slot is
            // present and not visited
            if (curr - 1 >= 1 &&
                !vis[curr - 1]) {
                vis[curr - 1] = true;
                q.push(curr - 1);
            }

            // If next slot is present
            // and not visited
            if (curr + 1 <= N &&
                !vis[curr + 1]) {

                vis[curr + 1] = true;
                q.push(curr + 1);
            }
        }

        // Increment the time
        // at each level
        time++;
    }

    // Print the answer
    document.write(time - 1);
}

// Driver Code
var N = 6;
var arr = [2, 6];
var K = arr.length;

// Function Call
minTime(arr, N, K);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)