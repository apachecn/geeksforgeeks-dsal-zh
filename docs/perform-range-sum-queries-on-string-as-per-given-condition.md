# 根据给定条件

对字符串进行范围和查询

> 原文:[https://www . geeksforgeeks . org/perform-range-sum-query-on-string-as-as-then-condition/](https://www.geeksforgeeks.org/perform-range-sum-queries-on-string-as-per-given-condition/)

给定一个只包含小写字母的字符串 **S** 和 **Q** 查询，其中每个查询包含一对 **{L，R}** 。对于每个查询{L，R}，都存在一个子串**S【L，R】**，任务是找到子串中每个字符的频率与它们在字母顺序中的位置的乘积的值。
**注:**考虑基于 1 的索引。
**示例:**

> **输入:**S =“ABCD”，Q = { {2，4}，{1，3} }
> **输出:** 9 6
> **解释:**
> 对于第 1 次查询，
> 子串为 S[2，4]=“BCD”。因此 b，c，d 的频率在 2 到 4 的范围内是 1，1，1。
> 值= 2*(1) + 3*(1) + 4*(1) = 9。
> 第二次查询，
> 子串为 S[1，3]=“ABC”。因此 a，b，c 的频率在 1 到 3 的范围内是 1，1，1。
> 值= 1*(1) + 2*(1) + 3*(1) = 6。
> **输入:** S = "geeksforgeeks "，Q = { {3，3}，{2，6}，{1，13} }
> **输出:** 5 46 133

**天真方法:**天真的想法是遍历查询中的每个范围**【L，R】**，并保持数组中每个字符的计数。遍历范围后，找到表达式 **1*(出现“a”)+2 *(出现“b”)+3 *(出现“c”)+的值)..+ 26*(出现‘z’)**。
***时间复杂度:** O(N*Q)，其中 N 为给定字符串的长度。*
***辅助空间:** O(1)*
**高效方法:**思路是使用整个字符串的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，通过这个前缀和我们可以在恒定时间内执行每个查询。以下是步骤:

1.  创建一个长度等于字符串长度的数组 **arr[]** 。
2.  遍历给定的字符串，对于字符串中每个对应的索引 **i** ，为 arr[i]指定**当前字符的值–“a”**。
3.  求数组 **arr[]** 的前缀和。这个前缀和数组将给出所有字符的出现和，直到每个索引 I。
4.  现在对于每个查询(比如 **{L，R }**)**arr[R–1]–arr[L–2]**的值将给出给定表达式的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform range sum queries
// on string as per the given condition
void Range_sum_query(string S,
                     vector<pair<int, int> > Query)
{
    // Initialize N by string size
    int N = S.length();

    // Create array A[] for prefix sum
    int A[N];

    A[0] = S[0] - 'a' + 1;

    // Iterate till N
    for (int i = 1; i < N; i++) {
        A[i] = S[i] - 'a' + 1;
        A[i] = A[i] + A[i - 1];
    }

    // Traverse the queries
    for (int i = 0; i < Query.size(); i++) {

        if (Query[i].first == 1) {

            // Check if if L == 1 range
            // sum will be A[R-1]
            cout << A[(Query[i].second) - 1]
                 << endl;
        }

        else {

            // Condition if L > 1 range sum
            // will be A[R-1] - A[L-2]
            cout << A[(Query[i].second) - 1]
                        - A[(Query[i].first) - 2]
                 << endl;
        }
    }
}

// Driver Code
int main()
{
    // Given string
    string S = "abcd";

    vector<pair<int, int> > Query;

    // Given Queries
    Query.push_back(make_pair(2, 4));
    Query.push_back(make_pair(1, 3));

    // Function call
    Range_sum_query(S, Query);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to perform range sum queries
// on String as per the given condition
static void Range_sum_query(String S,
                            Vector<pair> Query)
{

    // Initialize N by String size
    int N = S.length();

    // Create array A[] for prefix sum
    int []A = new int[N];

    A[0] = S.charAt(0) - 'a' + 1;

    // Iterate till N
    for(int i = 1; i < N; i++)
    {
        A[i] = S.charAt(i) - 'a' + 1;
        A[i] = A[i] + A[i - 1];
    }

    // Traverse the queries
    for(int i = 0; i < Query.size(); i++)
    {
        if (Query.get(i).first == 1)
        {

            // Check if if L == 1 range
            // sum will be A[R-1]
            System.out.print(
                A[(Query.get(i).second) - 1] + "\n");
        }

        else
        {

            // Condition if L > 1 range sum
            // will be A[R-1] - A[L-2]
            System.out.print(
                A[(Query.get(i).second) - 1] -
                A[(Query.get(i).first) - 2] + "\n");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String S = "abcd";

    Vector<pair> Query = new Vector<pair>();

    // Given Queries
    Query.add(new pair(2, 4));
    Query.add(new pair(1, 3));

    // Function call
    Range_sum_query(S, Query);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to perform range sum queries
# on string as per the given condition
def Range_sum_query(S, Query):

    # Initialize N by string size
    N = len(S)

    # Create array A[] for prefix sum
    A = [0] * N

    A[0] = ord(S[0]) - ord('a') + 1

    # Iterate till N
    for i in range(1, N):
        A[i] = ord(S[i]) - ord('a') + 1
        A[i] = A[i] + A[i - 1]

    # Traverse the queries
    for i in range(len(Query)):
        if(Query[i][0] == 1):

            # Check if if L == 1 range
            # sum will be A[R-1]
            print(A[Query[i][1] - 1])

        else:

            # Condition if L > 1 range sum
            # will be A[R-1] - A[L-2]
            print(A[Query[i][1] - 1] -
                  A[Query[i][0] - 2])

# Driver Code

# Given string
S = "abcd"

Query = []

# Given Queries
Query.append([2, 4])
Query.append([1, 3])

# Function call
Range_sum_query(S, Query)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  class pair
  {
    public int first, second;
    public pair(int first, int second)
    {
      this.first = first;
      this.second = second;
    }
  }

  // Function to perform range sum queries
  // on String as per the given condition
  static void Range_sum_query(String S, List<pair> Query)
  {

    // Initialize N by String size
    int N = S.Length;

    // Create array []A for prefix sum
    int[] A = new int[N];

    A[0] = S[0] - 'a' + 1;

    // Iterate till N
    for (int i = 1; i < N; i++)
    {
      A[i] = S[i] - 'a' + 1;
      A[i] = A[i] + A[i - 1];
    }

    // Traverse the queries
    for (int i = 0; i < Query.Count; i++)
    {
      if (Query[i].first == 1)
      {

        // Check if if L == 1 range
        // sum will be A[R-1]
        Console.Write(A[(Query[i].second) - 1] + "\n");
      }

      else
      {

        // Condition if L > 1 range sum
        // will be A[R-1] - A[L-2]
        Console.Write(A[(Query[i].second) - 1] -
                      A[(Query[i].first) - 2] + "\n");
      }
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given String
    String S = "abcd";

    List<pair> Query = new List<pair>();

    // Given Queries
    Query.Add(new pair(2, 4));
    Query.Add(new pair(1, 3));

    // Function call
    Range_sum_query(S, Query);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to perform range sum queries
// on string as per the given condition
function Range_sum_query(S, Query)
{

    // Initialize N by string size
    var N = S.length;

    // Create array A[] for prefix sum
    var A = Array(N);

    A[0] = S[0].charCodeAt(0) - 'a'.charCodeAt(0) + 1;

    // Iterate till N
    for (var i = 1; i < N; i++) {
        A[i] = S[i].charCodeAt(0) - 'a'.charCodeAt(0) + 1;
        A[i] = A[i] + A[i - 1];
    }

    // Traverse the queries
    for (var i = 0; i < Query.length; i++) {

        if (Query[i][0] == 1) {

            // Check if if L == 1 range
            // sum will be A[R-1]
            document.write( A[(Query[i][1]) - 1]+ "<br>");
        }

        else {

            // Condition if L > 1 range sum
            // will be A[R-1] - A[L-2]
            document.write( A[(Query[i][1]) - 1]
                        - A[(Query[i][0]) - 2]+ "<br>");
        }
    }
}

// Driver Code
// Given string
var S = "abcd";
var Query = [];

// Given Queries
Query.push([2, 4]);
Query.push([1, 3]);

// Function call
Range_sum_query(S, Query);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
9
6
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(N)