# 根据给定的任务执行顺序精确完成 K 个任务所需的最短时间

> 原文:[https://www . geesforgeks . org/根据给定的任务执行顺序完成 k 个任务所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-complete-exactly-k-tasks-based-on-given-order-of-task-execution/)

给定一个大小为 **N** 的 **2D** [阵](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[][]** ，每一排由完成 **3** 不同类型任务所需的时间组成 **A** 、 **B** 、和 **C** 。行元素 arr[i][0]、arr[i][1]和 arr[i][2]分别是完成类型为 **A、B** 和 **C** 的**I**T20 任务所需的时间。任务是根据以下条件从数组中找到准确完成 **K** 任务的最短完成时间:

*   同一类型的任务将同时运行。
*   只有当 **K** 类型的 **A** 任务已经完成时，才能执行 **B** 类型的任务。
*   只有当 **K** 类型的 **B** 任务已经完成时，才能执行 **C** 类型的任务。

**示例:**

> **输入:** N = 3，K = 2，arr[[]= { { 1，2，2}，{3，4，1}，{3，1，2}}
> **输出:** 7
> **说明:**
> 完成 A 类 K 个任务所需的最短时间= min(max(arr[0][0]，arr[2][0])，max(arr[0][0]，arr[1][0])，max(arr[1][0]，arr[2][0]
> 因此，完成 C 类 K 个任务的时间=最大值(arr[0][2]，arr[2][2]) = 2
> 因此，完成所有类型 K(= 2)的最短时间= 3 + 2 + 2 = 7
> 
> **输入** : N = 3，K = 3，arr[][] = {{2，4，5}，{4，5，4}，{3，4，5}}
> 输出: 14

**逼近**:使用[递归](https://www.geeksforgeeks.org/recursion/)可以解决问题。想法是要么从给定的数组中选择第 i <sup>行</sup>行，要么不选择。以下是循环关系。

> minime(t<sub>a</sub>、t<sub>b</sub>、t<sub>c</sub>、k、I)= min(minime(max(arr[I][0]、t<sub>a</sub>、max(arr[i][1]、t<sub>b))</sub>
> 
> MinTime(T <sub>A</sub> ，T <sub>B</sub> ，T <sub>C</sub> ，K，I)存储完成 **K** 任务的最短时间。
> i 存储给定数组元素的第 I 行的位置。
> 
> 基本情况:如果 K == 0:
> 返回 T<sub>A</sub>+T<sub>B</sub>+T<sub>C</sub>T7】如果 i < = 0:
> 返回无穷大

按照以下步骤解决问题:

1.  初始化一个变量，说 **X** 和 **Y** ，同时使用上述递归关系递归遍历每一行。
2.  **X** 通过选择给定数组的 **i <sup>第</sup>T5】行来存储最小完成时间。**
3.  **Y** 通过不选择给定数组的 **i <sup>第</sup>T5】行来存储最小完成时间。**
4.  利用上述递推关系求出 **X** 和 **Y** 的值。
5.  最后，为每一行返回 **min(X，Y)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;
#define N 3

// Function to get the minimum
// completion time to select
// exactly K items
int MinTime(int arr[][N],int i, 
                int Ta, int Tb,
                int Tc, int K)
{
    // Base case
    if(K == 0) {
        return Ta + Tb + Tc;
    }
    if(i == 0)
        return INT_MAX;

    // Select the ith item
    int X = MinTime(arr, i - 1,
            max(Ta, arr[i - 1][0]),
            max(Tb, arr[i - 1][1]),
            max(Tc, arr[i - 1][2]), K -1);

    // Do not select the ith item
    int Y = MinTime(arr, i - 1,
                    Ta, Tb, Tc, K);

    return min(X, Y);
}

// Driver Code
int main()
{
  int K = 2;
  int n = 3;
  int arr[N][N] = {{1, 2, 2} ,
                   {3, 4, 1} ,
                   {3, 1, 2}
                  };

  cout<<MinTime(arr, N, 0, 0, 0, K);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement 
// the above approach
import java.util.*;

class GFG{

// Function to get the minimum
// completion time to select
// exactly K items
public static int MinTime(int arr[][], int i,
                          int Ta, int Tb,
                          int Tc, int K)
{

    // Base case
    if (K == 0)
    {
        return Ta + Tb + Tc;
    }
    if (i == 0)
        return Integer.MAX_VALUE;

    // Select the ith item
    int X = MinTime(arr, i - 1,
                    Math.max(Ta, arr[i - 1][0]),
                    Math.max(Tb, arr[i - 1][1]),
                    Math.max(Tc, arr[i - 1][2]), K - 1);

    // Do not select the ith item
    int Y = MinTime(arr, i - 1, Ta,
                    Tb, Tc, K);

    return Math.min(X, Y);
}

// Driver Code
public static void main(String args[])
{
    int K = 2;
    int n = 3;
    int arr[][] = { { 1, 2, 2 },
                    { 3, 4, 1 },
                    { 3, 1, 2 } };

    System.out.println(MinTime(arr, n, 0, 0, 0, K));
}
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
N = 3

# Function to get the minimum
# completion time to select
# exactly K items
def MinTime(arr, i, Ta, Tb, Tc, K):

    # Base cas
    if (K == 0):
        return Ta + Tb + Tc
    if (i == 0):
        return 10**9

    # Select the ith item
    X = MinTime(arr, i - 1,
            max(Ta, arr[i - 1][0]),
            max(Tb, arr[i - 1][1]),
            max(Tc, arr[i - 1][2]), K -1)

    # Do not select the ith item
    Y = MinTime(arr, i - 1,
                Ta, Tb, Tc, K)

    return min(X, Y)

# Driver Code
if __name__ == '__main__':

    K = 2
    n = 3
    arr = [ [ 1, 2, 2 ],
            [ 3, 4, 1 ],
            [ 3, 1, 2 ] ]

    print(MinTime(arr, N, 0, 0, 0, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement 
// the above approach
using System;
class GFG{

// Function to get the minimum
// completion time to select
// exactly K items
public static int MinTime(int [,]arr, int i,
                          int Ta, int Tb,
                          int Tc, int K)
{   
  // Base case
  if (K == 0)
  {
    return Ta + Tb + Tc;
  }
  if (i == 0)
    return int.MaxValue;

  // Select the ith item
  int X = MinTime(arr, i - 1,
                  Math.Max(Ta,
                           arr[i - 1, 0]),
                  Math.Max(Tb,
                           arr[i - 1, 1]),
                  Math.Max(Tc,
                           arr[i - 1, 2]),
                               K - 1);

  // Do not select the ith item
  int Y = MinTime(arr, i - 1, Ta,
                  Tb, Tc, K);

  return Math.Min(X, Y);
}

// Driver Code
public static void Main(String []args)
{
  int K = 2;
  int n = 3;
  int [,]arr = {{1, 2, 2},
                {3, 4, 1},
                {3, 1, 2}};

  Console.WriteLine(MinTime(arr, n, 0,
                            0, 0, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement 
// the above approach

// Function to get the minimum
// completion time to select
// exactly K items
function Mletime(arr, i, Ta, Tb, Tc, K)
{

    // Base case
    if (K == 0)
    {
        return Ta + Tb + Tc;
    }
    if (i == 0)
        return Number.MAX_VALUE;

    // Select the ith item
    let X = Mletime(arr, i - 1,
                    Math.max(Ta, arr[i - 1][0]),
                    Math.max(Tb, arr[i - 1][1]),
                    Math.max(Tc, arr[i - 1][2]), K - 1);

    // Do not select the ith item
    let Y = Mletime(arr, i - 1, Ta,
                    Tb, Tc, K);

    return Math.min(X, Y);
}

// Driver code
K = 2;
let n = 3;
let arr = [ [ 1, 2, 2 ],
            [ 3, 4, 1 ],
            [ 3, 1, 2 ] ];

document.write(Mletime(arr, n, 0, 0, 0, K));

// This code is contributed by splevel62 

</script>
```

**Output**

```
7
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**接近 2**T2:-

## C++

```
#include <iostream>
#include <bits/stdc++.h>

using namespace std;
int MinTime(vector<vector<int>>& tasks, int k)
{
    // if k == 0 then return 0
    if (k == 0)
    {
        return 0;
    }
    vector<pair<int, pair<int, int>>> arr;

    // make a pair of pair DS
    for (auto t : tasks)
    {
        arr.push_back({t[0], {t[1], t[2]}});
    }

    // sort the pairs
    sort(arr.begin(), arr.end());

    // initialize the ans as INT_MAX/2
    int ans = INT_MAX / 2;
    for (int i = k - 1; i < arr.size(); i++)
    {
        vector<pair<int, int>> pr;

        // push the pairs into the pr vector
        for (int j = 0; j <= i; j++)
        {
            pr.push_back(arr[j].second);
        }

        // sort the pairs
        sort(pr.begin(), pr.end());

        // priority queue
        priority_queue<int> q;
        for (int j = 0; j < pr.size(); j++)
        {
            q.push(pr[j].second);
            if (q.size() > k)
            {
                q.pop();
            }
            if (q.size() == k)
            {
                ans = min(ans, arr[i].first + q.top() + pr[j].first);
            }
        }
    }
    return ans;
}

// Driver Code
int main() {

   int K = 2;
  int n = 3;
  vector<vector<int>> arr =
                  {{1, 2, 2} ,
                   {3, 4, 1} ,
                   {3, 1, 2}
                  };

  cout<<MinTime(arr,K)<<endl;
  //This code is given by Akshay Verma
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement 
// the above approach
import java.util.*;
class GFG
{
  static int MinTime(int[][] tasks, int k)
  {

    // if k == 0 then return 0
    if (k == 0)
    {
      return 0;
    }
    ArrayList<int[]> arr = new ArrayList<>();

    // make a pair of pair DS
    for (int[] t : tasks)
    {
      arr.add(new int[]{t[0], t[1], t[2]});
    }

    // sort the pairs
    Collections.sort(arr, (a, b)->a[0] - b[0]);

    // initialize the ans as INT_MAX/2
    int ans =Integer.MAX_VALUE / 2;
    for (int i = k - 1; i < arr.size(); i++)
    {
      ArrayList<int[]> pr = new ArrayList<>();

      // push the pairs into the pr vector
      for (int j = 0; j <= i; j++)
      {
        pr.add(new int[]{arr.get(j)[1],arr.get(j)[2]});
      }

      // sort the pairs
      Collections.sort(pr, (a, b)->a[0] - b[0]);

      // priority queue
      PriorityQueue<Integer> q = new PriorityQueue<>();
      for (int j = 0; j < pr.size(); j++)
      {
        q.add(pr.get(j)[1]);
        if (q.size() > k)
        {
          q.poll();
        }
        if (q.size() == k)
        {
          ans = Math.min(ans, arr.get(i)[0] +
                         q.peek() + pr.get(j)[0]);
        }
      }
    }
    return ans;
  }

  // Driver code
  public static void main (String[] args)
  {
    int K = 2;
    int n = 3;
    int arr[][] = { { 1, 2, 2 },
                   { 3, 4, 1 },
                   { 3, 1, 2 } };

    System.out.println(MinTime(arr,K));

  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program to implement 
# the above approach
import sys

def MinTime(tasks,k):

   # if k == 0 then return 0
    if (k == 0):
        return 0

    arr = []

     # make a pair of pair DS
    for t in tasks:
        arr.append([t[0], t[1], t[2]])

     # sort the pairs
    arr.sort()

    # initialize the ans as INT_MAX/2
    ans = sys.maxsize//2

    for i in range(k - 1, len(arr)):
        pr = []

    # push the pairs into the pr vector
        for j in range(i+1):
            pr.append([arr[j][1],arr[j][2]])

         # sort the pairs
        pr.sort()

        # priority queue
        q = []

        for j in range(len(pr)):
            q.append(pr[j][1])

            if(len(q) > k):
                q.pop(0)
            if(len(q) == k):
                ans=min(ans, arr[i][0] + q[0] + pr[j][0])
    return ans

  # Driver code
K = 2
n = 3

arr = [[1, 2, 2], [ 3, 4, 1 ], [3, 1, 2 ]]
print(MinTime(arr, K))

# This code is contributed by unknown2108
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  static int MinTime(int[,] tasks, int k)
  {

    // if k == 0 then return 0
    if (k == 0)
    {
      return 0;
    }
    List<List<int>> arr = new List<List<int>>();

    // make a pair of pair DS
    for(int i = 0; i < tasks.GetLength(0); i++)
    {
        arr.Add(new List<int>());
        for(int j = 0; j < tasks.GetLength(1); j++)
        {
         arr[i].Add(tasks[i,j]);  
        }
    }

    // initialize the ans as INT_MAX/2
    int ans = Int32.MaxValue / 2;
    for (int i = k - 1; i < arr.Count; i++)
    {
      List<List<int>> pr = new List<List<int>>();

      // push the pairs into the pr vector
      for (int j = 0; j <= i; j++)
      {
        pr.Add(new List<int>());
        pr[j].Add(arr[j][1]);
        pr[j].Add(arr[j][2]);
      }

      // priority queue
      List<int> q = new List<int>();
      for (int j = 0; j < pr.Count; j++)
      {
        q.Add(pr[j][1]);
        q.Sort();
        q.Reverse();
        if (q.Count > k)
        {
          q.RemoveAt(0);
        }
        if (q.Count == k)
        {
          ans = Math.Min(ans, arr[i][0] + q[0] + pr[j][0]) + 1;
        }
      }
    }
    return ans;
  }

  // Driver code
  static void Main() {
    int K = 2;
    int[,] arr = { { 1, 2, 2 },
                   { 3, 4, 1 },
                   { 3, 1, 2 } };

    Console.Write(MinTime(arr,K));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

function MinTime(tasks,k)
{
    // if k == 0 then return 0
    if (k == 0)
    {
      return 0;
    }
    let arr = [];

    // make a pair of pair DS
    for (let t=0;t< tasks.length;t++)
    {
      arr.push([tasks[t][0], tasks[t][1], tasks[t][2]]);
    }

    // sort the pairs
    arr.sort(function(a,b){return a[0]-b[0];});

    // initialize the ans as INT_MAX/2
    let ans =Number.MAX_VALUE / 2;
    for (let i = k - 1; i < arr.length; i++)
    {
      let pr = [];

      // push the pairs into the pr vector
      for (let j = 0; j <= i; j++)
      {
        pr.push([arr[j][1],arr[j][2]]);
      }

      // sort the pairs
      pr.sort(function(a,b){return a[0]-b[0];});

      // priority queue
      let q = [];
      for (let j = 0; j < pr.length; j++)
      {
        q.push(pr[j][1]);
        if (q.length > k)
        {
          q.shift();
        }
        if (q.length == k)
        {
          ans = Math.min(ans, arr[i][0] +
                         q[0] + pr[j][0]);
        }
      }
    }
    return ans;
}

// Driver code
let K = 2;
let n = 3;
let arr=[[ 1, 2, 2 ],
                   [ 3, 4, 1 ],
                   [ 3, 1, 2 ]];
document.write(MinTime(arr,K));

// This code is contributed by patel2127
</script>
```

**Output**

```
7
```

**时间复杂度:-O(N)<sup>2</sup>logN)**
T5】空间复杂度:- O(N)