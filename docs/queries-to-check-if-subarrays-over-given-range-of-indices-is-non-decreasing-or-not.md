# 查询给定索引范围内的子阵列是否不减少

> 原文:[https://www . geeksforgeeks . org/query-to-check-如果子阵列超过给定的索引范围-是-不减少还是-不减少/](https://www.geeksforgeeks.org/queries-to-check-if-subarrays-over-given-range-of-indices-is-non-decreasing-or-not/)

给定一个由 **N** 整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个由 **K** 类型的 **{L，R}** 查询组成的数组 **Q[][2]** ，每个查询的任务是检查[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) **{arr[L]，..数组的 arr[R]}** 是不减还是不减。如果发现是真的，则打印**“是”**。否则，打印“**否**”。

**示例:**

> ***输入:** arr[] = {1，7，3，4，9}，K = 2，Q[][] = {{1，2}，{2，4}}*
> ***输出:***
> *是*
> *否*
> ***解释:***
> ***查询 1:** 范围内的子阵列[1 因此，打印“是”。*
> ***查询 2:** 范围[2，4]内的子阵为{7，3，4，9}，非递减。因此，打印“否”。*
> 
> ***输入:** arr[] = {3，5，7，1，8，2}，K = 3，Q[][] = {{1，3}，{2，5}，{4，6}}*
> ***输出:***
> *是*
> *否*
> *否*

**简单方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的索引范围**【L，R】**进行每次查询，并检查[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)是否为按升序排序的。如果发现是真的，则打印**“是”**。否则，打印“**否**”。

***时间复杂度:** O(N * Q)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过预计算在范围**【1，I】**内满足**arr【I】>arr【I+1】**的相邻元素的计数来优化，这导致在范围**【L，R–1】**内这些指数的数量的恒定时间计算。按照以下步骤解决问题:

*   初始化一个数组，比如说 **pre[]** ，以存储从起始索引开始的索引计数，相邻元素按递增顺序排列。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**并分配**pre[I]= pre[I–1]**，然后将 **pre[i]** 增加 **1** ，如果**arr[I–1]>arr[I]**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**Q【】【】**对于每个查询 **{L，R}** ，如果**pre【R–1】–pre【L–1】**为 **0** ，则打印**“是”**。否则，打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform queries to check if
// subarrays over a given range of indices
//  is non-decreasing or not
void checkSorted(int arr[], int N,
                 vector<vector<int> >& Q)
{
    // Stores count of indices up to i
    // such that arr[i] > arr[i + 1]
    int pre[N] = { 0 };

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // Update pre[i]
        pre[i] = pre[i - 1]
                 + (arr[i - 1] > arr[i]);
    }

    // Traverse the array Q[][]
    for (int i = 0; i < Q.size(); i++) {

        int l = Q[i][0];
        int r = Q[i][1] - 1;

        // If pre[r] - pre[l-1] exceeds 0
        if (pre[r] - pre[l - 1] == 0)
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 7, 3, 4, 9 };
    vector<vector<int> > Q = { { 1, 2 },
                               { 2, 4 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    checkSorted(arr, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to perform queries to check if
  // subarrays over a given range of indices
  //  is non-decreasing or not
  static void checkSorted(int[] arr, int N, int[][] Q)
  {

    // Stores count of indices up to i
    // such that arr[i] > arr[i + 1]
    int[] pre = new int[N];

    // Traverse the array
    for (int i = 1; i < N; i++)
    {

      // Update pre[i]
      if((arr[i - 1] > arr[i]))
        pre[i] = pre[i - 1] + 1;
      else
        pre[i] = pre[i - 1];
    }

    // Traverse the array Q[][]
    for (int i = 0; i < Q.length; i++)
    {
      int l = Q[i][0];
      int r = Q[i][1] - 1;

      // If pre[r] - pre[l-1] exceeds 0
      if (pre[r] - pre[l - 1] == 0)
        System.out.println("Yes");
      else
        System.out.println("No");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 7, 3, 4, 9 };
    int Q[][] = { { 1, 2 }, { 2, 4 } };

    int N = arr.length;

    // Function Call
    checkSorted(arr, N, Q);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to perform queries to check if
# subarrays over a given range of indices
# is non-decreasing or not
def checkSorted(arr, N, Q):

    # Stores count of indices up to i
    # such that arr[i] > arr[i + 1]
    pre = [0]*(N)

    # Traverse the array
    for i in range(1, N):

        # Update pre[i]
        pre[i] = pre[i - 1] + (arr[i - 1] > arr[i])

    # Traverse the array Q[][]
    for i in range(len(Q)):
        l = Q[i][0]
        r = Q[i][1] - 1

        # If pre[r] - pre[l-1] exceeds 0
        if (pre[r] - pre[l - 1] == 0):
            print("Yes")
        else:
            print("No")

# Driver Code
if __name__ == '__main__':
    arr =[1, 7, 3, 4, 9]
    Q = [ [ 1, 2 ],[ 2, 4 ] ]
    N = len(arr)

    # Function Call
    checkSorted(arr, N, Q)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach

using System;

public class GFG{

    // Function to perform queries to check if
    // subarrays over a given range of indices
    // is non-decreasing or not
    static void checkSorted(int[] arr, int N, int[,] Q)
    {
        // Stores count of indices up to i
    // such that arr[i] > arr[i + 1]
    int[] pre = new int[N];

    // Traverse the array
    for (int i = 1; i < N; i++)
    {

      // Update pre[i]
      if((arr[i - 1] > arr[i]))
      {
          pre[i] = pre[i - 1] + 1;
      }
      else
      {  pre[i] = pre[i - 1];}
    }

    // Traverse the array Q[][]
    for (int i = 0; i < Q.GetLength(0); i++)
    {

      int l = Q[i,0];
      int r = Q[i,1] - 1;

      // If pre[r] - pre[l-1] exceeds 0
      if (pre[r] - pre[l - 1] == 0)
      {  Console.WriteLine("Yes");}
      else
        {Console.WriteLine("No");}
    }
    }

    // Driver Code

    static public void Main (){

        int[] arr = { 1, 7, 3, 4, 9 };
    int[,] Q = { { 1, 2 }, { 2, 4 } };

    int N = arr.Length;

    // Function Call
    checkSorted(arr, N, Q);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to perform queries to check if
// subarrays over a given range of indices
//  is non-decreasing or not
function checkSorted(arr, N, Q)
{

    // Stores count of indices up to i
    // such that arr[i] > arr[i + 1]
    var pre = Array(N).fill(0);

    // Traverse the array
    for(var i = 1; i < N; i++)
    {

        // Update pre[i]
        pre[i] = pre[i - 1] +
                (arr[i - 1] > arr[i]);
    }

    // Traverse the array Q[][]
    for(var i = 0; i < Q.length; i++)
    {
        var l = Q[i][0];
        var r = Q[i][1] - 1;

        // If pre[r] - pre[l-1] exceeds 0
        if (pre[r] - pre[l - 1] == 0)
            document.write("Yes" + "<br>");
        else
            document.write("No" + "<br>");
    }
}

// Driver Code
var arr = [ 1, 7, 3, 4, 9 ];
var Q = [ [ 1, 2 ], [ 2, 4 ] ];
var N = arr.length;

// Function Call
checkSorted(arr, N, Q);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
Yes
No
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)