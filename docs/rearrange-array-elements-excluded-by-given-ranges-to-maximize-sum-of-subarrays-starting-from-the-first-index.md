# 重新排列由给定范围排除的阵列元素，以从第一个索引

开始最大化子阵列的总和

> 原文:[https://www . geeksforgeeks . org/rearray-array-elements-按给定范围排除-最大化子阵和-从第一个索引开始/](https://www.geeksforgeeks.org/rearrange-array-elements-excluded-by-given-ranges-to-maximize-sum-of-subarrays-starting-from-the-first-index/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **Q[][]** ，其中每行表示一个范围 **{l，r }**(**0≤l≤r≤N–1**)。任务是从索引 **0** 开始，通过重新排列除 **Q[][]** 中给定范围内的元素之外的数组，找到所有[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的最大和。

**示例:**

> **输入:** arr[] = {-8，4，-2，-6，4，7，1}，Q[][] = {{0，0}，{4，5}} **输出:** -15
> **解释:**
> 给定数组可以重新排列为{-8，4，1，-2，4，7，-6}。现在，从第一个索引开始的所有子阵列的和为:
> arr[0，0]之和=-8
> arr[0，1]之和=-8+4 =-4
> arr[0，2]之和=-8+4+1 =-3
> arr[0，3]之和=-8+4+1+(-2)=-5
> arr[0，4]之和= -8 + 4 +1 + (-2) + 4 = - 5]=-8+4+1+(-2)+4+7 = 6
> arr[0，6]之和= -8 + 4 +1 + (-2) + 4 + 7 + (-6) = 0
> 之和=-8+(-4)+(-3)+(-5)+(-1)+6+0 =-15
> 
> **输入:** arr[] = {-8，4，3}，Q[][] = {{0，2}}
> **输出:** -13
> **解释:**所有元素都存在于给定的范围集合中。因此，任何元素都不能重新排列。现在，来自第一个索引的所有子阵列的和为:
> arr[0，0]之和=-8
> arr[0，1]之和=-8+4 =-4
> arr[0，2]之和= -8 + 4 + 3 = -1
> 总和= -8 + (-4) + (-1) = -13

**做法:**思路是先找到不能重排的元素。然后，按降序对剩余元素进行排序，并将它们分配给索引，这样最大的元素将被分配给允许重新排列的最小索引。按照以下步骤解决问题:

*   创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **s** 和 **v** 分别存储索引和元素，可以重新排列。
*   遍历每个范围 **{l，r}** 的元素，并标记为已访问。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并存储索引 **i** ，如果它没有被标记为已访问。
*   [按降序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **v** 。
*   将给定数组中的元素插入为 **arr[s[i]] = v[i]** ，其中 **i** 是允许重新排列的元素数量。
*   完成上述步骤后，打印[给定数组的前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)之和作为最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the maximum sum
// all subarrays from the starting index
// after rearranging the array
int maxSum(int n, int a[], int l[][2], int q)
{
    // Stores elements after rearranging
    vector<int> v;

    // Keeps track of visited elements
    int d[n] = { 0 };

    // Traverse the queries
    for (int i = 0; i < q; i++) {

        // Mark elements that are not
        // allowed to rearranged
        for (int x = l[i][0];
             x <= l[i][1]; x++) {

            if (d[x] == 0) {
                d[x] = 1;
            }
        }
    }

    // Stores the indices
    set<int> st;

    // Get indices and elements that
    // are allowed to rearranged
    for (int i = 0; i < n; i++) {

        // Store the current index and
        // element
        if (d[i] == 0) {
            v.push_back(a[i]);
            st.insert(i);
        }
    }
    // Sort vector v in descending order
    sort(v.begin(), v.end(),
         greater<int>());

    // Insert elements in array
    int c = 0;
    for (auto it : st) {
        a[it] = v;
        c++;
    }

    // Stores the resultant sum
    int pref_sum = 0;

    // Stores the prefix sums
    int temp_sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {
        temp_sum += a[i];
        pref_sum += temp_sum;
    }

    // Return the maximum sum
    return pref_sum;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { -8, 4, -2, -6, 4, 7, 1 };

    // Given size
    int N = sizeof(arr) / sizeof(arr[0]);

    // Queries
    int q[][2] = { { 0, 0 }, { 4, 5 } };

    // Number of queries
    int queries = sizeof(q) / sizeof(q[0]);

    // Function Call
    cout << maxSum(N, arr, q, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function that finds the maximum sum
// all subarrays from the starting index
// after rearranging the array
static int maxSum(int n, int a[], int [][]l, int q)
{
    // Stores elements after rearranging
    Vector<Integer> v = new Vector<>();

    // Keeps track of visited elements
    int []d = new int[n];

    // Traverse the queries
    for (int i = 0; i < q; i++)
    {

        // Mark elements that are not
        // allowed to rearranged
        for (int x = l[i][0];
             x <= l[i][1]; x++)
        {

            if (d[x] == 0)
            {
                d[x] = 1;
            }
        }
    }

    // Stores the indices
    HashSet<Integer> st = new HashSet<>();

    // Get indices and elements that
    // are allowed to rearranged
    for (int i = 0; i < n; i++)
    {

        // Store the current index and
        // element
        if (d[i] == 0)
        {
            v.add(a[i]);
            st.add(i);
        }
    }

    // Sort vector v in descending order
    Collections.sort(v);
    Collections.reverse(v);

    // Insert elements in array
    int c = 0;
    for (int it : st)
    {
        a[it] = v.get(c);
        c++;
    }

    // Stores the resultant sum
    int pref_sum = 0;

    // Stores the prefix sums
    int temp_sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++)
    {
        temp_sum += a[i];
        pref_sum += temp_sum;
    }

    // Return the maximum sum
    return pref_sum;
}

// Driver Code
public static void main(String[] args)
{
    // Given array
    int []arr = { -8, 4, -2, -6, 4, 7, 1 };

    // Given size
    int N = arr.length;

    // Queries
    int [][]q = { { 0, 0 }, { 4, 5 } };

    // Number of queries
    int queries = q.length;

    // Function Call
    System.out.print(maxSum(N, arr, q, queries));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function that finds the
# maximum sum all subarrays
# from the starting index
# after rearranging the array
def maxSum(n, a, l, q):

    # Stores elements after
    # rearranging
    v = []

    # Keeps track of visited
    # elements
    d = [0] * n

    # Traverse the queries
    for i in range(q):

        # Mark elements that are not
        # allowed to rearranged
        for x in range(l[i][0],
                       l[i][1] + 1):

            if (d[x] == 0):
                d[x] = 1

    # Stores the indices
    st = set([])

    # Get indices and elements
    # that are allowed to rearranged
    for i in range(n):

        # Store the current index and
        # element
        if (d[i] == 0):
            v.append(a[i])
            st.add(i)

    # Sort vector v in descending
    # order
    v.sort(reverse = True)

    # Insert elements in array
    c = 0
    for it in st:
        a[it] = v
        c += 1

    # Stores the resultant sum
    pref_sum = 0

    # Stores the prefix sums
    temp_sum = 0

    # Traverse the given array
    for i in range(n):
        temp_sum += a[i]
        pref_sum += temp_sum

    # Return the maximum sum
    return pref_sum

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [-8, 4, -2,
           -6, 4, 7, 1]

    # Given size
    N = len(arr)

    # Queries
    q = [[0, 0], [4, 5]]

    # Number of queries
    queries = len(q)

    # Function Call
    print(maxSum(N, arr, q, queries))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that finds the maximum sum
// all subarrays from the starting index
// after rearranging the array
static int maxSum(int n, int []a, int [,]l, int q)
{

    // Stores elements after rearranging
    List<int> v = new List<int>();

    // Keeps track of visited elements
    int []d = new int[n];

    // Traverse the queries
    for (int i = 0; i < q; i++)
    {

        // Mark elements that are not
        // allowed to rearranged
        for (int x = l[i, 0];
             x <= l[i, 1]; x++)
        {

            if (d[x] == 0)
            {
                d[x] = 1;
            }
        }
    }

    // Stores the indices
    HashSet<int> st = new HashSet<int>();

    // Get indices and elements that
    // are allowed to rearranged
    for (int i = 0; i < n; i++)
    {

        // Store the current index and
        // element
        if (d[i] == 0)
        {
            v.Add(a[i]);
            st.Add(i);
        }
    }

    // Sort vector v in descending order
    v.Sort();
    v.Reverse();

    // Insert elements in array
    int c = 0;
    foreach (int it in st)
    {
        a[it] = v;
        c++;
    }

    // Stores the resultant sum
    int pref_sum = 0;

    // Stores the prefix sums
    int temp_sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++)
    {
        temp_sum += a[i];
        pref_sum += temp_sum;
    }

    // Return the maximum sum
    return pref_sum;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array
    int []arr = { -8, 4, -2, -6, 4, 7, 1 };

    // Given size
    int N = arr.Length;

    // Queries
    int [,]q = { { 0, 0 }, { 4, 5 } };

    // Number of queries
    int queries = q.GetLength(0);

    // Function Call
    Console.Write(maxSum(N, arr, q, queries));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds the maximum sum
// all subarrays from the starting index
// after rearranging the array
function maxSum(n, a, l, q)
{

    // Stores elements after rearranging
    let v = [];

    // Keeps track of visited elements
    let d = new Array(n);

     for(let i = 0; i < n; i++)
    {
        d[i] = 0;
    }

    // Traverse the queries
    for(let i = 0; i < q; i++)
    {

        // Mark elements that are not
        // allowed to rearranged
        for(let x = l[i][0];
               x <= l[i][1]; x++)
        {
            if (d[x] == 0)
            {
                d[x] = 1;
            }
        }
    }

    // Stores the indices
    let st = new Set();

    // Get indices and elements that
    // are allowed to rearranged
    for(let i = 0; i < n; i++)
    {

        // Store the current index and
        // element
        if (d[i] == 0)
        {
            v.push(a[i]);
            st.add(i);
        }
    }

    // Sort vector v in descending order
    v.sort(function(a, b){return b - a;});

    // Insert elements in array
    let c = 0;
    for(let it of st.values())
    {
        a[it] = v;
        c++;
    }

    // Stores the resultant sum
    let pref_sum = 0;

    // Stores the prefix sums
    let temp_sum = 0;

    // Traverse the given array
    for(let i = 0; i < n; i++)
    {
        temp_sum += a[i];
        pref_sum += temp_sum;
    }

    // Return the maximum sum
    return pref_sum;
}

// Driver Code

// Given array
let arr = [ -8, 4, -2, -6, 4, 7, 1 ];

// Given size
let N = arr.length;

// Queries
let q = [ [ 0, 0 ], [ 4, 5 ] ];

// Number of queries
let queries = q.length;

// Function Call
document.write(maxSum(N, arr, q, queries));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
-15
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*