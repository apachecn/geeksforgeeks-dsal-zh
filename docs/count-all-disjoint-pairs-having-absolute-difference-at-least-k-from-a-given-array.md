# 统计给定数组中绝对差值至少为 K 的所有不相交对

> 原文:[https://www . geeksforgeeks . org/count-all-distanced-pairs-with-absolute-difference-at-k-from-a-给定数组/](https://www.geeksforgeeks.org/count-all-disjoint-pairs-having-absolute-difference-at-least-k-from-a-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算所有绝对差[至少为 **K** 的不相交对。
**注:**对 **(arr[i]、arr[j])** 和 **(arr[j]、arr[i])** 视为同一对。](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)

**示例:**

> **输入:** arr[] = {1，3，3，5}，K = 2
> **输出:** 2
> **说明:**
> 以下两对满足必要条件:
> 
> *   {arr[0]，arr[1]} = (1，3)，其绝对值差为| 1–3 | = 2
> *   {arr[2]，arr[3]} = (3，5)，其绝对值差为| 3–5 | = 2
> 
> **输入:** arr[] = {1，2，3，4}，K = 3
> **输出:** 1
> **解释:**
> 唯一满足必要条件的对是{arr[0]，arr[3]} = (1，4)，因为| 1–4 | = 3。

**天真方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，并对那些绝对差值至少为**K 的对进行计数**并跟踪已经成对的元素，使用辅助数组**访问了【】**来标记成对的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count distinct pairs
// with absolute difference atleast K
void countPairsWithDiffK(int arr[],
                         int N, int K)
{
    // Track the element that
    // have been paired
    int vis[N];
    memset(vis, 0, sizeof(vis));

    // Stores count of distinct pairs
    int count = 0;

    // Pick all elements one by one
    for (int i = 0; i < N; i++) {

        // If already visited
        if (vis[i] == 1)
            continue;

        for (int j = i + 1; j < N; j++) {

            // If already visited
            if (vis[j] == 1)
                continue;

            // If difference is at least K
            if (abs(arr[i] - arr[j]) >= K) {

                // Mark element as visited and
                // increment the count
                count++;
                vis[i] = 1;
                vis[j] = 1;
                break;
            }
        }
    }

    // Print the final count
    cout << count << ' ';
}

// Driver Code
int main()
{
    // Given arr[]
    int arr[] = { 1, 3, 3, 5 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given difference K
    int K = 2;

    // Function Call
    countPairsWithDiffK(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count distinct pairs
// with absolute difference atleast K
static void countPairsWithDiffK(int arr[],
                                int N, int K)
{

    // Track the element that
    // have been paired
    int []vis = new int[N];
    Arrays.fill(vis, 0);

    // Stores count of distinct pairs
    int count = 0;

    // Pick all elements one by one
    for(int i = 0; i < N; i++)
    {

        // If already visited
        if (vis[i] == 1)
            continue;

        for(int j = i + 1; j < N; j++)
        {

            // If already visited
            if (vis[j] == 1)
                continue;

            // If difference is at least K
            if (Math.abs(arr[i] - arr[j]) >= K)
            {

                // Mark element as visited and
                // increment the count
                count++;
                vis[i] = 1;
                vis[j] = 1;
                break;
            }
        }
    }

    // Print the final count
    System.out.print(count);
}

// Driver Code
public static void main(String args[])
{

    // Given arr[]
    int arr[] = { 1, 3, 3, 5 };

    // Size of array
    int N = arr.length;

    // Given difference K
    int K = 2;

    // Function Call
    countPairsWithDiffK(arr, N, K);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count distinct pairs
# with absolute difference atleast K
def countPairsWithDiffK(arr, N, K):

    # Track the element that
    # have been paired
    vis = [0] * N

    # Stores count of distinct pairs
    count = 0

    # Pick all elements one by one
    for i in range(N):

        # If already visited
        if (vis[i] == 1):
            continue

        for j in range(i + 1, N):

            # If already visited
            if (vis[j] == 1):
                continue

            # If difference is at least K
            if (abs(arr[i] - arr[j]) >= K):

                # Mark element as visited and
                # increment the count
                count += 1
                vis[i] = 1
                vis[j] = 1
                break

    # Print the final count
    print(count)

# Driver Code
if __name__ == '__main__':

    # Given arr[]
    arr = [ 1, 3, 3, 5 ]

    # Size of array
    N = len(arr)

    # Given difference K
    K = 2

    # Function Call
    countPairsWithDiffK(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count distinct pairs
// with absolute difference atleast K
static void countPairsWithDiffK(int[] arr, int N,
                                int K)
{

    // Track the element that
    // have been paired
    int[] vis = new int[N];

    // Stores count of distinct pairs
    int count = 0;

    // Pick all elements one by one
    for(int i = 0; i < N; i++)
    {

        // If already visited
        if (vis[i] == 1)
            continue;

        for(int j = i + 1; j < N; j++)
        {

            // If already visited
            if (vis[j] == 1)
                continue;

            // If difference is at least K
            if (Math.Abs(arr[i] - arr[j]) >= K)
            {

                // Mark element as visited and
                // increment the count
                count++;
                vis[i] = 1;
                vis[j] = 1;
                break;
            }
        }
    }

    // Print the final count
    Console.Write(count);
}

// Driver Code
public static void Main()
{

    // Given arr[]
    int[] arr = { 1, 3, 3, 5 };

    // Size of array
    int N = arr.Length;

    // Given difference K
    int K = 2;

    // Function Call
    countPairsWithDiffK(arr, N, K);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript implementation
// for above approach

// Function to count distinct pairs
// with absolute difference atleast K
function countPairsWithDiffK(arr, N, K)
{
    // Track the element that
    // have been paired
    var vis = new Array(N);
    vis.fill(0);

    // Stores count of distinct pairs
    var count = 0;

    // Pick all elements one by one
    for (var i = 0; i < N; i++) {

        // If already visited
        if (vis[i] == 1)
            continue;

        for (var j = i + 1; j < N; j++) {

            // If already visited
            if (vis[j] == 1)
                continue;

            // If difference is at least K
            if (Math.abs(arr[i] - arr[j]) >= K) {

                // Mark element as visited and
                // increment the count
                count++;
                vis[i] = 1;
                vis[j] = 1;
                break;
            }
        }
    }

    // Print the final count
    document.write( count + " ");
}

    var arr = [ 1, 3, 3, 5 ];

    // Size of array
    var N = arr.length;

    // Given difference K
    var K = 2;

    // Function Call
    countPairsWithDiffK(arr, N, K);

// This code is contributed by SoumikMondal

</script>
```

**Output**

```
2 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**高效的思路是利用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到第一个至少有 K 个差异的**出现。以下是步骤:**

*   [给定数组按递增顺序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   将 **cnt** 初始化为 **0** ，这将存储所有可能对的计数。
*   按照以下步骤执行**二分搜索法**:
    *   将**左侧**初始化为 **0** ，**右侧**初始化为 **N/2 + 1** 。
    *   求**中间**的值为**(左+右)/ 2** 。
    *   检查最左边的 **M** 元素与最右边的 **M** 元素配对是否可以形成**中间的**对数量，即检查**arr[0]–arr[N–M]≥d，arr[1]–arr[N-M+1]≥d，…，arr[M–1]–arr[N–1]≥d**。
    *   在上述步骤中，[在范围**【0，M】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果存在一个其**ABS(arr[N–M+I]–arr[I])**小于 **K** 的索引，则更新右为**(mid–1)**。
    *   否则，更新左侧为**中间+ 1** ， **cnt** 为**中间**。
*   完成上述步骤后，打印 **cnt** 的值作为所有可能的对计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to
// form M pairs with abs diff at least K
bool isValid(int arr[], int n, int m,
             int d)
{
    // Traverse the array over [0, M]
    for (int i = 0; i < m; i++) {

        // If valid index
        if (abs(arr[n - m + i]
                - arr[i])
            < d) {
            return 0;
        }
    }

    // Return 1
    return 1;
}

// Function to count distinct pairs
// with absolute difference atleasr K
int countPairs(int arr[], int N, int K)
{
    // Stores the count of all
    // possible pairs
    int ans = 0;

    // Initialize left and right
    int left = 0, right = N / 2 + 1;

    // Sort the array
    sort(arr, arr + N);

    // Perform Binary Search
    while (left < right) {

        // Find the value of mid
        int mid = (left + right) / 2;

        // Check valid index
        if (isValid(arr, N, mid, K)) {

            // Update ans
            ans = mid;
            left = mid + 1;
        }
        else
            right = mid - 1;
    }

    // Print the answer
    cout << ans << ' ';
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 3, 3, 5 };

    // Given difference K
    int K = 2;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    countPairs(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if it is possible to
// form M pairs with abs diff at least K
static int isValid(int arr[], int n, int m,
                   int d)
{

    // Traverse the array over [0, M]
    for(int i = 0; i < m; i++)
    {

        // If valid index
        if (Math.abs(arr[n - m + i] - arr[i]) < d)
        {
            return 0;
        }
    }

    // Return 1
    return 1;
}

// Function to count distinct pairs
// with absolute difference atleasr K
static void countPairs(int arr[], int N, int K)
{

    // Stores the count of all
    // possible pairs
    int ans = 0;

    // Initialize left and right
    int left = 0, right = N / 2 + 1;

    // Sort the array
    Arrays.sort(arr);

    // Perform Binary Search
    while (left < right)
    {

        // Find the value of mid
        int mid = (left + right) / 2;

        // Check valid index
        if (isValid(arr, N, mid, K) == 1)
        {

            // Update ans
            ans = mid;
            left = mid + 1;
        }
        else
            right = mid - 1;
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[]
    int arr[] = { 1, 3, 3, 5 };

    // Given difference K
    int K = 2;

    // Size of the array
    int N = arr.length;

    // Function call
    countPairs(arr, N, K);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible to
# form M pairs with abs diff at least K
def isValid(arr, n, m, d):

    # Traverse the array over [0, M]
    for i in range(m):

        # If valid index
        if (abs(arr[n - m + i] - arr[i]) < d):
            return 0

    # Return 1
    return 1

# Function to count distinct pairs
# with absolute difference atleasr K
def countPairs(arr, N, K):

    # Stores the count of all
    # possible pairs
    ans = 0

    # Initialize left and right
    left = 0
    right = N // 2 + 1

    # Sort the array
    arr.sort(reverse = False)

    # Perform Binary Search
    while (left < right):

        # Find the value of mid
        mid = (left + right) // 2

        # Check valid index
        if (isValid(arr, N, mid, K)):

            # Update ans
            ans = mid
            left = mid + 1
        else:
            right = mid - 1

    # Print the answer
    print(ans, end = "")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 3, 3, 5 ]

    # Given difference K
    K = 2

    # Size of the array
    N = len(arr)

    # Function call
    countPairs(arr, N, K)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to check if it
// is possible to form M
// pairs with abs diff at
// least K
static int isValid(int []arr, int n,
                   int m, int d)
{   
  // Traverse the array over
  // [0, M]
  for(int i = 0; i < m; i++)
  {
    // If valid index
    if (Math.Abs(arr[n - m + i] -
                 arr[i]) < d)
    {
      return 0;
    }
  }

  // Return 1
  return 1;
}

// Function to count distinct
// pairs with absolute difference
// atleast K
static void countPairs(int []arr,
                       int N, int K)
{   
  // Stores the count of all
  // possible pairs
  int ans = 0;

  // Initialize left
  // and right
  int left = 0,
      right = N / 2 + 1;

  // Sort the array
  Array.Sort(arr);

  // Perform Binary Search
  while (left < right)
  {
    // Find the value of mid
    int mid = (left +
               right) / 2;

    // Check valid index
    if (isValid(arr, N,
                mid, K) == 1)
    {
      // Update ans
      ans = mid;
      left = mid + 1;
    }
    else
      right = mid - 1;
  }

  // Print the answer
  Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{   
  // Given array arr[]
  int []arr = {1, 3, 3, 5};

  // Given difference K
  int K = 2;

  // Size of the array
  int N = arr.Length;

  // Function call
  countPairs(arr, N, K);
}
}

// This code is contributed by surendra_gangwar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to check if it is possible to
    // form M pairs with abs diff at least K
    function isValid(arr , n , m , d) {

        // Traverse the array over [0, M]
        for (i = 0; i < m; i++) {

            // If valid index
            if (Math.abs(arr[n - m + i] - arr[i]) < d) {
                return 0;
            }
        }

        // Return 1
        return 1;
    }

    // Function to count distinct pairs
    // with absolute difference atleasr K
    function countPairs(arr , N , K) {

        // Stores the count of all
        // possible pairs
        var ans = 0;

        // Initialize left and right
        var left = 0, right = N / 2 + 1;

        // Sort the array
        arr.sort();

        // Perform Binary Search
        while (left < right) {

            // Find the value of mid
            var mid = parseInt((left + right) / 2);

            // Check valid index
            if (isValid(arr, N, mid, K) == 1) {

                // Update ans
                ans = mid;
                left = mid + 1;
            } else
                right = mid - 1;
        }

        // Print the answer
        document.write(ans);
    }

    // Driver Code

        // Given array arr
        var arr = [ 1, 3, 3, 5 ];

        // Given difference K
        var K = 2;

        // Size of the array
        var N = arr.length;

        // Function call
        countPairs(arr, N, K);

// This code contributed by gauravrajput1
</script>
```

**Output**

```
2 
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*