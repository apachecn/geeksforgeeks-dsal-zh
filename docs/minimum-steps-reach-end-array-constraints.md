# 在约束条件下到达数组末尾的最少步数

> 原文:[https://www . geesforgeks . org/最小步数-到达-结束-数组-约束/](https://www.geeksforgeeks.org/minimum-steps-reach-end-array-constraints/)

给定一个只包含一位数的数组，假设我们站在第一个索引处，我们需要用最少的步数到达数组的末尾，在这一步中，我们可以跳到相邻的索引，也可以跳到具有相同值的位置。
换句话说，如果我们在索引 I，那么在一个步骤中，你可以达到，arr[i-1]或 arr[i+1]或 arr[K]，这样 arr[K]= arr[i](arr[K]的值与 arr[I]相同)
**示例:**

```
Input : arr[] = {5, 4, 2, 5, 0}
Output : 2
Explanation : Total 2 step required.
We start from 5(0), in first step jump to next 5 
and in second step we move to value 0 (End of arr[]).

Input  : arr[] = [0, 1, 2, 3, 4, 5, 6, 7, 5, 4,
                 3, 6, 0, 1, 2, 3, 4, 5, 7]
Output : 5
Explanation : Total 5 step required.
0(0) -> 0(12) -> 6(11) -> 6(6) -> 7(7) ->
(18)                                                          
(inside parenthesis indices are shown)
```

这个问题可以使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 解决。我们可以将给定的数组视为未加权图，其中每个顶点都有两条边指向下一个和上一个数组元素，更多的边指向具有相同值的数组元素。现在为了快速处理第三类边缘，我们保留了 10 个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，用于存储数字 0 到 9 所在的所有索引。在上面的例子中，对应于 0 的向量将存储[0，12]，2 个索引，其中 0 出现在给定的数组中。
使用了另一个布尔数组，这样我们就不会多次访问同一个索引。由于我们正在使用 BFS 和 BFS 一级一级地进行，最佳的最低步骤是有保证的。

## C++

```
// C++ program to find minimum jumps to reach end
// of array
#include <bits/stdc++.h>
using namespace std;

//  Method returns minimum step to reach end of array
int getMinStepToReachEnd(int arr[], int N)
{
    // visit boolean array checks whether current index
    // is previously visited
    bool visit[N];

    // distance array stores distance of current
    // index from starting index
    int distance[N];

    // digit vector stores indices where a
    // particular number resides
    vector<int> digit[10];

    //  In starting all index are unvisited
    memset(visit, false, sizeof(visit));

    //  storing indices of each number in digit vector
    for (int i = 1; i < N; i++)
        digit[arr[i]].push_back(i);

    //  for starting index distance will be zero
    distance[0] = 0;
    visit[0] = true;

    // Creating a queue and inserting index 0.
    queue<int> q;
    q.push(0);

    //  loop until queue in not empty
    while(!q.empty())
    {
        // Get an item from queue, q.
        int idx = q.front();        q.pop();

        //  If we reached to last index break from loop
        if (idx == N-1)
            break;

        // Find value of dequeued index
        int d = arr[idx];

        // looping for all indices with value as d.
        for (int i = 0; i<digit[d].size(); i++)
        {
            int nextidx = digit[d][i];
            if (!visit[nextidx])
            {
                visit[nextidx] = true;
                q.push(nextidx);

                //  update the distance of this nextidx
                distance[nextidx] = distance[idx] + 1;
            }
        }

        // clear all indices for digit d, because all
        // of them are processed
        digit[d].clear();

        //  checking condition for previous index
        if (idx-1 >= 0 && !visit[idx - 1])
        {
            visit[idx - 1] = true;
            q.push(idx - 1);
            distance[idx - 1] = distance[idx] + 1;
        }

        //  checking condition for next index
        if (idx + 1 < N && !visit[idx + 1])
        {
            visit[idx + 1] = true;
            q.push(idx + 1);
            distance[idx + 1] = distance[idx] + 1;
        }
    }

    //  N-1th position has the final result
    return distance[N - 1];
}

//  driver code to test above methods
int main()
{
    int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 5,
                 4, 3, 6, 0, 1, 2, 3, 4, 5, 7};
    int N = sizeof(arr) / sizeof(int);
    cout << getMinStepToReachEnd(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum jumps
// to reach end of array
import java.util.*;
class GFG
{

// Method returns minimum step
// to reach end of array
static int getMinStepToReachEnd(int arr[],
                                int N)
{
    // visit boolean array checks whether
    // current index is previously visited
    boolean []visit = new boolean[N];

    // distance array stores distance of
    // current index from starting index
    int []distance = new int[N];

    // digit vector stores indices where a
    // particular number resides
    Vector<Integer> []digit = new Vector[10];
    for(int i = 0; i < 10; i++)
        digit[i] = new Vector<>();

    // In starting all index are unvisited
    for(int i = 0; i < N; i++)
        visit[i] = false;

    // storing indices of each number
    // in digit vector
    for (int i = 1; i < N; i++)
        digit[arr[i]].add(i);

    // for starting index distance will be zero
    distance[0] = 0;
    visit[0] = true;

    // Creating a queue and inserting index 0.
    Queue<Integer> q = new LinkedList<>();
    q.add(0);

    // loop until queue in not empty
    while(!q.isEmpty())
    {
        // Get an item from queue, q.
        int idx = q.peek();    
        q.remove();

        // If we reached to last
        // index break from loop
        if (idx == N - 1)
            break;

        // Find value of dequeued index
        int d = arr[idx];

        // looping for all indices with value as d.
        for (int i = 0; i < digit[d].size(); i++)
        {
            int nextidx = digit[d].get(i);
            if (!visit[nextidx])
            {
                visit[nextidx] = true;
                q.add(nextidx);

                // update the distance of this nextidx
                distance[nextidx] = distance[idx] + 1;
            }
        }

        // clear all indices for digit d,
        // because all of them are processed
        digit[d].clear();

        // checking condition for previous index
        if (idx - 1 >= 0 && !visit[idx - 1])
        {
            visit[idx - 1] = true;
            q.add(idx - 1);
            distance[idx - 1] = distance[idx] + 1;
        }

        // checking condition for next index
        if (idx + 1 < N && !visit[idx + 1])
        {
            visit[idx + 1] = true;
            q.add(idx + 1);
            distance[idx + 1] = distance[idx] + 1;
        }
    }

    // N-1th position has the final result
    return distance[N - 1];
}

// Driver Code
public static void main(String []args)
{
    int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 5,
                 4, 3, 6, 0, 1, 2, 3, 4, 5, 7};
    int N = arr.length;
    System.out.println(getMinStepToReachEnd(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find minimum jumps to reach end# of array

# Method returns minimum step to reach end of array
def getMinStepToReachEnd(arr,N):

    # visit boolean array checks whether current index
    # is previously visited
    visit = [False for i in range(N)]

    # distance array stores distance of current
    # index from starting index
    distance = [0 for i in range(N)]

    # digit vector stores indices where a
    # particular number resides
    digit = [[0 for i in range(N)] for j in range(10)]

    # storing indices of each number in digit vector
    for i in range(1,N):
        digit[arr[i]].append(i)

    # for starting index distance will be zero
    distance[0] = 0
    visit[0] = True

    # Creating a queue and inserting index 0.
    q = []
    q.append(0)

    # loop until queue in not empty
    while(len(q)> 0):

        # Get an item from queue, q.
        idx = q[0]
        q.remove(q[0])

        # If we reached to last index break from loop
        if (idx == N-1):
            break

        # Find value of dequeued index
        d = arr[idx]

        # looping for all indices with value as d.
        for i in range(len(digit[d])):
            nextidx = digit[d][i]
            if (visit[nextidx] == False):
                visit[nextidx] = True
                q.append(nextidx)

                # update the distance of this nextidx
                distance[nextidx] = distance[idx] + 1

        # clear all indices for digit d, because all
        # of them are processed

        # checking condition for previous index
        if (idx-1 >= 0 and visit[idx - 1] == False):
            visit[idx - 1] = True
            q.append(idx - 1)
            distance[idx - 1] = distance[idx] + 1

        # checking condition for next index
        if (idx + 1 < N and visit[idx + 1] == False):
            visit[idx + 1] = True
            q.append(idx + 1)
            distance[idx + 1] = distance[idx] + 1

    # N-1th position has the final result
    return distance[N - 1]

# driver code to test above methods
if __name__ == '__main__':
    arr = [0, 1, 2, 3, 4, 5, 6, 7, 5, 4, 3, 6, 0, 1, 2, 3, 4, 5, 7]
    N = len(arr)
    print(getMinStepToReachEnd(arr, N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find minimum jumps
// to reach end of array
using System;
using System.Collections.Generic;

class GFG
{

// Method returns minimum step
// to reach end of array
static int getMinStepToReachEnd(int []arr,
                                int N)
{
    // visit boolean array checks whether
    // current index is previously visited
    bool []visit = new bool[N];

    // distance array stores distance of
    // current index from starting index
    int []distance = new int[N];

    // digit vector stores indices where a
    // particular number resides
    List<int> []digit = new List<int>[10];
    for(int i = 0; i < 10; i++)
        digit[i] = new List<int>();

    // In starting all index are unvisited
    for(int i = 0; i < N; i++)
        visit[i] = false;

    // storing indices of each number
    // in digit vector
    for (int i = 1; i < N; i++)
        digit[arr[i]].Add(i);

    // for starting index distance will be zero
    distance[0] = 0;
    visit[0] = true;

    // Creating a queue and inserting index 0.
    Queue<int> q = new Queue<int>();
    q.Enqueue(0);

    // loop until queue in not empty
    while(q.Count != 0)
    {
        // Get an item from queue, q.
        int idx = q.Peek();    
        q.Dequeue();

        // If we reached to last
        // index break from loop
        if (idx == N - 1)
            break;

        // Find value of dequeued index
        int d = arr[idx];

        // looping for all indices with value as d.
        for (int i = 0; i < digit[d].Count; i++)
        {
            int nextidx = digit[d][i];
            if (!visit[nextidx])
            {
                visit[nextidx] = true;
                q.Enqueue(nextidx);

                // update the distance of this nextidx
                distance[nextidx] = distance[idx] + 1;
            }
        }

        // clear all indices for digit d,
        // because all of them are processed
        digit[d].Clear();

        // checking condition for previous index
        if (idx - 1 >= 0 && !visit[idx - 1])
        {
            visit[idx - 1] = true;
            q.Enqueue(idx - 1);
            distance[idx - 1] = distance[idx] + 1;
        }

        // checking condition for next index
        if (idx + 1 < N && !visit[idx + 1])
        {
            visit[idx + 1] = true;
            q.Enqueue(idx + 1);
            distance[idx + 1] = distance[idx] + 1;
        }
    }

    // N-1th position has the final result
    return distance[N - 1];
}

// Driver Code
public static void Main(String []args)
{
    int []arr = {0, 1, 2, 3, 4, 5, 6, 7, 5,
                4, 3, 6, 0, 1, 2, 3, 4, 5, 7};
    int N = arr.Length;
    Console.WriteLine(getMinStepToReachEnd(arr, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find minimum jumps
// to reach end of array

// Method returns minimum step
// to reach end of array
function getMinStepToReachEnd(arr,N)
{
    // visit boolean array checks whether
    // current index is previously visited
    let visit = new Array(N);

    // distance array stores distance of
    // current index from starting index
    let distance = new Array(N);

    // digit vector stores indices where a
    // particular number resides
    let digit = new Array(10);
    for(let i = 0; i < 10; i++)
        digit[i] = [];

    // In starting all index are unvisited
    for(let i = 0; i < N; i++)
        visit[i] = false;

    // storing indices of each number
    // in digit vector
    for (let i = 1; i < N; i++)
        digit[arr[i]].push(i);

    // for starting index distance will be zero
    distance[0] = 0;
    visit[0] = true;

    // Creating a queue and inserting index 0.
    let q = [];
    q.push(0);

    // loop until queue in not empty
    while(q.length!=0)
    {
        // Get an item from queue, q.
        let idx = q.shift();    

        // If we reached to last
        // index break from loop
        if (idx == N - 1)
            break;

        // Find value of dequeued index
        let d = arr[idx];

        // looping for all indices with value as d.
        for (let i = 0; i < digit[d].length; i++)
        {
            let nextidx = digit[d][i];
            if (!visit[nextidx])
            {
                visit[nextidx] = true;
                q.push(nextidx);

                // update the distance of this nextidx
                distance[nextidx] = distance[idx] + 1;
            }
        }

        // clear all indices for digit d,
        // because all of them are processed
        digit[d]=[];

        // checking condition for previous index
        if (idx - 1 >= 0 && !visit[idx - 1])
        {
            visit[idx - 1] = true;
            q.push(idx - 1);
            distance[idx - 1] = distance[idx] + 1;
        }

        // checking condition for next index
        if (idx + 1 < N && !visit[idx + 1])
        {
            visit[idx + 1] = true;
            q.push(idx + 1);
            distance[idx + 1] = distance[idx] + 1;
        }
    }

    // N-1th position has the final result
    return distance[N - 1];
}

// Driver Code
let arr=[0, 1, 2, 3, 4, 5, 6, 7, 5,
                 4, 3, 6, 0, 1, 2, 3, 4, 5, 7];
let N = arr.length;
document.write(getMinStepToReachEnd(arr, N));   

// This code is contributed by rag2127
</script>
```

**输出:**

```
5
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。