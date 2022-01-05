# 查询以检查数组中是否存在任何值最多等于给定对的对

> 原文:[https://www . geesforgeks . org/query-to-check-if-any-pair-in-a-array-with-values-至多等于给定的对/](https://www.geeksforgeeks.org/queries-to-check-if-any-pair-exists-in-an-array-having-values-at-most-equal-to-the-given-pair/)

给定一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)**arr【】**和 **Q** 的[向量，以数组**查询【】**中的对的形式进行查询，每个查询的任务是检查是否存在两个值都小于当前查询对中的值的对。如果发现是真的，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

**示例:**

> **输入:** arr[][] = {{3，5}、{2，7}、{2，3}、{4，9}}，查询[][] = {{3，4}、{3，2}、{4，1}、{3，7}}
> **输出:**
> 是
> 否
> 否
> 是
> **解释:**
> 查询 1: Pair {2，3}存在于同时具有
> 查询 2:在{3，2}的 arr[]中找不到有效的对。
> 查询 3:在{4，1}的 arr[]中找不到有效的对。
> 查询 4:对{2，7}存在于{3，7}的 arr[]中。
> 
> **输入:** arr[][] = {{2，1}，{4，2}，{4，4}，{7，2}}，查询[][] = {{2，1}，{1，1}}
> **输出:**
> 是
> 否

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **查询【】【】**对于每一对，遍历给定的对数组，检查是否存在对应值大于或等于对 **{p1，p2}** 的对，然后打印**“是”**。否则，打印**“否”**。

***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。按照以下步骤解决此问题:

*   [按照递增的顺序，相对于配对中的第一个元素对配对数组进行排序。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)如果存在两个第一值相同的对，则基于对的第二个元素排列对。
*   排序后，[遍历对的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于所有具有相同第一值的对，用所有具有相同第一值的对中的最小值替换第二值。
*   现在，遍历给定的**查询[]** 数组，并对数组中的每一对执行二分搜索法运算 **arr[]** 。
*   如果以上步骤得到的对小于**查询【】**中的当前对，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that performs binary search
// to find value less than or equal to
// first value of the pair
int binary_search(vector<pair<int, int> > vec,
                  int n, int a)
{
    int low, high, mid;
    low = 0;
    high = n - 1;

    // Perform binary search
    while (low < high) {
        // Find the mid
        mid = low + (high - low + 1) / 2;

        // Update the high
        if (vec[mid].first > a) {
            high = mid - 1;
        }

        // Else update low
        else if (vec[mid].first <= a) {
            low = mid;
        }
    }

    // Return the low index
    return low;
}

// Function to modify the second
// value of each pair
void modify_vec(
    vector<pair<int, int> >& v, int n)
{
    // start from index 1
    for (int i = 1; i < n; i++) {
        v[i].second
            = min(v[i].second,
                  v[i - 1].second);
    }
}

// Function to evaluate each query
int evaluate_query(vector<pair<int, int> > v,
                   int n, int m1,
                   int m2)
{
    // Find value less than or equal to
    // the first value of pair
    int temp = binary_search(v, n, m1);

    // check if we got the required
    // pair or not
    if ((v[temp].first <= m1)
        && (v[temp].second <= m2)) {
        return 1;
    }

    return 0;
}

// Function to find a pair whose values is
// less than the given pairs in query
void checkPairs(vector<pair<int, int> >& v,
                vector<pair<int, int> >& queries)
{

    // Find the size of the vector
    int n = v.size();

    // sort the vector based on
    // the first value
    sort(v.begin(), v.end());

    // Function Call to modify the
    // second value of each pair
    modify_vec(v, n);

    int k = queries.size();

    // Traverse each queries
    for (int i = 0; i < k; i++) {
        int m1 = queries[i].first;
        int m2 = queries[i].second;

        // Evaluate each query
        int result
            = evaluate_query(v, n, m1, m2);

        // Print the result
        if (result > 0)
            cout << "Yes\n";
        else
            cout << "No\n";
    }
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr
        = { { 3, 5 }, { 2, 7 }, { 2, 3 }, { 4, 9 } };

    vector<pair<int, int> > queries
        = { { 3, 4 }, { 3, 2 }, { 4, 1 }, { 3, 7 } };

    // Function Call
    checkPairs(arr, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class GFG{

  // Function that performs binary search
  // to find value less than or equal to
  // first value of the pair
  static int binary_search(int[][] vec,
                           int n, int a)
  {
    int low, high, mid;
    low = 0;
    high = n - 1;

    // Perform binary search
    while (low < high)
    {

      // Find the mid
      mid = low + (high - low + 1) / 2;

      // Update the high
      if (vec[mid][0] > a)
      {
        high = mid - 1;
      }

      // Else update low
      else if (vec[mid][1] <= a)
      {
        low = mid;
      }
    }

    // Return the low index
    return low;
  }

  // Function to modify the second
  // value of each pair
  static void modify_vec(
    int[][] v, int n)
  {
    // start from index 1
    for (int i = 1; i < n; i++)
    {
      v[i][1] =  Math.min(v[i][1],
                          v[i - 1][1]);
    }
  }

  // Function to evaluate each query
  static int evaluate_query(int[][] v,
                            int n, int m1,
                            int m2)
  {

    // Find value less than or equal to
    // the first value of pair
    int temp = binary_search(v, n, m1);

    // check if we got the required
    // pair or not
    if ((v[temp][0] <= m1)
        && (v[temp][1] <= m2))
    {
      return 1;
    }

    return 0;
  }

  // Function to find a pair whose values is
  // less than the given pairs in query
  static void checkPairs(int[][] v,
                         int[][] queries)
  {

    // Find the size of the vector
    int n = v.length;

    // sort the vector based on
    // the first value
    Arrays.sort(v, (a, b)->a[0]-b[0]);

    // Function Call to modify the
    // second value of each pair
    modify_vec(v, n);
    int k = queries.length;

    // Traverse each queries
    for (int i = 0; i < k; i++)
    {
      int m1 = queries[i][0];
      int m2 = queries[i][1];

      // Evaluate each query
      int result
        = evaluate_query(v, n, m1, m2);

      // Print the result
      if (result > 0)
        System.out.println("Yes");
      else
        System.out.println("No");
    }
  }

  // Driver function
  public static void main (String[] args)
  {
    int[][] arr
      = { { 3, 5 }, { 2, 7 }, { 2, 3 }, { 4, 9 } };

    int[][] queries
      = { { 3, 4 }, { 3, 2 }, { 4, 1 }, { 3, 7 } };

    // Function Call
    checkPairs(arr, queries);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that performs binary search
# to find value less than or equal to
# first value of the pair
def binary_search(vec, n, a):
    low, high, mid = 0, 0, 0
    low = 0
    high = n - 1

    # Perform binary search
    while (low < high):

      # Find the mid
        mid = low + (high - low + 1) // 2

        # Update the high
        if (vec[mid][0] > a):
            high = mid - 1

        # Else update low
        elif vec[mid][0] <= a:
            low = mid

    # Return the low index
    return low

# Function to modify the second
# value of each pair
def modify_vec(v, n):

    # start from index 1
    for i in range(n):
        v[i][1] = min(v[i][1], v[i - 1][1])

    return v

# Function to evaluate each query
def evaluate_query(v, n, m1, m2):

    # Find value less than or equal to
    # the first value of pair
    temp = binary_search(v, n, m1)

    # check if we got the required
    # pair or not
    if ((v[temp][0] <= m1)
        and (v[temp][1] <= m2)):
        return 1

    return 0

# Function to find a pair whose values is
# less than the given pairs in query
def checkPairs(v, queries):

    # Find the size of the vector
    n = len(v)

    # sort the vector based on
    # the first value
    v = sorted(v)

    # Function Call to modify the
    # second value of each pair
    v = modify_vec(v, n)

    k = len(queries)

    # Traverse each queries
    for i in range(k):
        m1 = queries[i][0]
        m2 = queries[i][1]

        # Evaluate each query
        result = evaluate_query(v, n, m1, m2)

        # Print the result
        if (result > 0):
            print("Yes")
        else:
            print("No")

# Driver Code
if __name__ == '__main__':
    arr= [ [ 3, 5 ], [ 2, 7 ], [ 2, 3 ], [ 4, 9 ] ]

    queries = [ [ 3, 4 ], [ 3, 2 ], [ 4, 1 ], [ 3, 7 ] ]

    # Function Call
    checkPairs(arr, queries)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function that performs binary search
  // to find value less than or equal to
  // first value of the pair
function binary_search(vec,a,n)
{
    let low, high, mid;
    low = 0;
    high = n - 1;

    // Perform binary search
    while (low < high)
    {

      // Find the mid
      mid = low + Math.floor((high - low + 1) / 2);

      // Update the high
      if (vec[mid][0] > a)
      {
        high = mid - 1;
      }

      // Else update low
      else if (vec[mid][1] <= a)
      {
        low = mid;
      }
    }

    // Return the low index
    return low;
}

 // Function to modify the second
  // value of each pair
function modify_vec(v,n)
{
    // start from index 1
    for (let i = 1; i < n; i++)
    {
      v[i][1] =  Math.min(v[i][1],
                          v[i - 1][1]);
    }
}

// Function to evaluate each query
function evaluate_query(v,n,m1,m2)
{
    // Find value less than or equal to
    // the first value of pair
    let temp = binary_search(v, n, m1);

    // check if we got the required
    // pair or not
    if ((v[temp][0] <= m1)
        && (v[temp][1] <= m2))
    {
      return 1;
    }

    return 0;   
}

 // Function to find a pair whose values is
  // less than the given pairs in query
function checkPairs(v, queries)
{
    // Find the size of the vector
    let n = v.length;

    // sort the vector based on
    // the first value
    v.sort(function(a, b){return a[0]-b[0]});

    // Function Call to modify the
    // second value of each pair
    modify_vec(v, n);
    let k = queries.length;

    // Traverse each queries
    for (let i = 0; i < k; i++)
    {
      let m1 = queries[i][0];
      let m2 = queries[i][1];

      // Evaluate each query
      let result
        = evaluate_query(v, n, m1, m2);

      // Print the result
      if (result > 0)
        document.write("Yes<br>");
      else
        document.write("No<br>");
    }
}

// Driver function
let arr=[[ 3, 5 ], [ 2, 7 ], [ 2, 3 ], [ 4, 9 ]];

let queries=[[ 3, 4 ], [ 3, 2 ], [ 4, 1 ], [ 3, 7 ]];

// Function Call
checkPairs(arr, queries);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Yes
No
No
Yes
```

***时间复杂度:** O(Q*log N)*
***辅助空间:** O(1)*