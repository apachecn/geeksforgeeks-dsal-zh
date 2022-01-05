# 子阵列数按位“或”> = K

> 原文:[https://www . geeksforgeeks . org/子阵数-have-bitwise-or-k/](https://www.geeksforgeeks.org/number-of-subarrays-have-bitwise-or-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是计算具有**位 OR ≥ K** 的子数组的数量。

**示例:**

> **输入:** arr[] = { 1，2，3 } K = 3
> **输出:** 4
> 子阵列的按位 OR:
> { 1 } = 1
> { 1，2 } = 3
> { 1，2，3 } = 3
> { 2 } = 2
> { 2，3 } = 3
> { 3 } = 3
> 4 个子阵列的按位 OR ≥ K
> 
> **输入:** arr[] = { 3，4，5 } K = 6
> T3】输出: 2

**天真的做法:**运行三个嵌套循环。最外面的循环决定了子数组的开始。中间的循环决定了子数组的结束。最里面的循环遍历子数组，子数组的边界由最外面和中间的循环确定。对于每个子阵列，计算或并更新**计数=计数+ 1** ，如果或大于 **K** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of required sub-arrays
int countSubArrays(const int* arr, int n, int K)
{
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            int bitwise_or = 0;

            // Traverse sub-array [i..j]
            for (int k = i; k <= j; k++) {
                bitwise_or = bitwise_or | arr[k];
            }
            if (bitwise_or >= K)
                count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 6;
    cout << countSubArrays(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// Function to return the count of required sub-arrays
static int countSubArrays(int arr[], int n, int K)
{
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            int bitwise_or = 0;

            // Traverse sub-array [i..j]
            for (int k = i; k <= j; k++) {
                bitwise_or = bitwise_or | arr[k];
            }
            if (bitwise_or >= K)
                count++;
        }
    }
    return count;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 3, 4, 5 };
    int n = arr.length;
    int k = 6;
    System.out.println(countSubArrays(arr, n, k));

}
}
// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# required sub-arrays
def countSubArrays(arr, n, K) :

    count = 0;
    for i in range(n) :
        for j in range(i, n) :

            bitwise_or = 0

            # Traverse sub-array [i..j]
            for k in range(i, j + 1) :
                bitwise_or = bitwise_or | arr[k]

            if (bitwise_or >= K) :
                count += 1

    return count

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 4, 5 ]
    n = len(arr)
    k = 6

    print(countSubArrays(arr, n, k))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// required sub-arrays
static int countSubArrays(int []arr,
                          int n, int K)
{
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {
            int bitwise_or = 0;

            // Traverse sub-array [i..j]
            for (int k = i; k <= j; k++)
            {
                bitwise_or = bitwise_or | arr[k];
            }
            if (bitwise_or >= K)
                count++;
        }
    }
    return count;
}

// Driver code
public static void Main()
{
    int []arr = { 3, 4, 5 };
    int n = arr.Length;
    int k = 6;
    Console.WriteLine(countSubArrays(arr, n, k));
}
}

// This code is contributed by
// Mohit kumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// required sub-arrays
function countSubArrays($arr, $n, $K)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            $bitwise_or = 0;

            // Traverse sub-array [i..j]
            for ($k = $i; $k < $j + 1; $k++)
                $bitwise_or = $bitwise_or | $arr[$k];

            if ($bitwise_or >= $K)
                $count += 1;
        }
    }
    return $count;
}

// Driver code
$arr = array( 3, 4, 5 );
$n = count($arr);
$k = 6;

print(countSubArrays($arr, $n, $k));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count of required sub-arrays
    function countSubArrays(arr, n, K)
    {
        let count = 0;
        for (let i = 0; i < n; i++) {
            for (let j = i; j < n; j++) {

                let bitwise_or = 0;

                // Traverse sub-array [i..j]
                for (let k = i; k <= j; k++) {
                    bitwise_or = bitwise_or | arr[k];
                }
                if (bitwise_or >= K)
                    count++;
            }
        }
        return count;
    }

    // Driver code
    let arr = [ 3, 4, 5 ];
    let n = arr.length;
    let k = 6;
    document.write(countSubArrays(arr, n, k));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
```

以上解的时间复杂度为**O(n<sup>3</sup>)****辅助空间**为 O(1)。
一种**高效解决方案**使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)来计算子阵列在 **O(log n)** 时间内的按位或。因此，现在我们直接查询段树，而不是遍历子数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 100002
int tree[4 * N];

// Function to build the segment tree
void build(int* arr, int node, int start, int end)
{
    if (start == end) {
        tree[node] = arr[start];
        return;
    }
    int mid = (start + end) >> 1;
    build(arr, 2 * node, start, mid);
    build(arr, 2 * node + 1, mid + 1, end);
    tree[node] = tree[2 * node] | tree[2 * node + 1];
}

// Function to return the bitwise OR of segment [L..R]
int query(int node, int start, int end, int l, int r)
{
    if (start > end || start > r || end < l) {
        return 0;
    }

    if (start >= l && end <= r) {
        return tree[node];
    }

    int mid = (start + end) >> 1;
    int q1 = query(2 * node, start, mid, l, r);
    int q2 = query(2 * node + 1, mid + 1, end, l, r);
    return q1 | q2;
}

// Function to return the count of required sub-arrays
int countSubArrays(int arr[], int n, int K)
{

    // Build segment tree
    build(arr, 1, 0, n - 1);

    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // Query segment tree for bitwise OR
            // of sub-array [i..j]
            int bitwise_or = query(1, 0, n - 1, i, j);
            if (bitwise_or >= K)
                count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 6;
    cout << countSubArrays(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class Main
{
  static int N = 100002;
  static int tree[] = new int[4 * N];

  // Function to build the segment tree
  static void build(int arr[], int node,
                    int start, int end)
  {
    if (start == end) {
      tree[node] = arr[start];
      return;
    }
    int mid = (start + end) >> 1;
    build(arr, 2 * node, start, mid);
    build(arr, 2 * node + 1, mid + 1, end);
    tree[node] = tree[2 * node] | tree[2 * node + 1];
  }

  // Function to return the bitwise OR of segment [L..R]
  static int query(int node, int start,
                   int end, int l, int r)
  {
    if (start > end || start > r || end < l)
    {
      return 0;
    }

    if (start >= l && end <= r)
    {
      return tree[node];
    }

    int mid = (start + end) >> 1;
    int q1 = query(2 * node, start, mid, l, r);
    int q2 = query(2 * node + 1, mid + 1, end, l, r);
    return q1 | q2;
  }

  // Function to return the count of required sub-arrays
  static int countSubArrays(int arr[], int n, int K)
  {

    // Build segment tree
    build(arr, 1, 0, n - 1);

    int count = 0;
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Query segment tree for bitwise OR
        // of sub-array [i..j]
        int bitwise_or = query(1, 0, n - 1, i, j);
        if (bitwise_or >= K)
          count++;
      }
    }
    return count;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 3, 4, 5 };
    int n = arr.length;

    int k = 6;
    System.out.print(countSubArrays(arr, n, k));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python implementation of the approach

N = 100002
tree = [0]*(4 * N)

# Function to build the segment tree
def build(arr, node, start, end):
    if start == end:
        tree[node] = arr[start]
        return
    mid = (start + end) >> 1
    build(arr, 2 * node, start, mid)
    build(arr, 2 * node + 1, mid + 1, end)
    tree[node] = tree[2 * node] | tree[2 * node + 1]

# Function to return the bitwise OR of segment[L..R]
def query(node, start, end, l, r):
    if start > end or start > r or end < l:
        return 0

    if start >= l and end <= r:
        return tree[node]

    mid = (start + end) >> 1
    q1 = query(2 * node, start, mid, l, r)
    q2 = query(2 * node + 1, mid + 1, end, l, r)
    return q1 or q2

# Function to return the count of required sub-arrays
def countSubArrays(arr, n, K):

    # Build segment tree
    build(arr, 1, 0, n - 1)

    count = 0
    for i in range(n):
        for j in range(n):

            # Query segment tree for bitwise OR
            # of sub-array[i..j]
            bitwise_or = query(1, 0, n - 1, i, j)
            if bitwise_or >= K:
                count += 1

    return count

# Driver code
arr = [3, 4, 5]
n = len(arr)

k = 6
print(countSubArrays(arr, n, k))

# This code is contributed by ankush_953
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

  static int N = 100002;
  static int[] tree = new int[4 * N];

  // Function to build the segment tree
  static void build(int[] arr, int node,
                    int start, int end)
  {
    if (start == end) {
      tree[node] = arr[start];
      return;
    }
    int mid = (start + end) >> 1;
    build(arr, 2 * node, start, mid);
    build(arr, 2 * node + 1, mid + 1, end);
    tree[node] = tree[2 * node] | tree[2 * node + 1];
  }

  // Function to return the bitwise OR of segment [L..R]
  static int query(int node, int start,
                   int end, int l, int r)
  {
    if (start > end || start > r || end < l)
    {
      return 0;
    }

    if (start >= l && end <= r)
    {
      return tree[node];
    }

    int mid = (start + end) >> 1;
    int q1 = query(2 * node, start, mid, l, r);
    int q2 = query(2 * node + 1, mid + 1, end, l, r);
    return q1 | q2;
  }

  // Function to return the count of required sub-arrays
  static int countSubArrays(int[] arr, int n, int K)
  {

    // Build segment tree
    build(arr, 1, 0, n - 1); 
    int count = 0;
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Query segment tree for bitwise OR
        // of sub-array [i..j]
        int bitwise_or = query(1, 0, n - 1, i, j);
        if (bitwise_or >= K)
          count++;
      }
    }
    return count;
  }

  // Driver code
  static void Main() {
    int[] arr = { 3, 4, 5 };
    int n = arr.Length;

    int k = 6;
    Console.WriteLine(countSubArrays(arr, n, k));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let N = 100002;
let tree = new Array(4 * N);

// Function to build the segment tree   
function build(arr, node, start, end)
{
    if (start == end)
    {
        tree[node] = arr[start];
        return;
    }
    let mid = (start + end) >> 1;
    build(arr, 2 * node, start, mid);
    build(arr, 2 * node + 1, mid + 1, end);
    tree[node] = tree[2 * node] | tree[2 * node + 1];
}

// Function to return the bitwise OR of segment [L..R]
function query(node, start, end, l, r)
{
    if (start > end || start > r || end < l)
    {
        return 0;
    }

    if (start >= l && end <= r)
    {
        return tree[node];
    }

    let mid = (start + end) >> 1;
    let q1 = query(2 * node, start, mid, l, r);
    let q2 = query(2 * node + 1, mid + 1, end, l, r);
    return q1 | q2;
}

// Function to return the count of
// required sub-arrays
function countSubArrays(arr, n, K)
{

    // Build segment tree
    build(arr, 1, 0, n - 1);

    let count = 0;
    for(let i = 0; i < n; i++)
    {
        for(let j = i; j < n; j++)
        {

            // Query segment tree for bitwise OR
            // of sub-array [i..j]
            let bitwise_or = query(1, 0, n - 1, i, j);
            if (bitwise_or >= K)
                count++;
        }
    }
    return count;
}

// Driver code
let arr = [ 3, 4, 5 ];
let n = arr.length;
let k = 6;

document.write(countSubArrays(arr, n, k));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```

上述解的时间复杂度为 **O(n <sup>2</sup> log n)** ，**辅助空间**为O(n)。

一个更有效的解决方案是使用 T2 二分搜索法 T3。按位“或”是一个永远不会随着输入数量减少的函数。例如:

> OR(a，b) ≤ OR(a，b，c)
> OR(a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> ，…) ≤ OR(a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> ，…，b)

借此性质， **OR(a <sub>i</sub> ，…，a <sub>j</sub> ) < = OR(a <sub>i</sub> ，…，a <sub>j</sub> ，a <sub>j+1</sub> )** 。因此，如果 **OR(a <sub>i</sub> ，…，a <sub>j</sub> )** 大于 K，那么 **OR(a <sub>i</sub> ，…，a <sub>j</sub> ，a <sub>j+1</sub> )** 也将大于 K。因此，一旦我们找到子阵列**【I..j]** 其 OR 大于 K，我们不需要检查子阵列**【I..j+1]，[i..j+2]，..以此类推**，因为它们的 OR 也会大于 k，我们可以把剩余子阵的计数加到当前的和上。从一个特定的起点开始，第一个子阵列的“或”大于“K”，这是用二分搜索法法找到的。

下面是上述想法的实现:

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>

#define N 100002
using namespace std;

int tree[4 * N];

// Function which builds the segment tree
void build(int* arr, int node, int start, int end)
{
    if (start == end) {
        tree[node] = arr[start];
        return;
    }
    int mid = (start + end) >> 1;
    build(arr, 2 * node, start, mid);
    build(arr, 2 * node + 1, mid + 1, end);
    tree[node] = tree[2 * node] | tree[2 * node + 1];
}

// Function that returns bitwise OR of segment [L..R]
int query(int node, int start, int end, int l, int r)
{
    if (start > end || start > r || end < l) {
        return 0;
    }

    if (start >= l && end <= r) {
        return tree[node];
    }

    int mid = (start + end) >> 1;
    int q1 = query(2 * node, start, mid, l, r);
    int q2 = query(2 * node + 1, mid + 1, end, l, r);
    return q1 | q2;
}

// Function to count requisite number of subarrays
int countSubArrays(const int* arr, int n, int K)
{
    int count = 0;
    for (int i = 0; i < n; i++) {

        // Check for subarrays starting with index i
        int low = i, high = n - 1, index = INT_MAX;
        while (low <= high) {

            int mid = (low + high) >> 1;

            // If OR of subarray [i..mid] >= K,
            // then all subsequent subarrays will have OR >= K
            // therefore reduce high to mid - 1
            // to find the minimal length subarray
            // [i..mid] having OR >= K
            if (query(1, 0, n - 1, i, mid) >= K) {
                index = min(index, mid);
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }

        // Increase count with number of subarrays
        //  having OR >= K and starting with index i
        if (index != INT_MAX) {
            count += n - index;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    // Build segment tree.
    build(arr, 1, 0, n - 1);
    int k = 6;
    cout << countSubArrays(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    static int N = 100002;

    static int tree[] = new int[4 * N];

    // Function which builds the segment tree
    static void build(int[] arr, int node,
                    int start, int end)
    {
        if (start == end)
        {
            tree[node] = arr[start];
            return;
        }
        int mid = (start + end) >> 1;
        build(arr, 2 * node, start, mid);
        build(arr, 2 * node + 1, mid + 1, end);
        tree[node] = tree[2 * node] | tree[2 * node + 1];
    }

    // Function that returns bitwise
    // OR of segment [L..R]
    static int query(int node, int start,
                    int end, int l, int r)
    {
        if (start > end || start > r || end < l)
        {
            return 0;
        }

        if (start >= l && end <= r)
        {
            return tree[node];
        }

        int mid = (start + end) >> 1;
        int q1 = query(2 * node, start, mid, l, r);
        int q2 = query(2 * node + 1, mid + 1, end, l, r);
        return q1 | q2;
    }

    // Function to count requisite number of subarrays
    static int countSubArrays(int[] arr,
                            int n, int K)
    {
        int count = 0;
        for (int i = 0; i < n; i++)
        {

            // Check for subarrays starting with index i
            int low = i, high = n - 1, index = Integer.MAX_VALUE;
            while (low <= high)
            {

                int mid = (low + high) >> 1;

                // If OR of subarray [i..mid] >= K,
                // then all subsequent subarrays will
                // have OR >= K therefore reduce
                // high to mid - 1 to find the
                // minimal length subarray
                // [i..mid] having OR >= K
                if (query(1, 0, n - 1, i, mid) >= K)
                {
                    index = Math.min(index, mid);
                    high = mid - 1;
                }
                else
                {
                    low = mid + 1;
                }
            }

            // Increase count with number of subarrays
            // having OR >= K and starting with index i
            if (index != Integer.MAX_VALUE)
            {
                count += n - index;
            }
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {3, 4, 5};
        int n = arr.length;

        // Build segment tree.
        build(arr, 1, 0, n - 1);
        int k = 6;
        System.out.println(countSubArrays(arr, n, k));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement the above approach
N = 100002
tree = [0 for i in range(4 * N)];

# Function which builds the segment tree
def build(arr, node, start, end):
    if (start == end):
        tree[node] = arr[start];
        return;  
    mid = (start + end) >> 1;
    build(arr, 2 * node, start, mid);
    build(arr, 2 * node + 1, mid + 1, end);
    tree[node] = tree[2 * node] | tree[2 * node + 1];

# Function that returns bitwise OR of segment [L..R]
def query(node, start, end, l, r):
    if (start > end or start > r or end < l):
        return 0;
    if (start >= l and end <= r):
        return tree[node];   
    mid = (start + end) >> 1;
    q1 = query(2 * node, start, mid, l, r);
    q2 = query(2 * node + 1, mid + 1, end, l, r);
    return q1 | q2;

# Function to count requisite number of subarrays
def countSubArrays(arr, n, K):
    count = 0;
    for i in range(n):

        # Check for subarrays starting with index i
        low = i
        high = n - 1
        index = 1000000000
        while (low <= high):
            mid = (low + high) >> 1;

            # If OR of subarray [i..mid] >= K,
            # then all subsequent subarrays will have OR >= K
            # therefore reduce high to mid - 1
            # to find the minimal length subarray
            # [i..mid] having OR >= K
            if (query(1, 0, n - 1, i, mid) >= K):
                index = min(index, mid);
                high = mid - 1;          
            else :
                low = mid + 1;

        # Increase count with number of subarrays
        #  having OR >= K and starting with index i
        if (index != 1000000000):
            count += n - index;      
    return count;

# Driver code
if __name__=='__main__':
    arr = [ 3, 4, 5 ]
    n = len(arr)

    # Build segment tree.
    build(arr, 1, 0, n - 1);
    k = 6;
    print(countSubArrays(arr, n, k))

# This code is contributed by rutvik_56.
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int N = 100002;

    static int []tree = new int[4 * N];

    // Function which builds the segment tree
    static void build(int[] arr, int node,
                    int start, int end)
    {
        if (start == end)
        {
            tree[node] = arr[start];
            return;
        }
        int mid = (start + end) >> 1;
        build(arr, 2 * node, start, mid);
        build(arr, 2 * node + 1, mid + 1, end);
        tree[node] = tree[2 * node] | tree[2 * node + 1];
    }

    // Function that returns bitwise
    // OR of segment [L..R]
    static int query(int node, int start,
                    int end, int l, int r)
    {
        if (start > end || start > r || end < l)
        {
            return 0;
        }

        if (start >= l && end <= r)
        {
            return tree[node];
        }

        int mid = (start + end) >> 1;
        int q1 = query(2 * node, start, mid, l, r);
        int q2 = query(2 * node + 1, mid + 1, end, l, r);
        return q1 | q2;
    }

    // Function to count requisite number of subarrays
    static int countSubArrays(int[] arr,
                            int n, int K)
    {
        int count = 0;
        for (int i = 0; i < n; i++)
        {

            // Check for subarrays starting with index i
            int low = i, high = n - 1, index = int.MaxValue;
            while (low <= high)
            {

                int mid = (low + high) >> 1;

                // If OR of subarray [i..mid] >= K,
                // then all subsequent subarrays will
                // have OR >= K therefore reduce
                // high to mid - 1 to find the
                // minimal length subarray
                // [i..mid] having OR >= K
                if (query(1, 0, n - 1, i, mid) >= K)
                {
                    index = Math.Min(index, mid);
                    high = mid - 1;
                }
                else
                {
                    low = mid + 1;
                }
            }

            // Increase count with number of subarrays
            // having OR >= K and starting with index i
            if (index != int.MaxValue)
            {
                count += n - index;
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {3, 4, 5};
        int n = arr.Length;

        // Build segment tree.
        build(arr, 1, 0, n - 1);
        int k = 6;
        Console.WriteLine(countSubArrays(arr, n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

    let N = 100002;

    let tree=new Array(4*N);

    // Function which builds the segment tree
    function build(arr,node,start,end)
    {
         if (start == end)
        {
            tree[node] = arr[start];
            return;
        }
        let mid = (start + end) >> 1;
        build(arr, 2 * node, start, mid);
        build(arr, 2 * node + 1, mid + 1, end);
        tree[node] = tree[2 * node] | tree[2 * node + 1];
    }

    // Function that returns bitwise
    // OR of segment [L..R]
    function query(node,start,end,l,r)
    {
        if (start > end || start > r || end < l)
        {
            return 0;
        }

        if (start >= l && end <= r)
        {
            return tree[node];
        }

        let mid = (start + end) >> 1;
        let q1 = query(2 * node, start, mid, l, r);
        let q2 = query(2 * node + 1, mid + 1, end, l, r);
        return q1 | q2;
    }

    // Function to count requisite number of subarrays
    function countSubArrays(arr,n,K)
    {
        let count = 0;
        for (let i = 0; i < n; i++)
        {

            // Check for subarrays starting with index i
            let low = i, high = n - 1, index = Number.MAX_VALUE;
            while (low <= high)
            {

                let mid = (low + high) >> 1;

                // If OR of subarray [i..mid] >= K,
                // then all subsequent subarrays will
                // have OR >= K therefore reduce
                // high to mid - 1 to find the
                // minimal length subarray
                // [i..mid] having OR >= K
                if (query(1, 0, n - 1, i, mid) >= K)
                {
                    index = Math.min(index, mid);
                    high = mid - 1;
                }
                else
                {
                    low = mid + 1;
                }
            }

            // Increase count with number of subarrays
            // having OR >= K and starting with index i
            if (index != Number.MAX_VALUE)
            {
                count += n - index;
            }
        }
        return count;
    }

    // Driver code
    let arr=[3, 4, 5];
    let n = arr.length;
    // Build segment tree.
    build(arr, 1, 0, n - 1);
    let k = 6;
    document.write(countSubArrays(arr, n, k));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

上述解的时间复杂度为 **O(n log <sup>2</sup> n)** 。
**辅助空间** : O(n)。