# 查询给定的子阵列乘以给定的数字 X 并打印总和

> 原文:[https://www . geesforgeks . org/query-to-乘-给定子数组-给定数字-x-and-print-sum/](https://www.geeksforgeeks.org/queries-to-multiply-the-given-subarray-with-given-number-x-and-print-sum/)

给定一个数组 **arr[]** 和 **Q** 查询，其中每个查询包含三个整数(l，r，x)，任务是在将每个元素乘以 x 后打印范围[l，r]中元素的总和。

```
Query(l, r, x) = 
   arr[l]*x + arr[l+1]*x + .... arr[r-1]*x + arr[r]*x
```

**注**:与 x 相乘是为了计算答案，在查询的任何一步都不会在输入数组中更新。
**例:**

> **输入:** arr[] = {2，3，4，2，5，1}
> Q[] = {{2，4，5}，{1，1， 4}}
> **输出:** 55 12
> **解释:**
> **查询 1:** l = 2 r = 4 x = 5
> 年= arr[2]*5 + arr[3]*6 + ar[4 8}}
> **输出:**【16】
> **【解释:**
> **查询 1:**【l = 1r = 1x = 8】
> 年= arr[1]*8
> = 2*8

**天真法:**思想是迭代数组的每个查询，对于每个查询迭代[l，r]范围的元素，求每个元素的和乘以 x.
**时间复杂度:** O(Q*N)
**高效法:**思想是预计算数组的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，然后对于每个查询求范围[l，r]的元素和乘以 x，求每个查询的答案。
以下是计算每个查询答案的公式:

```
// pre_sum[i] denotes the prefix sum of
// the array from the array 0 to i
answer = x * (pre_sum[r] - pre_sum[l-1])
```

以下是上述方法的实现:

## C++

```
// C++ implementation to multiply
// the given subarray by the x
// for multiple queries of the Q

#include <bits/stdc++.h>

using namespace std;

// Function to answer each query
int query(vector<int> pre_sum, int n,
         int l, int r, int val)
{
    int ans;
    int temp = 0;
    if (l > 0) {
        temp = pre_sum[l-1];
    }
    ans = val * (pre_sum[r] - temp);
    return ans;
}

// Function to multiply the subarray
// by the x for multiple Queries
void multiplyArray(int arr[],
 vector<pair<pair<int, int>, int>> q,
                             int n){
    vector<int> pre_sum;
    int s = 0;

    // Loop to compute the prefix
    // sum of the array
    for (int i = 0; i < n; i++){
        s += arr[i];
        pre_sum.push_back(s);
    }

    // Loop to answer each query
    for(auto i: q){
        cout << query(pre_sum, n, i.first.first,
         i.first.second, i.second) << endl;
    }
}

// Driver Code
int main()
{
    // Array
    int arr[] = { 2, 3, 4, 2, 5, 1 };
    int n = 6;
    vector<pair<pair<int, int>, int>> q;
    q.push_back({{2, 4}, 5});
    q.push_back({{1, 1}, 4});
    q.push_back({{1, 3}, -2});

    // Function Call
    multiplyArray(arr, q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
// Java implementation to multiply
// the given subarray by the x
// for multiple queries of the Q
import java.io.*;
import java.util.ArrayList;
class GFG
{

  // Function to answer each query
  public static int query(ArrayList<Integer> pre_sum,
                          int n, int l, int r, int val)
  {
    int ans;
    int temp = 0;
    if (l > 0)
    {
      temp = pre_sum.get(l - 1);
    }
    ans = val * (pre_sum.get(r) - temp);
    return ans;
  }

  // Function to multiply the subarray
  // by the x for multiple Queries
  public static void multiplyArray(int arr[],
                                   ArrayList<pair> q,
                                   int n)
  {
    ArrayList<Integer> pre_sum = new ArrayList<>();
    int s = 0;

    // Loop to compute the prefix
    // sum of the array
    for (int i = 0; i < n; i++)
    {
      s += arr[i];
      pre_sum.add(s);
    }

    // Loop to answer each query
    for(int i = 0; i < q.size(); i++)
    {
      System.out.println(query(pre_sum, n,
                               q.get(i).pr.a,
                               q.get(i).pr.b,
                               q.get(i).second));
    }
  }

  // Driver Code
  public static void main(String [] args)
  {
    // Array
    int arr[] = { 2, 3, 4, 2, 5, 1 };
    int n = 6;
    ArrayList<pair> q = new ArrayList<>();
    q.add(new pair(new pair1(2, 4), 5));
    q.add(new pair(new pair1(1, 1), 4));
    q.add(new pair(new pair1(1, 3), -2));

    // Function Call
    multiplyArray(arr, q, n);
  }
}
class pair
{

  pair1 pr;
  int second;

  pair(pair1 pr, int second)
  {
    this.pr = pr;
    this.second = second;
  }
}
class pair1
{
  int a;
  int b;
  pair1(int a, int b)
  {
    this.a = a;
    this.b = b;
  }
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python3 implementation to multiply
# the given subarray by the x
# for multiple queries of the Q

# Function to answer each query
def query(pre_sum, n, l, r, val):

    ans = 0
    temp = 0;
    if (l > 0):
        temp = pre_sum[l - 1];

    ans = val * (pre_sum[r] - temp);
    return ans;

# Function to multiply the subarray
# by the x for multiple Queries
def multiplyArray(arr, q, n):

    pre_sum = []
    s = 0;

    # Loop to compute the prefix
    # sum of the array
    for i in range(n):

        s += arr[i];
        pre_sum.append(s);

    # Loop to answer each query
    for i in q:
        print(query(pre_sum, n, i[0][0], i[0][1], i[1]))

# Driver Code
if __name__=='__main__':

    # Array
    arr = [ 2, 3, 4, 2, 5, 1 ]
    n = 6;
    q = []
    q.append([[2, 4], 5])
    q.append([[1, 1], 4])
    q.append([[1, 3], -2])

    # Function Call
    multiplyArray(arr, q, n);

# this code is contribute by rutvik_56
```

## C#

```
// C# implementation to multiply
// the given subarray by the x
// for multiple queries of the Q
using System;
using System.Collections.Generic;
class GFG
{

    // Function to answer each query
    static int query(List<int> pre_sum, int n,
             int l, int r, int val)
    {
        int ans;
        int temp = 0;
        if (l > 0)
        {
            temp = pre_sum[l - 1];
        }
        ans = val * (pre_sum[r] - temp);
        return ans;
    }

    // Function to multiply the subarray
    // by the x for multiple Queries
    static void multiplyArray(int[] arr, List<Tuple<Tuple<int, int>, int>> q, int n)
    {
        List<int> pre_sum = new List<int>();
        int s = 0;

        // Loop to compute the prefix
        // sum of the array
        for (int i = 0; i < n; i++)
        {
            s += arr[i];
            pre_sum.Add(s);
        }

        // Loop to answer each query
        foreach(Tuple<Tuple<int, int>, int> i in q)
        {
            Console.WriteLine(query(pre_sum, n, i.Item1.Item1,
                                    i.Item1.Item2, i.Item2));
        }
    }

  // Driver code
  static void Main()
  {

    // Array
    int[] arr = { 2, 3, 4, 2, 5, 1 };
    int n = 6;
    List<Tuple<Tuple<int, int>, int>> q = new List<Tuple<Tuple<int, int>, int>>();
    q.Add(new Tuple<Tuple<int, int>, int>(new Tuple<int, int>(2,4), 5));
    q.Add(new Tuple<Tuple<int, int>, int>(new Tuple<int, int>(1,1), 4));
    q.Add(new Tuple<Tuple<int, int>, int>(new Tuple<int, int>(1,3), -2));

    // Function Call
    multiplyArray(arr, q, n);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript implementation to multiply
// the given subarray by the x
// for multiple queries of the Q

// Function to answer each query
function query(pre_sum, n, l, r, val)
{
    var ans;
    var temp = 0;
    if (l > 0) {
        temp = pre_sum[l-1];
    }
    ans = val * (pre_sum[r] - temp);
    return ans;
}

// Function to multiply the subarray
// by the x for multiple Queries
function multiplyArray(arr, q, n){
    var pre_sum = [];
    var s = 0;

    // Loop to compute the prefix
    // sum of the array
    for (var i = 0; i < n; i++){
        s += arr[i];
        pre_sum.push(s);
    }

    // Loop to answer each query
    q.forEach(i => {
        document.write( query(pre_sum, n, i[0][0],
         i[0][1], i[1]) + "<br>");
    });
}

// Driver Code
// Array
var arr = [2, 3, 4, 2, 5, 1];
var n = 6;
var q = [];
q.push([[2, 4], 5]);
q.push([[1, 1], 4]);
q.push([[1, 3], -2]);

// Function Call
multiplyArray(arr, q, n);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
55
12
-18
```

**时间复杂度:**O(Q+N)
T3】辅助空间: O(N)